# Try

A dead simple and freaking easy to use continuous integration service.

## Specifications

- [ ] Feature #1
    - Given Try is started
    - It should listen to port 3000

- [ ] Feature #2
    - Given POST / on port 3000
    - It should trigger Try

- [ ] Feature #3
    - Given POST / on port 3000 with a branch parameter
    - It should trigger Try with that branch

- [ ] Feature #4
    - Given Github web hooks POST / on port 3000
    - It should trigger Try with the payload's referred branch

- [ ] Feature #5
    - Given Try is triggered
    - It should create an new uncompleted attempt in its database

- [ ] Feature #6
    - Given Try is triggered
    - It should fill the current attempt log

- [ ] Feature #7
    - Given Try is triggered
    - When it stops
    - It should complete the current attempt

- [ ] Feature #8
    - Given Try is triggered
    - It should go within the context of my target repository

- [ ] Feature #9
    - Given Try is triggered
    - It should load the config file found in the repository

- [ ] Feature #10
    - Given Try is triggered
    - When the config file is missing
    - Try should stop

- [ ] Feature #11
    - Given Try is triggered without a branch
    - It should stop

- [ ] Feature #12
    - Given Try is triggered with a branch
    - It should checkout that branch

- [ ] Feature #13
    - Given GET /attempts on port 3000
    - It should output a JSON formated list of all uncompleted attempts

- [ ] Feature #14
    - Given GET /attempts/history on port 3000
    - It should output a JSON formated list of the 10 latest completed attempts

- [ ] Feature #15
    - Given GET /attempts/history/n on port 3000
    - It should output a JSON formated list of the latest completed attempts from 10\*n to 10\*n+10

- [ ] Feature #16
    - Given the config file contains white-listed branches
    - When Try is triggered with a non-matching branch
    - It should stop

- [ ] Feature #17
    - Given the config file contains white-listed branches
    - When Try is triggered with a matching branch
    - It should check it out

- [ ] Feature #18
    - Given the config file contains blacklisted branches
    - When Try is triggered with a non-matching branch
    - It should check it out

- [ ] Feature #19
    - Given the config file contains blacklisted branches
    - When Try is triggered with a matching branch
    - It should stop

- [ ] Feature #20
    - Given the config file contains white-listed and blacklisted branches
    - When Try is triggered with a branch matching both
    - It should stop

- [ ] Feature #21
    - Given the config file's branch names contain regular expressions
    - When Try is triggered with a branch
    - It should test the regular expressions against it

- [ ] Feature #22
    - Given the config file contains no targets
    - When Try is triggered with a branch
    - It should use the local machine as target

- [ ] Feature #23
    - Given the config file contains commands
    - When Try is triggered with a branch
    - It should run the commands on the target machine

- [ ] Feature #24
    - Given the config file contains commands
    - When a command fails on a target
    - Try should not execute the next commands

- [ ] Feature #25
    - Given the config file contains a target
    - When Try is triggered with a branch
    - Try should run the commands on the target

- [ ] Feature #26
    - Given the config file contains multiple targets
    - When Try is triggered with a branch
    - Try should run the commands on all the target simultaneously

- [ ] Feature #27
    - Given the config file contains prepare commands
    - When Try is triggered with a branch
    - It should run the prepare commands on the local machine before running the other commands

- [ ] Feature #28
    - Given the config file contains success commands
    - When no command failed
    - Try should run the success commands on the local machine and stop

- [ ] Feature #29
    - Given the config file contains failure commands
    - When at least one command failed
    - Try should run the failure commands on the local machine and stop

- [ ] Feature #30
    - Given the config file contains targets
    - When a target doesn't have a port parameter
    - Try should use port 22 as default

- [ ] Feature #31
    - Given the config file contains targets
    - When a target doesn't have an user parameter
    - Try should use the USER environment variable as default

- [ ] Feature #32
    - Given the config file contains targets
    - When a target doesn't have a host parameter
    - Try should stop

- [ ] Feature #33
    - Given a command contains the [BRANCH] placeholder
    - When Try is triggered with a branch
    - Try should replace it with that branch
