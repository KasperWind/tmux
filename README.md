# tmux configuration

## Installation
clone repo to ```home/.config/tmux```

clone ```git clone https://github.com/tmux-plugins/tpm ~/.tmux/plugins/tpm```

create ```plugins``` folder

clone following repos
```
git clone https://git::@github.com/dreamsofcode-io/catppuccin-tmux
git clone https://git::@github.com/catppuccin/tmux
git clone https://git::@github.com/tmux-plugins/tmux-sensible
git clone https://git::@github.com/tmux-plugins/tmux-yank
git clone https://git::@github.com/tmux-plugins/tpm
```


## Shared usage

If using same user as login, just as normal
If sharing instance between different users.

1. Users have to be in a shared group
   - create group
   - add users
   - remember user either have to run newgr or log out and then log in
```
sudo group add multiuser
sudo usermod -a -G multiuser <user1>
sudo usermod -a -G multiuser <usern>
```  
2. Create a folder that all in the group can access
   - make directory
   - change directory group
   - set permissions
   - set group id

```
sudo mkdir /var/tmux/
sudo chgrp multiuser /var/tmux/
sudo chmod 770 /var/tmux/
sudo chmod +s /var/tmux
```
3. Create a tmux shared session
   - create session with custom path
   - add new file to group and set permissions
   - shared tmux session
```
tmux -S /var/tmux/tm1 new -s <shared session name>
sudo chgrp multiplexer /var/tmux/tm1
sudo chmod g+rw /var/tmux/tm1
tmux -S /var/tmux/tm1 server-access -a <user to share with>
```

4. Users then connect with 

```
tmux -S /var/tmux/tm1 attach -t <shared session name>
```

As allways remember to detach with `tmux detach` and not run exit :-)

