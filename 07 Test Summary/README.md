# Test Summary

**Description:**

Congrats, your tests have passed! Your test results were exported to `~/project/results/test_results.xml`. Let's see if you can display the test results in the _test summary_ tab, and export the file as an _artifact_ in case we want to inspect it later.

**Goals:**

- Get a green build
- Have test results displayed in the _test summary_ tab
- Export the test results to an artifact.
- Share link to green job.

**Help:**
<details>
  <summary>Spoiler warning</summary>

  * https://circleci.com/docs/collect-test-data/
  * https://circleci.com/docs/artifacts/
  
</details>

version: 2.1

orbs:
  build-tools: circleci/build-tools@3.0.0 # This is an orb. If you are not yet familiar with orbs, we will go over them soon. Orbs allow us to make our configs shorter by allowing us to "import" config in a similar way to a programming language's package manager.

jobs:
  build:
    docker: 
      - image: cimg/base:2022.10 

    steps:
      - build-tools/test-results:
          data-dir: ~/project/results
          upload: true # Don't cheat! 

# Add below this line, do not modify above
      - store_test_results:
          path: test-results 

# Add above this line, do not modify below

workflows:
  build-workflow:
    jobs:
      - build

