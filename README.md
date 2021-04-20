## Automatically Generate A Helpful Changelog From Your Git Commit Messages

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
- Create a ``package.json`` file [Creating a package.json](https://docs.npmjs.com/creating-a-package-json-file)
   - You can add a package.json file to your package to make it easy for others to manage and install. Packages published to the registry must contain a package.json file.
   - To create a package.json file with values that you supply, use the ``npm init`` command.
   - On the command line, navigate to the root directory of your package.
        - ```cd /path/to/package```
   - Run the following command:
        - ```npm init```
   - Example package.json
   
       ```
            > npm init --yes
            Wrote to /home/monatheoctocat/my_package/package.json:
            
            {
              "name": "my_package",
              "description": "",
              "version": "1.0.0",
              "scripts": {
                "test": "echo \"Error: no test specified\" && exit 1"
              },
              "repository": {
                "type": "git",
                "url": "https://github.com/monatheoctocat/my_package.git"
              },
              "keywords": [],
              "author": "",
              "license": "ISC",
              "bugs": {
                "url": "https://github.com/monatheoctocat/my_package/issues"
              },
              "homepage": "https://github.com/monatheoctocat/my_package"
            }
      ```     
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
   
- Update ``package.json`` to Husky check if the commits follow the conventional standard using commitlint:

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
- The first release can be created by running ``npm run release -- --first-release`` in the terminal:  

## Semantic Versioning

- ``fix``: a commit of this type ``patches`` a bug in your codebase and correlates with the 
  ``patch version`` in semantic versioning. ``1.0.0 -> 1.0.1``
- ``feat``: a commit of this type introduces a new ``feature`` to the codebase and correlates with a
  ``minor version`` in semantic versioning. ``1.0.1 -> 1.1.1``
- ``BREAKING CHANGE``: a commit that has the text ``BREAKING CHANGE:`` at the beginning of its 
  ``optional body or footer section`` introduces a breaking API change and correlates with a 
  ``major version`` in semantic versioning. A ``breaking change`` can be part of commits of any type. 
   e.g., a fix:, feat: & chore: types would all be valid, in addition to any other type.
   ``1.1.1 -> 2.0.0``
- Other types like ``chore:``, ``docs:``, ``style:``, ``refactor:``, ``perf:``, ``test:`` are recommended 
  by the Angular convention. These types have no implicit effect on semantic versioning and are not part of 
  the conventional commit specification.
  
  Example:
  
  Definition | Description
  -----------|------------
  feat | A new feature
  fix | A bug fix
  docs | Documentation only changes
  style | Changes that do not affect the meaning of the code (white-space, formatting, missing semi-colons, etc)
  refactor | A code change that neither fixes a bug nor adds a feature
  perf | A code change that improves performance
  test | Adding missing or correcting existing tests
  chore | Changes to the build process or auxiliary tools and libraries such as documentation generation
  
  Take special note on a [revert commit](https://github.com/angular/angular.js/blob/master/DEVELOPERS.md#revert)
  
  Here is how semantic-release will map these to release types and how it maps to [semantic verioning](https://semver.org/#summary):
  
  Commit message | Release type
  ----------------|--------------
  `fix(pencil): stop graphite breaking `<br>`when too much pressure applied` | Patch Release (PATCH)
  `feat(pencil): add 'graphiteWidth' option` | Feature Release (MINOR)
  `perf(pencil): remove 'graphiteWidth' option`<br> `BREAKING CHANGE: The graphiteWidth option `<br>`has been removed. The default graphite`<br>` width of 10mm is always used for performance reasons.` | Breaking Release (MAJOR)
  
  
    
    



