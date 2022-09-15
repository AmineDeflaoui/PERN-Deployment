# Full Stack Web Application (PERN) Deployment

## 1.Domain Purchase:
#### Purchase domain from Name cheap.
#### Purchase mail service from Name cheap.
#### Connect to mail service.
#### Connect to web Mail in privateemail.com.

## 2.Mail Jet Setup:
#### Link domain with mail jet by creating a TXT Record.
#### Host: default._domainkey
#### Set up SPF record and DKIM authentication.
#### For SPF -> Host: theclassmap.com.
#### Fix SPF/KDIM issues by replacing host value with @ and remove .theclassmap. from DKIM host.

## 3.Digital Ocean Setup:
#### Link PayPal with account.
#### Receive 100$.
#### Create a Droplet.
#### Install Putty, generate ssh private key. By putty Gen.
#### open puttyGen in your system and generate and ssh key also don’t forget to RSA option.
#### After generating key, you can save public and private key in your system and also copy public key and paste in droplet Authentication section.
#### Select Session and paste your droplet ip address and select SSH radio button.
#### Connection -> SSH -> Auth and then browse your saved private ssh key.
#### Now let’s save your configuration, give it a name and click on save, now you are ready to login.
#### Connect to ssh.
#### Give passphrase if you have given any while creating ssh key.

## 4.Initial Server Setup:
    ssh root@your_server_ip
#### Once you are logged in as root, we’re prepared to add the new user account that we will use to log in from now on.
    adduser sammy
#### Now, we have a new user account with regular account privileges. However, we may sometimes need to do administrative tasks.
#### To avoid having to log out of our normal user and log back in as the root account, we can set up what is known as “superuser” or root privileges for our normal account. #### This will allow our normal user to run commands with administrative privileges by putting the word sudo before each command.
#### To add these privileges to our new user, we need to add the new user to the “sudo” group. 
#### By default, on Ubuntu 16.04, users who belong to the “sudo” group are allowed to   use the sudo command.
    usermod -aG sudo Sammy
#### Set Up a Basic Firewall
#### Ubuntu 16.04 servers can use the UFW firewall to make sure only connections to certain services are allowed.
#### We can set up a basic firewall very easily using this application.
Different applications can register their profiles with UFW upon installation.
#### These profiles allow UFW to manage these applications by name. OpenSSH, the service allowing us to connect to our server now, has a profile registered with UFW.
    sudo ufw app list.
#### We need to make sure that the firewall allows SSH connections so that we can log back in next time. We can allow these connections by typing:
    sudo ufw allow OpenSSH
#### 
    sudo ufw allow ssh
#### 
    sudo ufw allow http
#### 
    sudo ufw allow https
#### Afterwards, we can enable the firewall by typing:
    sudo ufw enable
#### Type “y” and press ENTER to proceed. You can see that SSH connections are still allowed by typing:
    sudo ufw status
#### Once you are logged in within the System then update and upgrade your system by using Linux command
    apt-get update && apt-get upgrade
#### 
    source ~/.profile
#### Install node using nvm (Node Virtual Manager)
    curl https://raw.githubusercontent.com/creationix/nvm/master/install.sh | bash
#### 
    nvm ls-remote
#### 
    nvm install v0.0.0
#### 
    nvm use v0.0.0
#### 
    cd /home
#### We are working inside /home because Nginx will not have permissions to access files in root folder.
#### Install Git.
    sudo apt-get install git
#### Install PM2:
    npm i -g pm2
#### PM2 is a production process manager for Node.js applications (with a built-in load balancer). Simply, allows you to keep node applications alive forever.
#### Deleting apache server
    Systemctl stop apache2
#### 
    Systemctl disable apache2
#### 
    Apt remove apache2
#### To delete related dependencies:
    Apt autoremove
#### 
    apt clean all && sudo apt update
#### Install Nginx:
    sudo apt-get install nginx -y
#### 
    sudo systemctl enable nginx
#### verify nginx status
    systemctl status nginx
#### Nginx is open source high-performance HTTP Server. It is one of the most popular web server because it is known for its stability, high performance, simple configuration.

## 5.About My App:
#### My node.js is running on port 3001 and react application is running on port 3000.
Upload your frontend and backend source code to GitHub repository.
## 6.Application cloning:
### a.Node.js:
#### Clone your backend project from GitHub.
    git clone https://github.com/backend-app.
