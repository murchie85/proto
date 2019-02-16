# CICD with BlueOcean


## TRIGGER
If you are not using a hook, then set minimum interval trigger check to 1 minute - this is less intesnive than polling. 

## ANACONDA/MINICONDA 

Yout have to set your path - which includes CONDA, remember the path will be relative to the jenkins user which is set to Jenkins directory. Jenkins is nologin by default.

## CONDA INSTALL


```
conda install --name ${BUILD_TAG}  --file requirements.txt -y
```

1. Conda installs from requirments.txt file 
2. -y flag means to proceed with changes (as this is interactive session)
3. ${BUILD_TAG} is a concatination of Build name and number


## STATIC CODE METRICS

1. Ensure that Jenkins has read/write access to wherever you wish to deposit your rests.
2. Ensure you have radon installed

## COVERAGE 

1. You will need to use the || true flag or it will abort on each run 
2. Ensure you have COVERAGE installed

## FEATURE TESTS

1. Install behave (as part of pip/conda)
2. create a directory called `features`
3. Need files with .feature that have something like the following : 

```
Feature: showing off behave

  Scenario: run a simple test
     Given we have behave installed
      When we implement a test
      Then behave will test it for us!
```
4. Make a new directory called `features/steps`
5. Add a integration test with .py prefix like below: 
```
from behave import *

@given('we have behave installed')
def step_impl(context):
    pass

@when('we implement a test')
def step_impl(context):
    assert True is not False

@then('behave will test it for us!')
def step_impl(context):
    assert context.failed is False
```