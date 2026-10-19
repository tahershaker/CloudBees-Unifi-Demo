# CloudBees Unify Demo: FinSure Bank

> A step-by-step walkthrough of a live CloudBees Unify demo for a financial services customer: one place to see delivery, a pipeline that creates evidence, a staged release, and an audit trail. To build the environment first, follow [README-ENVIRONMENT-SETUP](./prepare_environment.md).

---

# Description

This file walks you through a 45-minute CloudBees Unify demo, based on the FinSure Bank scenario. 

The demo tells one story. A large bank has many teams and many CI/CD tools, and it needs a safe, repeatable release process that it can audit. We show how Unify helps, in this order:

- A CI run that builds, tests and scans a small service, and publishes evidence for each job.
- A staged release that moves the same artifact through `staging` and `prod`.
- An approval gate and an audit trail that a compliance team can read.
- A short look at the dashboards and the AI assistant.

Two parts of the demo are simulated on purpose: the deployment, and the approval. The pipelines, the release workflow and the evidence do run in CloudBees. 

**Before you start:** the demo environment is already built, so this file starts straight with the demo. If you want to build the same environment in your own CloudBees trial, follow the step-by-step guide in [README-ENVIRONMENT-SETUP](./prepare_environment.md).

---

# The customer scenario: FinSure Bank

This demo follows a customer scenario provided by CloudBees. We assume discovery is already finished. The customer knows CloudBees at a high level and has agreed to see a demo built around their own situation. Before we open the product, let us make sure we understand who FinSure Bank is, what hurts, and what they want.

## Who they are

FinSure Bank is a financial services company with about 20,000 employees and more than 600 engineering teams. It has grown through acquisition. Each acquired business unit brought its own way of building and shipping software, and nobody has forced them into one model.

Their environment today:

| Area | Tools in use |
| --- | --- |
| CI/CD | Jenkins, GitHub Actions, GitLab CI, Azure DevOps |
| Runtime | Kubernetes |
| Work and change tracking | Jira, ServiceNow |
| Quality and artifacts | SonarQube, Artifactory |

The important point is that this is not a greenfield. The bank has four different CI/CD tools, and each one has teams, pipelines and years of habits built around it.

## Who is in the room

We assume five roles are in the audience. They care about different things, and a good demo speaks to all of them.

- **VP Engineering** cares about delivery speed, release risk and what leadership can see.
- **Director of Platform Engineering** owns the standard. This person wants consistency without a fight with 600 teams.
- **DevOps engineers** care about how pipelines run, how releases are wired and what they must maintain.
- **Software developers** care about whether their daily work gets harder or easier.
- **Enterprise architects** care about how a new platform fits next to what already exists.

Some of them want technical detail. Others only want the business outcome.

## Their pain points

**1. Teams operate differently.** With four CI/CD tools and 600+ teams, there is no common way to build, test, scan or release. Each team defines "done" in its own way. This makes quality uneven and makes it hard for cross-teams collaboration.
**2. Releases need manual coordination.** A release across teams means chat threads, spreadsheets, meetings and sign-offs by hand. This is slow, and it depends on people remembering every step. In a bank, a missed step can become a compliance problem.
**3. Compliance reporting is difficult.** The proof that a release followed the rules is spread across many tools. Someone has to collect it, and it is not in one format. When a regulator or an internal auditor asks "show me that this change was tested and approved", the answer takes long time and effort to build.
**4. Audit preparation takes weeks.** This is the cost of the first three problems. Teams stop their work to collect evidence for an audit. That is lost engineering time, and it repeats on every audit cycle.
**5. Leadership has little visibility.** The VP Engineering cannot easily answer simple questions. How fast do we deliver? Where are releases stuck? Which teams follow the standard? Without a single view across all the tools, decisions rely on reports that people build by hand.
**6. Platform Engineering wants standardization without forcing a migration.** This one is a constraint, not only a pain. The platform team knows that telling 600 teams to leave Jenkins or GitLab will fail. The standard has to work with the tools that teams already use.

