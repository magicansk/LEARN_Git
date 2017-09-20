# GIT IS AN OPEN SOURCE VERSION CONTROL SYSTEM(VCS) #

## CH1 ##

1. `sudo apt-get install git-core` 

2. 
>* ***NOTICE! Git username for associate commits with an identity. not the same as github username.***
>
>* ***NOTICE! Changing the name associated with your Git commits using git config will only affect future commits and will not change the name used for past commits.***


### **SETTING GIT USERNAME FOR EVERY REPOSITORY** ###
 `git config --global user.name "aaa lee"`

 ***FOR CONFIRM***  
 `git config --global user.name` 

3.
### **SETTING GIT USERNAME FOR SINGLE REPOSITORY** ###
>* ***Changing Current working directory to the local repository where you want to configure the name that is associated with your Git commits.***

`git config user.name "aaa lee"`

***FOR CONFIRM***   
`git config user.name`

4.
### **SETTING COMMIT EMAIL ADDRESS IN GIT** ###
> * ***GitHub uses the email address set in your local Git configuration to associate commits pushed from the command line with your GitHub account.***
>
>* ***Same as setting username above there are every and single repository.***

`git config --global user.email "example@example.com"` 

***FOR CONFIRM***  
`git config --global user.email` 


* ***FOR SINGLE REPOSITORY***
    *  ***You can change the email address associated with commits you make in a single repository. This will override your global Git config settings in this one repository, but will not affect any other repositories.***  
`git config user.email "example@example.com"` 

    * ***FOR CONFIRM***  
    `git config  user.email` 


5.
### **AUTHENTICATION WITH GITHUB FROM GIT** ###
>* ***When you connect to a github repository from git, you'll need to authenticate with github using either https or ssh.***

5-1. 
#### **CONNECTING OVER HTTPS (RECOMMENDED)** ####
* ***If you clone with https, you can cache your github password in git using a credential helper***  
     * **Turn on credential helper git will save your password in memory cache 15 min default.**
       ```
       git config --global credential.helper cache //SET GIT TO USE THE CREDENTIAL MEMORY CAHCE
       git config --global credential.helper 'cache --timeout=3600' //CHANGE THE DEFAULT PASSWORD CACHE TIMEOUT (AFTER 1 HOUR IN SECONDS)
       git config --global credential.helper //FOR CONFIRM
       ```
* ***The https clone URLs are available on all repositories, public and private. These URLs work everywhere even if you are behind a firewall or proxy. In certain cases, if you'd rather use SSH, you might be able to use SSH over the HTTPS port.***  
     *  **FOR SSH OVER THE HTTPS PORT**  
       ***firewalls refuse to allow SSH connections entirely, you can attempt to clone using an SSH     connection made over the HTTPS port. Most firewall rules should allow this, but proxy servers may interfere***  
 
       * **TO test if SSH over HTTPS port is possible, run**  
         `ssh -T //(disable pseudo-terminal allocation) -p 443 git@ssh.github.com`  
  
       * **ABOVE YOU SHOULD BE SEE**  
       `Hi username! You've successfully authenticated, but GitHub does not provide shell access` 
       * ***IF NOT,  SEE [Trobleshoot](https://help.github.com/articles/error-permission-denied-publickey/#platform-linux)***
   
       * **ENABLING SSH CONNECTIONS OVER HTTPS**
         * ***If you able ssh into git@ssh.github.com over port 443, override your ssh setting to force any connection to github through the server and port***
         *  **SET SSH CONFIG EDIT FILE  ~/.ssh/config**
            ```
              Host github.com
              Hostname ssh.github.com
              Port 443 
            ```
       
       * **TEST CONNECTION TO GITHUB**
   ```
   ssh -T git@github.com //IF YES, YOU SHOULD SEE ABOVE THE HI USERNAME MESSAGES
   ```

* ***When you git clone, git fetch, git pull, or git push to a remote repository using HTTPS URLs on the command line, you'll be asked for your GitHub username and password.***

* ***If you have enabled two-factor authentication, or if you are accessing an organization that uses SAML single sign-on, you must provide a personal access token instead of entering your password for HTTPS Git.***


     * ***[FOR TWO-FACTOR AUTHENTICATION](https://help.github.com/articles/securing-your-account-with-two-factor-authentication-2fa)***
     * ***[FOR SAML SINGLE SIGN-ON](https://help.github.com/articles/about-authentication-with-saml-single-sign-on)***
     * ***[FOR PROVIDE A PERSONAL ACCESS TOKEN](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line)***


5-2 
#### **CONNECTING OVER SSH** ####
>* ***When you set up SSH, you'll generate an SSH key and add it to the ssh-agent and then add the key to your GitHub account. Adding the SSH key to the ssh-agent ensures that your SSH key has an extra layer of security through the use of a passphrase.***
>
>* ***NOTICE!  SAML single sign-on (SSO) cannot be accessed with SSH. To access repositories in organizations that use SAML SSO, use an authorized personal access token with HTTPS.*** 
>
>* ***IF TOU CLONE OVER SSH, YOU MUST GENERATE SSH KEYS ON EACH COMPUTER YOU USE TO PUSH OR PULL FROM GITHUB***
>
>* ***If you clone GitHub repositories using SSH, then you authenticate using SSH keys instead of a username and password*** 
* #### **GENERATING A NEW SSH KEY** #### 
  * **OPEN TERMINAL**
  *  ```
     ssh-keygen -t rsa -b 4096 -C "your_email@example.com" //WITH YOU GITHUB EMAIL
     -t (Specifies the type of key to create)
     -b (The desired length of the primes may be specified) //SEE MORE IN man page ssh-keygen(1)
     -C (Provide for a comment)
     ```  
     **This creates a new ssh key, using the provided email as a label. It will show above:**   
      `Generating public/private rsa key pair.`
  * **When you're prompted to "Enter a file in which to save the key," press Enter. This accepts the default file location.**    
    `Enter a file in which to save the key (/home/you/.ssh/id_rsa): [Press enter]`
  * **At the prompt, type a secure passphrase**  
    ```
    Enter passphrase (empty for no passphrase): [Type a passphrase]
    Enter same passphrase again: [Type passphrase again]
    ```
    ***[FOR WINDOWS SSH KEY PASSPHRASES](https://help.github.com/articles/working-with-ssh-key-passphrases/)***
* #### ADDING YOUR SSH KEY TO THE SSH-AGENT ####  
>* **Before adding a new SSH key to the ssh-agent to manage your keys, you should have checked for existing SSH keys and generated a new SSH key.**
   * **START THE SSH-AGENT IN THE BACKGROUND**

