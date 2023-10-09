# Domain Model

## Model Diagram

- (Link to the domain model file)

### Proof of concept: mermaid.js

```mermaid
classDiagram
  class Clinician{
	- uid: int
    - created: datetime
    - lastUpdated: datetime
    + email: String
    + firstName: String
    + lastName: String
    - commitments: List<Commitment>
    - coursesTaught: List<Course>
    - coursesEnrolledIn: List<Course>	
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
  }

  class Course{
    - uid: int
    - created: datetime
    - lastUpdated: datetime
    + title: String
    + description: String
    - instructors: List<User>
    - students: List<User>
    - associatedCommitments: List<Commitment>
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
    + createCourse(): Course
    + deleteCourse(Course)
    + getProviderSuccessRate(): double
  }

  Commitment "owner: 1" o-- "commitments: *" Clinician
  Commitment "associatedCourse: ? (0..1)" o-- "associatedCommitments: *" Course
  Clinician "coursesEnrolledIn: *, coursesTaught: *" o-- "instructors: *, students: *" Course
  Course "provider: 1" o-- "courses: *" Provider

```

  


## Classes
- Class 1
  - Explanation

- Class 3
  - Explanation
