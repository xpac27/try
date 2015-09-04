# try

A dead simple and freaking easy to use continuous integration service.

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