#### Go inside the folder and install dependencies.
    cd backend-app && npm install
### b.React.js:
#### Clone your frontend project from GitHub.
    git clone https://github.com/ frontend-app
#### Go inside the folder and install the required dependencies.
    cd frontend-app && npm install
#### Let’s bundle our code for production using this command.
#### Checking the System for Swap Information
    sudo swapon -show
#### You can verify that there is no active swap using the free utility
    free -h
#### Checking Available Space on the Hard Drive Partition
    df -h
#### Creating a Swap File
    sudo fallocate -l 1G /swapfile
#### We can verify that the correct amount of space was reserved by typing
    ls -lh /swapfile
#### Enabling the Swap File
    sudo chmod 600 /swapfile
#### Verify the permissions change by typing:
    ls -lh /swapfile
#### We can now mark the file as swap space by typing:
    sudo mkswap /swapfile
#### we can enable the swap file, allowing our system to start utilizing it:
    sudo swapon /swapfile
#### 
    sudo swapon -show
#### 
    free -h
#### Making the Swap File Permanent
    sudo cp /etc/fstab /etc/fstab.bak
#### Add the swap file information to the end of your /etc/fstab file by typing:
    echo '/swapfile none swap sw 0 0' | sudo tee -a /etc/fstab
#### Tuning your Swap Settings
    cat /proc/sys/vm/swappiness
#### 
    sudo sysctl vm.swappiness=10
#### This setting will persist until the next reboot. We can set this value automatically at restart by adding the line to our /etc/sysctl.conf file:
    sudo nano /etc/sysctl.conf
#### 
    vm.swappiness=10
#### Adjusting the Cache Pressure Setting
    cat /proc/sys/vm/vfs_cache_pressure
#### 
    sudo sysctl vm.vfs_cache_pressure=50
#### 
    sudo nano /etc/sysctl.conf
#### 
    vm.vfs_cache_pressure=50
#### **IF Node.js heap out of memory**
#### you want to increase the memory usage of the node globally - not only single script, you can export environment variable, like this:
    export NODE_OPTIONS=--max_old_space_size=4096
#### 
    npm run build

## 7.Hosting Application
#### Hosting node.js application using PM2
#### Before hosting your node.js application let’s check if the API is working fine.
#### I am running my app using npm start because I am using express-generator. You can run node app.js also.  
    cd backend-app && npm start
#### If It’s working fine, then move to the next step.
#### It’s time to use our process management tool (PM2).
    cd backend-app
#### 
    pm2 start /folder/folderapp.js –name [name]
#### Now, pm2 will keep your application alive.
#### to stop process :
    pm2 stop [name | id]
#### to show status :
    pm2 status
#### to delete :   
    pm2 delete [name | id] 
#### Configure PM2 to automatically startup the process after a reboot
    pm2 startup
#### it will come back with a response as a command as follows:
    sudo env PATH=$PATH:/usr/bin /usr/lib/node_modules/pm2/bin/pm2 startup systemd -u ubuntu --hp /home/ubuntu
#### to take a snapshot therefor remember processes :
    pm2 save
## 8.Deploying React.js application using Nginx
#### As we have already done npm run build.
    npm install
#### We just need to configure NGINX.
    cd /etc/nginx/sites-available/
#### 
    sudo cp default theclassmap.com
#### 
    nano theclassmap.com
#### Cut out all lines with Ctrl+K. and copy this code there with your IP Address.
    server {
    listen 80;
    listen [::]:80;

    root /home/amine/theclassmap/Client-The-ClassMap/build;

    index index.html index.htm index.nginx-debian.html;

    server_name theclassmap.com www.theclassmap.com;

    location / {
    try_files $uri /index.html;
    }

    location /API {
    proxy_pass http://localhost:3001;
    proxy_http_version 1.1;
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection 'upgrade';
    proxy_set_header Host $host;
    proxy_cache_bypass $http_upgrade;
    }
    }
#### server_name will be your dropletIP for which it will listen for requests.
#### then I am checking If there is any match for /api in the request, then forward the request to localhost:3001/ where our node.js server is running.
#### Otherwise map the url to the file(index.html) located at /home/frontend-app/dist/
#### Enable the new site
    sudo ln -s /etc/nginx/sites-available/theclassmap.com /etc/nginx/sites-enabled/
#### Test and Reload Nginx
#### First of all, check if the configurations are valid.
    sudo nginx -t
