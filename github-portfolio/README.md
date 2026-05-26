<div align="center">
  <h1>Learning Hub</h1>

  <p><strong>Governed enterprise learning workspace for onboarding, upskilling, and measurable completion</strong></p>

  <p>
    <img src="https://img.shields.io/badge/Enterprise%20Learning-013444?style=flat-square" alt="Enterprise Learning" />
    <img src="https://img.shields.io/badge/Guided%20Lessons-0381A9?style=flat-square" alt="Guided Lessons" />
    <img src="https://img.shields.io/badge/Interactive%20Practice-E7C66A?style=flat-square&amp;labelColor=013444" alt="Interactive Practice" />
    <img src="https://img.shields.io/badge/Governed%20AI-244B5A?style=flat-square" alt="Governed AI" />
    <img src="https://img.shields.io/badge/Knowledge%20Retrieval-0381A9?style=flat-square" alt="Knowledge Retrieval" />
    <img src="https://img.shields.io/badge/Completion%20Evidence-E7C66A?style=flat-square&amp;labelColor=013444" alt="Completion Evidence" />
  </p>
</div>

![Learning Hub presentation banner](./assets/learning-hub-cover.jpg)

## Product Overview

**Learning Hub** is an enterprise learning platform designed for organizations that need more than a collection of courses and videos. It connects structured learning, instructor-led delivery, practical exercises, content governance, and evidence of completion in one digital workspace.

The product supports internal academies, employee onboarding, role-transition programs, technical training, and knowledge-transfer initiatives where progress must be visible and outcomes must be trustworthy.

> Learning Hub turns corporate learning into a managed journey: discover, learn, practise, validate, complete, and report.

## The Challenge

Many organizations deliver learning through disconnected tools: documents in one place, live sessions in another, exercises without tracking, and reporting that cannot show whether a learner is truly ready.

Learning Hub addresses that gap by bringing together:

| Business need | Platform response |
| --- | --- |
| Clear learning journeys | Guided lessons with theory, concept, video, quiz, practice, and summary stages |
| Hands-on skill validation | Interactive notebook practice with feedback and grading workflows |
| Instructor visibility | Cohort, session, and attendance operations in a dedicated workspace |
| Controlled content quality | Review, approval, publishing, and versioning workflows |
| Proof of achievement | Completion rules, learner attestation, and issued completion evidence |
| Management oversight | Reporting foundations for delivery, governance, and learning risk |

## Experience Ecosystem

Learning Hub is structured around four connected product surfaces.

| Surface | Purpose | Primary users |
| --- | --- | --- |
| **Public Learning Portal** | Course discovery, program information, sign-in journeys, and entry into the academy | Visitors and prospective learners |
| **Learner Workspace** | Assigned courses, lessons, calendar, recordings, support, practice, and personal progress | Employees and trainees |
| **Instructor Workspace** | Cohort supervision, live sessions, attendance, delivery coordination, and learner support | Trainers and subject experts |
| **Admin Control Plane** | Course building, governance, publishing, roles, reporting, and operational oversight | Academy owners and administrators |

<p align="center">
  <img src="./assets/learning-journey.jpg" width="720" alt="Illustration of a structured learning journey" />
</p>

## Learner Journey

1. **Discover and enter**  
   Learners find the relevant learning path and securely enter their personal workspace.

2. **Follow a structured lesson flow**  
   Each lesson can guide the learner through explanation, concept review, video content, checks for understanding, practical tasks, and a final summary.

3. **Practise in a real working environment**  
   Selected technical lessons connect to JupyterLab-based notebook exercises, allowing learners to work through realistic tasks rather than only reading content.

4. **Receive support and feedback**  
   Built-in assistance can provide guidance, hints, and AI-supported learning interactions within controlled course content.

5. **Demonstrate readiness**  
   Progress, attendance requirements, graded submissions, and attestation rules determine whether a learner has completed the expected path.

6. **Produce trusted evidence**  
   The platform can issue completion evidence so managers and academy operators can see not only participation, but confirmed outcomes.

## Governed AI Architecture

