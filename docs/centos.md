
These steps were tested on CentOS 8.
They may also work for other versions.

```bash
# install node.js
sudo yum install wget
wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash
# reopen terminal
nvm install 16.11

mkdir jsreportapp
cd jsreportapp
npm i -g @jsreport/jsreport-cli
jsreport init
jsreport configure

# install chrome dependencies
wget -qO- https://intoli.com/install-google-chrome.sh | bash

sudo yum install nano
nano jsreport.config.json

# add to the jsreport.config.json the following
# it makes chrome less secure but currently the only way on CentOS
# make sure there is only single chrome node in the config
"chrome": {
  "launchOptions": {
    "args": ["--no-sandbox"]
  }
}

# save and start jsreport to see it running on port 5488
jsreport start

# the next steps are optional to start jsreport on boot
npm install pm2 -g
pm2 start server.js
pm2 startup
# run the output of previous command
```
Note that on headless centos you may need to install additional libs mentinoned [here](https://github.com/GoogleChrome/puppeteer/blob/master/docs/troubleshooting.md#chrome-headless-doesnt-launch-on-unix).
