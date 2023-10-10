# Characteristics of Excellent Requirements (REMOVE ME BEFORE SUBMITTING!)

1. Complete
2. Correct
3. Feasible
4. Necessary
5. Prioritized
6. Unambiguous
7. Verifiable

Noah's notes: 
- Do we want to add an in-app notification system on top of email notifications?
- Making comments on commitments: should it be 2 separate functional requirements?

# Functional Requirements

## Platform (Registration, Moderation, etc)

- FR1: Users can register for an account via email and log in using that email.
  - High priority
  - BR3 and others (we need some account to keep track of commitments made by
a clinician, and visibility may be private)

- FR13: Admins can moderate by banning users.
  - Medium priority
  - BR9
  
- FR14: Admins can moderate by editing content.
  - Medium priority
  - BR9

- FR15: Users can block other users.
  - Medium priority
  - BR9

## Commitment Creation

- FR2: Users can create commitments to track their personal goals.
  - High priority
  - BR2

- FR3: Users can create commitments in the context a CME course they are 
enrolled in.
  - High priority
  - BR4

- FR8: Users can create sub-goals for commitments.
  - Medium priority
  - BR3 (Being able to show partial completion invokes the sunk-cost fallacy)

- FR18: Users should be able to create commitments with milestones.
  - Medium priority
  - BR6

- FR24: Remind clinicians about SMART goals when creating commitments.

- FR25: Remind clinicians about HIPAA(?) when creating commitments.

- FR26: Rate commitments

- FR27: Value commitments


## Commitment Management

- FR17: Users can track their own commitments and see their progress in completing their commitment.
  - High priority
  - BR6

- FR101: Users can edit the details of their commitments, including changing the type, deadline, title, description, etc.

- FR6: Users can receive reminders via email for commitments approaching their deadlines.
  - Medium priority
  - BR3
 
## CME Courses

- FR4: CME providers can create courses.
  - High priority
  - BR4

- FR5: CME providers can add users to courses via a code or link.
  - High priority
  - BR4

- FR9: CME providers can view commitments created in the context of a course.
  - High priority
  - BR4

- FR10: CME providers can view a percentage breakdown of the state of commitments in a course (in progress, expired, completed)
  - Medium priority
  - BR7

- FR23: Courses may have optional content tags relating to the subject matter.
  - Medium priority
  - BR8

- FR102: Users can comment within a given course.

- FR103: CME Providers can view a comparison of commitment success rates relative to their other courses.

- FR104: 

## Gamification

- FR19: CME providers can create badges for specific courses.
  - Medium priority
  - BR3
  

- FR20: Users can show their badges on their account
  - Medium priority
  - BR3
  

- FR21: Point system for users by doing and completing commitments
  - Low priority
  - BR3
  

- FR22: Users can share rewards or levels on social media.
  - Low priority
  - BR3
 
## Other Social Elements

- FR7: Users can comment on both their own commitments and those of others.
  - Medium priority
  - BR5 

- FR11: Users can change visibility of commitments made.
  - Medium priority
  - BR9

- FR12: Users can create and join groups.
  - Low priority
  - BR5

- FR16: Users can share their commitments through Twitter.
  - High priority
  - BR3

  
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
  - Medium priority?
  - BR1

