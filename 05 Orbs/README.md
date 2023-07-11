# Orbs

**Description:**

We have a config file that requires a specific Ruby version be installed, however the image we are using doesn't have Ruby, so the build fails. Utilizing the Ruby Orb (`circleci/ruby`) install Ruby version `2.6.3` so the build will be green.

**Goals:**

- Add the Ruby Orb to the config file
- Install Ruby version `2.6.3` with Orb
- Build should be green if Ruby installed properly

**Help:**
<details>
  <summary>Spoiler warning</summary>

  * https://circleci.com/orbs/registry/orb/circleci/ruby#usage-examples
  
</details>


version: 2.1

orbs:
  # Add Orb here

jobs:
  build:
    docker:
      - image: cimg/ruby:2.6.3
    steps:
      - checkout
      # Add step below to install Ruby version 2.6.3

      
      - run: ruby -v

workflows:
  run-jobs:
    jobs:
      - build
