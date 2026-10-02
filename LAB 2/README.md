Patient Health Record Consent Management System
Lab 2: Agile Backlog Creation & Sprint Simulation in Jira
Course: Software Engineering
University: PES University, Bengaluru
Student: Harshit Vaish
SRN: PES1UG24AM116
Section: B
Date: 01 October 2026
1. Project Overview
The Patient Health Record Consent Management System is the subject of
this Software Engineering lab. The project focuses on organizing the
requirements of a healthcare consent system into an Agile product
backlog and simulating sprint execution using Jira.
The system's requirements concern patient control over diagnostic-record
access, doctor verification, consent duration and revocation, emergency
access, notifications, audit history, and security.
The objective of Lab 2 is to apply Agile and Scrum practices to:
- Convert requirements from Lab 1 into Epics and User Stories.
- Organize and prioritize the product backlog.
- Estimate story effort using Fibonacci story points.
- Plan and simulate two one-week sprints.
- Track work through Jira and examine sprint burndown charts.
- Reflect on planning, estimation, completion, and team capacity.
This repository documents the requirements breakdown and Jira-based
planning and simulation. It does not, by itself, represent a fully
implemented healthcare application.

2. Problem Context
Patients need control over who can access their diagnostic records and
for how long. A consent-management workflow should support granting
access to verified clinic doctors, revoking access before expiry, and
automatically ending permissions when their validity period is over.
The requirements also include a process for doctors to request records,
a mechanism for emergency access under specified conditions,
notifications, and an auditable history of consent-related events.
The Lab 2 exercise takes these requirements and organizes them into
manageable work items that can be prioritized and planned across
sprints.
3. Agile Approach
The project uses a Scrum-style workflow in Jira.
Main concepts used
  Concept                             How it was used
  Epic                                A larger functional area grouping
                                      related work
  User Story                          A smaller requirement expressed as
                                      a user-focused work item
  Product Backlog                     The ordered collection of work
                                      items
  Priority                            Indicates the relative importance
                                      of stories
  Story Points                        Relative estimates of work size and
                                      complexity
  Sprint                              A time-boxed period for completing
                                      selected stories
  Sprint Board                        Tracks the status of work during a
                                      sprint
  Burndown Chart                      Shows remaining estimated work over
                                  the sprint
The work was organized into five Epics and fourteen User Stories. The
stories were assigned priorities and estimated using Fibonacci values.
4. Epics and User Stories
The Lab 1 requirements were grouped into the following five Epics.
Epic 1: Consent Granting & Access Requests
Jira key: SCRUM-11
This Epic groups work related to granting access to patient records and
handling access requests.
It covers:
- Granting time-bound access to selected diagnostic records.
- Allowing a patient to choose the records and doctor.
- Setting the consent duration.
- Submitting record-access requests with the required information.
- Supporting the consent-grant workflow.
Epic 2: Consent Revocation & Expiry Notifications
Jira key: SCRUM-12
This Epic covers ending consent and communicating relevant changes.
It includes:
- Revoking active access before the consent expires.
- Automatically expiring consent at its expiry time.
- Notifying relevant users about grant or revocation events.
- Reminding patients before active consent expires.
Epic 3: Audit Trail & Transparency
Jira key: SCRUM-13
This Epic focuses on recording consent-related activity and allowing
patients to inspect it.
It includes:
- Viewing a filterable audit history.
- Recording grant, revocation, and access events.
- Maintaining append-only audit records.
- Supporting transparency around access to patient information.
Epic 4: Emergency Access Override
Jira key: SCRUM-14
This Epic groups requirements for exceptional access during an
emergency.
It includes:
- Marking records as eligible for emergency access.
- Allowing a verified doctor to request emergency access.
- Requiring a justification.
- Granting temporary access when eligibility conditions are satisfied.
- Recording emergency access activity and notifying the patient.
Epic 5: Security & Authentication
Jira key: SCRUM-15
This Epic covers security foundations and the protection of sensitive
information.
It includes:
- User authentication and doctor verification.
- Preventing unverified doctors from receiving access.
- Protecting health records and consent data.
- Applying the specified encryption requirements.
5. Product Backlog
The five Epics were broken down into fourteen User Stories, totaling
68 story points.
The stories represent the functional and security-related work selected
for the Jira simulation. Each story was associated with an Epic,
prioritized, and assigned an estimate.
Backlog organization
The backlog was structured to make the larger requirements easier to
plan:
1. Group related requirements under Epics.
2. Express individual capabilities as User Stories.
3. Set story priorities.
4. Estimate story size using Fibonacci values.
5. Select stories for sprint planning.
The Jira backlog screenshot in the lab report shows the Epic panel and
the associated stories, including their parent Epic and story-point
information.
6. Story-Point Estimation
Story points were assigned using Fibonacci values:
2, 3, 5, and 8
These values were used as relative estimates rather than direct measures
of hours.
The estimation approach was described as a Planning Poker-style
discussion. The purpose of estimating was to compare the relative size
of stories and help the team decide how much work to include in a
sprint.
A higher point value indicates a story estimated as relatively larger or
more complex within this backlog. The estimates were used for planning
and for interpreting the burndown charts.
Total estimated work
  Measure                          Value
  Number of Epics                      5
  Number of User Stories              14
  Total story points                  68
  Estimation values used      2, 3, 5, 8
  Planned sprint duration       One week
