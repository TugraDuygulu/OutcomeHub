# OutcomeHub

OutcomeHub is the shared CSE 311 (Software) + CSE 321 (Data Systems) semester project for Fall 2026.

## Project goal

Design and develop a web-based system that manages and maintains each student's Program Outcome (PO) scores. The system converts assessment results into Learning Outcome (LO) scores and then into Program Outcome scores using weighted mappings.

**Required stack:** Python + Django.

## Core flow

```text
Assessment grades
      ↓
Assessment → Learning Outcome mappings
      ↓
Learning Outcome scores
      ↓
Learning Outcome → Program Outcome mappings
      ↓
Program Outcome scores
      ↓
Student PO profile/dashboard
```

Weighted scores follow the project brief's model:

```text
score = Σ(weight × score) / Σ(weights)
```

## Users and roles — initial design

### Department Admin / Head
- Manage programs and Program Outcomes
- Create/manage courses
- Manage users
- View department-wide outcome analytics

### Instructor
- Manage assigned courses
- Define Learning Outcomes
- Create assessments
- Map assessments → LOs
- Map LOs → POs
- Enter/import grades
- View course outcome results

### Student
- View their course results
- View Learning Outcome scores
- View Program Outcome scores
- Track progress over time

### System Admin
- Technical/user administration through Django admin initially

## MVP

The first complete vertical slice should let an instructor:

1. Log in
2. Create/open a course
3. Define Learning Outcomes
4. Create assessments
5. Map assessments to Learning Outcomes
6. Map Learning Outcomes to Program Outcomes
7. Enter grades
8. Calculate LO scores
9. Calculate PO scores
10. Let a student log in and view the result

The MVP is complete when this full path works end-to-end.

## Initial data model

```text
User
 ├── StudentProfile
 └── InstructorProfile

Program
 └── ProgramOutcome

Course
 ├── Enrollment
 ├── LearningOutcome
 │     └── LearningOutcomeProgramOutcome
 │
 └── Assessment
       ├── AssessmentLearningOutcome
       └── Grade
```

Suggested models:

- `Program`
- `ProgramOutcome`
- `Course`
- `LearningOutcome`
- `LOPOMapping`
- `Assessment`
- `AssessmentLOMapping`
- `Enrollment`
- `Grade`

## Development workflow

Keep the process simple and visible:

```text
GitHub Issue
   ↓
feature branch
   ↓
commits
   ↓
Pull Request
   ↓
review
   ↓
merge to main
```

Branch naming examples:

```text
feature/3-user-roles
feature/8-lo-po-mapping
fix/17-student-results
```

Rules:

- Do not push unfinished feature work directly to `main`.
- One issue should represent one clear task.
- Pull requests should reference the issue they implement.
- Prefer small, reviewable changes.
- Every team member should make attributable commits and use issues/PRs.

## Planned enhancements after MVP

High-value ideas:

- CSV/Excel bulk grade import
- Student PO dashboard and charts
- Department/course performance reports
- Historical PO progression by semester
- Threshold alerts for weak POs/students
- CSV/PDF exports
- Syllabus-assisted course configuration
- Notifications when results are published

## Course-specific project focus

### CSE 311 — Software
Focuses on **how we build**:

- Agile/Scrum process
- backlog/task management
- estimation and sprint velocity
- Git/GitHub workflow
- testing and TDD
- CI/CD
- teamwork and documented contributions

### CSE 321 — Data Systems
Focuses on **what we build**:

- system architecture
- class/object relationships
- data model/schema
- indexes
- scalability and fault tolerance
- partitioning/replication
- transactions and consistency

## Important dates

- **Oct 13:** Team + repo registration
- **Nov 8:** Internal checkpoint freeze
- **Nov 10:** CSE 311 Midterm I
- **Nov 12:** CSE 321 project presentation + report
- **Nov 17:** CSE 311 project presentation + report
- **Nov 19:** CSE 321 Midterm I
- **Dec 20:** Internal final feature freeze
- **Dec 22:** CSE 311 Midterm II
- **Dec 24:** CSE 321 Midterm II
- **Dec 29–30:** Final demo + hardcopy reports

## Current status

**Sprint 0 — project setup**

Immediate priorities:

- [ ] Finalize four-person team
- [ ] Register team + repo
- [ ] Initialize Django project
- [ ] Establish backlog and issue workflow
- [ ] Build the first data-model draft
- [ ] Get one end-to-end MVP path working before expanding scope

---

This plan is intentionally a starting point. Architecture, roles, and backlog items should be refined with the full team during kickoff rather than treated as immutable decisions.
