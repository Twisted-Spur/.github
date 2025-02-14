## Twisted Spur
### Company Mission
Twisted Spur is a small business specializing in customized T-shirts, cups, hats, etc.  In addition, it offers other various types of brand clothing and accessories.  It strives to make strong connections with each customer across every sale made.  This is a small town business that just simply loves the work it does to make its customers happy.

### What does Github have anything to do with this?
This github organization owner, Gerrid Rose, is the son in law of the actual company owner of Twisted Spur.  He saw an opportunity to further his development skills by working on an e-commerce site for Twisted Spur, whether it ever got to production or not, it would at least be a good experience builder, starting this work during my second child's birth while on paternity leave.  Working in the defense industry, all of my work is hidden from potential external recruiters.  These companies that I may want to apply for, I would like to be able to at least offer some concrete examples of how I work.

### Contribution Guidelines
Anyone's inputs on the work done within any of these repos are welcome feedback and anyone can contribute.

## Deployment Notes
### Microsoft Azure
1. Create PostgresSQL Flex Server instance
2. Create Ubuntu 20.04 LTS VM instance (in same resource group)
    1. Configure SSH access via private key to VM
        1. ssh-add C:/Users/{username}/.ssh/{private_key} (or wherever you put the key)
        2. If needed run ssh-keygen -R hostname to remove previous records from known_hosts file 
    2. ssh into VM
    3. # Add the AdoptOpenJDK repository
    sudo apt update
    sudo apt install -y wget apt-transport-https
    wget -qO - https://packages.adoptium.net/artifactory/api/gpg/key/public | sudo apt-key add -
    echo "deb https://packages.adoptium.net/artifactory/deb $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/adoptium.list

    # Update the package list
    sudo apt update

    # Install Temurin JRE 21
    sudo apt install -y temurin-21-jre
    4. sudo update-alternatives --config java
    5. java -version (to confirm JRE 21 default)
    6. scp ts-services over and run
    7. Set TS_POSTGRES_PW and other envvars needed before services start in /etc/environment.
    8. Start services.
    7. npm run build ts-client
    8. scp ./dist/* to client-dist/
    9. Set up NGINX to host client-dist/
        1. sudo apt install nginx
        2. sudo systemctl start nginx
        3. sudo systemctl enable nginx
        4. cp ts-client/nginx/twistedspur to /etc/nginx/sites-available/twistedspur
        5. sudo ln -s /etc/nginx/sites-available/twistedspur /etc/nginx/sites-enabled/
        6. sudo nginx -t
        7. sudo systemctl reload nginx
    10. Go to http://twistedspur.centralus.cloudapp.azure.com/ in web browser.
        * If any access issues occur, review VM ports in Azure Portal.