AI in Learning Hub is not a single chatbot feature. It is a controlled learning and content-operations layer that supports discovery, guided study, practical work, course creation, and administrative oversight.

### AI Capability Map

| AI subsystem | User value | Control model |
| --- | --- | --- |
| **Public Course Finder** | Helps visitors discover relevant learning paths in the public catalog | Uses public catalog context only |
| **Lesson Assistant** | Answers learner questions and supports lesson comprehension | Context is assembled from the active structured lesson and, when supplied, the learner's practice input |
| **Training Knowledge Assistant** | Delivers content-grounded answers with citations and follow-up prompts | Retrieval is limited to learning content visible to the authenticated learner |
| **AI Quiz Engine** | Generates knowledge checks and returns learner feedback | Quiz scoring is performed on the server and attempts are retained |
| **Notebook / Jupyter Assistant** | Brings guidance into hands-on notebook exercises | Protected runtime proxy resolves notebook and related lesson context before calling the configured AI provider |
| **Course Builder Orchestration** | Creates lesson drafts from approved text or transcribed video source material | Produces reviewable lesson structures; it does not publish content or decide access |
| **AI Governance Console** | Gives administrators visibility into unresolved answers, index health, provider status, and operational risk | Human assignment, resolution notes, escalation handling, and audit records remain part of the workflow |

### AI Processing Flow

| Stage | How the platform handles it |
| --- | --- |
| **1. Managed source content** | Training content can be maintained through the content-management workflow and synchronized into the learning domain. Published content is eligible for AI indexing; retired or unpublished content is removed from active retrieval. |
| **2. Knowledge indexing** | Content is divided into traceable chunks with section labels, snippets, checksums, and embedding metadata. The platform supports vector-based retrieval through PostgreSQL/pgvector with an application-level fallback strategy. |
| **3. Permission-aware retrieval** | The assistant starts from the learner's active content and only expands to referenced material that the user is allowed to see. Hidden cross-references are not exposed as AI citations. |
| **4. Provider execution** | A provider layer supports deterministic demo behaviour and a configured OpenAI-compatible runtime. This keeps the product demonstrable without external AI dependencies while allowing production integration. |
| **5. Response and assessment** | AI responses can include citations, suggested follow-up prompts, and a resolution status. AI-generated quizzes become trackable attempts with server-side evaluation. |
| **6. Human governance** | Partial or escalation-required answers can enter an administrative review queue, be routed to a responsible course owner, receive a resolution note, and be resolved or archived. |
| **7. Audit and analytics** | The platform tracks AI questions, response failures, quiz events, escalations, index rebuilds, content synchronization health, unresolved workload, and FAQ coverage. |

### Content Generation and Authoring Support

The content-production layer supports AI-assisted lesson drafting while preserving review and publishing responsibility:

- Lesson drafts can be assembled from approved source text into a structured flow of theory, concept, video, quiz, practice, and wrap-up.
- Video-based lesson creation can transcribe uploaded source material and turn the transcript into a reviewable lesson draft.
- A conservative provider-based path remains available as a stable baseline.
- An optional agent-orchestrated path can create structured lesson blueprints, including quiz and practice material, from approved context.
- If AI generation is unavailable or insufficient, the workflow falls back to a deterministic structured draft rather than blocking content work.

### AI Safety and Accountability

The AI layer is designed around accountability rather than unrestricted generation:

- authenticated access for learner-facing training AI;
- visibility-scoped retrieval and citation boundaries;
- controlled notebook runtime tokens for AI interaction inside Jupyter-based practice;
- rate-limited AI and synchronization operations;
- audit events for questions, responses, escalations, quizzes, index rebuilds, notebook actions, and failures;
- human-owned resolution workflow for answers that are incomplete or require escalation;
- administration metrics for stale knowledge, unindexed published content, provider configuration, failed operations, and owner gaps.

This structure is important for enterprise learning: AI helps users move faster, while content ownership, access rights, publishing decisions, and evidence remain governable.

## Key Capabilities

### Structured Learning Delivery

