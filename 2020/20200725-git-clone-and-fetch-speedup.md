## git clone and fetch speed up
### keywords: git clone fetch slowly speed up 
### system: macOS

1. first way speed up with SSH & proxy
    ```
    1. configure your SSH config file, filepath: ~/.ssh/config
        
        Host		github.com
        Hostname	github.com
        ProxyCommand	nc -X 5 -x 127.0.0.1:1080 %h %p
        User		licheng351@outlook.com
        PreferredAuthentications publickey
        IdentityFile	~/.ssh/id_rsa_github
        
        ## Attention:
        ##  1. -X 5 means protocol SOCKS5
        ##  2. -x ip:port your proxy info
        
    2. git clone git@github.com:licheng351/daily.git
    
    ```
2. second way via proxychains-ng
    ```
    procychains4 git clone https://github.com/licheng351/daily.git
    ```

3. third way configure your git config with proxy
    ```
    git config --global https.proxy http://127.0.0.1:8090
    git config --global https.proxy https://127.0.0.1:8090
    git config --global http.proxy socks5://127.0.0.1:1080

    git config --global --unset http.proxy
    git config --global --unset https.proxy
    ```


### References
- https://stackoverflow.com/a/62079208
- http://www.perkin.org.uk/posts/ssh-via-http-proxy-in-osx.html
- https://github.com/lmk123/blog/issues/65
- https://github.com/itgoyo/500Days-Of-Github/issues/180
- https://git-scm.com/docs/git-config
- https://gist.github.com/laispace/666dd7b27e9116faece6
