# GIT IS AN OPEN SOURCE VERSION CONTROL SYSTEM(VCS) #

## CH1. SET UP A GIT ##

1. `sudo apt-get install git-core` 
1-1 **FOR CORE EDITOR**  
`git config --global core.editor vi`  
`git config --global core.editor gedit`
1-2 **FOR GUI**  
`sudo apt-get install gitg`
OR
`sudo apt-get install gitk`
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
       git config --global credential.helper cache #SET GIT TO USE THE CREDENTIAL MEMORY CAHCE
       git config --global credential.helper 'cache --timeout=3600' #CHANGE THE DEFAULT PASSWORD CACHE TIMEOUT (AFTER 1 HOUR IN SECONDS)
       git config --global credential.helper #FOR CONFIRM
       ```
* ***The https clone URLs are available on all repositories, public and private. These URLs work everywhere even if you are behind a firewall or proxy. In certain cases, if you'd rather use SSH, you might be able to use SSH over the HTTPS port.***  
     *  **FOR SSH OVER THE HTTPS PORT**  
       ***firewalls refuse to allow SSH connections entirely, you can attempt to clone using an SSH     connection made over the HTTPS port. Most firewall rules should allow this, but proxy servers may interfere***  
 
       * **TO test if SSH over HTTPS port is possible, run**  
         `ssh -T #disable pseudo-terminal allocation -p 443 git@ssh.github.com`  
  
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
   ssh -T git@github.com #IF YES, YOU SHOULD SEE ABOVE THE HI USERNAME MESSAGES
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
>* ***NOTICE!  SAML single sign-on (SSO) cannot be accessed with SSH. To access repositories in organizations that use SAML SSO, use an authorized personal access token with HTTPS see above.*** 
>
>* ***IF TOU CLONE OVER SSH, YOU MUST GENERATE SSH KEYS ON EACH COMPUTER YOU USE TO PUSH OR PULL FROM GITHUB***
>
>* ***If you clone GitHub repositories using SSH, then you authenticate using SSH keys instead of a username and password*** 
>* ***You can also use [SSH agent forwarding](https://developer.github.com/v3/guides/using-ssh-agent-forwarding/) with your deploy script to avoid managing keys on the server.***

>1. **[ABOUT SSH](https://help.github.com/articles/about-ssh/)**
>     * **SSH protocol, connect and authenticate to remote servers & service.**
>     * **SSH keys, connect to Github without supplying your username or password at each visit.**
>2. **[CHECKING FOR EXISITING SSH KEYS](https://help.github.com/articles/checking-for-existing-ssh-keys/)**
>      * **If you don't have an existing public and private key pair, or don't wish to use any that are available to connect to GitHub, then see below generate a new SSH key.**
>      * **If you see an existing public and private key pair listed (for example id_rsa.pub and id_rsa) that you would like to use to connect to GitHub, you can add your SSH key to the ssh-agent.**
>3. **GENERATING A NEW SSH KEY AND ADDING IT TO THE SSH-AGENT**
>      * **After checking for exisiting SSH keys, you can generate a new SSH key to use for authentication then add it ti the ssh-agent.**
>4. **[ADDING A NEW SSH KEY TO YOUR GITHUB ACCOUNT](https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/#platform-linux)**
>      * **To configure your GitHub account to use your new (or existing) SSH key, you'll also need to add it to your GitHub account.**
>5. **TESTING YOUR SSH CONNECTION**
>      * **After set up your SSH key and added it to your GitHub account, you can test your connection.**
>6. **[WORKING WITH SSH KEY PASSPHRASES](https://help.github.com/articles/working-with-ssh-key-passphrases/)**
>      * **You can secure your SSH keys and configure an authentication agent so that you won't have to reenter your passphrase every time you use your SSH keys.**
* #### **GENERATING A NEW SSH KEY** #### 
  * **OPEN TERMINAL**
  *  ```
     ssh-keygen -t rsa -b 4096 -C "your_email@example.com" #WITH YOU GITHUB EMAIL
     -t (Specifies the type of key to create)
     -b (The desired length of the primes may be specified) #SEE MORE IN man page ssh-keygen(1)
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
   ```
   eva1 "$(ssh-agent -s)"
   Agent pid 59566
   
   -s options for Generate Bourne shell commands on stdout. 
   ```
   [Eval command](https://www.tutorialspoint.com/unix_commands/eval.htm) comes in handy when you have a unix or linux command stored in a variable and you want to execute that command stored in the string. The eval command first evaluates the argument and then runs the command stored in the argument.
   * **Add your SSH private key to the ssh-agent. If you created your key with a different name, or if you are adding an existing key that has a different name, replace id_rsa in the command with the name of your private key file.**  
   `ssh-add ~/.ssh/id_rsa`  
   * **[Adding a new SSH key to your Github Account](https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/#platform-linux)**  
* #### **TESTING SSH CONNECTION** ####  
>* **Before testing your SSH connection, you should have:**
>    1. **[Checked for existing SSH keys](https://help.github.com/articles/checking-for-existing-ssh-keys/)**
>    2. **[Generated a new SSH key](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/)**
>    3. **[Added a new SSH key to your GitHub account](https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/#platform-linux)**  
>    
   * ***When you test your connection, you'll need to authenticate this action using your password, which is the SSH key passphrase you created earlier.***
     
   * ```
     ssh -T git@github.com #Attempts to ssh to github 
     # -T for  Disable pseudo-terminal allocation.
     ```   
     * ***YOU MAY SEE THESE WARNING***
     ```
      The authenticity of host 'github.com (192.30.252.1)' can't be established.
      RSA key fingerprint is 16:27:ac:a5:76:28:2d:36:63:1b:56:4d:eb:df:a6:48.
      Are you sure you want to continue connecting (yes/no)?
    
      The authenticity of host 'github.com (192.30.252.1)' can't be established.
      RSA key fingerprint is SHA256:nThbg6kXUpJWGl7E1IGOCspRomTxdCARLviKw6E5SY8.
      Are you sure you want to continue connecting (yes/no)?
     ```
   * ***Note: The example above lists the GitHub IP address as 192.30.252.1. When pinging GitHub, you may see a range of [IP addresses](https://help.github.com/articles/github-s-ip-addresses/)***  
     
   * **Verify that the fingerprint in the message you see matches one of the messages in step 2, then type yes**
   ```
   Hi username! You've successfully authenticated, but GitHub does not
provide shell access.  
  ```  
 * **ERROR MESSAGES**   
      
      ``` 
        Agent admitted failure to sign using the key.
        debug1: No more authentication methods to try.
        Permission denied (publickey).
      ```   
      
      * **["Error: Agent admitted failure to sign" for certain Linux Distribution](https://help.github.com/articles/error-agent-admitted-failure-to-sign/)**
       * **["Error: Permission denied (publickey)" resulting contain your username](https://help.github.com/articles/error-permission-denied-publickey/)**
      
      