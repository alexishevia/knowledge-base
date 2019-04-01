# Unix Commands CheatSheet

## Find out registrar info for a domain
`whois domain.com`

## Find out dns name servers for a domain
`dig +short NS domain.com`

## Change permissions recursively
`chmod -R 755 directoryNameHere`

## Extract tar.gz
`tar -zxvf file.tar.gz`

## Find files by name
`find /start/point -name myFileName`
[see advanced features for more complex searches](http://content.hccfl.edu/pollock/unix/findcmd.htm)
[3 basic refactoring tools for your command line](http://blog.crowdint.com/2013/08/23/3-basic-refactoring-tools-for-your-command-line.html)

## Find and replace all instances of a string in a directory
```
find /start/point -name '*.js' -print0 | xargs -0 sed -i 's/var/const/g'
```

## Find out which process is using port
```
netstat -tulpn | grep portNumber
lsof -i -P | grep portNumber
```

## Kill process
```
kill -9 processID
```

## Check Memory Usage
http://www.cyberciti.biz/faq/linux-check-memory-usage/

## Run a command in a different directory without cd-ing into it
```
pushd folder/path; yourCommand; popd;
pushd build; python -m SimpleHTTPServer; popd;
```

## Send Data Across Networked Computers with Netcat Using the Command Line
```
netcat -l 4444 #on 1st machine
netcat FIRST_MACHINE_IP 4444 #on 2nd machine
```

## Bash loops
http://tldp.org/HOWTO/Bash-Prog-Intro-HOWTO-7.html

```
arr='foo bar baz'
for i in $arr; do
  echo "hello ${i}"
done
```

## Useful utils

- [json-minify](https://www.npmjs.com/package/json-minify)  
  The opposite of Pretty-Print JSON; For all the times you want to rid of
  whitespace.

- [jq](https://stedolan.github.io/jq/)
  lightweight and flexible command-line JSON processor

## Crop PNGs automatically
[Using ImageMagick](https://askubuntu.com/questions/351767/how-to-crop-borders-white-spaces-from-image)
```
mkdir cropped
find ./ -name "*.png" -exec convert {} -trim ./cropped/{} \;
```

## Running nodeJS programs directly in bash
```
# run the command
node <<EOF
  console.log('hello');
EOF

# store the result in a variable
FOO=$(node <<EOF
  console.log('foo')
EOF
)

# or, if it is a single line
FOO=$(node -e 'console.log(Date.now())')

# pipe output to another command
(
node <<EOF
  console.log('foo')
  console.log('bar')
EOF
) | grep oo
```

## Open command result in vim (or your default editor)
    ```
    curl google.com | $EDITOR -
    ```

## Silver Surfer (ag)
- Specify a file pattern
    ```sh
    ag -G .js$ myword
    ```

- Ignore a file pattern
    ```sh
    ag --ignore test myword
    ```

## Ack (ack-grep)
- Recursively Search All Files For A String:
    ```sh
    cd /path/to/dir
    ack-grep myword
    ```

- Avoid a specific dir
    ```sh
    ack-grep --ignore-dir=build myword
    ```
    Note: take a look at `~/.ackrc` for default ignored directories

- Search for specific file types
    ```sh
    ack-grep --js myword
    ```
    Note: take a look at `~/.ackrc` for other types to use

- Only return instances of pattern surrounded by word boundaries
    ```
    # will match "ten", but not "tenet" or "attend"
    ack-grep -w ten
    ```

- Ignore a file path pattern
    ```
    ack -f | grep -v -x '.*test.*' | ack -x myword
    ```

- Only return filenames where matches were found instead of the complete match result
    ```
    ack-grep -cl myword
    ```

## Check available versions for a package
```
apt-cache policy <packageName>
```
