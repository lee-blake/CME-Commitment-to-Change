# Functional Requirements

The functional requirements are loosely grouped by concept.

## Platform (Registration, Moderation, etc)

- FR101: Users can register for an account via email and log in.
  - High priority
  - BR1 

- FR102: Admins can moderate by banning user accounts.
  - Medium priority
  - BR1
  
- FR103: Admins can moderate by editing commitments and comments.
  - Medium priority
  - BR1

- FR104: Users can block other users.
  - Medium priority
  - BR1
 
- FR105: The user login page will include password reset functionality under a "Forgot password?" link.
  - High priority
  - BR1
 
- FR106: Users can change their passwords without using the "forgot password"/password reset functionality.
  - Medium priority
  - BR1

- FR107: The system will automatically prune non-activated accounts with unverified emails that are at least a certain age. Alternatively, this functionality can be disabled and run manually via a script that is documented in Deployment.md.
  - High priority
  - BR2

## Commitment Creation

- FR201: Users can create commitments to track their personal goals in changing
their medical practice.
  - High priority
  - BR1

- FR202: Users can create commitments so that they are associated with a CME 
course on the site.
  - High priority
  - BR2

- FR203: Users should be able to create commitments with a number of 
milestones, each of which has their own title, description, and possible 
deadline.
  - Medium priority
  - BR1

- FR204: Users should be able to create commitments where they target a certain
rate over a period (for example, 50% vaccination rate).
  - Medium priority
  - BR1 

- FR205: Users should be able to create commitments where they target reaching a
certain value over a period (for example, 20 clinic hours in the next month).
  - Medium priority
  - BR1

 
## Commitment Management

- FR301: Users can view a list of their commitments that also displays their deadlines and the progress the user has made in completing them.
  - High priority
  - BR1

- FR302: Users can edit every field of a commitment that they can set during 
creation. This includes changing the type of commitment (for example, from 
milestone to value).
  - High priority
  - BR1

- FR303: Users can mark a commitment as complete.
  - High priority
  - BR1

- FR304: Users can mark the individual milestones of a milestone commitment as 
complete.
  - Medium priority
  - BR1

- FR305: Users update the rate achieved so far for a rate commitment.
  - Medium priority
  - BR1

- FR306: Users update the total quantity achieved so far for a value commitment.
  - Medium priority
  - BR1

- FR307: Users can receive reminders via email for commitments approaching their deadlines.
  - Medium priority
  - BR1

- FR308: Users can opt out of receiving email reminders for a commitment when 
they create or edit it.
  - Medium priority (but should go with FR306!)
  - BR1

- FR309: Users can view details and status of individual commitments in a non-editable display view.
  - High Priority
  - BR1

- FR310: Users can mark commitments as discontinued.
  - High Priority
  - BR1

- FR311: The system will automatically mark commitments as expired/past due once
they pass their deadlines.
  - High Priority
  - BR1

- FR312: Users can delete commitments.
  - High Priority
  - BR1 

- FR313: Users can reopen completed and discontinued commitments.
  - High Priority
  - BR1

- FR314: Course providers can view the aggregate status  statistics (total, complete, in progress...) of all commitments made from a commitment template.
  - High priority
  - BR2
 
- FR315: Providers can download a .csv file containing the aggregate statistics of the statuses of their respective derived commitments (total, complete, in progress...) for all of their commitment templates.
  - High priority
  - BR2
 
- FR316: CME Providers can view a comparison of commitment template success rates 
relative to the average of their other commitment templates.
  - Medium priority
  - BR2

## CME Courses

- FR401: CME providers can create courses.
  - High priority
  - BR2

- FR402: CME providers can edit every field of a course that they can set 
during creation. Editing should not disenroll students or instructors.
  - High priority
  - BR2

- FR403: CME providers can add users to courses via a code or link. Clicking 
the link should prompt the user to log in and add them to the course once they
have registered or logged in. Entering the code should enroll the user the same
way as the link.
  - High priority
  - BR2

- FR404: CME providers can view commitments that clinicians associate with a 
course offered by that provider.
  - High priority
  - BR2

- FR405: CME providers can view a percentage breakdown of the state (in 
progress, expired, complete) of commitments in a given course they offer.
  - Medium priority
  - BR2

- FR406: During course creation or editing, optional content tags can be added 
to the course.
  - Medium priority
  - BR2

- FR407: Users can add comments within a given course.
  - Low priority
  - BR1

- FR408: CME Providers can view a comparison of commitment success rates 
relative to the average of their other courses.
  - Medium priority
  - BR2

- FR409: CME Providers can view a comparison of commitment success rates 
relative to other courses with the same tag.
  - Medium priority
  - BR2

