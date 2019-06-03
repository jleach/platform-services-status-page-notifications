# Platform Services Status Page Notifications
This repository contains: 
- The status update files (in markdown) used to populate the status page

This repository does NOT contain: 
- The code required to re-generate the status page dashboard when updates are made
  - This is located in the [platform-services](https://github.com/BCDevOps/platform-services/tree/master/apps/statuspage/dashboard_updater) main repo
- The code required to build the Status Page components; 
  - This is located in the [platform-services](https://github.com/BCDevOps/platform-services/tree/master/apps/statuspage) main repo

## Usage to post Status Update Notifications
The general usage of this repository is as follows: 
- Create a branch of the repo
- Add a file to the `notifications` folder in the format: 
  - Filename: `MM-DD-YY-HHMM.md`
  - Content: The relevant notification content

# Webhook Configuration
A webhook should be configured on this repo once it's obtained from the Pipeline style BuildConfig in the OpenShift `tools` namespace. 
A `Generic` webhook should be used, which helps OpenShift not reject the webhook on the basis that it comes from a separate repo. 
