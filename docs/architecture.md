# OutcomeHub Architecture — Draft v0.1

This document records the team's initial architecture proposal. It is deliberately provisional and should be revised as the project kickoff clarifies requirements.

## Product boundary

OutcomeHub is a Django web application that converts student assessment grades into Learning Outcome (LO) scores and then into Program Outcome (PO) scores through weighted mappings.

## Initial system context

```text
Student ───────────────┐
                      │
Instructor ────────> Django Web Application ───────> Relational Database
                      │
Department Admin ─────┘
```

Possible later integrations:

- CSV/Excel grade import
- PDF/CSV report export
- email/notification service
- syllabus-assisted setup

Do not add external services until they solve a real requirement.

## Initial domain model

```text
User
 ├── StudentProfile
 └── InstructorProfile

Program
 └── ProgramOutcome

Course
 ├── Enrollment
 ├── LearningOutcome
 │     └── LOPOMapping ─────────────> ProgramOutcome
 │
 └── Assessment
       ├── AssessmentLOMapping ─────> LearningOutcome
       └── Grade ───────────────────> Student
```

## Proposed models

### Program
Represents an academic program/department context.

Suggested fields:
- `name`
- `code`

### ProgramOutcome
Represents one official Program Outcome.

Suggested fields:
- `program`
- `number`
- `title`
- `description`

### Course
Represents a course offering.

Suggested fields:
- `code`
- `title`
- `semester`
- `instructor`
- `program`

### LearningOutcome
Represents a course-specific Learning Outcome.

Suggested fields:
- `course`
- `number`
- `description`

### LOPOMapping
Maps one Learning Outcome to one Program Outcome.

Suggested fields:
- `learning_outcome`
- `program_outcome`
- `weight` (expected 1–5)

### Assessment
Represents a graded item such as a midterm, final, quiz, assignment, or project.

Suggested fields:
- `course`
- `name`
- `max_score`

### AssessmentLOMapping
Maps an Assessment to a Learning Outcome with a weight.

Suggested fields:
- `assessment`
- `learning_outcome`
- `weight`

### Enrollment
Connects a student to a course.

Suggested fields:
- `student`
- `course`

### Grade
Stores one student's result for one assessment.

Suggested fields:
- `student`
- `assessment`
- `score`

## Calculation model

For any weighted result:

```text
score = Σ(weight × source_score) / Σ(weights)
```

LO score calculation:

```text
Assessment grades
    ↓ weighted by AssessmentLOMapping
Learning Outcome score
```

PO score calculation:

```text
Learning Outcome scores
    ↓ weighted by LOPOMapping
Program Outcome score
```

A student's overall PO profile may later aggregate contributions from multiple courses.

## Initial permissions

### Department Admin / Head
- manage programs and Program Outcomes
- manage courses/users
- view department-wide results

### Instructor
- manage assigned courses
- define LOs and mappings
- define assessments
- enter/import grades
- view course results

### Student
- view own results and outcome profile

### System Admin
- use Django admin for technical/user administration initially

## MVP architecture target

The first milestone should remain a single Django application backed by a relational database. Avoid unnecessary microservices, caches, queues, or cloud dependencies until requirements justify them.

The MVP must prove one complete path:

```text
Instructor configures course
        ↓
Instructor enters grades
        ↓
System calculates LO scores
        ↓
System calculates PO scores
        ↓
Student views results
```

## Open questions for kickoff

- Who is allowed to create Program Outcomes?
- Are courses tied to exactly one program?
- Can one course have multiple instructors?
- Do assessment-to-LO weights need to sum to a fixed total?
- How should grades be imported in bulk?
- When are results visible to students?
- Are PO scores historical by semester or recomputed from all available data?
- What reports does the department head actually need?
- What scale/volume should the system be designed for?

These questions should be answered before locking the database schema.
