# Introduction
This will install pimcore with several docker images running in parallel.
The database content is not 'safe' by default, is stored inside a container (the mysql container) and thus the data is gone when you delete the container. To change this, you need to change the 'docker-compose.yml' file (potentially we will add more infos on this in the future).
The application by default will be reachable on localhost at port 80.

# Preconditions for mac users
You must install the 'brew' package manager to be able to use a bunch tools, such as python3:
 
## Download brew itself
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
 
## Install python 3
brew install python3
brew install coreutils
brew install tmux

# First steps
Since you already downloaded this repo, then you actually already made the first step :-).
After that you will need to consider the following steps:
- Prepare a directory where pimcore is installed, this tool-set considers the installation to be outside this directory inside '../pimcore'.
- Prepare an installation of pimcore. For example execute the pimcore sample installation as described below.
- Prepare the database.
- Execute the 'install-pimcore' helper function to have an admin user.

# Execute the command shell in which you can control pimcore, docker and the universe
Execute in this docker folder to be able to run python helper commands provided in this repository.
This basically sets up a shell in which you can work with pimcore and its tools now:

./environment screen

This create a default configuration and store is it in a config file called '.env'. This file is not visible. To see its content, execute 'cat .env' in the base folder (compose-pimcore).

# Install pimcore locally, outside of docker, on your disk
The above script sends you to your install directory automatically, execute 'pwd' to check!
If you want that to be a different repository, you need to change it in the '.evn' file located under the original 'compose-pimcore' directory (As described above). Note that the file is hidden and thus not visible in your terminal/finder.
Execute composer commands to install pimcore, the below install a demo only:

COMPOSER_MEMORY_LIMIT=3G composer create-project pimcore/demo-ecommerce .

# execute composer commands to install web2print tools
Pimcore comes quite bare-bone and you will need to install the web2print extensions to make use of web2print. To do this, you will use the PHP package manager that can add and remove features to your local pimcore installation. Note that you need the './environment screen' to be executed to run this, otherwise the 'composer' tools are not available in your shell.

composer require pimcore/web2print-tools-bundle

# Start the actual docker runtime and pimcore linux environment
Now you will download all required docker images and start the containers that will run pimcore. The images already contain a version of pimcore installed with all required dependencies from PHP and the database as well as an nginx web service:

run up

Every time you kill the docker runtime, you can then do the following steps to get you pimcore back up running:

1) Execute the './environment screen' again
2) Execute the 'run up' again.

# Install the database
This executes a python script that installs the base DB for pimcore. You can execute this again to flatten the DB if you need to:

create_db pimcore

# Install pimcore users/permission basics
This actually now sets up pimcore itself and updates users/permissions etc:

install-pimcore

# Setup the web2print tools to make use of the local PDFreactor service running

Under settings in your pimcore installation, you need to enter the server where the web2print is running. For this installation you need:
- version is '9.0'
- server is 'pdfreactor'
- port is 9423
- protocol is 'http' (not https)
- License: <enter your license from the PDFreactor website>

All other fields can remain empty.
