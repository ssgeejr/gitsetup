# gitsetup
Setup Git for Use with Github

## For Windows

### Step 1:
Create github account.  Navigate to https://github.com and sign up for a new account.
Make sure to enable MFA (Multi-Factor Authentication) 

### Step 2: 
Download git client. Grab the version that suits your OS from here: https://git-scm.com/downloads

make sure to install the openSSH client as well. On windows this will be installed to `C:\Windows\System32\OpenSSH\`

### Step 3: 
create your .ssh directory.  To create this directory, on windows, you will need t
mkdir %HOMEPATH%\.ssh or create it using Explorer

### Step 4:
Create config file. Create the file %HOMEPATH%\.ssh\config and add the following to it. 
```
Host *
    StrictHostKeyChecking no
Host github.com
 Hostname github.com
 IdentityFile %HOMEPATH%\.ssh\<username>_github
Host hyperion
 Username <username>
 IdentityFile %HOMEPATH%\.ssh\<username>_hyperion
Host *
 IdentityFile %HOMEPATH%\.ssh\<username>_wmmc

```

Save this file and move on to the next step

### Step 5: 
execute the following command to build your new ssh key (you will do this multiple times, for multiple systems so the names are important) 
`ssh-keygen -t rsa -b 2048 -C "<your_meail>" -f %HOMEPATH%\.ssh\<username>_github`

When asked for the passpharse, just hit <enter> you do not want a password on this key (you will do this twice) 

What does this do? 
* -t type of key
* -b byte size (any block of 1024)
* -C comment, this is almost exlusively your email address associated with the account (optional)
* -f output file (optional, as it will ask you when you save the key if this is not addedd)

### Verify key creation
navigater to %HOMEPATH%\.ssh and ensure you have a <username>_github and a <username>_github.pub
the .pub key is pubilc and you can share this with anyone - you will need to send me this file in an email, no encryption required, so I can add you to our cloud server to test that you have everything configured correctly 

*NEVER Share your private key with anyone* 

DO this two more times, creating the keys <username>_hyperion and <username>_wmmc

### Step 6: Edit Host File
since we push our code to the cloud where anyone can see it, we only connect to our servers by their hostfile entry. This protects the real IP and prevent attack on those servers. 

Edit your host file, which you file here:  c:\Windows\System32\drivers\etc\hosts 
The easiest way to edit this file is to hit the windows key, type in "notepad", right click and "run as administrator" - as standard users aren't allowed to edit the hostfile - (We have talked before about this being a way to spoof websets and a common attack for hackers)
In the hosts file (notice the s on the end) you will want to add the following: 
```
<IP>	tethys
<IP>	hyperion
```

*I will message you the actual IP's for these two servers, and moving forward you will always connect to the server via its name and never it's IP address* 

### Step 7: Final test ... 

If you have sent me your public key (via email or teams) from a command promt (either wt or cmd) you will be able to connect to the server with the following command
`ssh hyperion` 
That's all it takes ... you are now logged into our cloud server and well move forward once we have all reached this point. 

To leave the server, just type `exit` 

## For Linux

This will come a little later as it is 100x easier to do
for Linux you can use `apt-get install -y git` or `yum install -y git` Depending on your Linux flavor