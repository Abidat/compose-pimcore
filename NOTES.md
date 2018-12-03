# First steps
Since you already downloaded this repo, then you actually already made the first step :-).
After that you will need to consider the following steps:
- Prepare a directory where pimcore is installed
- Prepare an installation of pimcore
-- For example execute the pimcore sample installation:
- Prepare the database installer
- Execute the 'install-pimcore' helper function

# execute in this docker folder to be able to run python helper commands:
./environment screen

# execute composer commands to install pimcore
COMPOSER_MEMORY_LIMIT=3G composer create-project pimcore/demo-ecommerce .

# execute composer commands to install web2print tools:
composer require pimcore/web2print-tools-bundle

# Preconditions for mac users
You must install the 'brew' package manager to be able to use a bunch tools, such as python3:

## Download brew itself
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

## Install python 3
brew install python3
