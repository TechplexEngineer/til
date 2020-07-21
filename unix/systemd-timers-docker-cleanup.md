Using systemd timer to perform weekly docker disk cleanup
============


On our Gitlab CI build runners, we sometimes run out of disk space.

This short script asks docker to remove containers, volumes and images.
Place in `/opt/docker-cleanup.sh`
```bash
#!/bin/bash

set -uo pipefail

# just keep running on error
set +e

# system prune should remove everything we care about
echo ">>> System Prune"
/bin/docker system prune -af

# these are just incase system prune leaves anything behind
echo ">>> Removing containers"
containers=$(/bin/docker ps -aq)
if [[ -n $containers ]]; then
	/bin/docker rm -f $containers
fi

echo ">>> Removing images"
images=$(/bin/docker images -q)
if [[ -n $images ]]; then
	/bin/docker rmi -f $images
fi

echo ">>> Removing volumes"
volumes=$(/bin/docker volume ls -q)
if [[ -n $volumes ]]; then
	/bin/docker rmi -f $volumes
fi

echo ">>> Done"
```

Place in `/etc/systemd/system/docker-cleanup.service`
```
[Unit]
Description=Docker Runner Cleanup
# this unit is intented to be run by the docker-cleanup.timer

[Service]
Type=oneshot

ExecStart=/opt/docker-cleanup.sh
```


Place in `/etc/systemd/system/docker-cleanup.timer`
```
[Unit]
Description=Twice daily check for cert renewal

[Timer]
#          DayOfWeek Year-Month-Day Hour:Minute:Second
OnCalendar=Mon  *-*-* *:*:*
Persistent=true
Unit=docker-cleanup.service

[Install]
WantedBy=timers.target
```