![Codeship Status](https://codeship.com/projects/5d8075f0-16fb-0133-586f-761f41fcaf85/status?branch=master)
# meteor-ci-example
Meteor continuous integration example project using Codeship.

## Digital Ocean
Create new droplet with two SSH Keys (your local machine + Codeship). You can find the SSH Key from Codeship in the Project Settings >> General tab.

## Setup Meteor-Up
Create a new folder ``.deployment`` and initialize a new mup file using ``mup init``. Configure the mup.json file as needed and run ``mup setup`` locally.

## Codeship

### Test
Project Settings >> Test
#### Setup Commands
```bash
nvm install 0.10.36
nvm use 0.10.36
npm install jshint -g
curl -o meteor_install_script.sh https://install.meteor.com/
chmod +x meteor_install_script.sh
sed -i "s/type sudo >\/dev\/null 2>&1/\ false /g" meteor_install_script.sh
./meteor_install_script.sh
export PATH=$PATH:~/.meteor/
npm install -g velocity-cli
meteor --version
```
#### Test Command
```bash
meteor --test --release velocity:METEOR@1.1.0.2_3
```

### Deployment
Project Settings >> Deployment
Add new deployment pipeline:

```bash
npm install -g mup
cd .deployment
mup deploy
``

---
More infos [here](http://howwedoapps.com/2015/07/27/how-i-develop-meteorjs-apps-part-3-continuous-integration-and-delivery-of-your-meteor-package-for-everything-project).