## What they are looking for

These are the business goals. We link each one to the pain it answers.

| Goal | The pain it answers |
| --- | --- |
| **Standardize software delivery** | Teams operate differently |
| **Improve governance** | Releases need manual coordination |
| **Improve auditability** | Compliance reporting is difficult, and audit preparation takes weeks |
| **Reduce release risk** | Manual steps and uneven quality |
| **Preserve existing investments** | Forcing a migration is not an option |
| **Increase developer productivity** | Time lost to manual coordination and audit work |
| **Enable responsible AI adoption** | Teams start using AI coding tools, and the bank needs control and visibility |

The last goal is worth a note. A regulated bank cannot adopt AI coding tools without guardrails. This is a goal the customer stated, but the scenario gives no detail on it. We treat it as a talking point in the demo.

---

# Demo path and strategy

## The strategy

The demo tells one story, in one line: **teams keep their tools, and Unify gives the bank one standard way to release and one place to prove it.**

Every part of the demo answers three questions: what problem does this solve, why should the customer care, and what business outcome does it create.

We speak to two audiences at once. For the VP Engineering and the Platform Engineering director, we talk about outcomes: less audit effort, lower release risk and better visibility. For the DevOps engineers and architects, we show how it works in the workflow files and in the Unify screens. 

## The two repositories

The demo spans two repositories. This mirrors how Unify separates a component from an application.

- **Component** (`cloudbees-unify-demo-kit`): the CI pipeline and the component deploy.
- **Application** (`cloudbees-unify-demo-app`): the staged release workflow and the governance and evidence material.

## The demo path

The session starts with three or four slides: the customer's pain points and goals, a short recap of Unify, and a diagram of what we will do. Then we move to the live demo. The table below shows the live part, in order. We start the CI run early, and we explain the component while it runs, so we do not wait on screen.

| Step | What we show | The pain it answers | The outcome | Minutes |
| --- | --- | --- | --- | --- |
| 1 | **The repositories.** In the kit: `.cloudbees/workflows/ci.yaml`, `deploy.yaml`, and `.github/workflows/ci.yml` as an example of existing CI. In the app: `release-finsure-bank.yaml` and `deployer.yaml`. | Platform Engineering cannot force a migration | Teams keep their tools | 3 |
| 2 | **The Unify UI walkthrough.** First, start the CI run from the component. Then tour the menu: Home, Components, Runs, Applications and Releases in a minute, then Security (Dashboard, Marketplace, SLA configuration), Audit history, Analytics, Feature management and Smart tests. | Leadership has little visibility, and inconsistent governance | One place for the whole delivery process | 5 |
| 3 | **Integrations.** The full list of tools Unify connects to, then our own GitHub integration. | Teams use different CI/CD tools | Standardize without forcing teams to move | 2 |
| 4 | **The component.** The CI run we started, its pipeline stages, and the artifact it registers. | Teams work differently | One standard build, test and scan pattern | 3 |
| 5 | **The application.** Its component, its two environments, and its workflows. | Manual release coordination | One place that owns the release | 3 |
| 6 | **The release.** Create it and run it from start to finish: governance, staging, approval, production and post-release. | Manual coordination, inconsistent governance | A repeatable release with controls | 5 |
| 7 | **The evidence.** The **Evidence** tab on the CI run and on the release run. | Compliance reporting is hard, and audits take weeks | A readable audit trail without collecting proof by hand | 4 |

Total: 25 minutes.

## How the time is used

The session is 45 minutes. This is the plan:

| Part | Minutes |
| --- | --- |
| Slides: customer pain points and goals, Unify recap, demo diagram | 5 |
| Live demo | 25 |
| Business value summary, next steps and follow-up actions | 5 |
| Questions and answers | 10 |

---

# The demo

## How we will start

We start with the customer, not the product. The first five minutes are a short presentation with six slides. It sets the scene, and then the demo shows it in action.

