Prerequisites
```
# Install nodejs current from https://nodejs.org/en/ 
#   - You'll need Node.js version > 8.x and npm > 5.x - check this by running node -v and npm -v
# Install Python 3 from https://www.python.org/downloads/
# Install the AWS CLI https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-install.html
pip3 install awscli --upgrade --user
# Configure the AWS CLI
aws configure
# Install the Amplify CLI
npm install -g @aws-amplify/cli
# Configure the Amplify CLI
amplify configure
# Install Serverless Framework https://serverless.com/
npm install serverless -g
```

Create a React App

```
# create a new react app
npm init react-app serverless-webapp
# change into your app dir
cd serverless-webapp
# check your webapp runs locally with
npm start
# hit ctrl-c to end the localhost server
# install amplify into your react project
npm install aws-amplify
# initialise the amplify project
amplify init
# add auth
amplify add auth
# add hosting
amplify add hosting
# update App.js (see below) to include the withAuthenticator Higher Order Component (HOC)
# publish
amplify publish
```


```
import React, {Component} from 'react';
import logo from './logo.svg';
import './App.css';
import { withAuthenticator } from 'aws-amplify-react';

class App extends Component {

  render(){
    return (
      <div className="App">
        <header className="App-header">
          <img src={logo} className="App-logo" alt="logo" />
          <p>
            Edit <code>src/App.js</code> and save to reload.
          </p>
          <a
            className="App-link"
            href="https://reactjs.org"
            target="_blank"
            rel="noopener noreferrer"
          >
            Learn React
          </a>
        </header>
      </div>
    );
  }
}

export default withAuthenticator(App,true); 
```


Create an API with Serveless Framework
```
# check Serverless is installed by running sls - you should see a help menu (don't use powershell)
# change dir into the serverless-webapp directory
cd serverless-webapp
# create a Serverless project
serverless create --template aws-python3 --path backend
# update serverless.yml (see below - basic)
# deploy your API
sls deploy
# test your API by browsing to it
```
```
service: backend
provider:
  name: aws
  runtime: python3.7
  stage: dev
  region: ap-southeast-2
functions:
  hello:
    handler: handler.hello
    events:
      - http:
          path: hello
          method: get
```