- FR410: CME Providers can create 'suggested commitments' for a course that 
users can join. Joining a commitment takes the user to commitment creation and 
auto-populates all fields the provider has specified, including the course, but
allows the user to make any modifications before they finalize the commitment.
  - High priority
  - BR1
 
- FR411: Course pages will clearly display which provider is offering the course in a header next to the title.
  - High priority
  - BR2
 
- FR412: Course invite links will have a button to immediately copy them to the clipboard
  - High priority
  - BR2

- FR413: Courses will have optional fields "unique identifier", "start date", and "end date". These will display
in the provider course dashboard.
  - High priority
  - BR2
 
- FR414: For a given course, providers can download a .csv containing a list of associated commitments and their statuses, as well as the name and email of the respective that made them.
  - High priority
  - BR2

- FR415: Providers can download a .csv file containing the aggregate statistics of the statuses of their respect associated commitments (total, complete, in progress...) for all of their courses.
  - High priority
  - BR2
 
- FR416: Courses will have an optional "course link" field so providers can link to the course on the provider website within the course page.
  - High priority
  - BR1

- FR417: For each suggested commitment in a course, it will display the aggregate status statistics (total, complete, in progress...) of all commitments made from it in that course.
  - High priority
  - BR2



## Gamification

- FR501: CME providers can create badges for specific courses. These badges are
awarded to users when they successfully complete a commitment associated with 
the resepctive course.
  - Medium priority
  - BR1
  

- FR502: Users can show the badges they have earned on their profile.
  - Medium priority
  - BR1
  

- FR503: Users can earn points/levels by completing commitments.
  - Low priority
  - BR1
  

- FR504: Users can share the badges or points they have earned on social media.
  - Low priority
  - BR1
 
## Other Social Elements

- FR601: Users can comment on their own commitments.
  - Medium priority
  - BR1 

- FR602: Users can comment on the commitments of others in the same course if 
the commitment in question is associated with a course they are enrolled in.
  - Medium priority
  - BR1 

- FR603: Users can change visibility of commitments made: public or course 
members only.
  - Medium priority
  - BR1

- FR604: Users can create and join groups.
  - Low priority
  - BR1

- FR605: Users can share their commitments through Twitter.
  - High priority
  - BR1

- FR606: Clinician profiles have optional name and insitutional affiliation fields. If present, these fields will display
where usernames normally would, with name replacing username and affiliation appended.
  - High priority
  - BR2

- FR607: Provider profiles will have an optional institution name field. This will show in place of the provider's username
where the provider's username might be displayed.
  - High priority
  - BR2
 
- FR608: Providers can use a "mailto" link or button within the course list of students to contact individual students about their commitments.
  - High priority
  - BR1

- FR609: Providers can use the "mailto" link functionality to create a single "mailto" link via visually selecting which students in the course that they want to email. All students selected will be collected into a single, one-click link.
  - High priority
  - BR1

## Help, Documentation, and Hints

- FR701: Each page will link to a help page describing what the page does and what next steps a user might take from it.
  - High priority
  - BR1

# Non-functional Requirements

- NR1: The software must be deployed to a cloud computing service.
  - High priority
  - BR1 

- NR2: The software must support layouts for desktop, tablet, and mobile device 
sizes.
  - High priority
  - BR1

- NR3: The software must scale well with users when deployed in a cloud 
environment.
  - High priority
  - BR1

- NR4: The software must be sufficiently clean and modular that another team 
can add new features shortly after transfer.
  - Medium priority
  - BR1 (design constraint)

- NR5: When creating a commitment, the system should suggest that the user 
try to make their commitment a SMART goal.
  - High priority
  - BR1

- NR6: When creating a commitment, the system should remind users not to 
disclose patient information as that would be a HIPAA violation.
  - High priority(!!!)
  - BR1 (more a legal constraint)

- NR7: When registering for an email account, the system will require the user
to verify their email.
  - Medium priority
  - BR1

- NR8: Users can log in using the email they registered with.
  - Medium priority
  - BR1

- NR9: Users can update the status of their commitments without being navigated away from the page they are currently on.
  - Low priority
  - BR1

- NR10: Users should be able to view their password when creating either a clinician
or provider account.
  - Low priority
  - BR1
 
- NR11: Users should be able to view the password that they have entered when
logging into an account.
  - Low priority
  - BR1

- NR12: In the course page, students will display next to the commitments they have made in that course so the student and their commitments can be clearly connected.
  - High priority
  - BR1 

- NR13: Clinicians can sort the list of students in the course page by name. Providers can as well, but can also sort the list by email.
  - Medium priority
  - BR1
 
- NR14: Providers can sort the commonly used Course and CommitmentTemplate tables in the dashboard by their fields.
  - Medium priority
  - BR2
 
- NR15: When using registration's email verification, the user can resend the email if they do not receive it.
  - Medium priority
  - BR1
