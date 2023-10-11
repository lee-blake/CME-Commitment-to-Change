# Characteristics of Excellent Requirements (REMOVE ME BEFORE SUBMITTING!)

1. Complete
2. Correct
3. Feasible
4. Necessary
5. Prioritized
6. Unambiguous
7. Verifiable


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

- FR201: Users can create commitments to track their personal goals in changing
medical practice.
  - High priority
  - BR1

- FR202: Users can create commitments in the context a CME course they are 
enrolled in.
  - High priority
  - BR2

- FR203: When creating a commitment, the system should suggest that the user 
try to make their commitment a SMART goal.
  - High priority
  - BR1

- FR204: When creating a commitment, the system should remind users not to 
disclose patient information as that would be a HIPAA violation.
  - High priority(!!!)
  - BR1 (more a legal constraint)

- FR204: Users should be able to create commitments with a number of 
milestones, each of which has their own title, description, and possible 
deadline.
  - Medium priority
  - BR1

- FR205: Users should be able to create commitments where they target a certain
rate over a period (for example, 50% vaccination rate).
  - Medium priority
  - BR1 

- FR206: Users should be able to create commitments where they target reaching a
certain value over a period (for example, 20 clinic hours in the next month).
  - Medium priority
  - BR1


## Commitment Management

- FR301: Users can track their own commitments and see their progress in completing their commitment.
  - High priority
  - BR1

- FR302: Users can edit the details of their commitments, including changing the type, deadline, title, description, etc.
  - High priority
  - BR1

- FR303: Users can mark the individual milestones of a milestone commitment as 
complete.
  - Medium priority
  - BR1

- FR304: Users update the rate achieved so far for a rate commitment.
  - Medium priority
  - BR1

- FR305: Users update the total quantity achieved so far for a value commitment.
  - Medium priority
  - BR1

- FR306: Users can receive reminders via email for commitments approaching their deadlines.
  - Medium priority
  - BR1

- FR 307: Users can opt out of receiving email reminders for a commitment when 
they create or edit it.
  - Medium priority (but should go with FR306!!!)
  - BR1
 
## CME Courses

- FR401: CME providers can create courses.
  - High priority
  - BR2

- FR402: CME providers can add users to courses via a code or link.
  - High priority
  - BR2

- FR403: CME providers can view commitments that clinicians associate with a 
course.
  - High priority
  - BR2

- FR404: CME providers can view a percentage breakdown of the state of 
commitments in a course (in progress, expired, completed)
  - Medium priority
  - BR2

- FR405: Courses may have optional content tags relating to the subject matter.
  - Medium priority
  - BR2

- FR406: Users can comment within a given course.
  - Low priority
  - BR1

- FR407: CME Providers can view a comparison of commitment success rates 
relative to the average of their other courses.
  - Medium priority
  - BR2

- FR408: CME Providers can view a comparison of commitment success rates 
relative to other courses with the same tag.
  - Medium priority
  - BR2

## Gamification

- FR501: CME providers can create badges for specific courses.
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

