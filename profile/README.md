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
    1. wget -qO - https://packages.adoptium.net/artifactory/api/gpg/key/public | sudo apt-key add - echo "deb https://packages.adoptium.net/artifactory/deb focal main" | sudo tee /etc/apt/sources.list.d/adoptium.list
    2. sudo apt update
    3. sudo apt install temurin-21-jre
    4. sudo update-alternatives --config java
    5. java -version (to confirm JRE 21 default)
