
**What is happening?**

CHG0022281 MCS SILVER - Move and Upgrade Trident to v21.1.1

- Upgrade Trident to the latest version in preperation for the OCP 4.6 upgrade
- Switch back to using the operator instead of the legacy CLI driven install (now that [the bug](https://github.com/NetApp/trident/issues/474) is fixed)
- Change the namespace Trident is installed in to leverage build in OCP monitoring

**When?**

Starting at [EXAMPLE: Thursday April 2 @ 06:00 AM] and finishing at [EXAMPLE: Thursday April 2 @ 09:00 AM]

**Will there be an impact on the Platform apps?**

While the playbook runs, storage provisioning will be unavailable. This means volume creation, deletion, or resizing operations will be in a pending state. The playbook is expected to take 30 min or less to run. Any pending operations should be picked up once the new Operator is in place.

Existing volumes should not be impacted.

**Do I need to do anything?**

No action required.

**Check the #devops-alert channel for the announcement of when the change is complete and check the health of your app.**

**Where do I get help if my app doesn't work after the change is complete?**

Each Platform application has an assigned DevOps Specialist within the Ministry so contact them first. If you don't know who your assigned DevOps Specialist, check with the app's Product Owner.

The DevOps Specialist will troubleshoot the issue with the app and if they need help, they will reach out to the Platform Services Team and the Developer Community in Rocket.Chat as per these [RocketChat Channel Use Guidelines](
https://developer.gov.bc.ca/Getting-human-support-for-issues-not-covered-by-devops-requests).
