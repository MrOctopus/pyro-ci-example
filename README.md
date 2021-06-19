# pyro-ci-example
A simple pre-made CI workflow file which you can edit to use for your own pyro projects on github.

## How To Use
### Prerequisite steps
1. Setup your pyro project files (.ppj) in the github repository
2. Setup a private github repository containing the Papyrus Compiler
    - Alternatively, you can use a [public](https://github.com/Osmosis-Wrench/JContainers-Compiler-Only) one

### CI steps
1. Copy the CI.yml workflow file into the ```.github/workflows``` folder of your repository
2. Update the commented settings in the .yml file:
```yml
  push:
    # Set the push branches
    branches:
    - main
    # Set the detected push folders, or remove this section entirely
    paths:
    - 'example/folder/path'

jobs:
  build:
    runs-on: windows-latest
    strategy:
      matrix:
      # Set the project file paths relative to the current repo
        project-path:
        - 'example.ppj'
        - 'subpath\example2.ppj'
    env:
      # Set these
      dist-path: dist                               # Folder containing the output from the project files
      compiler-repo: MrOctopus/papyrus-compiler     # Github repository containing your papyrus compiler
      compiler-token: ${{ secrets.PRIVATE_TOKEN }}  # Just use ${{ github.token }} if the compiler repository is not private
      pyro-token: ${{ secrets.PRIVATE_TOKEN }}      # Just use ${{ github.token }} if the ppj file does not use private imports
```
3. You can now compile your papyrus scripts by pushing new commits to the repository
    - Alternatively, you can start builds manually in the github actions tab
    - Builds will be available as artifacts under github action runs

## Good To Know
### Useful
Many of the most commonly used papyrus source files are available online at this [link](https://github.com/MrOctopus/nl_online).

### Important
At the moment, the workflow setup does not support the '.' character in pyro-generated zip filenames. \
Please opt for using another character such as '_' instead.

## Credits
Although you do not need to credit me for the workflow setup, it is a nice gesture. \
Specifically, I made two custom github actions to support Pyro CI builds.