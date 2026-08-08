# Programming Classroom — Step-by-Step Guide

This guide walks through the full Programming Classroom flow: from a faculty member creating and publishing an assignment, to a student connecting GitHub and submitting a final commit.

> Programming Classroom is **not** GitHub Classroom. Students use their **own** GitHub accounts and repositories. No GitHub Education seats or organization membership are required.

---

## Overview

```text
Faculty creates draft
        ↓
Faculty configures tests, deadline, sections
        ↓
Faculty publishes
        ↓
Students receive invite email (secure public link)
        ↓
Student opens link → connects GitHub → selects repo
        ↓
Student develops & pushes code on GitHub
        ↓
Student runs autograder (optional) and submits final commit SHA
        ↓
Autograder grades exact commit in isolated sandbox
        ↓
Faculty reviews results, adjusts score, publishes feedback
```

**Where it lives in the app**

| Who | Where |
|-----|--------|
| Faculty / Admin | **Classroom → Programming Classroom** (`/programming-classroom`) |
| Student | Public invite link (`/public/programming/{token}`) — no faculty login |

---

## Prerequisites

Before using the feature:

1. Set in environment:
   ```env
   PROGRAMMING_CLASSROOM_ENABLED=true
   GITHUB_OAUTH_CLIENT_ID=...
   GITHUB_OAUTH_CLIENT_SECRET=...
   GITHUB_OAUTH_REDIRECT_URI="${APP_URL}/public/programming/github/callback"
   ```
2. Faculty must have Programming Classroom permissions (seeded with Faculty role).
3. Students must be **enrolled** in the target section(s) and have a valid **email** on their student record (used for invitations).
4. Queue workers must be running so invitation emails and autograder jobs process:
   - Default queues for mail / general jobs
   - `autograder` queue for grading jobs (see [PROGRAMMING_CLASSROOM_AUTOGRADER.md](./PROGRAMMING_CLASSROOM_AUTOGRADER.md))

---

## Part A — Faculty: Create the assignment

### Step 1. Open Programming Classroom

1. Sign in as Faculty (or Admin).
2. Go to **Classroom → Programming Classroom**.
3. Click **New assignment**.

### Step 2. Fill in basic information

| Field | Purpose |
|-------|---------|
| **Title** | Name shown to students (e.g. “Laboratory Activity 02 — Event Handling”) |
| **Subject** | Course this assignment belongs to |
| **Total points** | Maximum score (e.g. 100) |
| **Description** | Short summary (optional) |
| **Instructions** | Full lab instructions shown on the student portal |

### Step 3. Choose sections

Select one or more **sections** you teach.  
When you publish, enrolled students in those sections become **recipients** (one invite per student).

### Step 4. Choose language and grading options

| Field | Purpose |
|-------|---------|
| **Language** | e.g. PHP, JavaScript, Web |
| **Runtime** | e.g. CLI, Laravel, Node, DOM |
| **Show automatic score** | Immediate / after deadline / hidden from students |
| **Enable autograding** | Queue isolated grading jobs for commits |

### Step 5. Set schedule and late policy

| Field | Purpose |
|-------|---------|
| **Deadline** | When work is due (app timezone, usually Asia/Manila) |
| **Max attempts** | Optional limit on grading attempts |
| **Late policy** | e.g. none, fixed deduction, percentage per day, no late |
| **Late deduction** | Points or percent used by the late policy |
| **Allow late submissions** | Whether students can still submit after the deadline |

### Step 6. Add automated tests

In **Automated tests**, add one or more checks. Phase 1 supports:

| Type | What it checks | Example config |
|------|----------------|----------------|
| **File exists** | Required file is present in the repo | Path: `index.php` |
| **Exact output** | Running a file produces expected stdout | File + expected output |

For each test, set:

- **Name** — shown in results (hidden tests keep names private based on settings)
- **Type** — file exists / exact output
- **Visibility** — `Visible` (students may see) or `Hidden` (students must not see the test source)
- **Points** — points awarded if the test passes

