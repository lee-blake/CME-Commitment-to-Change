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
  - BR1
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
  - BR1
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

- UC3: Clinician updates progress on a commitment
  - BR1
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
  - While this may help some clinicians organize their commitments and therefore
    organize their progression towards completion, the real reason this is a 
    use case is that it allows clinicians to demonstrate to peers on the site 
    and patients on social media that they are progressing with their 
    commitment. In particular, if clinicians can show their progress for their 
    commitments, they will be more willing to share them to social media. They 
    are then more likely to feel accountable to the public for their commitment,
    and therefore will be motivated both to progress in it and to update 
    progress for others to see. This is likely to be the primary form of 
    engagement with the platform outside of the brief creation and completion 
    of commitments.

- UC4: Individual clinicians mark commitments as complete
  - BR1
  - Clinicians
  - Flow:
    1. Clinician logs in.
    2. Clinician navigates to the page displaying their commitments.
    3. Clinician clicks on a commitment to view details about it.
    4. (Optional) Clinician may update progress, as per UC3, before marking it
as complete.
    5. (Optional) Clinician may mark the commitment as complete.
    6. (Optional) Clinician may delete the commitment.
  - (paragraph explaining why this is a use case)

- UC5: CME Providers associate clinicians with a course
  - BR2
  - CME Providers, CME Educators, Clinicians
  - Flow:
    1. (May already be complete) CME Provider creates a course.
    2. (Optional) CME Provider designates educators for a course. Should they
    not wish to do so, CME Provider replaces CME educator in the steps below.
    3. CME Educator obtains invite link for a specific course.
    4. CME Educator distributes invite link to clinicians.
    5. Clinicians accept the link to join the course.
  - This interaction will be the one that CME providers spend most of their 
    time performing. While their main goal is to get data about the courses, it
    is first necessary to organize by course to create that data. Making this 
    as easy on individual clinicians as possible will make them more likely to 
    associate with a course and therefore generate that data; thus, it falls to
    the CME Provider and potentially their Educators to perform the bulk of 
    this step.

- UC6: Clinician creates a commitment within a course
  - BR2
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
  - For CME Providers to get data about the implementation of their education, 
    it is necessary to connect clinician practice with the courses themselves. 
    Since the way this platform determines implementation of practice is 
    through commitments, it is necessary to associate the commitments with 
    courses. In most circumstances, these commitments will come out of a 
    course, and therefore it makes sense for the clinician to create them in 
    the context of a course page.

- UC7: Clinician asks for help in meeting a commitment
  - BR1
  - Clinicians
  - Flow:
    1. Clinician logs in 
    2. Clinician navigates to the page displaying their commitments.
    3. Clinician clicks on a commitment to view details about it.
    4. Clinician comments on that commitment asking for help.
    5. Other clinicians who are watching that commitment may see and offer help.
    6. Clinician clicks on the course associated with the commitment.
    7. Clinician comments in the course asking for assistance with completing 
    the commitment.
    8. Other clinicians in the course can see the comment and may offer help. 
    This may include educators for that course.
    9. Clinician shares the commitment to social media asking for help.
    10. Other clinicians on social media may offer help.
  - One of the benefits of associating clinicians into courses is that it 
    socially connects them. Leveraging this to help them complete commitments 
    furthers one of the main business requirements for the platform. Offering a
    number of different methods to resolve difficulties is important, as we 
    cannot be sure that all clinicians will interact in the same manner on the 
    platform.

- UC8: CME providers gather relative course effectiveness data for commitments
to change
  - BR2
  - CME Providers
  - Flow:
    1. CME provider navigates to show the commitment statistics for the course.
    2. CME provider examines section "courses in same provider" to see average
    of their other courses.
    3. CME provider examines section "similar courses" to see statistics for 
    courses with similar tags. 
    4. CME provider repeats the process for any other courses of interest.
    5. CME provider may make make note of unusually high or low relative rates
    of commitment completion.
  - The primary benefit to CME providers that this platform will provide is 
    data about implementation of education through commitments. While this will
    likely involve much less time than associating clinicians and courses, it 
    is just as important and will be reason providers stay on the platform. 
    Comparisons to other courses offered by the same provider and similar 
    courses offered by other providers are both likely to occur, as both can 
    offer significant lessons about which courses need the most improvement.

- UC9: Clinician receives reminder email 
  - BR1
  - Clinicians
  - Flow:
    1. Clinician creates a commitment with a deadline.
    2. Time passes until some interval near deadline or some time passes
    without updating commitment progress.
    3. Email is sent to Clinician reminding them of the commitment deadline.
    4. Clinician revisits commitment page.
    5. Clinician is reminded of their commitment and how much time is left.
  - Reminders are important in two cases. First, the clinician may have 
    forgotten about their commitment. Second, the clinician may have made 
    progress on the commitment, but simply not updated it. In the first case, 
    reminding helps the clinician accomplish their commitment. In the second, 
    it helps get more accurate data for CME providers. Automated reminders via 
    email are an easy and relatively nonintrusive way to accomplish this 
    important function.

- UC10: Administrator moderates the website
  - BR1
  - Administrators
  - Flow:
    1. User disrupts other clinicians and the community.
    2. User's comments or commitments are reported.
    3. Administrator logs in.
    4. (optional) Admin may edit offending comments and commitments
    5. (optional) Admin may delete offending comments and commitments
    6. (optional) Admin may ban user for a period of time
    7. (optional) Admin may ban user permanently
  - While it is unlikely that many clinicians will abuse the platform, the 
    occasional bad actor will occur. It is necessary to handle these abuses 
    promptly before they derail the main purposes of the platform - enabling 
    clinicians to meet their commitments and gathering data for CME providers. 
    This will likely occur occasionally and the administrator will be 
    responding to reports.

