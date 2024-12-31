```bash
pkg update
pkg install openssh

ifconfig


Check if SSH server is running on Termux
Make sure the SSH server is running in Termux. You can check it by running the following command:

ps aux | grep sshd



If the SSH server isn't running, try starting it again:
sshd



### 2. **Ensure Termux permissions**

If it doesn't start, check if Termux has the necessary permissions to bind to port 22. You can use a different port, like 2222, as follows:

sshd -p 2222



//run whoami to see username
ssh u0_a353@192.168.1.227




// b4 run set password with "passwd"
ssh u0_a353@192.168.1.227 -p 2222


```