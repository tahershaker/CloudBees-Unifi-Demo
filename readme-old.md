# CloudBees Unify Demo: FinSure Bank

**Role:** Senior Solutions Engineer, CloudBees (Dubai)
**Format:** 45-minute customer demo to a panel playing FinSure Bank
**Before you start:** do everything in [README-ENVIRONMENT-SETUP.md](./README-ENVIRONMENT-SETUP.md). This file assumes it is done.

---

## The idea in one paragraph

FinSure has good tools but no single view. Each business unit builds and releases in a different way. Releases are coordinated by hand, and audits take weeks. We do not ask them to replace anything. We show how CloudBees Unify connects what they have, runs one governed release process, and produces audit evidence automatically. Every click proves one of those points.

**Your story in five words:** *Keep your tools. Gain control.*

**The three questions behind every click** (from the CloudBees deck):
1. What problem does this solve?
2. Why should the customer care?
3. What business outcome does it create?

---

## How to use this file

Each step has four parts:

- **DO:** what you click.
- **SAY:** what you say. Learn the meaning, not the exact words. They said they do not want a scripted talk.
- **WHY IT MATTERS:** the business point. Say this part with more energy.
- **📸:** where to add your screenshot.

Lines marked **(verify)** are where I was not sure of the exact name on screen. Check them when you take screenshots.

---

## Time plan (45 minutes)

| Time | Part | Minutes |
|---|---|---|
| 0:00 | 1. Customer recap and agenda | 3 |
| 0:03 | 2. Why it matters, and how CloudBees approaches it (no product yet) | 2 |
| 0:05 | 3. Live demo: steps D1 to D7 | 23 |
| 0:28 | 4. Business value summary and next steps | 7 |
| 0:35 | 5. Questions and answers | 10 |

This is slightly tight on purpose. It leaves buffer in the demo and Q&A. **The most common mistake in their deck is running out of time before the summary.** If the demo runs long, cut D7 first, then shorten D2. Never cut the summary.

---

## PART 1: Customer recap and agenda (3 minutes)

**No product on screen.** Use a simple title slide, or nothing.

**SAY:**

> "Thank you for your time. Before I show anything, I want to check I understood what we learned in discovery.
>
> FinSure has grown through acquisition. You have over 600 engineering teams. They use Jenkins, GitHub Actions, GitLab CI and Azure DevOps. Around that you have Jira, ServiceNow, SonarQube, Artifactory and Kubernetes.
>
> The tools are not the problem. The problem is what sits between them. Releases need manual coordination. Compliance reporting is hard. Audit preparation takes weeks. And leadership has little visibility into delivery.
>
> Platform Engineering wants one standard way to deliver, without forcing 600 teams to migrate. And you want to adopt AI in a responsible way.
>
> Is that still right? Is there anything I should add?"

**Pause and let them answer.** This shows customer focus. If they add something, write it down and mention it again in the summary.

**Agenda (say it in one breath):**

> "Today I will show you how Unify handles four things: one view, your existing tools, a governed release, and automatic audit evidence. Then I will summarise the business value and suggest a next step. Please stop me with questions at any time."

**WHY IT MATTERS:** The deck says to start with the customer problem, not the product. This is that.

> 📸 `[ADD SCREENSHOT: opening slide, optional]`

---

## PART 2: Why it matters, and how CloudBees approaches it (2 minutes)

**Still no product.** This is where you win the executives.

**SAY (business value first):**

> "Let me say why this matters, in business terms.
>
> First, **audit and compliance**. If evidence is collected by hand after the release, audits take weeks and mistakes happen. For a bank, that is real regulatory risk.
>
> Second, **release risk**. When releases depend on emails and spreadsheets, each release is different. Different means risky.
>
> Third, **developer time**. Engineers lose time on release coordination and on building the same approval steps again and again.
>
> Fourth, **visibility**. Leaders cannot manage what they cannot see."

**SAY (how CloudBees approaches it):**

> "CloudBees Unify takes a simple approach: **embrace, do not replace**. It connects the tools your teams already use. On top, it adds one place to see delivery, one way to orchestrate releases, and governance that is built in, not added later. It also supports Platform Engineering, so you can offer a standard path without forcing everyone onto one tool.
>
> Let me show you."

**WHY IT MATTERS:** You set the success criteria before the demo starts. Later you can say "this is the audit point I mentioned."

---

## PART 3: Live demo (23 minutes)