#### Check if the test is successful.
#### Let’s reload Nginx
    sudo systemctl restart nginx
#### Now It’s time to verify if our server is working or not.
## 9.Add a domain to Digital Ocean
#### Enter the domain name that you own below and start managing your DNS.
#### Create A record
#### Host: @
#### Direct to: choose project 
#### Host: www
#### Direct to: choose project
#### Go to name cheap change name servers to 
    ns1.digitalocean.com
#### 
    ns2.digitalocean.com
#### 
    ns3.digitalocean.com
## 10.Set up Database
    sudo apt install postgresql postgresql-contrib -y
#### Use psql to enter DB (error FATAL role root does not exist)
#### See all the user on local machine.
    sudo cat /etc/passwd
#### Switch to postgres user
    sudo -i -u postgres
####     
    psql
#### For this tutorial, the node process will be run under the ubuntu user and for the sake of simplicity, an ubuntu user will be created on Postgres as well. If you want to use a different user feel free to create a different user in postgres.
#### To create a Postgres user run the following command which will give an interactive prompt for configuring the new user. For the sake of simplicity, the ubuntu user will be a superuser, which is the equivalent of being a root user on Linux.
#### The super user will have the ability to create/delete/modify databases and users.
#### Stay as postgres user to preform:
    createuser --interactive
#### to see DB users and their roles
    \du
#### To log in as user to psql use following syntax because postgres uses normally the user name the same as database so psql will access postgres database that’s why we use following syntax:
    psql -d postgres
####     
    \conninfo
#### To create a password for db user
    ALTER USER ubuntu PASSWORD 'password';
#### 
    Create database name;
#### As with most sql database PostgreSQL allows us to easily copy our database schema and data from our local development postgres instance and copy it over to the Postgres instance running in our production server.
    pg_dump -U postgres -f theclassmap.pgsql -C theclassmap
#### The -U flag specifies the user u want to login as, if you are using a different username, update it accordingly. The -f yelp.pgsql flag will write the database schema and data to a file called yelp.pgsql in the current directory -C flag add the create database command to the file as well yelp is the name of the database in our local dev server that we want to dump. If your database is called something else update that accordingly. If you leave out the database name altogether it will dump all databases.
#### Copy the yelp.pgsql file to the production server
#### If path to pem file exists add it, else just remove -i path
    scp -i [path to pem file] [path to yelp.pgsql] username@[server-ip]:[directory to copy file to]
#### In this example the pem file and yelp.gsql file are located in the current directory and my server ip is 1.1.1.1 and the username is Ubuntu
#### Import the database schema & data from the yelp.pgsql file
    psql theclassmap < /home/amine/theclassmap/theclassmap.pgsql
#### to list all databases :
    \l
#### connect to db :
    \c dbName
#### create a password :
\password
#### exit a db :
    \q
## 11.Setup Https with ssl let’s Encrypt
#### Run this command on the command line on the machine to install Certbot.
    sudo snap install --classic certbot
#### Execute the following instruction on the command line on the machine to ensure that the certbot command can be run.
    sudo ln -s /snap/bin/certbot /usr/bin/certbot
#### Choose how you'd like to run Certbot
#### Either get and install your certificates...
#### Run this command to get a certificate and have Certbot edit your nginx configuration automatically to serve it, turning on HTTPS access in a single step.
    sudo certbot --nginx
## 12.Configure Environment Variables
#### We now need to make sure that all of the proper environment variables are setup on our production Ubuntu Server. In our development environment, we made use of a package called dotenv to load up environment variables. In the production environment the environment variables are going to be set on the OS instead of within Node.
#### Create a file called .env in /home/ubuntu/. The file does not need to be named .env and it does not need to be stored in /home/ubuntu, these were just the name/location of my choosing. The only thing I recommend avoid doing is placing the file in the same directory as the app code as we want to make sure we don't accidentally check our environment variables into git and end up exposing our credentials.
    source .env
    printenv 
#### You'll notice I also set 
    NODE_ENV=production
#### Although it’s not required for this example project, it is common practice. For many other projects (depending on how the backend is setup) they may require this to be set in a production environment.
#### In the /root/.profile add the following line to the bottom of the file
    set -o allexport; source /home/amine/theclassmap/.env; set +o allexport
#### For these changes to take effect, close the current terminal session and open a new one.
#### Verify that the environment variables are set by running the printenv

