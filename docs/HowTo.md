# This software is simple to use.


## Basic use case:

You are using a configuration management system to manage your linux servers (possibly windows as well).
It would be convenient to develop configuration management in a similar way to how software is developed in test driven development.
In essence the process flow ideally would be to:

- create a test for what should fail first.
- run the test and observe it fail
- develop the configuration management state / playbook / manifest / recipe / bash script
- run the configuration management state / playbook / manifest / recipe / bash script
- run the test and observe it pass


## Requirements:

* You must install a saltstack master.
* The salt master must either control servers via zeromq (default) or ssh.

`salt_check.py` enables this to be done easily, without having to program.


## Syntax

Input files are simple yaml and have the following syntax:

```yaml
TEST-ID:
  module_and_function:  SALT-MODULE.SALT_FUNCTION
  args: ARG-TO-FUNCTION
  kwargs: KWARGS-TO-FUNCTION
  pillar-data: PILLAR-DATA-ON-THE-FLY
  assertion: PICK-A-SUPPORTED-ASSERTION
  expected-return: VALUE-COMPARED-TO-ASSERTION
```

Here is an example which tests if a specific version of apache is installed on an ubuntu server:

```yaml
correct-version-apache2-installed:
  module_and_function: pkg.version
  args: 'apache2'
  kwargs: ''
  pillar-data: ''
  assertion: assertEqual
  expected-return: 2.4.7-1ubuntu4.9
```

An input file may contain multiple test cases.
The modules and functions supported depend entirely on the version of saltstack installed.
