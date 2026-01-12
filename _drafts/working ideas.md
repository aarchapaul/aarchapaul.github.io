[[2024-06-08-Graphql]] - need more work
[[2026-01-13-Nmap-cheatsheet]] - cleanup and consolidate
subdomain takeover article
substack writing research
applets in cinnamon
cron jobs in security and how automating backups is important??

```bash
sudo rsync -avxHAX -z --delete --progress --exclude-from='aarcha/excludelist.txt' aarcha/ /timeshift/snapshots

sudo rsync -avxHAX --delete --progress /mnt/backup/system_backup/ /

```

```txt
aarcha/.cache/*
aarcha/.android/*
aarcha/.bundle/*
aarcha/.byobu/*
aarcha/.cinnamon/*
aarcha/.continuum/*
aarcha/.dbus/*
aarcha/.dotnet/*
aarcha/.FBReader/*
aarcha/.gconf/*
aarcha/.gem/*
aarcha/.gnome/*
aarcha/.gnupg/*
aarcha/.icons/*
aarcha/.java/*
aarcha/.linuxmint/*
aarcha/.mume/*
aarcha/.ob/*
aarcha/.pki/*
aarcha/.pylint.d/*
aarcha/.themes/*
aarcha/.vscode/*

```
