## Twisted Spur
### Company Mission
Twisted Spur is a small business specializing in customized T-shirts, cups, hats, etc.  In addition, it offers other various types of brand clothing and accessories.  It strives to make strong connections with each customer across every sale made.  This is a small town business that just simply loves the work it does to make its customers happy.

### What does Github have anything to do with this?
This github organization owner, Gerrid Rose, is the son in law of the actual company owner of Twisted Spur.  He saw an opportunity to further his development skills by working on an e-commerce site for Twisted Spur, whether it ever got to production or not, it would at least be a good experience builder, starting this work during my second child's birth while on paternity leave.  Working in the defense industry, all of my work is hidden from potential external recruiters.  These companies that I may want to apply for, I would like to be able to at least offer some concrete examples of how I work.

### Contribution Guidelines
Anyone's inputs on the work done within any of these repos are welcome feedback and anyone can contribute.

## Development Notes

### Self-signed Certificate Creation
A self signed cert can be created with openssl with the following command:

```openssl req -x509 -newkey rsa:4096 -sha256 -days 3650 -keyout twistedspur.com.key -out twistedspur.com.crt -subj "//CN=twistedspur.com"   -addext "subjectAltName=DNS:twistedspur.com,DNS:twistedspur.*.com,DNS:localhost,IP:127.0.0.1,IP:::1"```

## Deployment Notes

### Microsoft Azure Deployment
1. Create PostgresSQL Flex Server instance
2. Create Ubuntu 20.04 LTS VM instance (in same resource group)
    1. Configure SSH access via private key to VM
        1. ssh-add C:/Users/{username}/.ssh/{private_key} (or wherever you put the key)
        2. If needed run ssh-keygen -R hostname to remove previous records from known_hosts file 
    2. ssh into VM
    3. Add the AdoptOpenJDK repository
        1. ```sudo apt update```
        2. ```sudo apt install -y wget apt-transport-https```
        3. ```wget -qO - https://packages.adoptium.net/artifactory/api/gpg/key public | sudo apt-key add -```
        4. ```echo "deb https://packages.adoptium.net/artifactory/deb $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/adoptium.list```
    4. Update the package list
        - ```sudo apt update```
    5. Install Temurin JRE 21
        1. ```sudo apt install -y temurin-21-jre```
        2. ```sudo update-alternatives --config java```
        3. ```java -version (to confirm JRE 21 default)```
    6. Use ```scp``` to move ts-services over to VM and run
    7. Set TS_POSTGRES_PW and other envvars needed before services start in /etc/environment.
    8. Start services.
    7. ```npm run build ts-client```
    8. ```scp ./dist/*``` to ```client-dist/``` on VM
    9. Set up NGINX to host client-dist/
        1. ```sudo apt install nginx```
        2. ```sudo systemctl start nginx```
        3. ```sudo systemctl enable nginx```
        4. ```cp ts-client/nginx/twistedspur to /etc/nginx/sites-available/twistedspur```
        5. ```sudo ln -s /etc/nginx/sites-available/twistedspur /etc/nginx/sites-enabled/```
        6. ```sudo nginx -t```
        7. ```sudo systemctl reload nginx```
    10. Go to http://twistedspur.centralus.cloudapp.azure.com/ in web browser.
        - If any access issues occur, review VM ports in Azure Portal.
