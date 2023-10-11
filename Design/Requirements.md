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

- FR101: Users can register for an account via email and log in using that 
email.
  - High priority
  - BR1 

- FR102: Admins can moderate by banning users.
  - Medium priority
  - BR1
  
- FR103: Admins can moderate by editing content.
  - Medium priority
  - BR1

- FR104: Users can block other users.
  - Medium priority
  - BR1

## Commitment Creation

- FR201: Users can create commitments to track their personal goals.
  - High priority
  - BR1

- FR202: Users can create commitments in the context a CME course they are 
enrolled in.
  - High priority
  - BR2

- FR203: Remind clinicians about SMART goals when creating commitments.
  - High priority
  - BR1

- FR204: Remind clinicians about HIPAA when creating commitments.
  - High priority(!!!)
  - BR1 (more a legal constraint)

- FR204: Users should be able to create commitments with milestones.
  - Medium priority
  - BR1

- FR205: Rate commitments
  - Medium priority
  - BR1 

- FR206: Value commitments
  - Medium priority
  - BR1


## Commitment Management

- FR301: Users can track their own commitments and see their progress in completing their commitment.
  - High priority
  - BR1

- FR302: Users can edit the details of their commitments, including changing the type, deadline, title, description, etc.
  - High priority
  - BR1

- FR303: Users can receive reminders via email for commitments approaching their deadlines.
  - Medium priority
  - BR1
 
## CME Courses

- FR401: CME providers can create courses.
  - High priority
  - BR2

- FR402: CME providers can add users to courses via a code or link.
  - High priority
  - BR2

- FR403: CME providers can view commitments created in the context of a course.
  - High priority
  - BR2

- FR404: CME providers can view a percentage breakdown of the state of commitments in a course (in progress, expired, completed)
  - Medium priority
  - BR2

- FR405: Courses may have optional content tags relating to the subject matter.
  - Medium priority
  - BR2

- FR406: Users can comment within a given course.
  - Low priority
  - BR1

- FR407: CME Providers can view a comparison of commitment success rates relative to their other courses.
  - Medium priority
  - BR2

- FR408: CME Providers can view a comparison of commitment success rates relative to other courses with the same tag.
  - Medium priority
  - BR2

## Gamification

- FR501: CME providers can create badges for specific courses.
  - Medium priority
  - BR1
  

- FR502: Users can show their badges on their account
  - Medium priority
  - BR1
  

- FR503: Point system for users by doing and completing commitments
  - Low priority
  - BR1
  

- FR504: Users can share rewards or levels on social media.
  - Low priority
  - BR1
 
## Other Social Elements

- FR601: Users can comment on both their own commitments and those of others.
  - Medium priority
  - BR1 

- FR602: Users can change visibility of commitments made: public or course 
members only.
  - Medium priority
  - BR1

- FR603: Users can create and join groups.
  - Low priority
  - BR1

- FR604: Users can share their commitments through Twitter.
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