1. **We listened, we understood, we are here to help.** A recap of FinSure Bank from discovery.
2. **Software delivery reality.** Many tools, many ways to build a pipeline, and hidden dependencies that nobody owns. Focusing on the pain point.
3. **Green is not the same as ready.** Every tool reports its own "green", but none of them agrees on what "fine" means. When a VP asks "Are we safe to ship?", no single tool can answer. Focusing on the cost of the pain point.
4. **The 2025 DevOps Migration Index.** Large migrations often miss their expected return, and organizations that integrate their tools rather than replace them report better delivery results. Focuse on avoiding rip-&-replace approache.
5. **CloudBees Unify.** CloudBees Unify sits above the existing tools. It collects signals from source, planning, build, test, security, packaging, release and operations, and adds governance, policy, security and compliance in one place. Focusing on the solution to the pain point without rip-&-replace.
6. **What we will see today.** A map of the demo in five steps: building the base for the demo activities.

## The demo path in plain text

The demo follows one service, `orders-api`, from a code change to a production release.

First, we run the CI pipeline for `orders-api`. It has four jobs: `validate`, `unit-tests`, `security-scan` and `package`. The last job registers a versioned artifact, `orders-api:1.4.<run number>`.

Then we release that artifact through the application. The release workflow, `finsure-bank-regulated-release`, moves it through five stages: Governance, Staging, Production Approval, Production and Post-Release. A person approves the release before it reaches production.

Finally, we look at the evidence that CloudBees recorded for the run and the release, and we take a short tour of the Unify screens that give leaders visibility.

## The GitHub repositories

The demo uses two repositories. This mirrors how Unify separates a component from an application.

| Repository | What it holds | What to show |
|------------|---------------|--------------|
| `cloudbees-unify-demo-kit` (component) | The `orders-api` service, its CI pipeline and the deploy workflow | The workflow files in `.cloudbees/workflows`: the four CI jobs and the deploy workflow |
| `cloudbees-unify-demo-app` (application) | The staged release workflow, `finsure-bank-regulated-release`, and the `deployer` workflow | The workflow files in `.cloudbees/workflows`: the five stages and the call to the deployer |

What to explain: the code stays in GitHub, and the pipelines are plain workflow files that the team already knows how to read. Unify does not take the code away. It runs and records the pipelines. The application is a different repository from the component, so release rules live in one place and do not need to be copied into every service.

## Demo step by step

### Step 1: Show the two GitHub repositories

**Steps in the UI**
1. Open `cloudbees-unify-demo-kit` in GitHub. Open the `.cloudbees/workflows` folder and show the workflow files.
2. Open `cloudbees-unify-demo-app`. Open its `.cloudbees/workflows` folder and show the release workflow and the deployer.

**What to say**
> "This is where your teams work today. The code and the pipelines are in GitHub, and they stay there. There are two repositories. The kit holds the `orders-api` service and its pipelines. This is the component. The app holds the release workflow. This is the application. The service and its release are kept apart, so one release process can serve many services."

**The three questions**
- *What does this solve?* Teams are afraid that a new platform means moving code and rewriting pipelines.
- *Why should the customer care?* A migration across 600+ teams is slow, risky and expensive.
- *What is the business outcome?* The bank starts to get value without a migration project.

**Key messages**
- *Business:* You keep what you have. Nothing in your process changes drastically, and your investment in GitHub and your pipelines is protected. There is no migration, so value arrives sooner and the total cost stays lower. (VP Engineering, Director of Platform Engineering)
- *Technical:* The code stays in GitHub and the pipelines are plain workflow files. DevOps Engineers read and edit them as they do today. Developers keep their current way of working. Architects see a clean split between a service (component) and its release (application).

**Bridge:** "Let me show you how Unify connects to GitHub."

### Step 2: Show the integration

**Steps in the UI**
1. In Unify, open **Configurations**, then the **Integrations** tab.
2. Show the GitHub App integration `CloudBees-Demo-Test-GitHub-App-01`.
3. Show the list of other integrations that are available.

