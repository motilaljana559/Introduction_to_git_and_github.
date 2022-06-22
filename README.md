# Steps for git.
## Initiating a git folder.
Git is a open source free softeware which help us to keep trak of the changes of all the files and folder of our choice. In this macbook git is preinstalled. I do not have to install anything. we can start right from here.

Currently I have created a folder named as "git" and I want to keep trak of some file and folders inside it, to do that I have to make this 'git' folder as a git folder by running the command 'git init' in the terminal at this folder location. It will create a branch(I will come later) named as 'master' as your default branch. you can also change the name of this branch by running the command 'git config --global init.defaultBranch main', here I have changed it to main. so everything inside it will be considered by the git. lets creat a folder 'Introduction_to_git_and_github.'. Now I want to place this document inside that folder as this file is a introduction to git. By typing 'git status' we will see the messege 'nothing added to commit but untracked files present (use "git add" to track)' - which means git detected one file but as we have not tell it to track it so it is still untracked. To make it trackeble we need to commit it. Commit is short of saying final saving. before that we have to keep that file in the staging area- it is the area where we can put our newly created file or modified file which we can commit. to put a file into the staging area we run the command 'git add <filename>'. After placing the file to the staging area if we change the file its change will not be reflect after commit. it will only update the file with the changes made before putting it to the staging area, to fully update it we have to add it again to the stage area and then commit it. So changes occurs after putting the file into stageing are will be reflect in the second commit. The command to commit the staged file is 'git commit -m 'your heading for the changes' -m 'description of the changes' '. By the way after staging the file we will see the file name in green colour when we run the command 'git status'. Now if we want to see my avilabe branches I can type 'git branch'. we can see the branch names only after commiting something in the main branch. before commiting the file 'README.md' I did not saw anything in the output of 'git branch'. After my first commit I have updated this file after the line 'By the way...' this is not commited or staged yet so to update this file upto this part I have to add and commit it again.

## Live telecast.
Now I want to save all of my history, all the works of this git repository( repository means folder in git language) so that I could not lose my data, I can share my data to other person by a link just like google drive... I can add experts or colueges so that they can help me finding bugs or modifying the code.

Firt I have to create a github account. Now to connect to that account I need to give the authenticaion and we can do that via adding ssh key. we will create a ssh key in our local machine then add the public key in the github account so that when I tried to connect that account from this machine it will identify this machine by that public ssh key. while creating the ssh key in my local machine two types of key will be generated one is called private and the other is called the public(somename.pub),we have to add only the public key to the github account. It is mathematically proved that on the this private key could generate the public key so while connecting to the github our local machine will use private key to show github that this machine is the only one who generated this public key.

### Creation of ssh key.
first check if there exist any ssh key in your system by typing
'ls -al ~/.ssh' - this is the default path to save the ssh key if they exist it will show some file name.
we see some key already exist so while creating new ssh key we have to be cautious while giving the name of the ssh key file name otherwise it will override the existing key. there is a great documentation about it 'https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent'.

to generate a ssh key we have to run the following command in the terminal.
'ssh-keygen -t ed25519 -C "motilaljana559@gmail.com"'- t flag is refered to the enkryption type here we have type 'ed25519', -C is the flage to give the email adress. This email adress will be used as a label in the public key which will be added to the git. at this moment I dont know what happen if I don't give this label please experiment about it for better understanding.

after running the command it shows 'Generating public/private ed25519 key pair.', 'Enter file in which to save the key (/Users/admin/.ssh/id_ed25519):' where '/Users/admin/.ssh/id_ed25519' is the default path to the key so I want to customize this path name to '/Users/admin/.ssh/ssh_key_for_motilaljana559_github_type_ed22519'. This will generate two key (public and private) inside the path '/Users/admin/.ssh'. I have left the passphrase option as emty. so I hit enter for this messege. lets open the public key 'ssh_key_for_motilaljana559_github_type_ed22519.pub' to see its content. First two word is 'ssh-ed25519' which transforms for the type of encryption. And at the end we have 'motilaljana559@gmail.com' which is the label. now I am goint to add this public key to my github account. for that I have to copy this public key -> goto github -> clich on logo -> Settings -> on the left pennal 'SSH and GPG keys' -> click on 'New SSH key' under 'SSH keys' -> give a title (for example 'ssh_key_from_computer_name')-> paste the public key inside the box 'Key' -> click on 'Add SSH Key'.

Now I have have to let the local command line interface know about the key I have just generated. so to do that I run the following command. the documentation is here 'https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent' under the section 'Adding your SSH key to the ssh-agent'.

commands:
eval "$(ssh-agent -s)" - will run the ssh-agent in the background
open ~/.ssh/config - if it '~/.ssh/config' does not exist then create one by the command 'touch ~/.ssh/config' and then open it.

Now paste the following line to the config file then save it(only for macOS Sierra 10.12.2 or later):
    "Host *
        AddKeysToAgent yes
        IdentityFile ~/.ssh/private_key_name"
The next step will be adding ssh key to the ssh-agent:
    ssh-add -K ~/.ssh/private_key_name

Now we are set to authenticate our local machine to our github account.

## Pust to github:
At this point github does not know where to put my local folder or files. So I am going to create a empty folder named 'Introduction_to_git_and_github.' and then send (push) all of my files which is inside my this folder(it has to be current git folder).
and then add the remote repository in the local machine. by 'git remote add origin git@github.com:motilaljana559/Introduction_to_git_and_github..git'
... run the command 'git remote -v' to see the current remote repository i.e if we push something it will be added to that repository.
now force the git to locally consider only the current folder (the content of the folder which I will push to the github) by
runnig git init on this current folder.

to push the content of the current folder to the remote repository run the below command:
'git push origin main'



