# Environment Setup: CloudBees Unify Demo (FinSure Bank)

> Preparing a CloudBees Unify trial for the FinSure Bank demo: connecting the two GitHub repos and creating the component, the application and the two environments. The demo itself, step by step, is in a separate file: [README.md](./README.md).

---

# Description

This file helps you build the demo environment for a CloudBees Unify demo, based on the FinSure Bank scenario. It only prepares the environment. The demo itself, step by step, is in [README.md](./README.md).

To prepare for the demo, we need to:

- Create a CloudBees Unify account.
- Fork the component repository: **[cloudbees-unify-demo-kit](https://github.com/cb-demos/cloudbees-unify-demo-kit)**. It holds the CI pipeline and a simulated deploy for a small service called `orders-api`.
- Fork the application repository: **[cloudbees-unify-demo-app](https://github.com/cb-demos/cloudbees-unify-demo-app)**. It holds the staged release workflow and a reusable deployer.

There are two repositories because, in CloudBees Unify, a component and an application cannot be the same repository. A component is one repository and its pipeline. An application is the product made of components, and it owns the release.

In the steps below, we connect GitHub to CloudBees Unify, then create the component, the two environments and the application. We also make one small change in the application fork, so the release can find the deploy workflow.

The deployment and the test results in the demo are simulated, so no cluster, secret or registry is needed. The pipelines and the release workflow do run in CloudBees.

---

# The FinSure Bank scenario (FYI)

The demo follows a customer scenario provided by CloudBees. It does not change how you build the environment, so this is only for context.

FinSure Bank is a financial services company with about 20,000 employees and more than 600 engineering teams. It grew through acquisition, so each business unit uses different CI/CD tools: Jenkins, GitHub Actions, GitLab CI and Azure DevOps. Around them sit Kubernetes, Jira, ServiceNow, SonarQube and Artifactory.

Releases need manual coordination, compliance reporting is hard, audit preparation takes weeks, and leadership has little visibility into delivery. The bank wants to standardize delivery, improve governance and auditability, and reduce release risk, without forcing teams to leave their current tools.

---

# What we are building

Before we start clicking, let us look at what the finished environment looks like. The diagram below shows it.

![image1](/Images/Prepare/image1.png)

On the left is GitHub. You will have two repositories there, both forked from the CloudBees demo repositories. On the right is CloudBees Unify, where we connect those repositories and build the demo around them.

The first repository, `cloudbees-unify-demo-kit`, becomes a **component** in Unify. A component is a repository and its pipeline. This one builds, tests, scans and packages a small service called `orders-api`. At the end, it registers a versioned artifact, such as `orders-api:1.4.<run>`, so there is something to release.

The second repository, `cloudbees-unify-demo-app`, becomes the **application** in Unify, which we call `customer-portal`. It holds the FinSure release workflow. Unify uses it to move the artifact through two environments, `staging` and `prod`. You will see that we add the component to the application. This is how the release knows which artifact to deploy.

So the code and its pipeline live in the component repository, and the release lives in the application repository. Keep this picture in mind. Every step in the rest of this file builds one part of it.

---

# Demo environment preparation: step-by-step

In this section we prepare everything the demo needs. We create the CloudBees account, fork the two demo repositories, and connect GitHub to CloudBees Unify.

## Step 1. Create a CloudBees account

Everything in this guide runs inside CloudBees Unify, so we start with an account. CloudBees offers a free trial, which is enough for this demo.

1. Open the [CloudBees free trial page](https://www.cloudbees.com/free-trial) and sign up.
2. Confirm your email if CloudBees asks for it.
3. Log in. You land on the **Welcome to Unify** page.

## Step 2. Fork the two demo repositories

CloudBees publishes two public repositories for this demo. We fork both into our own GitHub account, so we can change them and so Unify can connect to them.

1. Open **[cloudbees-unify-demo-kit](https://github.com/cb-demos/cloudbees-unify-demo-kit)** and select **Fork** at the top right.
2. Choose your GitHub account as the owner. Keep the repository name as it is, `cloudbees-unify-demo-kit`.
3. Select **Create fork**.
4. Repeat the same for **[cloudbees-unify-demo-app](https://github.com/cb-demos/cloudbees-unify-demo-app)**. Keep the name `cloudbees-unify-demo-app`.

> [!IMPORTANT]
> Do not rename the forks. The release workflow reads the component name from the repository name. A different name breaks the deploy step later.

## Step 3. Connect CloudBees Unify to your GitHub

Unify can only see your code if you give it permission. We do this with an integration, which uses a GitHub App. Unify reads your repositories and runs the workflows in them. Your code stays in GitHub, and nothing moves.

1. In Unify, select your organization, then go to **Configurations** > **Integrations**.
2. Select **Create integration**, then choose **GitHub App**.
3. Enter a **Name**, for example `github-demo`. A description is optional. Leave everything else on the default values.
4. Select **Install GitHub App**. GitHub opens.
5. Choose your GitHub account.
6. Under **Repository access**, choose **Only select repositories**. Do not choose **All repositories**. This gives CloudBees access to the two demo forks only, and nothing else in your account.
7. Select **Select repositories**, then pick `cloudbees-unify-demo-kit` and `cloudbees-unify-demo-app`. The page shows **Selected 2 repositories**.
8. Review the permissions and select **Install & Authorize**. You return to Unify.

![image2](/Images/Prepare/image2.png)

Expected: **Configurations** > **Integrations** shows your integration with the type **GitHub App** and the status **Completed**.

## Step 4. Point the deployer at your fork

When you forked the repositories, GitHub copied them exactly as they were. Some files inside still point to the original repository, which belongs to the `cb-demos` account, not to your fork. The deployer in the application repository is one of them. It has a line that calls the deploy workflow in the component repository, and that line names `cb-demos` as the owner. If we leave it, the release would use the original copy instead of the one in your fork. We change the account name to yours, so everything stays inside your own fork.

1. On GitHub, open your fork `cloudbees-unify-demo-app`.
2. Open the file `.cloudbees/workflows/deployer.yaml`.
3. Select the pencil icon (**Edit this file**).
4. Find this line (line 28):

```yaml
   uses: cb-demos/cloudbees-unify-demo-kit/.cloudbees/workflows/deploy.yaml@main
```

5. Replace `cb-demos` with your GitHub username:

```yaml
   uses: <your-github-username>/cloudbees-unify-demo-kit/.cloudbees/workflows/deploy.yaml@main
```

6. Select **Commit changes**, and commit directly to the `main` branch.

![image3](/Images/Prepare/image3.png)

> [!IMPORTANT]
> Change only the account name at the start of the line. Do not change `cloudbees-unify-demo-kit` or anything else in the file. The release reads those names later.

## Step 5. Create the component

A component is one repository and its pipeline. Here, the component is `cloudbees-unify-demo-kit`. It holds the CI workflow that builds, tests and scans the Orders API. Creating the component tells Unify to start tracking this repository.

1. In Unify, select your organization, then go to **Components**.
2. Select **Create component**. A three-step wizard opens.
3. In step **1/3 Select repositories**, make sure the organization dropdown shows your GitHub account.
4. Tick `cloudbees-unify-demo-kit` only. Do not tick `cloudbees-unify-demo-app`.
5. Click **Create Components**, then on the next page, click **Finish & Close**.

![image4](/Images/Prepare/image4.png)

> [!IMPORTANT]
> Tick only the kit repository. The app repository becomes the application in Step 7, not a component.

Expected: `cloudbees-unify-demo-kit` appears in the **Components** list.

## Step 6. Create the environments

The release workflow deploys to two environments, `staging` and `prod`. In this demo, nothing is actually deployed. The deploy step is simulated and only prints messages, so no cluster or server sits behind these environments.

We still create them. The release workflow refers to them by name, and we do not want to risk a failure if Unify checks that they exist. They are empty labels, but they keep the demo safe and let Unify show where each version has reached.

1. In Unify, select your organization, then go to **Configurations** > **Environments**.
2. Select **Create environment**.
3. Enter the name `staging`. Leave the **Approvers** field empty.
4. Select **Create**.
5. Repeat the steps to create a second environment named `prod`. Leave **Approvers** empty here as well.

![image5](/Images/Prepare/image5.png)

> [!IMPORTANT]
> Use the names `staging` and `prod`, in lowercase. The release workflow looks for these exact names.

Expected: the **Environments** list shows `staging` and `prod`.

## Step 7. Create the application

The application is the product that the release is for. It brings together the app repository, which holds the release workflow, the component from Step 5, and the two environments from Step 6. The release is created and run from the application.

1. In Unify, select your organization, then go to **Applications**.
2. Select **Create application**.
3. Enter a **Name**, for example `customer-portal`.
4. Click on **Add Environment** and select  the environments `staging` and `prod`.
5. Click on **Add Repository** and select the repository `cloudbees-unify-demo-app`. This is the repository that holds the release workflow.
6. Click on **Add Component** and select the component `cloudbees-unify-demo-kit`.
7. Select **Create**.

![image6](/Images/Prepare/image6.png)

> [!IMPORTANT]
> The application must use the app repository, `cloudbees-unify-demo-app`, and not the component repository. An application and its components cannot share the same repository.

Expected: the list shows `finsure-bank-regulated-release` and `deployer`.

---

# What you have now

Your trial now has everything the demo needs:

- Two forks, `cloudbees-unify-demo-kit` and `cloudbees-unify-demo-app`, connected to Unify through one GitHub App integration.
- A component, `cloudbees-unify-demo-kit`, which holds the CI pipeline.
- Two environments, `staging` and `prod`.
- An application, `customer-portal`, which holds the release workflow.

Nothing has been run yet. The next file, [README.md](./README.md), starts with a short check run and then walks through the demo step by step.

---