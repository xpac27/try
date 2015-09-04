# try

A dead simple and freaking easy to use continuous integration service.

- [ ] Given Try is started, it should listen to port 3000
- [ ] Given POST / on port 3000, it should trigger Try
- [ ] Given POST / on port 3000 with a branch parameter, it should trigger Try with that branch
- [ ] Given Github web hooks POST / on port 3000, it should trigger Try with the payload's referred branch
- [ ] Given Try is triggered, it should create an new uncompleted attempt in its database
- [ ] Given Try is triggered, it should fill the current attempt log
- [ ] Given Try is triggered, when it stops, it should complete the current attempt
- [ ] Given Try is triggered, it should go within the context of my target repository
- [ ] Given Try is triggered, it should load the config file found in the repository
- [ ] Given Try is triggered, when the config file is missing, Try should stop
- [ ] Given Try is triggered without a branch, it should stop
- [ ] Given Try is triggered with a branch, it should checkout that branch
- [ ] Given GET /attempts on port 3000, it should output a JSON formated list of all uncompleted attempts
- [ ] Given GET /attempts/history on port 3000, it should output a JSON formated list of the 10 latest completed attempts
- [ ] Given GET /attempts/history/n on port 3000, it should output a JSON formated list of the latest completed attempts from 10\*n to 10\*n+10
- [ ] Given the config file contains white-listed branches, when Try is triggered with a non-matching branch, it should stop
- [ ] Given the config file contains white-listed branches, when Try is triggered with a matching branch, it should check it out
- [ ] Given the config file contains blacklisted branches, when Try is triggered with a non-matching branch, it should check it out
- [ ] Given the config file contains blacklisted branches, when Try is triggered with a matching branch, it should stop
- [ ] Given the config file contains white-listed and blacklisted branches, when Try is triggered with a branch matching both, it should stop
- [ ] Given the config file's branch names contain regular expressions, when Try is triggered with a branch, it should test the regular expressions against it
- [ ] Given the config file contains no targets, when Try is triggered with a branch, it should use the local machine as target
- [ ] Given the config file contains commands, when Try is triggered with a branch, it should run the commands on the target machine
- [ ] Given the config file contains commands, when a command fails on a target, Try should not execute the next commands
- [ ] Given the config file contains a target, when Try is triggered with a branch, Try should run the commands on the target
- [ ] Given the config file contains multiple targets, when Try is triggered with a branch, Try should run the commands on all the target simultaneously
- [ ] Given the config file contains prepare commands, when Try is triggered with a branch, it should run the prepare commands on the local machine before running the other commands
- [ ] Given the config file contains success commands, when no command failed, Try should run the success commands on the local machine and stop
- [ ] Given the config file contains failure commands, when at least one command failed, Try should run the failure commands on the local machine and stop
- [ ] Given the config file contains targets, when a target doesn't have a port parameter, try should use port 22 as default
- [ ] Given the config file contains targets, when a target doesn't have an user parameter, try should use the USER environment variable as default
- [ ] Given the config file contains targets, when a target doesn't have a host parameter, try should stop
- [ ] Given a command contains the [BRANCH] placeholder, when Try is triggered with a branch, try should replace it with that branch

## Config samples

### The minimal configuration file

    # empty... :)

This will do nothing but it's still valid.

### The minimal valuable configuration file

    commands: 
        - make

Checkout the specified branch and run the make command on the local machine.

### Multiple commands

    commands: 
        - make clean
        - make configure
        - make compile
        - make test

Checkout the specified branch and run the make clean, make configure, make compile and make test commands on the local machine.

### Filtering branches

    whitelist: features/.* master
    blacklist: features/experimental
    commands: 
        - make

Checkout the specified branch if white-listed and not blacklisted and run the make command on the local machine.

### Specifying a target

    target:
        host: 172.9.0.23
        user: build
        port: 22
    commands: 
        - make

Checkout the specified branch and run the make command on the targeted machine.

### Specifying multiple targets

    target:
        osx:
            host: 172.9.0.23
            user: build
            port: 22
        linux:
            host: 172.9.0.24
            user: build
            port: 22
    commands: 
        - make

Checkout the specified branch and run the make command on all targeted machines.

### Pre and post commands

    commands: 
        - make
    prepare:
        - curl "https://api.hipchat.com/v1/rooms/message?room_id=10&from=Try&message=Trying [BRANCH] now!"
    success:
        - curl "https://api.hipchat.com/v1/rooms/message?room_id=10&from=Try&message=Atempt at [BRANCH] was a success :)"
    failure:
        - curl "https://api.hipchat.com/v1/rooms/message?room_id=10&from=Try&message=Atempt at [BRANCH] was a failure :("

Checkout the specified branch and run the make command on the local machine and notify us on Hipchat so we know what's happening in real time ^^
