# Cooper Casino Monorepo    
This is a "source of truth" on what could be considered a stable release for our    
project. Pull the main branch recursively, grabbing the frontend, backend, and  
database repo, and launch using docker compose. More comprehensive instructions,    
soon.   
`main` reflects what is `main` on our module repos. 
# For deployers
Pull this 

# For developers    
Lets say you have a branch you're working on, on one of the other module repos. 
You want to deploy against a stable frontend, and db, while you want to test    
changes on backend. How do we do this?  
First: clone this repo recursively! Its easiest if this is a clean clone.   
```
git clone --recurse-submodules git@github.com:ECE-366-Final-Project/monorepo.git 
``` 
Please make a new branch, so you can save your work, if you need to.    
```
git checkout -b <username>/<branch-name>
``` 
Second: All our modules are pointing to the hash associated with each modules   
`main` branch. How do we get backend to point somewhere else? We tell git to    
pull our submodule from a different commit hash.    
The easiest way is to `cd` in, and tell the repo to look somewhere else.    
```
git submodule update --init --recursive --remote #yells at git to get remote branches 
cd Back-End
git checkout <name of remote branch you want>
``` 
Now see the deployment section for getting the program running! 

# Headless mode 
Headless mode deploys the casino with no Flutter dependency, ie just    
Spring/Java and Postgres. This is useful for testing API changes which havent   
been given a proper implementation in the frontend, yet!    
<b>YOUR MILEAGE WILL VARY, IF YOU JUST WANT TO PLAY SOME SLOTS, THIS IS NOT 
RECOMMENDED.</b>    
Setting it up: Go into frontend and checkout the `headless` branch. Done! :D    