### D1. One place to see delivery (2 minutes)

**DO:**
1. Open **Tab 1** (Unify home or dashboard).
2. Open **Applications**, then open **customer-portal**.
3. Point to the application, its linked component `cloudbees-unify-demo-kit`, and its environments `staging` and `prod`. (verify: where the component and environments show on the application page.)

**SAY:**

> "This is Unify. Here is an application, our customer portal. It has a component, which is the code and its pipeline, and it has the environments where it is released: staging and production.
>
> The point is simple. Leadership and engineers look at the same thing here. Not ten dashboards from ten tools."

**WHY IT MATTERS:** *Problem:* no single view. *Outcome:* leaders get visibility without asking teams for reports.

**Be honest:** this is a small demo environment. Say: *"In your case this would show many applications across business units."* Do not suggest it is already connected to all your tools.

> 📸 `[ADD SCREENSHOT: Applications list]`
> 📸 `[ADD SCREENSHOT: customer-portal application page]`

---

### D2. Embrace, do not replace (3 minutes)

**DO:**
1. Open **Tab 2** (GitHub, kit repo, `.github/workflows/ci.yml`). Say this is a normal GitHub Actions pipeline.
2. Go back to Unify. Open **Configurations** > **Integrations**. Show the connected GitHub App.
3. *(Optional, only if it works in your trial: verify.)* Open the component and check if the GitHub Actions run also shows in Unify. The docs have a page called "Display GitHub Actions workflows and runs".
4. Open the CloudBees workflow `ci.yaml` in the same repo (in the `.cloudbees/workflows/` folder) to show it is also simple YAML.

**SAY:**

> "Here is a normal GitHub Actions pipeline. One of your teams could own this. We do not ask them to change it.
>
> Unify connects to GitHub through an integration. Unify also connects to Jenkins controllers, and I know that matters to you because of your Jenkins estate. In this demo I have only connected GitHub. For Jenkins, GitLab and Azure DevOps I would confirm the exact setup with you in a follow-up.
>
> Teams keep the tools they like. Platform Engineering gets one layer above, for visibility and control."

**WHY IT MATTERS:** *Problem:* 600 teams, many tools, no appetite for migration. *Outcome:* you standardise **without** a migration project. This protects the investment they already made. Say this clearly. It is the main message in both scenarios.

**Be honest:** You are only showing GitHub. Do not claim you connected Jenkins, GitLab or Azure DevOps.

> 📸 `[ADD SCREENSHOT: ci.yml in GitHub]`
> 📸 `[ADD SCREENSHOT: Integrations page, GitHub App connected]`
> 📸 `[ADD SCREENSHOT: GitHub Actions run visible in Unify, only if it works]`

---

### D3. A standard pipeline that creates evidence (4 minutes)

**DO:**
1. Start the CI workflow (your usual method from Setup Step 8). If it is slow, switch to **Tab 3** (the finished run).
2. Open **Runs**, then open the run. Show the jobs in order: validate, unit tests, security scan, package.
3. Select **Jobs**, pick one job, then select the **EVIDENCE** tab.
4. Show the unit tests evidence.
5. Show the `package` job evidence and the registered artifact `orders-api` version.
6. Open the security finding on the component (only if Setup Step 9 worked).

**SAY while it runs:**

> "This is the same four steps for every team: validate, test, scan, package. A Platform team defines it once. Teams reuse it."

**SAY on the Evidence tab:**

> "Each job writes its own evidence. This is the key point for audit. The proof is created while the work happens. Nobody has to collect screenshots three weeks later."

**SAY on the failed test:**

> "You can see one test failed. This is sample data I kept on purpose. It shows that results are visible in one place. In a real setup, a policy would stop a release when a test fails. I want to be clear that in this demo the run itself still goes green, because the test step only reports the result."

**SAY on the artifact:**

> "At the end, the pipeline registers a versioned artifact, `orders-api` 1.4. That exact version is what we release next. So what we tested is what we ship."

**SAY on the security finding (if shown):**

> "Unify also found a hardcoded credential in the code. The security finding sits next to delivery, not in another tool nobody checks."

**WHY IT MATTERS:** *Problem:* audit preparation takes weeks. *Outcome:* a continuous audit trail, and less time spent preparing for audits.

**Do not say:** "this scan passed with zero critical issues." The mock data file in the repo says that, but it does not match what Unify shows live.