**What to say**
> "Unify connects to the tools you already use. This is the GitHub integration. We connected it with a few clicks. There was no plugin to install and no custom code to write, and we gave it access only to the repositories we chose. The same approach applies to the other tools in your toolchain."

**The three questions**
- *What does this solve?* Integrations between tools are built by hand, and plugins need installing and maintaining.
- *Why should the customer care?* Manual integrations take effort, break after upgrades and differ from team to team.
- *What is the business outcome?* Faster onboarding of teams and lower cost to maintain the toolchain.

**Key messages**
- *Business:* You get an extensive ecosystem without changing your tools. Teams connect in minutes, so you see results quickly and avoid the cost of custom integration work. (VP Engineering, Director of Platform Engineering)
- *Technical:* Connecting is a click, not a project. DevOps Engineers do not install or patch plugins. Developers do not change how they push code. Architects get one connection model across tools, with access limited to selected repositories.

![image1](/Images/Demo/image1.png)

**Bridge:** "Now that Unify is connected, let me show what it builds from our repository: the component."

### Step 3: Show the component

**Steps in the UI**

> Create a new components during the demo, but use the existing one ad the creation would take time

1. Open **Components** in the left menu.
2. Open `cloudbees-unify-demo-kit`.
3. Point out the repository link, the workflows, and the runs and artifacts tabs.

**What to say**
> "A component is the central place for one piece of software, something a team is building. It is tested, packaged, scanned, deployed and versioned. The component collects all of these actions and connects them, so you get end-to-end traceability for that one piece of software."

**The three questions**
- *What does this solve?* Information about one service is scattered across the build tool, the scanner, the registry and the deploy tool.
- *Why should the customer care?* Nobody can answer "what happened to this service?" without asking several teams.
- *What is the business outcome?* Faster answers and less time spent on audits and incidents.

**Key messages**
- *Business:* One record for each piece of software means faster audits and clearer accountability, with no extra tooling to buy. (VP Engineering, Director of Platform Engineering)
- *Technical:* The component links builds, tests, scans, packages and deployments for a service. DevOps Engineers find everything in one place. Developers see the history of their own service. Architects get one model of a service, whatever tools sit underneath.

![image2](/Images/Demo/image2.png)

**Bridge:** "A component can have more than one pipeline. Let me show you that."

### Step 4: Show the different workflows in the component

**Steps in the UI**
1. In the component, open the **Workflows** list.
2. Show the CloudBees workflow, and then show the GitHub Actions workflow in the same component.

**What to say**
> "This component has two pipelines. One is a CloudBees workflow. The other is a GitHub Actions workflow. Your teams can keep their GitHub Actions pipelines, and they appear in the same component. You do not have to migrate anything to see them together."

**The three questions**
- *What does this solve?* Teams use different pipeline tools, so there is no common view.
- *Why should the customer care?* Forcing everyone onto one pipeline tool would take years.
- *What is the business outcome?* Standardization without a migration project.

**Key messages**
- *Business:* You get one view without a forced migration. Teams adopt it at their own pace, so there is no disruption to delivery and the investment in current pipelines is kept. (VP Engineering, Director of Platform Engineering)
- *Technical:* Pipelines stay as they are. DevOps Engineers can keep GitHub Actions and add CloudBees workflows where they want to. Developers do not rewrite their pipelines. Architects see GitHub Actions and CloudBees workflows under the same component model.

![image3](/Images/Demo/image3.png)

**Bridge:** "Let me run the CloudBees pipeline first."

### Step 5: Run the CloudBees CI

**Steps in the UI**

> Create a new run during the demo, but use the existing one ad the creation would take time

1. In the component, start a run with **New run**.
2. Open the run and show the four jobs: `validate`, `unit-tests`, `security-scan` and `package`.
3. Open the output of each job as it completes.

**What to say**
> "This is one standard path for a service: validate, test, scan, package. Every team can follow the same path. Each job reports its result here, and the last job creates a versioned artifact."

