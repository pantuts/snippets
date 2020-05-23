[![tux](http://files.softicons.com/download/system-icons/tux-penguin-icons-by-yellow-icon/png/128/Penguin_2.png)]()

# curl
Download with resume
```
curl -L -O -C - URL.file
```

# docker
Import sql
```
docker exec -i ID mysql -u root --password=PASSWORD dbname < sql.sql
```

# ffmpeg
Cut from-to
```
ffmpeg -i FILEINPUT -ss "2:25" -to "3:29" -f mp4 -y OUTPUT.mp4
```

# git
.idea in gitignore fix
```
git rm --cached -r .idea
```
Reset initial commit
```
git update-ref -d HEAD
```
Show files
```
git ls-tree -r master --name-only
```
With heroku
```
# heroku create APP_NAME_STAGE
git remote add STAGE git@heroku.com:APP_NAME_STAGE.git
git push stage master
```

# gource
Visualize commits
```
gource -s .1 -1920x1080 --auto-skip-seconds .1 --multi-sampling --stop-at-end --highlight-users --hide mouse,progress --file-idle-time 15 --max-files 0 --background-colour 000000 --font-size 24 --title "TITLE" --output-ppm-stream - --output-framerate 30 .git| ffmpeg -y -f image2pipe -vcodec ppm -i - ~/Desktop/test.mp4
```

# ls
Sort by modified date
```
ls -t
ls -tr # reverse
```

# pacman
Query first then remove by file
```
pacman -Qs 'python2-*' | grep '/python' | cut -d '/' -f 2 | awk '{print $1}' > /tmp/remove.txt
while read line; do sudo pacman -Rd --noconfirm --nodeps $line; done < /tmp/remove.txt
```
Remove package+deps
```
pacman -Rcn package
```
Clear cache of uninstalled packages
```
pacman -Sc
```

# rsync
With key file
```
rsync -avz --progress -e "ssh -i ~/FILE.pem" user@ip: .
```
With different port
```
rsync -avz --progress -e "ssh -i ~/FILE.pem -p PORT" user@ip: .
```

# ssh
Change key file permission
`chmod 400 FILE.pem`
With key file
`ssh -i FILE.pem user@ip`

# wget
Download all images
```
wget -U "Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:49.0) Gecko/20100101 Firefox/49.0" -nd -r --level=1  -e robots=off -A jpg,jpeg,png,gif,bmp -H --domains DOMAIN DOMAIN
```

# while
Read text line by line
```
while read line; do echo $line; done < file
```

# youtube-dl
mp3
```
youtube-dl --extract-audio --audio-format mp3 -o "%(title)s.%(ext)s" --verbose URL
```


# OTHERS

Convert vdi to qcow2
```
qemu-img convert -f vdi -O qcow2 Centos7.8.vdi Centos7.8.qcow2
```