> 📸 `[ADD SCREENSHOT: CI run, jobs in order]`
> 📸 `[ADD SCREENSHOT: EVIDENCE tab, unit tests]`
> 📸 `[ADD SCREENSHOT: EVIDENCE tab, package, with the artifact]`
> 📸 `[ADD SCREENSHOT: security finding]`

---

### D4. A staged, repeatable release (6 minutes)

This is the main part of the demo. Take your time.

**DO:**
1. Open **Tab 4**: **Applications** > **customer-portal** > **Releases** tab > **Release 2**.
2. Show the release details: the workflow `finsure-bank-regulated-release` and the manifest. The manifest shows which artifact version will be released.
3. Select the run icon (or **Run workflow**) to start the release.
4. Show the stages as they run: **Governance**, **Staging**, **Production Approval**, **Production**, **Post-Release**.
5. While it runs, open the **Runs** tab of the release to show progress. If it is slow, switch to **Tab 5** (finished Release 1).

**SAY before you start:**

> "Today, this release would be a spreadsheet, a meeting and a lot of messages. Here it is one process, with the same stages every time.
>
> I created this release and chose the artifact version in a manifest. So the version that passed CI is the version that goes forward. Nobody can swap it by accident."

**SAY while the stages run:**

> "Stage one is governance. It checks that the evidence exists. We link a change ticket, here `CHG-10482`, and a release window.
>
> Stage two deploys to staging and runs smoke tests.
>
> Stage three is production approval.
>
> Stage four deploys to production.
>
> Stage five collects the final evidence package."

**SAY about the deployer:**

> "The deploy step is a reusable deployer. Platform Engineering writes it once. Every application uses it. That is the standard path without forcing teams to rebuild it."

**Be honest (say this clearly):**

> "To be transparent, the deployments are simulated in this demo. There is no real cluster behind it. I want to show the pattern: stages, controls and evidence. In your environment the same deployer would call your real Kubernetes deployment."

**WHY IT MATTERS:** *Problem:* manual release coordination, inconsistent process. *Outcome:* faster, repeatable and lower-risk releases, and fewer people needed to run them.

> 📸 `[ADD SCREENSHOT: release details with manifest]`
> 📸 `[ADD SCREENSHOT: release running, stages visible]`
> 📸 `[ADD SCREENSHOT: all five stages complete]`

---

### D5. The approval gate (simulated) (2 minutes)

Do this while the **Production Approval** stage is on screen.

**DO:**
1. Point to the **Production Approval** stage.
2. Open that job's **EVIDENCE**. It shows approvers: Release Manager, Security, Application Owner, and the decision.
3. Open **Configurations** > **Environments** > `prod` (or the create screen) and point to the optional **Approvers** field. (verify: the field name on screen.)
4. Open **Tab 6**: the file `policies/production-approval-policy.yaml` in GitHub.

**SAY (use these words, they matter):**

> "This is the production gate. I want to be very clear about this one: **in this demo the approval is simulated.** The workflow records an approved decision, but no person clicked approve.
>
> In a real setup, there are two ways to make it real. An environment can require named approvers before a deployment goes ahead. And the workflow editor lets you insert an approval step in the staged workflow. I have not set that up in this demo, so I do not want to claim more than I showed.
>
> This policy file shows what we would agree with you. For example, two approvers from release management and security, and four pieces of evidence required before production. It is an example I prepared to start the conversation. It is not a setting that is switched on in this environment."

**WHY IT MATTERS:** *Problem:* security approvals vary by team. *Outcome:* the same controls every time, and the approval is recorded as evidence. This is "governance without slowing developers," because the gate is part of the flow, not a separate meeting.

**Why this honesty helps you:** the panel scores honesty and technical credibility. The deck says *"Overstating product capabilities"* is a common mistake. A clear "this is simulated, here is how it becomes real" scores better than a bluff.

> 📸 `[ADD SCREENSHOT: Production Approval stage]`
> 📸 `[ADD SCREENSHOT: approval evidence]`
> 📸 `[ADD SCREENSHOT: prod environment Approvers field]`
> 📸 `[ADD SCREENSHOT: production-approval-policy.yaml in GitHub]`

---

### D6. The audit trail (3 minutes)