**The three questions**
- *What does this solve?* Every team builds and checks software in a different way, so quality and security checks are not comparable.
- *Why should the customer care?* An inconsistent process means inconsistent quality and security.
- *What is the business outcome?* Consistent quality and security across teams, with less risk in each release.

**Key messages**
- *Business:* One standard path gives consistent quality and lower release risk across all teams, with no extra tools to buy. (VP Engineering, Director of Platform Engineering)
- *Technical:* The path is a reusable workflow. The Platform team defines it once. DevOps Engineers reuse it instead of copying pipelines. Developers get fast, clear feedback on each job. Architects see a standard that other services can follow.

![image4](/Images/Demo/image4.png)

**Bridge:** "That is the CloudBees pipeline. Now let me show that the tools you use today work too."

### Step 6: Run the GitHub Actions workflow from GitHub

**Steps in the UI**
1. Open the repository in GitHub and go to the **Actions** tab.
2. Select the GitHub Actions workflow and click **Run workflow**.
3. Switch to Unify and open the component. Show the run that appears there.

**What to say**
> "I started this run from GitHub, the way your developers do today. They did not change anything. Now look in CloudBees. The same work appears in the component. You keep using your current tools, and CloudBees shows the work."

**The three questions**
- *What does this solve?* Work done in existing tools is invisible to leadership and to the platform team.
- *Why should the customer care?* Without visibility, the bank cannot standardize or prove anything.
- *What is the business outcome?* Visibility across teams without a migration.

**Key messages**
- *Business:* You get unified visibility and governance on top of your current tools. Nothing is replaced, so the return is faster and the total cost is lower. (VP Engineering, Director of Platform Engineering)
- *Technical:* Developers run GitHub Actions as they do today. DevOps Engineers add nothing to their pipelines. Architects see that Unify works alongside existing tools, not instead of them.

![image5](/Images/Demo/image5.png)

**Bridge:** "Now let us look at what these runs recorded."

### Step 7: Review the CI run and its evidence

**Steps in the UI**
1. Open the finished CloudBees run.
2. Show the job results.
3. Open the **Evidence** tab.

**What to say**
> "Each job recorded its result. This is the record an auditor asks for. It was created whilst the work was done. Nobody had to collect it afterwards."

**The three questions**
- *What does this solve?* Audit preparation takes weeks because evidence is gathered by hand from many tools.
- *Why should the customer care?* Audits are slow, costly and stressful for engineers.
- *What is the business outcome?* Faster, cheaper audits with less effort from engineering teams.

**Key messages**
- *Business:* Easier auditing and compliance. The evidence is recorded in the same place where the work happens, so audit cycles take less time and effort. (VP Engineering, Director of Platform Engineering)
- *Technical:* DevOps Engineers do not collect screenshots and logs. Developers are not pulled away to answer audit questions. Architects get a consistent evidence model across tools.

![image6](/Images/Demo/image6.png)

> Run it again after adding the security scaning Gitleaks
```yaml
      - name: Scan for secrets with Gitleaks
        uses: https://github.com/cloudbees-io/gitleaks-plugin@v1
        continue-on-error: true
```

**Bridge:** "The run also produced something that we can release: the artifact."

### Step 8: Show the artifact

**Steps in the UI**
1. In the component or in the run, open the **Artifacts** section.
2. Show the artifact `orders-api:1.4.<run number>` and its version.

**What to say**
> "The package job registered this artifact, and it has a version. This is the exact thing that will be released. We can trace it back to the run and the commit that produced it."

**The three questions**
- *What does this solve?* Teams cannot always say which build is running in production.
- *Why should the customer care?* An untraceable release is a risk in an incident and in an audit.
- *What is the business outcome?* Clear traceability and lower release risk.

**Key messages**
- *Business:* You know exactly what you release, and you can prove it. This lowers risk and shortens audits. (VP Engineering, Director of Platform Engineering)
- *Technical:* Every artifact is versioned and linked to its build. DevOps Engineers trace a deployment back to its source. Developers find their build quickly. Architects get one traceable unit that moves from build to release.

