# Actors

- Administrators
  - Administrators are appointed by the owner of the platform to manage it.
- Clinicians
  - Clinicians  are physicians and practicioners that use the platform to make 
and keep commitments. In most, but not all, cases, they will be in some form of 
continuing medical education (CME).
- CME Providers
  - CME providers are the organizations that deliver CME courses. They use 
the platform to enable commitments related to their courses by clinicians. 
CME providers are accredited and are much easier to verify than individual 
clinicians. CME providers are also entire organizations that may run many 
courses with large numbers of clinicians as students.
- CME educators
  - CME educators are the professionals that teach CME courses. They are part 
of a CME provider organization.

# Use Cases

- UC1: Individual clinicians make commitments
  - BR2
  - Clinicians
  - Flow:
    1. Clinician logs in. 
    2. Clinician navigates through interface to "make a new commitment" screen.
    3. Clinician gives a title describing the commitment.
    4. (Optional) Clinician may add subgoals, a longer description, etc to 
commitment.
    5. Clinician sets a deadline for the commitment.
    6. Commitment is saved when the clinician hits the button to submit.
    7. (Optional) Clinician may share the newly-made commitment to a social 
media website.
  - (paragraph explaining why this is a use case)

- UC2: Individual clinicians change commitment details
  - BR3
  - Clinicians
  - Flow:
    1. Clinician logs in.
    2. Clinician navigates to the page displaying their commitments.
    3. Clinician clicks on a commitment to view details about it.
    4. (Optional) Clinician may change deadline.
    5. (Optional) Clinician may change the visibility of the commitment.
  - (paragraph explaining why this is a use case)

- UC3: Individual clinicians mark commitments as complete
  - BR2
  - Clinicians
  - Flow:
    1. Clinician logs in.
    2. Clinician navigates to the page displaying their commitments.
    3. Clinician clicks on a commitment to view details about it.
    4. (Optional) Clinician may mark subgoals as complete.
    5. (Optional) Clinician may mark the commitment as complete.
    6. (Optional) Clinician may delete the commitment.
  - (paragraph explaining why this is a use case)

- UC4: CME providers associate clinicians with a course
  - BR4
  - CME Providers, CME Educators, Clinicians
  - Flow:
    1. (Optional, may already be complete) CME provider creates a course.
    2. (Optional, may already be complete) CME provider designates educators
for a course.
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