7. Sprint Planning
Two one-week sprints were created in Jira.
Sprint 1
Sprint goal: Core consent, revocation and authentication
Sprint 1 was planned with:
- 6 stories
- 34 story points
The sprint focused on core consent functionality and the security
foundations needed for the system.
Outcome: 29 points were completed out of 34 committed points. One
5-point story, SCRUM-19 (Submit Access Request with Reason), was carried
over.
Sprint 2
Sprint goal: Emergency access, audit visibility and notifications
Sprint 2 was initially planned at 34 points. It also included the
5-point story carried over from Sprint 1.
The resulting sprint commitment was:
- 8 stories shown in the Sprint 2 planning screenshot
- 34 points planned originally
- 39 points committed including the carry-over
Outcome: All 39 committed points were completed, including the
carried-over story.
Sprint summary
  Measure                                   Sprint 1      Sprint 2
  Stories in planning screenshot                   6             8
  Original planned points                         34            34
  Points committed including carry-over           34            39
  Points completed                                29            39
  Carry-over                                       5   0 remaining
Across the two sprints, the team completed all 68 points of estimated
backlog work.
8. Jira Workflow and Sprint Simulation
The Jira project was used to organize and simulate the work.
The workflow represented in the lab was:
To Do → In Progress → Done
During the simulation, stories were moved through these statuses and the
sprints were completed. Since the sprints were closed, the report
presents Jira's sprint summaries of completed work items as evidence of
the outcomes.
The screenshots in the report document:
- The backlog and Epic panel.
- Story-point assignments and Sprint 1 planning.
- Sprint 2 planning.
- Burndown charts for both sprints.
- Completed work items for both sprints.
9. Burndown Charts
Burndown charts were generated for Sprint 1 and Sprint 2 using story
points as the estimation field.
Sprint 1 burndown
Sprint 1 started with 34 committed points. The sprint completed 29
points, leaving 5 points unfinished.
The remaining-work line stopped above zero, reflecting the story that
was carried into Sprint 2.
Sprint 2 burndown
Sprint 2 began with 39 committed points, consisting of the original
34-point plan and the 5-point carry-over.
The sprint completed all 39 points, and the remaining-work line reached
zero.
Important limitation
The report notes that the cards were moved within minutes rather than
gradually across the one-week sprint. As a result, the burndown charts
show the simulated completion totals, but not realistic day-by-day work
progress.
The charts therefore provide evidence of the planning and completion
figures in the simulation, but should not be treated as a reliable
measurement of real team pacing or capacity.
10. Sprint Outcomes
Sprint 1
- Planned: 34 points across 6 stories.
- Completed: 29 points.
- Carried over: 5 points.
- Main observation: the sprint was not fully completed within its
  planned scope.