- Public catalog and learning entry experience
- Learner dashboard with course and lesson progress
- Course paths composed of modules, lessons, recordings, resources, and practical activities
- Calendar and session visibility for cohort-based learning

### Hands-On Practice

- Notebook-based exercises for technical and analytical training
- Guided validation, hints, submission, and automated grading flows
- Repeatable practice designed for measurable learning outcomes
- Suitable use cases including programming, data workflows, and financial-analysis scenarios

### Instructor Operations

- Dedicated instructor workspace
- Cohort and session management
- Attendance monitoring and delivery checkpoints
- Visibility into assigned learning responsibilities and upcoming activity

### Administration and Governance

- Course and lesson structure management
- Content lifecycle stages from draft through review, approval, publication, and archive
- Accountability assignments for academy, course, and cohort scopes
- Audit and governance signals for operational review

### AI-Supported Learning and Governance

- Public catalog guidance, in-lesson support, and content-grounded learner assistance
- Permission-aware knowledge retrieval with citations and follow-up guidance
- AI quiz attempts, notebook support, lesson-authoring assistance, and video-to-lesson drafting
- Administrative oversight of escalations, knowledge-index health, AI usage signals, and resolution ownership

### Completion and Evidence

- Progress and completion-rule evaluation
- Attendance thresholds when required by a program
- Learner attestation before final completion
- Issued completion evidence for auditable training outcomes

## Why This Product Matters

Learning Hub is not positioned as a simple course website. Its value lies in connecting the learner experience with organizational control.

| For learners | For instructors | For administrators and managers |
| --- | --- | --- |
| Clear path through content and practice | Structured delivery and attendance visibility | Controlled content publishing and accountability |
| Practical exercises and feedback | Cohort and session coordination | Completion evidence and reporting foundations |
| Progress they can understand | Support for learner success | Auditability and operational oversight |

## Enterprise Foundations

The platform is designed with enterprise adoption in mind:

- Role-aware experiences for learners, instructors, and administrators
- Scoped accountability for academy, course, and cohort ownership
- Content approval history and controlled publication lifecycle
- Audit events for governance and operational actions
- Completion evidence linked to learning requirements and attestation
- Identity-provider foundation for organizational authentication scenarios
- Operational structure for secure deployment, retention, and recovery planning

**Current scope note:** local sign-in and the identity-provider foundation are present; enterprise identity activation and automated provisioning depend on the target deployment and are not presented here as universally enabled defaults.

## Product Use Cases

- Internal corporate academies
- Employee onboarding and role-transition programs
- Technical upskilling with practical assignments
- Cohort-based instructor-led training
- Compliance-sensitive learning where completion evidence matters
- Finance and analytics education requiring controlled exercises

## Discussion Themes

This case study provides a strong basis for an interview discussion about:

- How a learning product can serve different roles without fragmenting the user journey
- How guided content, live delivery, and practical assignments form one measurable training experience
- Why governance, auditability, and completion evidence matter in enterprise software
- How permission-aware retrieval/RAG, pgvector-backed indexing, and citations support trustworthy learner assistance
- How human-in-the-loop AI governance handles escalation, ownership, resolution, and analytics
- How agent-orchestrated lesson drafting can accelerate authoring while preserving review and publishing control
- How a platform moves from a learning portal toward a credible enterprise learning workspace

## Keywords

`enterprise-learning` `learning-management` `internal-academy` `learner-experience` `instructor-workspace` `admin-console` `course-governance` `interactive-practice` `jupyterlab` `ai-assistant` `rag` `pgvector` `ai-governance` `human-in-the-loop` `agent-orchestration` `auditability` `completion-evidence` `role-based-access` `onboarding` `upskilling`

## Portfolio Note

This repository presentation is intentionally limited to a high-level product description and original presentation artwork. It does not publish the underlying application source code or claim a specific individual contribution; contribution details should reflect the presenter's verified role in the project.

---

<div align="center">
  <strong>Learning Hub</strong><br/>
  Structured learning. Governed delivery. Verifiable outcomes.
</div>