Hidden tests are stored server-side and injected only into the grader workspace. They are **never** committed into the student’s GitHub repository.

### Step 7. Save as draft

Click **Create draft**.  
The assignment is saved but students are **not** notified yet. You can still edit it from **Edit**.

---

## Part B — Faculty: Publish and monitor

### Step 8. Publish the assignment

1. Open the assignment from the Programming Classroom list.
2. Review roster sync / details.
3. Click **Publish**.

What happens on publish:

1. Recipients are created from **active enrolled students** in the selected sections.
2. Each recipient gets a unique hashed **invite token**.
3. Invitation emails are queued to students who have an email address.
4. Status becomes `published`.

Students without email will appear on the roster but will not receive an automatic invite. Faculty can still manage them from the roster.

### Step 9. Monitor the roster

On the assignment **Show** page you can see:

- How many students have submitted vs total recipients
- Per-student submission status
- Scores when available

Typical student statuses include:

| Status | Meaning |
|--------|---------|
| `not_submitted` | Invite exists; no final submission yet |
| `repo_connected` | Student linked a GitHub repository |
| `grading` | An autograder attempt is running |
| `submitted` / `submitted_late` | Official submission recorded |

### Step 10. Review a student submission

1. Open a student from the roster (or submission detail when available).
2. Review:
   - Official commit SHA
   - Attempt history
   - Per-test pass/fail and points
   - Automatic score, late deduction, final score
3. Optionally:
   - Apply a **faculty score adjustment** (+/− points)
   - Write **feedback**
   - **Publish feedback** so the student can see it
4. Use **Regrade** when you need to run the autograder again on the same (or updated) submission.

### Step 11. Export grades

Click **Export** on the assignment (when your plan allows) to download an Excel roster with scores and GitHub metadata.

### Step 12. Close when finished (optional)

Use **Close** to stop further submissions while keeping records for review and audit.

---

## Part C — Student: Receive invite and connect GitHub

Students do **not** log into the faculty web app for this flow.

### Step 13. Open the invitation link

The student receives an email with a unique link:

```text
https://YOUR_APP_DOMAIN/public/programming/{token}
```

Opening the link shows:

- Assignment title and instructions
- Deadline
- Student name / section (read-only identity from the invite)

If the link is expired, invalidated, or the assignment is closed, the portal will show an error.

### Step 14. Connect GitHub

1. Click **Connect GitHub**.
2. Authorize GradeVision via GitHub OAuth.
3. Return to the assignment portal; the page should show the connected GitHub username.

Notes:

- This links the student’s **personal** GitHub account to this invite.
- GradeVision does **not** require joining a school GitHub organization.
- Tokens are stored encrypted; passwords are never stored.

### Step 15. Create or choose a repository

MVP workflow (recommended):

1. On GitHub, the student creates a repository under their own account  
   (example: `github.com/juan-delacruz/lab-02-events`).
2. Optionally copy any starter code the faculty provided in instructions.
3. Back in GradeVision, choose the repository from the dropdown and click **Connect**.

The app stores repository metadata only (name, URL, default branch, etc.).

---

## Part D — Student: Develop, grade, and submit

### Step 16. Develop normally on GitHub

Students work as usual:

```text
git clone ...
# write code
git add .
git commit -m "Complete lab"
git push origin main
```

GradeVision grades an **exact commit SHA**, not a moving branch tip without recording it.

### Step 17. Run the autograder (optional practice)

On the public portal, click **Run Autograder**.

What happens:

1. GradeVision resolves the latest commit on the connected repo’s default branch.
2. A grading job is queued on the `autograder` queue.
3. The worker downloads that exact commit, injects hidden tests, and runs checks in an isolated sandbox.
4. Results appear on the portal (according to faculty visibility settings).

This does **not** freeze the official submission unless the student also submits a final attempt.

### Step 18. Submit the final attempt

When ready:

1. Copy the commit SHA from GitHub (full or short SHA is fine; the system resolves it).
2. On the portal, paste the **Commit SHA** (and branch if prompted).
3. Click **Submit Final Attempt**.

What is frozen:

| Field | Meaning |
|-------|---------|
| Repository | Connected student repo |
| Branch | Branch name recorded with the submission |
| Commit SHA | Exact commit graded as official work |
| Submitted at | Timestamp used for late calculation |

Later pushes do **not** silently replace the official submission.  
If resubmission is allowed by policy/attempts, a new attempt/submission is created instead of overwriting quietly.

### Step 19. View results (as allowed)

Depending on faculty settings, the student may see:

- Automatic score immediately, after the deadline, or not at all
- Failed visible-test names (if enabled)
- Faculty feedback only after it is published (if release is manual)

Hidden test **source code** is never shown to students.

---

## Part E — What the system does behind the scenes

```text
GitHub commit (student)
        ↓
Run Autograder / Submit Final / (optional) webhook
        ↓
Laravel queues job on `autograder`
        ↓
Host downloads exact commit archive (OAuth token stays on host)
        ↓
Hidden tests injected into temporary workspace
        ↓
Disposable sandbox runs checks (network disabled when using Docker)
        ↓
Per-test results + automatic score saved
        ↓
Late deduction applied → adjusted score
        ↓
Faculty may override → final score + feedback
```

Security reminders:

- Student code is **never** executed inside the main Laravel web process.
- Grading containers must not receive production secrets, Docker socket, or the app database credentials.
- Invite tokens are stored hashed; raw tokens appear only in the emailed link.

---

## Quick checklist

### Faculty

- [ ] Feature enabled and GitHub OAuth configured
- [ ] Assignment created with subject, sections, language, deadline
- [ ] Tests configured (visible / hidden + points)
- [ ] Assignment published
- [ ] Roster monitored
- [ ] Submissions reviewed / overridden if needed
- [ ] Feedback published
- [ ] Grades exported (optional)

### Student

- [ ] Opened invite email link
- [ ] Connected personal GitHub account
- [ ] Connected own repository
- [ ] Pushed working code to GitHub
- [ ] (Optional) Ran autograder for practice
- [ ] Submitted final commit SHA
- [ ] Viewed allowed score / feedback

---

## Related docs

| Doc | Contents |
|-----|----------|
| [PROGRAMMING_CLASSROOM_ARCHITECTURE.md](./PROGRAMMING_CLASSROOM_ARCHITECTURE.md) | Integration design and data model |
| [PROGRAMMING_CLASSROOM_GITHUB_SETUP.md](./PROGRAMMING_CLASSROOM_GITHUB_SETUP.md) | OAuth App + webhook setup |
| [PROGRAMMING_CLASSROOM_AUTOGRADER.md](./PROGRAMMING_CLASSROOM_AUTOGRADER.md) | Sandbox / queue / driver settings |
| [PROGRAMMING_CLASSROOM_FACULTY_WORKFLOW.md](./PROGRAMMING_CLASSROOM_FACULTY_WORKFLOW.md) | Short faculty checklist |
| [PROGRAMMING_CLASSROOM_STUDENT_WORKFLOW.md](./PROGRAMMING_CLASSROOM_STUDENT_WORKFLOW.md) | Short student checklist |

---

## Troubleshooting

| Problem | What to check |
|---------|----------------|
| No **Programming Classroom** menu | Feature flag off, or missing `programming_classroom.view` permission |
| Publish creates few/no recipients | Section enrollments empty, or students inactive / missing email |
| Student cannot connect GitHub | OAuth app callback URL / client ID / secret / `APP_URL` mismatch |
| Autograder stays queued | `autograder` queue worker not running |
| Autograder fails on Cloud | Docker may be unavailable; see autograder docs (`AUTOGRADER_DRIVER`) |
| Student link invalid | Token expired, regenerated, or assignment closed |
| Score not visible to student | `show_score` / `feedback_release` settings, or feedback not published yet |
