# Initial Documentation for salt_check.py

The goal of this software is to enable easy testing of configuration managed servers.
Bluntly, the question of whether what was to be an end state of a server actually
happened after setting up configuration managment software system (salt states,
ansible playbook, puppet mainfest, chef recipe), and applying the software
(salt, ansible, puppet, chef).


## Use case: test driven configuration management, without having to program

#### Example process flow:

- create a test case for a server (e.g. is the right version of apache installed)
- run the test case, and see it fail
- run the config mgmt system (which installs apache)
- re-run the test case for a server and observe if the right version of apache is installed (hopefully it is)

### Usage:

* `salt '*' salt_check.run_state_tests apache`
* `salt '*' salt_check.run_highstate_tests`

#### Test case syntax:

```yaml
UNIQUE-TEST-CASE-NAME:
  module_and_function: SALT_MODULE.FUNCTION
  args:
    - argument1
    - argument2
  kwargs:
    - FOO=BAR
    - HELLO=HI
  assertion: assertEqual
  expected-return: COMPARE-VALUE
```

#### Definitions:

* **salt_module.function** denotes a saltstack execution module and function to call in that module
* **args** are arguments supported by the function
* **kwargs** are arguments keyword arguments supported by the function
* **assertions** are used to compare what was returned from the salt_module.function to what we expected to get
* **expected-return** is the value we want expect to see returned from the function


## Test case example:

```yaml
correct-version-apache2-installed:
  module_and_function: pkg.version
  args:
    - apache2
  kwargs:
  pillar-data:
  assertion: assertEqual
  expected-return: 2.4.7-1ubuntu4.9

Requirements:
  SaltStack master server with ability to control target servers
  Any state to be tested should have a subdirectory of "salt-check-tests", which contains 1+ *.tst files

Installation:
  pip install --upgrade salt_check-2016-5-1.1.tar.gz

Uninstall:
  pip uninstall salt_check
```