The carried-over work was SCRUM-19, Submit Access Request with Reason.
Sprint 2
- Planned originally: 34 points.
- Committed including carry-over: 39 points.
- Completed: 39 points.
- Main observation: the sprint finished all work shown in its
  completed-work summary.
The second sprint included the 5-point carry-over from Sprint 1.
11. Reflection and Lessons Learned
11.1 Did the estimations reflect the actual effort?
The report's reflection concludes that the estimates were broadly usable
for the simulation. Sprint 2 completed all 39 committed points, while
Sprint 1 completed 29 of 34.
The unfinished 5-point story in Sprint 1 highlighted a planning miss.
The reflection also identifies the 8-point stories as having more risk
because they combined unknowns and dependencies.
Since this was a simulation rather than real development, the exercise
cannot establish how closely the story points would correspond to actual
development hours.
Lesson: Larger stories with multiple dependencies may benefit from
being split into smaller stories, and estimates should be revisited
after real development work.
11.2 Was the backlog well-prioritized?
The reflection describes the backlog as prioritizing core capabilities
such as authentication, time-bound access, revocation, and emergency
override early.
Notification and reminder work was placed later in the plan.
The reflection also identifies a planning weakness: the access-request
story was closely related to access-grant functionality, but it was left
at the edge of Sprint 1 and became the carry-over.
Lesson: Prioritization should consider not only importance but also
dependencies and how closely related stories fit together.
11.3 How did the simulated sprints align with the plan?
Sprint 1 completed 29 of its 34 committed points, while Sprint 2
completed all 39 points, including the carried-over 5-point story.
The first sprint's goal was completed only after the carry-over was
finished in Sprint 2. The second sprint's stated goal was met according
to the report.
The carry-over suggests that Sprint 1 may have been slightly
over-committed. Sprint 2 then handled a larger total commitment.
Lesson: Sprint planning should account for dependencies and leave
room for work that may take longer than expected.
11.4 What did the burndown chart reveal about team capacity?
The report records:
- Sprint 1 velocity: 29 points.
- Sprint 2 velocity: 39 points.
- Average across the two simulated sprints: 34 points per sprint.
The charts show Sprint 1 ending with 5 points remaining and Sprint 2
reaching zero.
However, because work was moved within minutes, the steep early drops do
not reflect realistic progress over the week. The figures can describe
what was completed in the simulation, but they cannot establish actual
day-to-day capacity.
Lesson: The report suggests planning around 30--34 points as a
cautious starting range, then recalibrating estimates and commitments
after observing real sprint performance.
12. Key Takeaways
The lab exercise provided practice in translating requirements into an
Agile backlog and using Jira to simulate sprint planning and execution.
Key takeaways:
1. Epics help group related requirements into larger functional areas.
2. User Stories make requirements easier to estimate and plan.
3. Priorities help determine which capabilities should be addressed
   earlier.
4. Fibonacci story points support relative estimation.
5. Sprint commitments should account for dependencies and uncertainty.
6. Carry-over work should be considered when planning the next sprint.
7. Burndown charts are only meaningful as pacing indicators when work
   is tracked over realistic dates.
8. Simulated velocity should not be treated as proven real-world team
   capacity.
13. Repository Contents
This repository documents the Lab 2 work and its supporting report.
Suggested contents:
- README.md --- Project and lab documentation.
- PES1UG24AM116_Lab2.pdf --- Lab 2 report with Jira screenshots,
  sprint outcomes, burndown charts, and reflection.
14. Conclusion
Lab 2 applied Scrum concepts to the Patient Health Record Consent
Management System by organizing its requirements into five Epics and
fourteen User Stories, estimating 68 story points, and simulating two
one-week sprints in Jira.
The simulation completed all 68 points across the two sprints, with a
5-point carry-over from Sprint 1 completed in Sprint 2. The exercise
also demonstrated how Jira can support backlog organization, sprint
planning, status tracking, and retrospective reflection.
The main limitation is that the sprint execution was simulated over a
very short period. Consequently, the burndown charts and velocity
figures describe the exercise rather than validated real development
capacity.
