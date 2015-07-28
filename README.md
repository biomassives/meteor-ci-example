![Codeship Cycle](https://d1089v03p3mzyq.cloudfront.net/assets/website/pages/features/features-automate-022f2152af1a83434bcd3d3230f880d7.svg)

# Meteor-CI-Example
Meteor continuous integration example project using [Codeship](https://codeship.com).

## Digital Ocean
Create new droplet with two SSH Keys (your local machine + Codeship). You can find Codeship's SSH Key in the Project Settings -> General tab.

## Setup Meteor-Up
Create a new folder ``.deployment`` and initialize a new mup file using ``mup init``. Configure the mup.json file as needed and run ``mup setup`` locally.

## Codeship

### Test
Configure test settings: Project Settings -> Test

#### Setup Commands
```bash
nvm install 0.10.36
nvm use 0.10.36
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
Configure deployment settings: Project Settings -> Deployment

Add a new deployment pipeline with the following custom script:

```bash
npm install -g mup
cd .deployment/production/
mup deploy
```

---
More infos [here](http://howwedoapps.com/2015/07/27/how-i-develop-meteorjs-apps-part-3-continuous-integration-and-delivery-of-your-meteor-package-for-everything-project).