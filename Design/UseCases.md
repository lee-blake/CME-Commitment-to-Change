# Actors

- Administrators
  - Administrators are appointed by the owner of the platform to manage it.
- Clinicians
  - Clinicians  are physicians and practitioners that use the platform to make 
and keep commitments. In most, but not all, cases, they will be in some form of 
continuing medical education (CME).
- CME Providers
  - CME providers are the organizations that deliver CME courses. They use 
the platform to enable commitments related to their courses by clinicians. 
CME providers are accredited and are much easier to verify than individual 
clinicians. CME providers are also entire organizations that may run many 
courses with large numbers of clinicians as students.
- CME Educators
  - CME educators are the professionals that teach CME courses. They are part 
of a CME provider organization.

# Use Cases

- UC1: Individual clinicians make commitments outside of a course
  - BR2
  - Clinicians
  - Flow:
    1. Clinician logs in. 
    2. Clinician navigates through interface to "make a new commitment" screen.
    3. Clinician gives a title describing the commitment.
    4. (Optional) Clinician may choose the type of commitment (yes/no, 
milestone, value, etc)
    4. (Optional) Clinician may add milestones, a longer description, etc to 
commitment.
    5. Clinician sets a deadline for the commitment.
    6. Commitment is saved when the clinician hits the button to submit.
    7. (Optional) Clinician may share the newly-made commitment to a social 
media website.
  - Creating commitments is the biggest feature of the application. CME providers
  want clinicians to make these commitments to hold them accountable to the 
  knowledge they obtained and to utilize it in their everyday practice. This
  accountability safeguards the knowledge provided in a CME course.

- UC2: Individual clinicians change commitment details
  - BR3
  - Clinicians
  - Flow:
    1. Clinician logs in.
    2. Clinician navigates to the page displaying their commitments.
    3. Clinician clicks on a commitment to view details about it.
    4. (Optional) Clinician may change deadline.
    5. (Optional) Clinician may change the visibility of the commitment.
    6. (Optional) Clinician may change the title and description.
    7. (Optional) Clinician may change the type of commitment.
    8. (Optional) Clinicians can change which course, if any, the commitment
is associated with.
  - While creating commitments is a big part of the application, if a mistake
  is made when initially creating a commitment or a clinician wants to change
  a specific part of the commitment, there should be a channel to do so. This
  use case covers this channel. 

- UC3: Individual clinicians mark commitments as complete
  - BR2
  - Clinicians
  - Flow:
    1. Clinician logs in.
    2. Clinician navigates to the page displaying their commitments.
    3. Clinician clicks on a commitment to view details about it.
    4. (Optional) Clinician may update progress, as per UC7, before marking it
as complete.
    5. (Optional) Clinician may mark the commitment as complete.
    6. (Optional) Clinician may delete the commitment.
  - (paragraph explaining why this is a use case)

- UC4: CME Providers associate clinicians with a course
  - BR4
  - CME Providers, CME Educators, Clinicians
  - Flow:
    1. (Optional, may already be complete) CME Provider creates a course.
    2. (Optional, may already be complete) CME Provider designates educators
for a course. Should they not wish to do so, CME Provider replaces CME educator
in the steps below.
    3. CME Educator obtains invite link for a specific course.
    4. CME Educator distributes invite link to clinicians.
    5. Clinicians accept the link to join the course.
  - (paragraph explaining why this is a use case)

- UC5: CME providers gather relative course effectiveness data for commitments
to change
  - BR7 & BR8
  - CME Providers
  - Flow:
    1. CME provider navigates to show the statistics for the course.
    2. CME provider examines section "courses in same provider" to see average
of their other courses.
    3. CME provider examines section "similar courses" to see statistics for courses with similar tags. 
  - (paragraph explaining why this is a use case)

- UC6: Clinician receives reminder email 
  - BR3
  - Clinicians
  - Flow:
    1. Clinician creates a commitment with a deadline.
    2. Time passes until some interval near deadline
    3. Email is sent to clinician reminding them of the commitment deadline.
  - (paragraph explaining why this is a use case)

- UC7: Clinician updates progress on a commitment
  - BR2
  - Clinicians
  - Flow:
    1. Clinician logs in.
    2. Clinician navigates to the page displaying their commitments.
    3. Clinician clicks on a commitment to view details about it.
    4. (Optional) Clinician may mark milestones complete if it is a milestone 
commitment.
    5. (Optional) Clinician may update values if it is a value commitment.
    6. (Optional) Clinician may comment on the commitment to note other 
progress.
  - (paragraph explaining why this is a use case)


- UC8: Clinician creates a commitment within a course
  - BR4
  - Clinicians
  - Flow:
    1. Clinician logs in.
    2. Clinician navigates to course page.
    3. (Optional) If the course has sample commitments, Clinician may select 
"Create from this commitment" to prefill all fields except deadline
    4. (Optional) Otherwise, Clinician selects a button creating a commitment
in the course.
    5. Clinician fills out or edits the usual details for a commitment.
    6. Upon submitting, the commitment is associated with the course.
  - (paragraph explaining why this is a use case)

- UC9: Administrator moderates the website
  - BR9
  - Administrators
  - Flow:
    1. User disrupts other clinicians and the community.
    2. Administrator logs in.
    2. (optional) Admin may edit offending comments and commitments
    3. (optional) Admin may delete offending comments and commitments
    4. (optional) Admin may ban user for a period of time
    5. (optional) Admin may ban user permanently
  - (paragraph explaining why this is a use case)

