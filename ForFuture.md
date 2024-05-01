# For Future
This file contains information relevant to future teams.

## Known Issues
Here are some known issues that should be fixed to continue work on the project.

### Dependency updates
We have frozen the version requirements with pip to avoid new versions potentially breaking things in the middle of an iteration. As a result, from time to time, you will need to unfreeze `requirements.txt` by changing every `==` to `>=` and then either rebuild your Docker containers or re-run the relevant install command. Either way, documentation for these is in `Development.md` on this repo. After the update is complete, you should verify that everything works, then change every `>=` back to `==` and pull request. This allows you to make releases to accommodate new versions of the software while remaining sure that you can still replicate without problems.

### Lack of frontend testing
At the advice of Dr. Ergin, we do not have frontend testing. The reason is it that we make so many calls to datatables and D3 that getting to his 70% threshold did not look feasible, and at the same time, our JS footprint has been pretty small. We recommend fixing this. With sufficient research, you should be able to find how to get datatables to work with some JS testing framework. D3 can be dummy-tested via checking if it creates some `<svg>` tag.

### Duplication, linting, etc
The current structure in view tests have separate inner classes for get/post. Add a third to just check access for unauthorized users and move those tests off of get/post. Then you can have a fixture to condense the general flow of target url, login, get/post to obtain response. Making `target_url` an attribute on the get/post class, or even higher up, should also be done to avoid declaring it every time you look for it in a post form.

We suppress a handful of pylint refactor inspections because they show up everywhere. Solving this duplication will most likely squash one of them. Some of the others are genuinely the fault of Django (too many ancestors) or pytest (fixtures can cause too many parameters). You can walk through and manually suppress them if they cannot be worked around.

### Template structure/organization
A number of templates could really use a rework. In most cases that means just splitting them up further, but in a few, some of the stuff outside the include should be moved into the include or vice versa. The best places to start are the larger pages - Course view, dashboards, possible statistics.


## Possible improvements
Here are some areas that would be good choices for the next features.

### Email unsubscribe mechanism
With reminder emails no longer being strictly triggered by the users, it would be good to implement this. That way, the risk of being reported a spam site decreases. You should also implement uniqueness-of-email requirements.

### Restricting reminder emails further
Requiring manually-scheduled emails to be unique per (commitment, date) pair should be done at a minimum to avoid users being able to get you banned from Gmail SMTP in one day. Also consider restricting creation to active commitments only. 

### Privacy filters
As the core functionality of the site is more or less in place, and as commitments can be shared to social media, allowing provider and clinicians to determine who can view their pages is a good idea. Reasonable defaults - similar to what rules we currently have - should be provided. Additionally, allowing clinicians an option to hide their email from providers might make them more willing to use the site.

### More CRUD/action options
Currently, you often have to navigate to a specific page to create or delete a new object, whether that be a course, a commitment, or something else. It would be nice to have more places to perform these CRUD actions. Some more specific examples would be:
- Creation buttons at the top of each section on the clinician dashboard (create commitments) and provider dashboard (create courses and commitment templates)
- Commitment complete/discontinue modals in the commitment view page for clinicians so they don't have to navigate back to the dashboard

### Breadcrumbs and navbar highlighting
Right now there is no indication of what page you are in relation to the rest of the website. To help improve navigation, you could add the bootstrap "active" class to a page in the navbar if the current url matches the navbar element url. Breadcrumbs could also be added to the rest of the pages to help users understand where they are in the site's page hierarchy.

### Better visual indication for commitment reminder emails
There is no indication that a commitment has a reminder email scheduled on either the clinician dashboard, or on the commitment view page itself. This means a user must navigate through two pages to see if a single commitment has a reminder email. It would be good to make an indication on the dashboard, maybe just an envelope icon could be present to show there are scheduled reminder emails. On the commitment view page, a more detailed description of the reminder emails could be present. A reminder emails page could also be created to show all currently scheduled reminder emails with links to those management pages.