![image7](/Images/Demo/image7.png)

**Bridge:** "We have a tested, versioned artifact. Now we need something that controls how it is released: the application."

### Step 9: Show the application

**Steps in the UI**
1. Open **Applications** in the left menu.
2. Open the application (named `customer-portal-test` today; rename it to `customer-portal`).
3. Show the workflows (`finsure-bank-regulated-release` and `deployer`) and the environments `staging` and `prod`.

**What to say**
> "An application is similar to a collection. It brings together the components that make up a product, and it owns the release. The release process is defined here once, not copied into every service."

**The three questions**
- *What does this solve?* Release rules are copied into every pipeline and drift apart.
- *Why should the customer care?* Each team follows a different release process, so governance is inconsistent.
- *What is the business outcome?* One governed release process for the whole bank.

**Key messages**
- *Business:* One release process means consistent governance, lower risk and a simple answer to "how do we release?". (VP Engineering, Director of Platform Engineering)
- *Technical:* The Platform team defines the release workflow once. DevOps Engineers do not maintain release logic in every pipeline. Developers use the process without having to learn it. Architects see release modelled apart from build.

![image8](/Images/Demo/image8.png)

**Bridge:** "Now let us release the artifact."

### Step 10: Release through the staged workflow

**Steps in the UI**
1. In the application, start a release of `orders-api:1.4.<run number>`.
2. Open the release and follow the stages: Governance, Staging, Production Approval, Production and Post-Release.
3. Open the output of the Governance stage.

**What to say**
> "Every release follows the same five stages. There is a governance check first, then staging, then production approval, then production. In this demo the deployment, the test results and the approval are simulated. The workflow and the record are real."

**The three questions**
- *What does this solve?* Releases need manual coordination across teams, by email and chat.
- *Why should the customer care?* Manual coordination is slow and error-prone, and it differs for every team.
- *What is the business outcome?* Faster, safer releases with less manual effort.

**Key messages**
- *Business:* One governed path to production lowers release risk and removes manual coordination, so teams ship faster with control. (VP Engineering, Director of Platform Engineering)
- *Technical:* The stages are defined in a workflow file. DevOps Engineers stop chasing approvals by hand. Developers see where their release is and what it waits for. Architects see governance built into the path, not added afterwards.

![image9](/Images/Demo/image9.png)

Show the evidence from the Audit report of the release

![image10](/Images/Demo/image10.png)

**Bridge:** "That release did not pause for a person. Let me show you what happens when a human has to approve."

### Step 11: Repeat the release with a human approver

#### Before you start: replace the simulated approval with a real one

In the kit, the `production-approval` job only prints a message and says "approved". Nothing is recorded, and nobody is asked. To show a real human approval, we replace this job with the manual approval job that CloudBees provides. It pauses the release, asks a named person to approve, and records who approved and when.

The change is made in your fork of the application repository, `cloudbees-unify-demo-app`.

1. Open the file `.cloudbees/workflows/release-finsure-bank.yaml` and find the `production-approval` job. It looks like this:

```yaml
  production-approval:
    needs:
      - staging-validation
    steps:
      - name: Production approval (demo talking point)
        uses: docker://alpine:3.20
        shell: sh
        run: |
          echo "TALKING POINT: add a manual approval gate here in the CloudBees Unify Workflow Composer."
          echo "Suggested approvers: Release Manager, Security, Application Owner"
          echo "Approval: SIMULATED / APPROVED"
      - name: Publish evidence
        uses: https://github.com/cloudbees-io/publish-evidence-item@v1
        with:
          content: |-
            ## Production approval
            - Approvers: Release Manager, Security, Application Owner
            - Change ticket: ${{ inputs.change_ticket }}
            - Decision: **approved** (simulated for demo)
```

2. Replace the whole job with the following. Change `<approver>` to the email address or user ID of the Unify user who will approve the release:

