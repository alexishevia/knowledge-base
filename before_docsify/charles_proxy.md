
https://www.charlesproxy.com/

## Setting Charles Proxy with iOS device
http://www.devsbedevin.com/debugging-ios-ssl-traffic/

## Setting Up Charles SSL Proxy on Mac (and phones)
https://fng-confluence.fox.com/pages/viewpage.action?pageId=96471705

## Setting UP Charles Proxy on Ubuntu
1. Open Charles
2. Open the Ubuntu Network tools > Network Proxy > Manual and set:
    `localhost:8888` for http and https
    Note: this is the default port used by Charles, you can modify it at `Proxy > Proxy Settings...`

For https requests to work, you need to add each host at Charles `Proxy > SSL Proxying Settings`

You will also need to install Charles root certificate following these instructions:
https://askubuntu.com/questions/73287/how-do-i-install-a-root-certificate

### Using an Android Virtual Device with Charles
Inside the running Android device, go to `Settings > Network & Internet > Wifi` and click on the pencil icon to edit.
Set the http proxy to be the IP address of your host computer + port 8888 (or whichever port you configured in Charles)
You can confirm your IP address by going to Charles `Help > Local IP Address`
