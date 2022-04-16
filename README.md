# MSO_E5_Dev_AutoRenew_REVISION_2
This is a python program based on Git Actions modified to automatically generate development actions via Microsoft Graph API like a real developer in order to active Microsoft Office 365 E5 Developer Trail subscription auto renew.
### Project description ###
* Use GitHub action to run api calls automatically at regular intervals to keep E5 development active.
* Free, no extra device/server needed, don't worry about it after deployment.
* Encrypted version, hide app id + secret, protect account security

### Special Notes/Thanks ###
* Normal version address: https://github.com/kylierst/MSO_E5_Dev_AutoRenew_REVISION_2
* Encrypted version address: https://github.com/wangziyingwen/AutoApiSecret

### Tutorial Summary ###
```
Fork MSO_E5_Dev_AutoRenew_REVISION_2 to GitHub.

Azure register the application, select any organization directory, redirect url select web, fill in http://localhost:53682/, register, save id and secret.

Set application permissions, select files.read.all files.readwrite.all sites.read.all sites.readwriter.all user.read.all user.readwrite.all directory.read.all directory.readwrite.all mail.read mail.readwrite mailboxsetting.read mailboxsetting.readwrite, all checked, should be the original 1 + 12, a total of 13, granted permissions.

rclone execute command .\rclone authorize "onedrive" "id" "confidential", a confirmation box pops up, confirm and return refresh_token.

go back to the GitHub own project, modify Secret.txt, paste refresh_token into it.

to the project setting item, respectively, add SECRETCONFIG_ID id=r'Application ID' CONFIG_KEY secret=r'secret'.

click user avatar, enter user setting item, select developer setting, select personal access tokens, add GITHUB_TOKEN, select repo, admin: repo_hook, workflow, generate token.

return to GitHub own project, star project, enter actions, then refresh the page appears workflow project, construction is complete, click enter, check testapi, whether ten times run successfully.

The default setting is to run three rounds every six hours from Monday to Friday, you can modify your own crontab 12 */6 * * 1-5.

### Difference ###
  The project uses a public repository (open code), where everyone can see the content of your code.

  So your application id, secrets, and tokens are displayed and are not secure.

 Encrypted version, I hide the application id, secret, token because it needs to be updated in real time, can not be hidden (I will not!) The security will be much higher!

--------------------------------------------------------------

### Steps ###

* Login/create a new GitHub account, go back to this project page, click the top right corner to fork the code of this project to your own repository.
* Follow the original tutorial to get the application id+secret key (copy and save it yourself), and modify Secret.txt in your own project.(don't change main.py)
  
* Click Setting > Secrets > Add a new secret in the upper column in order to create two new secrets as shown: CONFIG_ID, CONFIG_KEY.

  The contents are as follows: (change your application id to your application id , your application secret to your secret, single quotes do not move )
  
  CONFIG_ID
id=r'your application id'
  CONFIG_KEY
  secret=r'your application secret'
  ```
  
* Go to your personal settings page (Settings in the top right header, not Settings in the repository) and select Developer settings > Personal access tokens > Generate new token,
  Generate new token
  Set the name to GITHUB_TOKEN , then check the options repo , admin:repo_hook , workflow , etc., and finally click Generate token.
  
* Click on the star/star in the upper right corner to call it once, and then click on the Action above to see the log of each run (see if the api is called in place and if there are any errors)

* If there are no errors, it's done, so don't worry about it. (If you can't read the following, don't worry about it)

  I set the automatic operation every 6 hours, each call 3 rounds (click on the upper right corner of the star / star can also immediately call a), you modify at your own discretion (I do not know how much active to call, how long):.

  - Timed auto-start modification place: (in the .github/workflow/autoapi.yml file, your own cron timing task format)
   
   
  - The number of rounds per time modified place: (at the end of main.py)
     
------------------------------------------------------------
### Off-topic ###
> API calls
  You can look at the graph browser yourselves and learn to modify what api to call (most importantly, call outlook, OneDrive)
  https://developer.microsoft.com/graph/graph-explorer/preview

### GitHub Action introduction ###
Virtual environment provided.

- 2-core CPU
- 7 GB RAM memory
- 14 GB SSD hard disk space

Usage limitations.
* Each repository can only support 20 concurrent workflows.
* You can call the GitHub API 1000 times per hour.
* Each job can run for up to 6 hours.
* The free version supports up to 20 jobs in parallel, and macOS only supports up to 5.
* There is a limit of 2000 minutes per month for private repositories, $0.008/minute after that, and no limit for public repositories.

(We use the public repository here, by definition, you can set an infinite loop to call, and then start once every 6 hours to ensure 24 hours a day call)

# Notice
This repo may lead to unknown issues, problems, information leaks, etc. 

Use at your own risk.

The author DO NOT provide help or further assistance for personal reasons.

Please DO NOT open issues or PR over this project, I do not have enough time to respond due to personal reasons, thanks for understanding.
