# Bash Scripts

## Recommended Shebang
```sh
#!/usr/bin/env bash
```

## Check if a file exists
```sh
if [ -e  ~/Desktop/myfile ]; then
  echo 'file exists'
else
  echo 'file does not exist'
fi
```

```sh
if [ ! -e  ~/Desktop/myfile ]; then
  echo 'file does not exist'
else
  echo 'file exists'
fi
```

## Check if a directory exists
```sh
if [ -d ~/bin ]; then
  'directory exists'
else
  'directory does not exist'
fi
```

## Download a file
```sh
curl -o /tmp/fiddler-linux.zip http://telerik-fiddler.s3.amazonaws.com/fiddler/fiddler-linux.zip
```

## Extract a zip
```sh
unzip file.zip -d destination_folder
```

## Extract a .tar.gz
```sh
# extract sshbackup tar into ~/
pushd ~;
tar -zxvf /tmp/backupmountdir/sshbackup.tar.gz
popd;
```

## Create a symbolic link
```sh
# create a ~/bin/postman link pointing to ~/.Postman/Postman
ln -s ~/.Postman/Postman ~/bin/postman
```

## Bash loops
http://tldp.org/HOWTO/Bash-Prog-Intro-HOWTO-7.html

```
arr='foo bar baz'
for i in $arr; do
  echo "hello ${i}"
done
```
