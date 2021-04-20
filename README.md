### Reference 
https://www.mokkapps.de/blog/how-to-automatically-generate-a-helpful-changelog-from-your-git-commit-messages/

https://dev.to/migu3l/commit-standard-and-semantic-versioning-for-any-project-1ihc

**Steps to Automatically Generate A Helpful Changelog From Your Git Commit Messages**

- Install Node.js on your system according to your OS
   
- Install ``global dependencies``
  ```
   - npm i -g commitizen
   - npm i -D husky @commitlint/cli @commitlint/config-conventional @semantic-release/git @semantic-release/changelog @semantic-release/commit-analyzer @semantic-release/release-notes-generator @semantic-release/npm
   ```
- Create a ``package.json`` file
   - You can add a package.json file to your package to make it easy for others to manage and install. Packages published to the registry must contain a package.json file.
   - To create a package.json file with values that you supply, use the ``npm init`` command.
   - On the command line, navigate to the root directory of your package.
        - ```cd /path/to/package```
   - Run the following command:
        - ```npm init```
- Create a ``package-lock.json`` file 
   - Execute **commitizen init cz-conventional-changelog -D -E** 
   - this will add the dependencies of cz-conventional-changelog and update our package with the configuration:
        ```
            "config": {
              "commitizen": {
                "path": "./node_modules/cz-conventional-changelog"
              }
            }
        ```
   
- Update ``package.json`` to Husky check if the commits follow the conventional standard using commitlint

        ```
            "dependencies": {
                   "@commitlint/cli": "latest",
                   "@commitlint/config-conventional": "latest",
                   "husky": "latest"
                 },
            "husky": {
              "hooks": {
                "commit-msg": "commitlint -E HUSKY_GIT_PARAMS"
              }
            },
            "commitlint": {
              "extends": [
                "@commitlint/config-conventional"
              ]
            }
        ```

- We create a .commitlintrc.json file which extends the rules from [config-conventional](https://github.com/conventional-changelog/commitlint/tree/master/%40commitlint/config-conventional):
  
    ```
       {
         "extends": ["@commitlint/config-conventional"]
       }
   ```
- Finally, we can create a CHANGELOG from our GIT history. Run the command inside the repository

   ```
        npm i --save-dev standard-version
   ```   
- Update ``npm scripts`` in our ``package.json``:

    ```

         "scripts": {
             "release": "standard-version",
             "release:minor": "standard-version --release-as minor",
             "release:patch": "standard-version --release-as patch",
             "release:major": "standard-version --release-as major"
           }, 

    ``` 
    
    



