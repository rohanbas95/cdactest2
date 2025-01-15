# Section2
| Lectures | Description |
| ----------- | ----------- |
| [1. Git Commands](#git-commands) | |
| [2. VIM Commands](#vim-commands) | |
| [3. Github Action](#github-action) | |
| [4. how to run project locally](#how-to-run-project-locally) | |
| [5. docker commands](#docker-commands) | |
| [6. terraform commands](#terraform-commands) | |


# Git Commands
### list of important git commands
1. `git init`
2. `git status`
3. `git add .`
4. `git commit` 
5. `git commit -am "COMMIT_MSG_HERE"`
6. `git log`
7. `git pull`
---
8. `git branch -l`
9. `git branch -D BRANCH_NAME`
10. `git checkout BRANCH_NAME`
11. `git checkout -B BRANCH_NAME`
---
12. `git stash`
13. `git stash pop`
14. `git stash push`
15. `git stash list`
---
16. `git merge BRANCH_NAME`
17. `git cherry-pick COMMIT_SHA`
---
18. `git pull --rebase`
19. `git pull --no-rebase`
---
20. `git reset --soft COMMIT_SHA`
21. `git reset --hard COMMIT_SHA`
22. `git push --force`

# Vim Commands
1. `gg`  - 
2. `G`   - 
3. `5G`  - 
4. `ff`  - 
5. `p`   -
6. `dd`  -
7. `:w`
7. `:q`
8. `:!q`
9. `:set number` 

#### vim has three modes 
1. command mode
2. insert mode
3. extended mode 

# Github action
setting up basic CI CD pipeline using github action
few keypoints to note
1. github action runner
2. branch protection
3. github secrets `${{ secrets.ORG_GITHUB_PACKAGES_READER }}`


refer below example

```yaml
name: PR Build #name of the workflow
on: # the trigger on which to run workflow
  push:  
    branches: [main, "fix/*", "feat/*"]
    paths: 
      - 'frontend/**'
  pull_request:
    branches: [main, "fix/*", "feat/*"]
    paths: 
      - 'frontend/**'
  workflow_dispatch:

env:
  NODE_VERSION: 20

jobs:
  pr-build-api:
    runs-on: ubuntu-latest
    steps:
      - name: 🐙 Checkout code
        uses: actions/checkout@v4

      - name: 🔥 Setup NodeJS
        uses: actions/setup-node@v4
        with:
          registry-url: "https://npm.pkg.github.com"
          always-auth: true
          node-version: ${{ env.NODE_VERSION }}

      - name: 🏗️ Build FrontEnd
        working-directory: ./frontend
        run: |
          npm install
          npm run build
```

# how to run project locally
1. open three terminals
2. in each terminal `cd` to folder frontend , product-service, user-service
3. run `brew services start mongodb/brew/mongodb-community` in new terminal
4. run `npm install` , `npm run build` and `npm run start` in each terminal
5. website will be live on http://localhost:3000/

#### how to install mongoDB on mac
1. brew tap mongodb/brew
2. brew install mongodb-community
3. brew install mongosh
4. brew services start mongodb/brew/mongodb-community

#### how to install mongoDb on windows
[refer](https://www.mongodb.com/docs/manual/tutorial/install-mongodb-on-windows/)

# docker commands
1. `docker ps` | `docker ps -a` 
2. `docker run -e POSTGRES_PASSWORD=password postgres:9.6`
3. `docker pull redis`
4. `docker run redis`
5. `docker run -d redis`
6. `docker images`
7. `docker start f32897c3b1c9`
8. `docker stop f32897c3b1c9`
---
9. `docker run -p6000:6379 -d redis`
10. `docker logs older`
11. `docker run -p6002:6379 -d --name older redis`
12. `docker exec -it afd05d2c05f6 /bin/bash`
---
13. `docker pull mongo`
14. `docker pull mongo-express`
15. `docker network ls`
16. `docker network create mongo-network`
17. 
```
docker run -d \
-p 27017:27017 \
-e MONGO_INITDB_ROOT_USERNAME=admin \
-e MONGO_INITDB_ROOT_PASSWORD=password \
--name mongodb \
--net mongo-network \
mongo
```
18.
```
docker run -d \
-p 8081:8081 \
-e ME_CONFIG_MONGODB_ADMINUSERNAME=admin \
-e ME_CONFIG_MONGODB_ADMINPASSWORD=password \
--net mongo-network \
--name mongo-express \
-e ME_CONFIG_MONGODB_SERVER=mongodb \
mongo-express
```
19. `docker-compose -f docker-compose.yaml up -d`
20. `docker-compose -f docker-compose.yaml down`
21. `docker build -t my-prod:1.2 .`

# setup docker on ec2
```bash
sudo dnf update -y
sudo dnf install docker -y
sudo systemctl start docker
sudo systemctl enable docker
sudo usermod -aG docker $USER
sudo rm /usr/local/bin/docker-compose
sudo curl -L "https://github.com/docker/compose/releases/latest/download/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
sudo usermod -aG docker $USER
groups $USER
sudo systemctl restart docker
```


# terraform commands

