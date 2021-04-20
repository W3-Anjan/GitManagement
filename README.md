### Reference 
https://www.mokkapps.de/blog/how-to-automatically-generate-a-helpful-changelog-from-your-git-commit-messages/

https://dev.to/migu3l/commit-standard-and-semantic-versioning-for-any-project-1ihc

**Steps to Automatically Generate A Helpful Changelog From Your Git Commit Messages**

- Install Node.js on your system according to your OS
   
- Install global dependencies
  ```
   - npm i -g commitizen
   - npm i -D husky @commitlint/cli @commitlint/config-conventional @semantic-release/git @semantic-release/changelog @semantic-release/commit-analyzer @semantic-release/release-notes-generator @semantic-release/npm
   ```
- Create a New Branch
   - **$ git checkout -b contributor-branch**
   
- Make Changes Locally
   - to commit message from text editor set to config **$ git config --global core.editor "nano"**
      (ctrl+X to exit the editor. Then it will ask for confirmation and write Y and press Enter)
   - to commit **$ git commit -m "contributor package added"**
   - to push **$ git push --set-upstream origin contributor-branch** 
   
- Update Local Repository

  - Configure a Remote for the Fork
  
    - To keep your local copy of the code base updated, you’ll need to sync changes.
    - configure a remote for a fork or add an upstream remote git repository
    - **Remote repositories** make it possible for you to collaborate with others on a Git project. 
    - You should set up the remote to the upstream repository only once.
    
    **Why we should configure a remote for a fork ?**
    
    
        Git is designed to give each developer an entirely isolated development environment. 
        This means that information is not automatically passed back and forth between repositories. 
        Instead, developers need 
         - to manually pull upstream commits into their local repository or 
         - to manually push their local commits back up to the central repository. 
        We must configure a remote that points to the upstream repository in Git to sync changes we make in a fork with the original repository. 
        This also allows us to sync changes made in the original repository with the fork.
        
   Ref: https://medium.com/@sarathkumarsivan/configuring-a-remote-for-a-fork-f697b8744d12
   
   - to check which remote servers you have configured **$ git remote -v**
   - Right now it will display the cloned repo as remote repository
      - origin  https://github.com/W3-Anjan/MockitoUnitTestTutorial.git (fetch)
      - origin  https://github.com/W3-Anjan/MockitoUnitTestTutorial.git (push)
   - Next, we’ll specify a new **remote upstream repository for us to sync with the fork**. 
     This will be the original repository that we forked from. We’ll do this with the git remote add command.  
     **$ git remote add upstream https://github.com/anjandebnath/MockitoUnitTestTutorial.git**
     
  - Sync the Fork 
  
    - To get the updates (new branches and codes after taking the fork) **$ git fetch upstream**
    - This way forked repo will be synced with the upstream repo
    - Sync the fork
    
    <kbd><img src="https://github.com/W3-Anjan/GitManagement/blob/feature/new-branchV2/img/upstream-fetch.png" align="center"></kbd>


- Create Pull request
      
 <kbd><img src="https://github.com/W3-Anjan/GitManagement/blob/feature/new-branchV2/img/pull%20request.png" align="center"></kbd>



- **in terms of Git, “upstream” refers to the repository that we cloned from.**

### Repository First time setup

<kbd><img src="https://github.com/W3-Anjan/GitManagement/blob/feature/new-branchV2/img/git-and-github-initial-setup.png" align="center"></kbd>

### Fork and Clone
<kbd><img src="https://github.com/W3-Anjan/GitManagement/blob/feature/new-branchV2/img/upstream-origin-local.png" align="center"></kbd>