```yaml
  production-approval:
    needs:
      - staging-validation
    with:
      approvers: "<approver>"
      disallowLaunchByUser: false
      instructions: "Review the change ticket and the release window, then approve the production release."
    timeout-minutes: 60
    delegates: cloudbees-io/manual-approval/custom-job.yml@v1
```

This job has no steps of its own. The `delegates` line tells Unify to use its ready-made approval job. `approvers` names who can approve. `disallowLaunchByUser: false` lets the person who started the release approve it as well. `timeout-minutes` sets how long the release waits for an answer.

3. Commit the change to the `main` branch.

From now on, every release stops at the **Production Approval** stage until the approver responds. The approval is recorded in the **Approvals** tab of the release audit report.

**Steps in the UI**
1. In the application, start another release of the same artifact.
2. Wait at the **Production Approval** stage.
3. Open the approval request and approve it as the approver.
4. Show the release continuing to Production and Post-Release.

**What to say**
> "This time the release stops and waits. A person must approve before it can go to production. The approval is recorded with the release."

**The three questions**
- *What does this solve?* Approvals happen outside the tools, so nobody can prove who approved what.
- *Why should the customer care?* In a bank, a release to production needs a recorded, accountable approval.
- *What is the business outcome?* Accountability and a clean audit trail without slowing the release.

**Key messages**
- *Business:* Human control stays in the process, and the approval is on record. This gives governance and audit evidence without extra paperwork. (VP Engineering, Director of Platform Engineering)
- *Technical:* The approval is a stage in the workflow. DevOps Engineers do not build a separate approval tool. Developers wait in one place, not in an email thread. Architects see human approval as one more step in the same flow.

**Bridge:** "Both releases are finished. Let me show what the bank can see afterwards."

### Step 12: Show visibility and evidence

**Steps in the UI**
1. Open the release and then its **Evidence**.
2. Open **Audit history**.
3. Open **Runs** to show the CloudBees run, the GitHub Actions run and the releases together.

**What to say**
> "This is the answer to the question 'are we safe to ship?'. The runs, the releases, the approvals and the evidence are in one place, across tools and teams."

**The three questions**
- *What does this solve?* No single tool can say what was built, tested, approved and released.
- *Why should the customer care?* Leadership cannot see delivery across 600+ teams.
- *What is the business outcome?* Better decisions, lower risk and shorter audit cycles.

**Key messages**
- *Business:* Unified visibility and governance, with easy auditing. Leaders see delivery across teams without asking for reports. (VP Engineering, Director of Platform Engineering)
- *Technical:* DevOps Engineers get one place to look when something breaks. Developers see the full path of their change. Architects see one record that spans several tools.

![image12](/Images/Demo/image12.png)

**Bridge:** "There is more in the platform. Let me show a few areas quickly."

### Step 13: A walk through the rest (if time permits)

**Steps in the UI**
1. Open **Security**: the dashboard, the Marketplace of scanners and the SLA configuration.
2. Open **Analytics**.
3. Name **Feature management**, **Smart tests** and **Jenkins management**. Do not open them unless asked.

**What to say**
> "These areas build on the same foundation. Security brings scan results and fix deadlines together. Analytics shows delivery performance. Feature management, Smart tests and Jenkins management are topics for a follow-up session, if they matter to your teams."

**The three questions**
- *What does this solve?* Security, delivery metrics and release controls live in separate tools.
- *Why should the customer care?* Fragmented tooling costs money and hides risk.
- *What is the business outcome?* One platform for several needs, built on the tools the bank already has.

**Key messages**
- *Business:* More value from the same investment. The bank can adopt more capabilities over time, with no migration. (VP Engineering, Director of Platform Engineering)
- *Technical:* Security teams and DevOps Engineers use scanners they know, such as those in the Marketplace. Developers get findings with fix deadlines. Architects see a platform that grows with the toolchain.

**Bridge:** "Let me summarise what this means for FinSure Bank."

---