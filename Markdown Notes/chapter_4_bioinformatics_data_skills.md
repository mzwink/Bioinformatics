## Chapter 4 Bioinformatics Data Skills 

### Working with Remote Machines


Most common way to connect to another machine over a network is through the secure shell (SSH)

	SSH shell is used because it is encryted and used on every Unix system
	
	To initialize an SSH connection to a host:
	$ ssh biocluster.myuniversity.edu
	Password:
	Last login: ...
	
After logging in with your password, you're granted a shell prompt on the remote host. 
 
Also works with IP addresses but if you use a different port or different local username, you'll need to specify these details when connecting
	
	$ ssh -p 50453 cdarwin@biocluster.myuniversity.edu
	
	-p will specify the port
	username = @domain
	
	If you're not able to to connect to a host, use ssh -v (-v for verbose) can help spot issue
	(see man)
	
	
Storing Frequent SSH hosts

SSH config file - stores details about hosts you frequently connect to

	To create a file, create and edit the file at ~/.ssh/config.
	
	Host bio_serv
		HostName 192.168.237.42
		User cdarwin
		Port 50453
		
	Won't need to specify user and port unless these differ from the remote host's default
	Use alias ssh bio_serv rather than typing out ssh -p 50453 cdarwin@biocluster.myuniversity.edu
	
hostname: Can access hostname with this command

whoami: Returns your username

	
*SSH public key* 

First need to generate a public/private key pair

	Command: ssh-keygen
	
	Generate an SSH key pair using ssh-keygen:
	
	$ ssh-keygen -b 2048
	Generating public/private rsa key pair
	Enter file...
	Enter passphrase..
	Saved in ...
	*Outputs key fingerprint
	
ssh-agent program runs in the background on your local machine and manages your SSH keys

	$ ssh-add
	Enter passphrase for ...
	Identity added: ...
	
### Maintaining Long-Running Jobs with nohop and tmux

nohup: a simple command that executes a command and catches hangup signals sent from the terminal

Because the nohup command is catching and ignoring these hangup signals, the program you're running won't be interrupted

	$ nohup program1 > output.txt &
	[1] 10900
	
	Run the command with all options and arguments as we would normally but by adding nohup this program will not be interrupted if your terminal were to close
	Also good to redirect output to another file to check output later
	nohup returns the process ID number which is how you can monitor or terminate this process if you need to 
	
	
### Working with Remote Machines Through Tmux

An alternative to nohup is to use a terminal multiplexer and will greatly increase your productivity when working over a remote connection

Tmux and terminal multiplexers in general allow you to create a session containing multiple windows each capable of running their own processes

Also allows you to maintain a persistent session that won't be lost if your connection drops or you close your terminal - just SSH back into the remote host and reattach the Tmux session

Can have a window open looking at a SNP, another window with R running, and another window interacting with a project notebook and all windows are within Tmux

### Common Tmux key sequences

	
	KEY SEQUENCE				ACTION
	
	control-ad					detach
	
	control-ac					Create new window
	
	control-an					Go to next window
	
	control-ap					Go to previous window
	
	control-a&					Kill current window
	
	control-a					Rename current window
	
	control-a?					List all key sequences
	
	
### Common Tmux subcommands

	SUBCOMMAND										ACTION
	
	tmux list-sessions						List all sessions
	
	tmux new-session -s 					Create a new session named "session-name""
	session-name				
	
	tmux attach-session -t 					Attach a session named "session-name"
	session-name
	
	tmux attach-session -d -t session name	Attach a session named "session name", detaching it first						
		
		
		
		
	
	




