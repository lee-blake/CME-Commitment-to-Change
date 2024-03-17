# Setting up IAM on AWS
This document details a basic IAM setup that enables a team to create and manage EC2 instances on an account owned by a third party (in this case, intended to be the client).

This setup does *not* use the IAM Identity Center and organizations. The advantage of avoiding these is simplicity, but this comes at the cost of poor scaling for organizations (lots of busywork if you do this for 100 people) and low granularity of permissions (usually giving more permissions than are strictly necessary to simplify things). **In particular, this second one could be an issue. This setup gives full admin access. Make sure you trust your team and that they will secure the credentials appropriately!**

If you wish to use the IAM Identity Center, the best place to start is AWS's full user documentation [here](https://docs.aws.amazon.com/SetUp/latest/UserGuide/setup-overview.html). Make sure to click the stuff in the left sidebar - there are many subpages to this.

## Preparation
Create an AWS account using the instructions [here](https://docs.aws.amazon.com/SetUp/latest/UserGuide/setup-prereqs-instructions.html). Note that you will most likely need to wait a day or two for them to verify payment info.

It is **strongly** recommended that you [create a budget](https://docs.aws.amazon.com/cost-management/latest/userguide/budget-templates.html) after you do so so that you will get notification if something goes wrong with costs.

## Creating a admin user for someone else

## Distributing credentials
Once you have created the user and saved the credentials, you will need to share them with the intended user(s). You should do this through secure channels - Zoom is preferred over email (email may not be encrypted, which could be a problem), but the meeting should *not* be recorded if this is the case.

Remember that these credentials provide admin management access on your AWS account. If compromised, they could allow for tampering with or deleting of EC2 instances (the machines running the app), as well as creation of malicious ones to distribute malware or run up your bill. **Make sure you trust anyone you distribute these credentials to and make sure they are distributed through secure channels.** One of the best things you can do is make sure that when you generate passwords, they are forced to change at next login. This makes it so that if whatever medium you used to transfer them is hacked later, the password for the account will have change and is not compromised by the loss of the original, generated password.

 Additionally, **make sure any future team understands the seriousness of the security of the management credentials.** Revoke credentials when they are no longer needed using the instructions [here](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_users_manage.html#id_users_deleting_console).

# Other stuff worth noting
While IAM access is necessary to manage deployment and is the main purpose for this document, we have included 

## Shutting down EC2 instances as root
If an EC2 instance is left up by mistake, it can run out hours and run up prices. Here is how you should shut it down as the root user.

TODO

## Adding a domain name
**NOTE: These instructions are still experimental at this point.** They are mostly intended to be a starting point for our work or a future team.

### Registering with Route 53
As far as we can tell, this most likely should be done from the root account by its owner. See [Amazon's instructions for this](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/domain-register.html).

### Routing from Route 53 domain name to an EC2 instance
See [Amazon's instructions](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/routing-to-ec2-instance.html). In theory, this should only need EC2 access and may be done by the deployment team.

### Sending emails from a Route 53 domain
While we cannot verify these instructions at this time due to a lack of a domain to work from, they may be useful for a future team. See [this](https://charlescampbell599.medium.com/setting-up-a-custom-domain-and-email-address-with-aws-ses-e9d39042e192). This will most likely need to be done by the organization handling day-to-day operations with the site.
