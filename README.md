# Improving Your Workflow with Keanu



## Update your system prefs

You can optimise your machine to respond faster:

- System Preferences > Keyboard
- System Preferences > Trackpad





## Increase your typing speed

https://www.typingtest.com



| Geek              | Score |
| ----------------- | ----- |
| Sam Tate          | 69    |
| Andy Speirs       | 34    |
| Laura Moss        | 63    |
| Martin Hymers     | 38    |
| Sam Bunting       | 45    |
| Ben Ely           | 58    |
| Charlotte Gaskell | 45    |
| Babs Comoglio     | 39    |
| Alessandro Melcam | 32    |
| Bev Evans         | 39    |
| Josh Bowley       | 44    |
| Warren Perkins    | 47    |







## Command Line



The command line is our friend. Mac terminal is good but I like to use Hyper and iTerm is also good.

- Hyper (https://hyper.is)

- iTerm (https://www.iterm2.com)



### Commands

```
#list files in current directory
ls

#list files in current directory in long format
ls -l

#list all files in current directory in long format
ls -al
```

Explain shell is a great resource that explains each command-line :

https://explainshell.com/



You can customise and configure your terminal by editing any of the following dependant on your setup:

- .bash_profile
- .bashrc
- .zshrc (what I use - https://ohmyz.sh)



```
# edit or create .zshrc with macvim
mvim ~/.zshrc
```



### Bash Aliases

Aliases are __super easy__ to create and will increase your productivity. 

https://linuxize.com/post/how-to-create-bash-aliases/

Examples:

```
# move up a directory
alias ..='cd ..'

# move list all files in long format
alias ll='ls -al'

# remove folder "rm -rf foldername"
alias rf='rm -rf $1'

# open .zshrc in macvim
alias zsh='mvim ~/.zshrc'

# source .zshrc to reflect our customisation
alias soz='source ~/.zshrc'

# git add all
alias gaa='git add .'
```



### Bash Functions

Another __easy__ way to save time by avoiding writing the same code time and time again.

https://linuxize.com/post/bash-functions/

Examples:

```
# make directory and cd in "mcd foldername"
function mcd() {
	mkdir -p $1
	cd $1
}

# create a github repo "gr user repo" a readme and commit
function gr() {
	curl -u $1 https://api.github.com/user/repos -d "{ \"name\": \"$2\" }"
	echo "# $2" >> README.md
	git init
	git add README.md
	git commit -m "first commit"
	git remote add origin https://github.com/$1/$2.git
	git push -u origin master
}

# git commit and push
function gm() {
	git commit -am "$1" && git push
}
```





## Vim

[Vim](http://www.vim.org/) is an open-source and free clone of vi, a text-editor developed in 1976 by Bill Joy.



Below is a link to a comparison of text editors and you can see it outscores everything in sight:

https://en.wikipedia.org/wiki/Comparison_of_text_editors



### Install vim

https://www.vim.org

```
# install without IT verification using our friend brew
brew install vim

# open vim
vim
```



### Install macvim

https://macvim-dev.github.io/macvim/

```
# install macvim without IT verification using our friend brew
brew install macvim

# open macvim
mvim
```



### Useful commands

You can find the vim cheat sheet here:

https://vim.rtorr.com/



#### Normal mode

| Key  | Command             |
| :--- | ------------------- |
| i    | insert mode         |
| v    | visual mode         |
| V    | visual line mode    |
| esc  | exit to normal mode |

#### Exiting

| Key  | Command                               |
| ---- | ------------------------------------- |
| :w   | write (save) the file, but don't exit |
| :wq  | write (save) and quit                 |
| :q   | quit                                  |

#### Cursor movement

| Key  | Command                          |
| ---- | -------------------------------- |
| h    | cursor left                      |
| j    | cursor down                      |
| k    | cursor up                        |
| l    | cursor right                     |
| H    | move to top of screen            |
| M    | move to the middle of the screen |
| L    | move to the bottom of the screen |
| $    | move to the end of the line      |
| 0    | move to the start of the line    |

#### Cut and paste

| Key  | Command                   |
| ---- | ------------------------- |
| yy   | yank (copy) a line        |
| dd   | delete (cut) a line       |
| p    | put (paste) before cursor |

#### Working with multiple files

| Key                  | Command                                                 |
| -------------------- | ------------------------------------------------------- |
| :sp file (optional)  | open a file in a new buffer and split window            |
| :vsp file (optional) | open a file in a new buffer and vertically split window |
| :bd                  | delete a buffer (close a file)                          |
| Ctrl + wh            | move cursor to the left window (vertical split)         |
| Ctrl + wl            | move cursor to the right window (vertical split)        |
| Ctrl + wj            | move cursor to the window below (horizontal split)      |
| Ctrl + wk            | move cursor to the window above (horizontal split)      |
| Ctrl + w \|          | expand current window (vertical split)                  |
| Ctrl + w =           | equalise windows (vertical split)                       |



### vimrc - the ultimate configuration

Vim really is the ultimate when it comes to configuration. You can basically customise it to absolutely fit your needs. You can use the ~/.vimrc file to add settings, key mappings and custom commands.

```
# open vimrc file
vim ~/.vimrc
```



### Making vim nicer

As with all editors we want to make them nice. Example theme:

https://github.com/gosukiwi/vim-atom-dark

```
# if you don't have wget
brew install wget

# cd into the vim directory, if you don't have it then create it
cd ~/.vim

# make a new colors directory
mkdir colors
cd colors

# get the colors vim file
wget https://raw.githubusercontent.com/gosukiwi/vim-atom-dark/master/colors/atom-dark.vim

# update vimrc
,eq

colorscheme atom-dark

# source the current file to reflect your updated vimrc
:so %
```



### Example vimrc file:

```
syntax enable

let mapleader = ','	"The default leader is \, but a comma is better
set number		"Activate line numbers

"-------------Visuals-------------

colorscheme atom-dark
set linespace=12
set tabstop=4

set guioptions-=l
set guioptions-=L
set guioptions-=r
set guioptions-=R

"-------------Search-------------

set hlsearch
set incsearch

"-------------Split Management-------------

set splitbelow
set splitright

nmap <C-J> <C-W><C-J>
nmap <C-K> <C-W><C-K>
nmap <C-H> <C-W><C-H>
nmap <C-L> <C-W><C-L>

"-------------Mappings------------

"Make it easy to edit the vimrc file
nmap <Leader>ev :tabedit $MYVIMRC<cr>

"Add search higlight removal
nmap <Leader><space> :nohlsearch<cr>


"-------------Auto-Commands-------------

"Automatically source the vimrc file

augroup autosourcing
	autocmd!
	autocmd BufWritePost .vimrc source %
augroup END
```



### Vim Plugins

This is best done with a plugin in manager such as Vundle (https://github.com/VundleVim/Vundle.vim).

```
git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim
```

### Vim Resources
[Become a Html Ninja with Emmet for Vim](https://medium.com/vim-drops/be-a-html-ninja-with-emmet-for-vim-feee15447ef1)



## Docker



### Commands

__docker__: spin up containers and control them, docker daemon running with API and mechanism to control the lifecycle of containers

__docker-compose__: utility to control starting, stopping and the lifecycle of multiple containers. Including setup of shared volumes, networks and connecting containers so they can communicate with each other (eg application talking to DB).

__docker-machine__: spin up containers on cloud (AWS etc.) that appear to run locally via commands



### Docker commands

```
#show all running containers
docker ps
#show all containers running and stopped
docker ps -a
#shows all images
docker images
```



### Your first container

```
#get ubuntu from docker and list the current directory
docker run ubuntu:16.04 ls -lah

#inspect containers metadata
docker inspect container_name_or_id

#finds all items in range and targets .NetworkID and outputs json
docker inspect --format="{{range .NetworkSettings.Networks}}{{.NetworkID}}{{end}}" container_name_or_id 
```



### Install jq

Installing jq provides a much more readable output

```
brew install jq

#pipe output to jq for a more readable json output
docker inspect container_name_or_id | jq

#-r parses the json output
docker inspect container_name_or_id | jq -r '.[0].NetworkSettings'
```



### Cleaning up

```
#removes container
docker rm container_name_or_id

#list all containers by containerID
docker ps -aq

#bash trick to delete all containers
docker rm $(docker ps -aq)

#runs container then removes
docker run --rm ubuntu:16.04 echo "Hello world"

#removes docker image
docker rmi container_name_or_id
```



### Interacting with a container

```
# Gives us input and output for the container
docker run -it ubuntu:16.04 bash

# Print working directory
pwd

# check processes running
ps aux

# Exit bash
exit

# Stop container
docker stop container_name_or_id

docker start -a container_name_or_id #because we've already run docker with bash - it starts in bash
```



### Nginx and sharing ports

```
# Start container with port 8888 forwarding to 80 in container
docker run -it -p 8888:80 ubuntu:16.04 bash

# Install Nginx
apt-get update && apt-get install -y nginx

which nginx

# localhost:8888 will go to the default nginx homepage in the container
nginx
```



### Sharing volumes

```
mkdir dockertest

cd dockertest

echo "We love Docker" >> index.html

docker run -it -p 8888:80 -v ~/Sites/dockertest:/var/www/html ubuntu:16.04 bash

# Install Nginx
apt-get update && apt-get install -y nginx

nginx

px aux

#browse to localhost:8888 and see your file
```



### Committing changes

```
# Spin up a new container
docker run -it ubuntu:16.04 bash

# Install Nginx
apt-get update && apt-get install -y nginx

# Exit container
exit

# Verify it has stopped
docker ps -a

# See differences
docker diff container_name_or_id

# Get the help menu
docker commit -h

# Commit our changes (installing Nginx)
docker commit -a "Jonny Frodsham" -m "Installed nginx" container_name_or_id jonnyfrodsham/nginx:0.1.0

# See our new image
docker images

# Create a new index.html file
echo "We love Docker" > index.html

# Spin up a container from the new image
docker run -it -p 8888:80 -v $(pwd):/var/www/html jonnyfrodsham/nginx:0.1.0 nginx

# Edit the image to set Nginx to no longer daemonize
docker run -it -p 8888:80 -v $(pwd):/var/www/html jonnyfrodsham/nginx:0.1.0 bash

echo "daemon off;" >> /etc/nginx/nginx.conf
exit

docker commit -a "Jonny Frodsham" -m "Nginx no longer daemonizes" container_name_or_id jonnyfrodsham/nginx:0.2.0

# Container runs in forgeround
docker run -it -p 8888:80 -v $(pwd):/var/www/html jonnyfrodsham/nginx:0.2.0 nginx

# Or put the container to the background with `-d`
docker run -d -it -p 8888:80 -v $(pwd):/var/www/html jonnyfrodsham/nginx:0.2.0 nginx

# See the history of an image
docker history jonnyfrodsham/nginx:0.2.0
```



### The Dockerfile

```
mkdir nginx
cd nginx
vim Dockerfile

# Add the following to the Dockerfile
FROM ubuntu:16.04

MAINTAINER Jonny Frodsham

RUN apt-get update && apt-get install -y nginx \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
    && echo "daemon off;" >> /etc/nginx/nginx.conf

CMD ["nginx"]

# Use docker build command to build the image
docker build -t jonnyfrodsham/nginx:0.1.0 .

# Run a new container from the image
docker run -d -p 8888:80 -v $(pwd)/../:/var/www/html jonnyfrodsham/nginx:0.1.0
```



### Building a PHP image

```
# Make php folder in dockertest
mkdir php
cd php
vim Dockerfile

# Add the following to the Dockerfile

FROM ubuntu:16.04

MAINTAINER Jonny Frodsham

RUN apt-get update \
    && apt-get install -y locales \
    && locale-gen en_US.UTF-8

ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

RUN apt-get update \
    && apt-get install -y curl zip unzip git software-properties-common \
    && add-apt-repository -y ppa:ondrej/php \
    && apt-get update \
    && apt-get install -y php7.0-fpm php7.0-cli php7.0-mcrypt php7.0-gd php7.0-mysql \
       php7.0-pgsql php7.0-imap php-memcached php7.0-mbstring php7.0-xml php7.0-curl \
    && php -r "readfile('http://getcomposer.org/installer');" | php -- --install-dir=/usr/bin/ --filename=composer \
    && mkdir /run/php \
    && apt-get remove -y --purge software-properties-common \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

ADD php-fpm.conf /etc/php/7.0/fpm/php-fpm.conf
ADD www.conf /etc/php/7.0/fpm/pool.d/www.conf

# Use docker build command to build the image
docker build -t jonnyfrodsham/php:0.1.0 .

docker run --rm -it jonnyfrodsham/php:0.1.0 php -v
docker run --rm -it jonnyfrodsham/php:0.1.0 composer -h
docker run --rm -it jonnyfrodsham/php:0.1.0 which php-fpm7.0
```



### Linking Nginx & PHP containers

```
# Make application folder in dockertest
mkdir -p application/public
echo "<?php phpinfo();" > application/public/index.php

# Use docker build command to build the image
docker build -t jonnyfrodsham/nginx:0.2.0 .

# Spin up PHP, naming the container "myphp"
docker run -d --name=myphp -v $(pwd)/application:/var/www/html jonnyfrodsham/php:0.1.0

# Spin up Nginx, linking the container "myphp" and aliasing it to "php"
# so the hostname "php" resolves to the IP address of the "myphp" container
docker run -d --link=myphp:php -p 8888:80 -v $(pwd)/application:/var/www/html jonnyfrodsham/nginx:0.2.0
```



### Full stack

```
# Nginx (80:80) --> PHP-FPM (--name, --link)  -> Redis/MySQL (--name, --link)

# Data containers. These don't link to anything 
# as they don't need to communicate externally to other containers.
docker run -d --name=redis redis:alpine

docker run -d --name=mysql \
    -e MYSQL_ROOT_PASSWORD=root \
    -e MYSQL_DATABASE=my-app \
    -e MYSQL_USER=app-user \
    -e MYSQL_PASSWORD=app-pass \
    mysql:5.7

# The PHP container links to the data containers
docker run -d --name=php \
    --link=redis:redis \
    --link=mysql:mysql \
    -v $(pwd)/application:/var/www/html \
    jonnyfrodsham/php:0.1.0
    
# The Nginx container links to the PHP container
# (It only communciates to the php container, no db or redis)
docker run -d  --name=nginx \
    --link=php:php \
    -p 8888:80 \
    -v $(pwd)/application:/var/www/html \
    jonnyfrodsham/nginx:0.2.0
```



### Docker networking

```
# Redis
docker run -d --name=redis --network=jf-net redis:alpine

# MySQL
docker run -d --name=mysql \
    --network=jf-net \
    -e MYSQL_ROOT_PASSWORD=root \
    -e MYSQL_DATABASE=my-app \
    -e MYSQL_USER=app-user \
    -e MYSQL_PASSWORD=app-pass \
    mysql:5.7

# PHP
docker run -d --name=php \
    --network=jf-net \
    -v $(pwd)/application:/var/www/html \
    jonnyfrodsham/php:0.1.0

# Nginx
docker run -d  --name=nginx \
    --network=jf-net \
    -p 8888:80 \
    -v $(pwd)/application:/var/www/html \
    jonnyfrodsham/nginx:0.2.0
```



### Docker volumes

```
docker stop $(docker ps -aq)
docker rm $(docker ps -aq)

docker volume rm $(docker volume ls -q)

# Create a new volume, giving it a name
docker volume create --driver=local --name=mysqldata

# See that it exists (and is empty at this point)
docker run --rm -it -v /:/vm-root alpine:latest ls -lah /vm-root/var/lib/docker/volumes/mysqldata/_data

# Redis
docker run -d --name=redis --network=jf-net redis:alpine

# MySQL
docker run -d --name=mysql \
    --network=jf-net \
    -v mysqldata:/var/lib/mysql \
    -e MYSQL_ROOT_PASSWORD=root \
    -e MYSQL_DATABASE=my-app \
    -e MYSQL_USER=app-user \
    -e MYSQL_PASSWORD=app-pass \
    mysql:5.7

# PHP
docker run -d --name=php \
    --network=jf-net \
    -v $(pwd)/application:/var/www/html \
    jonnyfrodsham/php:0.1.0

# Nginx
docker run -d  --name=nginx \
    --network=jf-net \
    -p 8888:80 \
    -v $(pwd)/application:/var/www/html \
    jonnyfrodsham/nginx:0.2.0
    
# We should now see MySQL database content
docker run --rm -it -v /:/vm-root alpine:latest ls -lah /vm-root/var/lib/docker/volumes/mysqldata/_data


docker exec -it mysql bash

> mysql -u root -p
> show databases;
```



### Docker Compose

```
docker-compose -h

# docker-compose.yml

version: '2'
services:
  nginx:
    image: jonnyfrodsham/nginx:0.2.0
    ports:
     - "80:80"
    volumes:
     - ./application:/var/www/html
    networks:
     - jf-net
  php:
    image: jonnyfrodsham/php:0.1.0
    volumes:
     - ./application:/var/www/html
    networks:
     - jf-net
  redis:
    image: redis:alpine
    networks:
     - jf-net
  mysql:
    image: mysql:5.7
    ports:
     - "3306:3306"
    environment:
      MYSQL_ROOT_PASSWORD: root
      MYSQL_DATABASE: my-app
      MYSQL_USER: app-user
      MYSQL_PASSWORD: app-pass
    volumes:
     - mysqldata:/var/lib/mysql
    networks:
     - jf-net
networks:
  sd-net:
    driver: "bridge"
volumes:
  mysqldata:
    driver: "local"
```



### Serving an application

```
# Delete our test application 
rm -rf application/*

# Create a new laravel application
docker run -it --rm \
    -v $(pwd):/opt \
    -w /opt \
    --network=dockertest_jf-net \
    jonnyfrodsham/php:0.1.0 \
    composer create-project laravel/laravel application

docker run -it --rm \
    -v $(pwd)/application:/opt \
    -w /opt \
    --network=dockertest_jf-net \
    jonnyfrodsham/php:0.1.0 \
    composer require predis/predis
    
docker run -it --rm \
    -v $(pwd)/application:/opt \
    -w /opt \
    --network=dockertest_jf-net \
    jonnyfrodsham/php:0.1.0 \
    php artisan make:auth
    
docker run -it --rm \
    -v $(pwd)/application:/opt \
    -w /opt \
    --network=dockertest_jf-net \
    jonnyfrodsham/php:0.1.0 \
    php artisan migrate
```



### Building images with Docker Compose

```
#Build Docker images from local resources instead of attempting to grab from an already existing image

version: '2'
services:
  nginx:
    build: ./nginx
    ports:
     - "8888:80"
    volumes:
     - ./application:/var/www/html
    networks:
     - sd-net
  php:
    build: ./php
    volumes:
     - ./application:/var/www/html
    networks:
     - sd-net
  redis:
    image: redis:alpine
    networks:
     - sd-net
  mysql:
    image: mysql:5.7
    environment:
      MYSQL_ROOT_PASSWORD: root
      MYSQL_DATABASE: my-app
      MYSQL_USER: app-user
      MYSQL_PASSWORD: app-pass
    volumes:
     - mysqldata:/var/lib/mysql
    networks:
     - sd-net
networks:
  sd-net:
    driver: "bridge"
volumes:
  mysqldata:
    driver: "local"
```



## Misc stuff

Other useful stuff to check out:

Use 'trash' command to delete things in the terminal - not `rm` or `rm -rf`

https://formulae.brew.sh/formula/trash

```bash
$ brew install trash
```

Terminal based file browser: `nnn`

https://formulae.brew.sh/formula/nnn#default

```bash
$ brew install nnn
```

## OSX

Keyboard shortcuts:

https://support.apple.com/en-gb/HT201236

__⌘ + k__ - clear console

__⌘ + ⌃ + space__ - open character viewer

__⇧ ⌘ 3__ - Screen capture

__⇧ ⌘ 4__ - Cropped screen capture

⇧ ⌘ __5__ -  Screen capture or screen recording





## VS Code

Keyboard shortcuts:

https://code.visualstudio.com/shortcuts/keyboard-shortcuts-macos.pdf

Customising VS Code:

https://code.visualstudio.com/docs/introvideos/configure





## Flycut

Clipboard manager for developers:

https://github.com/TermiT/Flycut