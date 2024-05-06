# Cooper Casino Monorepo    
This is a "source of truth" on what could be considered a stable release for our     
project. Pull the main branch recursively, grabbing the frontend, backend, and      
database repo, and launch using docker compose. More comprehensive instructions,        
soon.   
`main` reflects what is `main` on our module repos.     
Our Module structure is as follows:     
```
monorepo
    |
    |---frontend
    |
    \---backend
        |---database
        |---commandline
```
- frontend: Contains Flutter-based frontend
- backend: Contains Spring backend
- database: Contains config files related to db deployment
- commandline: Basic Command line API Interface for headless operation

# For deployers
Pull recursively (if you havent done so already)    
```
git clone --recurse-submodules git@github.com:ECE-366-Final-Project/monorepo.git
```
Make sure that docker and docker-compose are installed  
[See the Docker docs for instructions!](https://docs.docker.com/compose/install/)

Lets say you have a branch you're working on, on one of the other module repos.     
You want to deploy against a stable frontend, and db, while you want to test    
changes on backend. How do we do this?      
First: clone this repo recursively! Its easiest if this is a clean clone.   
```
git clone --recurse-submodules git@github.com:ECE-366-Final-Project/monorepo.git    
``` 
Please make a new branch (within monorepo!), so you can save your work, if you need to.    
```
git checkout -b <username>/<branch-name>    
``` 
Second: All our modules are pointing to the hash associated with each modules   
`main` branch. How do we get backend to point somewhere else? We tell git to    
pull our submodule from a different commit hash.    
The easiest way is to `cd` in, and tell the repo to look somewhere else.    
```
git submodule update --init --recursive --remote #yells at git to get remote branches 
cd <backend || frontend>
git switch <name of remote branch you want>
``` 

Now, the fun part! Build and initialize the project with   
```
$ docker compose up --build -d
```
Ensure that ports `80`, `8080` and `5432` are not already bound!      

If you have issues pulling the modules, replace `git@github.com:` with    
`https://github.com/` in all .gitmodules! Or make an ssh key and attach    
it to GitHub.

# Headless mode 
Headless mode deploys the casino with no Flutter dependency, ie just    
Spring/Java and Postgres. This is useful for testing API changes which havent   
been given a proper implementation in the frontend, yet!    
<b>YOUR MILEAGE WILL VARY, IF YOU JUST WANT TO PLAY SOME SLOTS, THIS IS NOT 
RECOMMENDED.</b>    
Setting it up: Go into frontend and checkout the `headless` branch. Done! :D  

# Engineering Ethics
Our project abides by the [ACM/IEEE-CS Software Engineering ethics](https://ethics.acm.org/code-of-ethics/software-engineering-code/) in the following ways:    

1. **(Principle 3.14)** _Maintain the integrity of data, being sensitive to outdated or flawed occurrences_- we addressed bugs and errors made earlier in project development through branches dedicated to fixes established later in our project. 
2. **(Principle 5.02)** _Ensure that software engineers are informed of standards before being held to them_- we went over this list of engineering ethics in class. We had both a list of GitHub issues and a group chat to keep each other accountable for the standards both the ACM/IEEE and our group have for one another. 
3. **(Principle 5.04)** _Assign work only after taking into account appropriate contributions of education and experience tempered with a desire to further that education and experience_- we took into account the fact that we are all still students so we learned from our experiences in the first half of the class and got our project reduced to more manageable means by the 2nd check-in.
4. **(Principle 5.08)** _Not unjustly prevent someone from taking a position for which that person is suitably qualified_- all members of the team were given a designated project role that was suited towards what they were most qualified for. If a member wanted to take on a portion that was not typically within their line of development, they were given a task within their interest.
5. **(Principle 6.08)** _Take responsibility for detecting, correcting, and reporting errors in software and associated documents on which they work_- If there were issues that one noticed in the code, structure, or documentation that required assistance, it was brought up in our group chat or during our weekly meeting. 
6. **(Principle 7.04)** _Review the work of others in an objective, candid, and properly documented way_- Consistent review was done through communication and reminders in our GitHub code reviews, in-person weekly group meetings, and our group chat to let each other know about the work we are doing and the need to constantly review it all.
7. **(Principle 7.06)** _Assist colleagues in being fully aware of current standard work practices including policies and procedures for protecting passwords, files, and other confidential information, and security measures in general_- we utilized GitHub code reviews, group meetings, and our group chat to remind and let each other know about the work we all committed one another to. Documentation was made to record proper procedures on how to access and edit our project. 
8. **(Principle 3.11)** _Ensure adequate documentation, including significant problems discovered and solutions adopted, for any project on which they work_- our trials and tribulations are recorded in the GitHub issues listed in each repository. Records on how to get our project up for those who want to run our project are listed in the README.md files of each repository. 
9. **(Principle 7.08)** _In situations outside of their own areas of competence, call upon the opinions of other professionals who have competence in that area_- when a member was concerned about a particular part of the project that warranted the advice of someone in a different portion (say someone working on frontend came across an error that was rooted in the backend), as this entire project is reliant all of its respective part, we would call upon one another for a more experienced opinion. 
10. **(Principle 8.01)** _Further their knowledge of developments in the analysis, specification, design, development, maintenance and testing of software and related documents, together with the management of the development process_- This project has taught us a lot whether it be how to connect the different portions of a software engineering project to how to work in a software development team. We plan to further our knowledge in these fields through the pursuit of our electrical engineering degree at the Cooper Union which involves a curriculum deeply invested in the pursuit of software development and related subjects.
