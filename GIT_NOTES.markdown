# GIT IS AN OPEN SOURCE VERSION CONTROL SYSTEM(VCS) #

## CH1 ##

1. `sudo apt-get install git-core` 

2-1. 
// ***NOTICE! GIT USERNAME FOR ASSOCIATE COMMITS WITH AN IDENTITY. NOT THE SAME AS GITHUB USERNAME***
// ***NOTICE! Changing the name associated with your Git commits using git config will only affect future commits and will not change the name used for past commits.***

2.
### **SETTING GIT USERNAME FOR EVERY REPOSITORY** ###
`git config --global user.name "aaa lee"`

//***CONFIRM***
`git config --global user.name`

3.
### **SETTING GIT USERNAME FOR SINGLE REPOSITORY** ###
//***Chang Current working directory to the local repository where you want to configure the name that is associated with your Git commits***
`git config user.name "aaa lee"`

//***CONFIRM*** 
`git config user.name`

4.
### **SETTING COMMIT EMAIL ADDRESS IN GIT** ###
//***GitHub uses the email address set in your local Git configuration to associate commits pushed from the command line with your GitHub account.***
//***SAME AS SETTING USERNAME ABOVE THERE ARE EVERY AND SINGLE REPOSITORY***
```
git config --global user.email "example@example.com"
git config --global user.email //***FOR CONFIRM***
```

//***FOR SINGLE REPOSITORY***
//***You can change the email address associated with commits you make in a single repository. This will override your global Git config settings in this one repository, but will not affect any other repositories.***
```
git config user.email "example@example.com"
git config user.email //***FOR CONFIRM***
```

5.
### **AUTHENTICATION WITH GITHUB FROM GIT** ###
//***WHEN YOU CONNECT TO A GITHUB REPOSITORY FROM GIT, YOU'LL NEED TO AUTHENTICATE WITH GITHUB USING EITHER HTTPS OR SSH.***

5-1 #### **CONNECTING OVER HTTPS (RECOMMENDED)** ####
- //***IF YOU CLONE WITH HTTPS, YOU CAN CACHE YOUR GITHUB PASSWORD IN GIT USING A CREDENTIAL HELPER***
    - //**TURN ON CREDENTIAL HELPER GIT WILL SAVE YOUR PASSWORD IN MEMORY CACHE 15 MIN DEFAULT. **
       ```
       git config --global credential.helper cache //***SET GIT TO USE THE CREDENTIAL MEMORY CAHCE***
       git config -global credential.helper 'cache --timeout=3600' //***CHANGE THE DEFAULT PASSWORD CACHE TIMEOUT (AFTER 1 HOUR IN SECONDS)***
       ```
- //***The https:// clone URLs are available on all repositories, public and private. These URLs work everywhere--even if you are behind a firewall or proxy. In certain cases, if you'd rather use SSH, you might be able to use SSH over the HTTPS port.***
       - // **FOR SSH OVER THE HTTPS PORT**
       ***(firewalls refuse to allow SSH connections entirely, you can attempt to clone using an SSH     connection made over the HTTPS port. Most firewall rules should allow this, but proxy servers may interfere)***
 
       - //** TO test if SSH over HTTPS port is possible, run** 
         `ssh -T ***(disable pseudo-terminal allocation)*** -p 443 git@ssh.github.com`
  
       - //**ABOVE YOU SHOULD BE SEE**
       `Hi username! You've successfully authenticated, but GitHub does not provide shell access` 
       - // ***IF NOT SEE [Trobleshoot](https://help.github.com/articles/error-permission-denied-publickey/#platform-linux)***
   
       - //**ENABLING SSH CONNECTIONS OVER HTTPS **
       - //***IF YOU ABLE SSH INTO GIT@SSH.GITHUB.COM OVER PORT 443, OVERRIDE YOUR SSH SETTING TO FORCE ANY CONNECTION TO GITHUB THROUGH THE SERVER AND PORT***
       -  //**SET SSH CONFIG EDIT FILE  ~/.ssh/config **
       ```   
              Host github.com
              Hostname ssh.github.com
              Port 443 
       ```
       - // **TEST CONNECTION TO GITHUB**
   ```
   ssh -T git@github.com //***IF YES, YOU SHOULD SEE ABOVE THE HI USERNAME MESSAGES***
```
- // ***When you git clone, git fetch, git pull, or git push to a remote repository using HTTPS URLs on the command line, you'll be asked for your GitHub username and password.***

- //***If you have enabled two-factor authentication, or if you are accessing an organization that uses SAML single sign-on, you must provide a personal access token instead of entering your password for HTTPS Git.***
     - ***[FOR TWO-FACTOR AUTHENTICATION](https://help.github.com/articles/securing-your-account-with-two-factor-authentication-2fa)***
     - ***[FOR SAML SINGLE SIGN-ON](https://help.github.com/articles/about-authentication-with-saml-single-sign-on)***
     - ***[FOR PROVIDE A PERSONAL ACCESS TOKEN](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line)***

5-2 
### **CONNECTING OVER SSH** ###
//***When you set up SSH, you'll generate an SSH key and add it to the ssh-agent and then add the key to your GitHub account. Adding the SSH key to the ssh-agent ensures that your SSH key has an extra layer of security through the use of a passphrase.


//***NOTICE!  SAML single sign-on (SSO) cannot be accessed with SSH. To access repositories in organizations that use SAML SSO, use an authorized personal access token with HTTPS. 

//***IF TOU CLONE OVER SSH, YOU MUST GENERATE SSH KEYS ON EACH COMPUTER YOU USE TO PUSH OR PULL FROM GITHUB 
//***If you clone GitHub repositories using SSH, then you authenticate using SSH keys instead of a username and password  
