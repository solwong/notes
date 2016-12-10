## Common usage

```shell
# See the uname code
lsb_release --short --code

# Make new group effective
newgrp $grpName
```

## No hup

### Output the log into a files, and keep a thread.

```shell
nohup $threadName &
```

### Keep multiple screen

```shell
screen -S $newScreen
screen -r $newScreen
screen --wipe $newScreen
```

## Excute remote tty command

```
ssh -t user@ip 'docker exec -it container bash'
```