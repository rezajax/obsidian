






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