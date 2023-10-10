# Domain Model

This file displays and describes the domain model for the project.

## Model Diagram

```mermaid
classDiagram
  direction RL 

  class Clinician{
	- uid: int
    - created: datetime
    - lastUpdated: datetime
    + email: String
    + firstName: String
    + lastName: String
    - commitments: List[Commitment]
    - coursesTaught: List[Course]
    - coursesEnrolledIn: List[Course]
    + createCommitment(): Commitment
    + deleteCommitment(Commitment)
    + teach(Course)
    + stopTeaching(Course)
    + enrollIn(Course)
    + drop(Course)
  }

  class Commitment{
    <<abstract>>
    - uid: int
    - created: datetime
    - lastUpdated: datetime
    + title: String
    + description: String
    + deadline: date
    - owner: User
    - status: CommitmentStatus
    - hasAssociatedCourse: boolean
    - associatedCourse: Course
    + markComplete(date)
    + markExpired()
    + isComplete(): boolean
    + isInProgress(): boolean
    + isExpired(): boolean
    + associateWithCourse(Course)
    + removeAssociation()
    + sendReminderEmail()
    + displayProgress(): double*
  }

  class CommitmentStatus{
    <<Enumeration>>
    SUCCESS
    IN_PROGRESS
    EXPIRED
  }

  class YesNoCommitment{
    + displayProgess(): double
  }

  class MilestoneCommitment{
    + milestones: List[Milestone]
    + displayProgess(): double
  }

  class Milestone{
    + uid: int
    + isComplete: boolean
  }

  class ValueCommitment{
    + targetValue: double
    + currentValue: double
    + displayProgress(): double
    + addValue(double)
    + removeValue(double)
  }

  class Course{
    - uid: int
    - created: datetime
    - lastUpdated: datetime
    + title: String
    + description: String
    - instructors: List[User]
    - students: List[User]
    - associatedCommitments: List[Commitment]
    + addInstructor(Clinician)
    + removeInstructor(Clinician)
    + addStudent(Clinician)
    + removeStudent(Clinician)
    + addCommitment(Commitment)
    + removeCommitment(Commitment)
    + getCommitmentSuccesRate(): double
    + getNumberOfCommitments(): int
    + getNumberOfStudents(): int
  }

  class Provider{
    - uid: int
    - created: datetime
    - lastUpdated: datetime
    + name: String
    - courses: List[Course]
    + createCourse(): Course
    + deleteCourse(Course)
    + getProviderSuccessRate(): double
  }

  Course "1" o-- "*" Provider
  Clinician "*, coursesTaught: *" o--o "*" Course
  Commitment "1" o-- "*" Clinician
  Commitment "0..1" o-- "*" Course
  Commitment "1" --> CommitmentStatus
  YesNoCommitment --|> Commitment
  MilestoneCommitment --|> Commitment
  ValueCommitment --|> Commitment
  Milestone o-- "*" MilestoneCommitment

```

  


## Classes
- Clinician
  - A medical professional, usually a physician and in continuing medical 
education. These are the main users of the platform who use to to make 
commitments. Medical educators are also modeled as this class, as they may also
make commitments and/or be taking CME courses.

- Commitment
  - A goal to positively change delivery of patient care that is made by a 
clinician. Most of these commitments should take place in the context of 
implementing practices learned in a CME course and therefore will have an 
associated Course. Note that several examples of commitment types are listed
below, but are not necessarily exhaustive.

- CommitmentStatus
  - The current state of a Commitment, whether completed successfully, in 
progress, or expired (reached the deadline without total completion). Other 
statuses might be possible in the future, so backwards compatibility is 
important for this enumeration.

- YesNoCommitment
  - The most simple type of Commitment. This covers goals that could be phrased
in terms of a yes or no question.

- MilestoneCommitment
  - This models Commitments that might have multiple steps along the way. This
allows clinicians to break bigger goals into smaller ones and display their 
progress, both to themself and to others in the community.

- ValueCommitment
  - This models Commitments that consist of trying to reach a specific quantity.
An example would be a commitment to hold a certain number of clinic hours 
before the deadline.

- Course
  - This represents a course in continuing medical education. Importantly,
associating commmitments with a course is important on gathering data for CME
providers on how much change the course actually caused.

- Provider 
  - These are the objects that represent CME providers. CME providers are 
organizations and therefore behave very differently from other clinician users.
Providers may create courses and optionally suggest commitments, but it is up
to clinicians to make changes in practice happen.

