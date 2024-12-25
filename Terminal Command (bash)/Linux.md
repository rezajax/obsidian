






```bash
export us="root@serveraddress"
`source ~/.bashrc`

ssh $us
scp baran-shadow-0.0.1.zip $us:/root

```


### Alternative Using `~/.ssh/config`:

```kotlin
nano ~/.ssh/config

Host us
    HostName 107.175.73.102
    User root


```

Now, you can type `ssh us`, and it will work as expected.



## Copy SSH pub Key

create
```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```

copy via `ssh-copy-id`
```bash

$ ssh-copy-id -i ~/.ssh/id_ed25519.pub us

/usr/bin/ssh-copy-id: INFO: Source of key(s) to be installed: "/home/reza/.ssh/id_ed25519.pub"
/usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
/usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
root@x.x.x.x's password: 

Number of key(s) added: 1

Now try logging into the machine, with:   "ssh 'us'"
and check to make sure that only the key(s) you wanted were added.



```
Here are some alternatives to `ssh-copy-id` and `scp` for SSH-based operations:

### 1. **Alternatives to `ssh-copy-id`**

The `ssh-copy-id` command is used to copy your SSH public key to a remote server to enable passwordless SSH login. If you prefer alternatives to this command, here are some options:

#### a. **Manual Method to Copy SSH Key:**

If `ssh-copy-id` isn't available or you prefer doing it manually, you can copy the SSH key using `cat` or `scp`. Follow these steps:

1. **On your local machine, display the contents of your public key:**
    
    bash
    
    Copy code
    
    `cat ~/.ssh/id_rsa.pub`
    
2. **On the remote server, open or create the `~/.ssh/authorized_keys` file:**
    
    bash
    
    Copy code
    
    `ssh username@hostname_or_ip "mkdir -p ~/.ssh && nano ~/.ssh/authorized_keys"`
    
3. **Paste the contents of your local public key into the `authorized_keys` file** on the remote server.
4. **Save the file** and ensure correct permissions:
    
    bash
    
    Copy code
    
    `ssh username@hostname_or_ip "chmod 700 ~/.ssh && chmod 600 ~/.ssh/authorized_keys"`
    

#### b. **Using `rsync` to Copy SSH Key:**

You can use `rsync` to copy the public key to the remote server's `authorized_keys`:

bash

Copy code

`rsync -avz ~/.ssh/id_rsa.pub username@hostname_or_ip:/tmp/id_rsa.pub`

Then SSH into the remote machine and append it to the `authorized_keys` file:

bash

Copy code

`ssh username@hostname_or_ip "mkdir -p ~/.ssh && cat /tmp/id_rsa.pub >> ~/.ssh/authorized_keys && rm /tmp/id_rsa.pub"`

### 2. **Alternatives to `scp`**

The `scp` command is used for copying files over SSH. Here are some alternatives:

#### a. **`rsync` (Recommended for File Transfers):**

`rsync` is more efficient than `scp`, especially for large files or directories, as it only transfers changed parts of the files. It also supports resuming transfers.

- **Copying files from local to remote:**
    
    bash
    
    Copy code
    
    `rsync -avz local_file username@hostname_or_ip:/path/to/destination`
    
- **Copying files from remote to local:**
    
    bash
    
    Copy code
    
    `rsync -avz username@hostname_or_ip:/path/to/remote_file /path/to/local/destination`
    
- **Copy a directory (recursively) from local to remote:**
    
    bash
    
    Copy code
    
    `rsync -avz local_directory/ username@hostname_or_ip:/path/to/destination`
    

#### b. **`sftp` (Secure FTP over SSH):**

`sftp` provides an interactive file transfer session over SSH. You can use it to upload or download files.

- **Start an `sftp` session:**
    
    bash
    
    Copy code
    
    `sftp username@hostname_or_ip`
    
- **Upload a file to the remote server:**
    
    bash
    
    Copy code
    
    `put local_file /path/to/remote/destination`
    
- **Download a file from the remote server:**
    
    bash
    
    Copy code
    
    `get /path/to/remote_file local_destination`
    
- **To copy an entire directory:**
    
    bash
    
    Copy code
    
    `put -r local_directory /path/to/remote/destination`
    

#### c. **`ftp` (File Transfer Protocol):**

If SSH is not a requirement, `ftp` can also be used to transfer files, although it is less secure than `sftp`.

- **Start an FTP session:**
    
    bash
    
    Copy code
    
    `ftp hostname_or_ip`
    

#### d. **`tar` Over SSH:**

You can use `tar` to compress and transfer directories over SSH, which can be useful for large directories.

- **Copy directory using `tar` and SSH:**
    
    bash
    
    Copy code
    
    `tar czf - /path/to/local_directory | ssh username@hostname_or_ip "tar xzf - -C /path/to/remote_destination"`
    
- **Copy a file using `tar` and SSH:**
    
    bash
    
    Copy code
    
    `tar czf - local_file | ssh username@hostname_or_ip "tar xzf - -C /path/to/remote_destination"`
    

These alternatives offer similar or improved functionality compared to `ssh-copy-id` and `scp`, and can be used based on your specific use case.