# Platform Services Status Page Notifications
This repository contains: 
- The status update files (in markdown) used to populate the status page
- The code required to re-generate the status page dashboard when updates are made

This repository does NOT contain: 
- The code required to build the Status Page components; 
  - This is located in the [platform-services](https://github.com/BCDevOps/platform-services/tree/master/apps/statuspage) main repo

## Usage to post Status Update Notifications
The general usage of this repository is as follows: 
- Create a branch of the repo
- Add a file to the `notifications` folder in the format: 
  - Filename: `MM-DD-YY-HHMM.md`
  - Content: The relevant notification content


# The Components

## The Ansible Playbook
The ansible playbook does most of the heavily lifting and is primarily responsible for the following tasks: 
- Generating the Grafana dashboard with Jijna2
- Populating the Markdown panel with all status updates in the `notifications` folder
- Sending an update to Rocket Chat with the latest update

## The Jenkinsfile
The Jenkinsfile is used with OpenShift to kick off the ansible playbook. The variables should be customized as desired. 

- Within the OpenShift tooling project, create the Pipeline BuildConfig
```
oc new-build [repo name] --context-dir=.pipeline
```

- Once generated, obtain the GitHub webhook and add it to the repository
- The Jenkinsfile pipeline will use a cusotmized podTemplate with Ansible installed; it also mounts up a secret that must exist in the same namespace: 
  - Secret name: `rocketchat`
  - Secret type: `Opaque`
  - Secret Contents: 
    - key: token
      - content: RocketChat webhook token
    - key: username
      - content: displayname of the user posting the message

## The Jenkins Agent
The Jenkins Agent folder holds the Dockerfile used to build the Jenkins agent that has ansible installed on it. 

## RocketChat Integration
A simple script is required on the incoming webhook for integration with Ansible. 

```
class Script {
  process_incoming_request({ request }) {
   // console.log(request.content);

    return {
      content: {
        text: request.content.text,
        icon_url: request.content.icon_url,
        username: request.content.username
      }
    };
  }
}
```