**DO:**
1. Open the finished release (Release 1 in **Tab 5** if Release 2 is still running).
2. Select the report icon next to the release, then **Audit report** > **Evidence**.
3. Scroll through the evidence by job: governance, staging validation, production approval, final evidence package.
4. Show the final table with the controls (unit tests, security scan, change approval, staging validation, production approval, change ticket).
5. Show **Download report** (PDF). Do not open it. Just point to it.

**SAY:**

> "This is the audit trail for the release. It was made by the pipeline, job by job. It lists the change ticket, the tests, the scan, the approval and the staging validation.
>
> Today, you told us audit preparation takes weeks. Here, an auditor can ask 'show me release X' and you open one page, or download a PDF.
>
> I want to be clear that the change ticket here is a text input. I have not connected ServiceNow or Jira in this demo. The next step is to link the real tickets, so the evidence points at your system of record."

**WHY IT MATTERS:** *Problem:* compliance reporting is hard and audits take weeks. *Outcome:* a continuous, automatic audit trail. This is the strongest business point of the whole demo. Slow down here.

> 📸 `[ADD SCREENSHOT: Audit report > Evidence]`
> 📸 `[ADD SCREENSHOT: final release evidence package table]`

---

### D7. Visibility, analytics and AI (1 to 2 minutes, talk-level)

**Show a page only if it has real data (Setup Step 12). If it is empty, do not open it. Just talk.**

**DO (only if populated):** open **Analytics** and show one dashboard. The docs list six: DORA metrics, Flow metrics, Software delivery activity, Test insights, Security insights, CI insights.

**SAY (analytics):**

> "As releases run through this one flow, Unify can show delivery metrics. For example, how often you deploy, how long changes take to reach production, and how often changes fail. This environment is new, so there is little data, but with 600 teams this is what your leadership would look at."

**SAY (AI):**

> "You also asked about responsible AI adoption. I did not prepare a live AI demo today because I did not want to show something I have not tested myself. What I can say is that the same idea applies. When AI helps write or change code, you want the same visibility and approval, and the same evidence. I would be glad to bring the right product specialist to a follow-up session to go deeper on AI governance."

**WHY IT MATTERS:** It answers the AI goal honestly and keeps you inside the time. The deck lists honesty and "admit when you don't know" as success signs.

**Do not say:** anything about AI guardrails, MCP or specific AI features as if you showed them. The repo's `ai-governance-policy.yaml` is only a mock file.

> 📸 `[ADD SCREENSHOT: Analytics dashboard, only if it has data]`

---

## PART 4: Business value summary and next steps (7 minutes)

Close the browser tabs or return to a clean slide. Look at the audience.

**SAY (problems → outcomes):**

> "Let me bring it together. You told us five things, and here is what we showed.
>
> **Too many tools, no migration appetite.** Unify connects what you have. Teams keep their tools. You protect your investment.
>
> **No single view.** One place for leaders and engineers to see the same delivery picture.
>
> **Manual release coordination.** A staged release with the same steps every time, and the exact tested version moves forward.
>
> **Inconsistent security approvals.** A governed gate in the flow, recorded as evidence. Governance without slowing developers.
>
> **Audit takes weeks.** Evidence is created automatically at every step, so audit preparation becomes opening a report, not weeks of collecting."

**SAY (measurable outcomes — do not invent numbers):**

> "I will not quote a percentage today, because I do not want to guess at your numbers. What I suggest is that we agree on a few measures together. For example: how long audit preparation takes today, how many manual steps a release needs, how many releases have complete evidence, and how often you deploy and how fast. We measure the baseline first, then we measure again after a pilot."

**SAY (why CloudBees):**

> "Why CloudBees? Three reasons. We work with the tools you already run, including Jenkins. We put governance and evidence inside the delivery flow. And we give Platform Engineering a standard path without forcing a migration."

**SAY (next step):**

> "My suggested next step is a short pilot. Pick two or three teams, ideally on different tools, for example one on GitHub Actions, one on Jenkins and one on GitLab. Connect them to Unify, and run one real application through a governed release. We agree the success measures before we start. We then link your real ServiceNow and Jira, and we look at AI governance with a product specialist. Would a pilot like that make sense for you? Who else should be in that conversation?"

**WHY IT MATTERS:** The deck says to finish with challenges, outcomes, why CloudBees and a next step. Ask for the next step. Ending with a question keeps control.

---

## PART 5: Questions and answers (10 minutes)

**Golden rule from CloudBees:** if you do not know, say so, and show how you would find out. Do not guess. Use this line:

> "Good question. I do not want to guess. My understanding is X. I will confirm it in the documentation and with our product team, and send you a written answer."

### Business questions

**"Do we have to replace our tools?"**
No. This is the main message. Unify connects the tools you have. You can adopt it one team at a time.

**"How does this help with compliance?"**
Each job produces evidence automatically. The release has an audit report. Approvals are part of the flow. So the audit trail is continuous, not built after the fact.

**"What is the ROI? Why now?"**
Less manual coordination, fewer release mistakes, less audit effort, one view for leaders. I would not quote numbers without your data. We would measure a baseline in a pilot.

**"How disruptive is adoption?"**
Low. You connect a team at a time. Existing pipelines keep running.

**"How does this help us with AI?"**
Honest answer: the principle is visibility, approval and evidence for any change, including AI-assisted ones. I did not demo AI features today, and I would bring a specialist to go deeper.

### Technical questions

**"How is this different from GitHub Actions?"**
The workflow model is similar, written in YAML. Unify adds what sits above one pipeline: connecting several tools, staged releases across environments, the evidence, and the application and component structure.

**"What is the difference between a component and an application?"**
A component is one repo and its pipeline. An application is a product made of components, and it owns the release. They must be separate repos.

**"How do approvals work?"**
In this demo they are simulated. In a real setup, an environment can require named approvers, and a staged workflow can include an approval step. I would confirm the exact options for your setup.

**"Where does deployment actually happen?"**
In this demo it is simulated. In a real setup the deployer workflow calls each component's deploy workflow for each environment, for example to Kubernetes.

**"Does it integrate with ServiceNow and Jira?"**
The deck and the repo treat them as part of the story. In this demo the change ticket is a plain input and I did not connect either tool. I would confirm exactly how the integrations work for your set-up.

**"What about Jenkins?"**
The documentation covers connecting Jenkins controllers to Unify. I did not set this up in the demo, so I would walk you through it in a follow-up.

**"The test failed but the run is green. Why?"**
It is sample data. The test step only reports results. In a real pipeline you would set the step to fail the job, and a policy would block the release.

**"Is it secure for a bank?"**
I do not want to answer security architecture questions from memory. I would bring our security documentation and a specialist, and answer in writing.

**"How does pricing work?"**
I would not quote pricing today. I would take this to the account team.

---

## What NOT to say

- "This scan passed with zero critical findings." (Not true in the live view.)
- "The approval is enforced." (It is simulated.)
- "It is connected to ServiceNow, Jira or Jenkins." (It is not, in this demo.)
- Any percentage or saving you cannot prove.
- Any AI feature you did not see yourself.
- "As you can see..." when the screen is empty. Skip empty pages.

---

## If something goes wrong

| Situation | What to do |
|---|---|
| A live run is slow | Say: "While this runs, let me show you the finished run." Switch to the backup tab. |
| A run fails | Stay calm. Say: "This is a good moment to show that failure is also visible." Then switch to the backup. |
| A page will not load | Use your screenshots in this README as a last option. Say what you are showing. |
| You forget a step | Go back to the business point: "The key idea here is..." |
| A question is outside your knowledge | Use the "I do not want to guess" line. |
| You run out of time | Cut D7, then shorten D2. Never cut Part 4. |

---

## One-page cheat sheet

| Step | Show | One-line message | Outcome |
|---|---|---|---|
| D1 | Application and component | One view for everyone | Visibility |
| D2 | GitHub Actions + Integrations | Keep your tools | Protect investment, no migration |
| D3 | CI run + Evidence | Evidence is automatic | Less audit effort |
| D4 | Staged release | Same process every time | Lower release risk |
| D5 | Approval (simulated) | Control built in | Governance without friction |
| D6 | Audit report | One page for the auditor | Less audit preparation (measure in pilot) |
| D7 | Analytics, AI (talk only) | Measure it, govern AI | Leadership insight |

**Last words:** *"Keep your tools. Gain control. Let us prove it with a small pilot."*

---

## Sources

The click paths and product facts come from the CloudBees documentation (see the list in [README-ENVIRONMENT-SETUP.md](./README-ENVIRONMENT-SETUP.md)), the CloudBees "SE Demo Stage 1" deck, and the two demo repos:
- [cloudbees-unify-demo-kit](https://github.com/cb-demos/cloudbees-unify-demo-kit)
- [cloudbees-unify-demo-app](https://github.com/cb-demos/cloudbees-unify-demo-app)
