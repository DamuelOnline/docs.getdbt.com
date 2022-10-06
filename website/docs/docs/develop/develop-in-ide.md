---
title: "Develop in the Cloud IDE"
id: develop-in-ide
description: "Develop,test, run, and build in the Cloud IDE."
sidebar_label: "Develop in the Cloud IDE"
---

:::📌 The Cloud IDE refresh is now available for General Availability! Join our dedicated [[Cloud IDE slack channel](https://getdbt.slack.com/archives/C03SAHKKG2Z)] for any feedback! 
:::

The Cloud IDE is a single interface for building, testing, running, and version-controlling dbt projects from your browser. With the IDE, you can compile dbt code into SQL and run it against your database directly, and also write, test and compile [Python models](url). The IDE leverages the open-source [dbt-rpc](/docs.getdbt.com/reference/commands/rpc) plugin to recompile only the changes made in your project.

## **Prerequisites**

To develop in the Cloud IDE, make sure you have the following:

- Your dbt project must be compatible with dbt v0.15.0. The dbt IDE is powered by the [dbt-rpc](/docs.getdbt.com/reference/commands/rpc) which was overhauled in dbt v0.15.0
- You must have a dbt Cloud account and [Developer seat license](/docs.getdbt.com/docs/dbt-cloud/access-control/cloud-seats-and-users)
- You must have a git repository set up. Git provider must have `write` access enabled. See [Connecting your GitHub Account](/docs.getdbt.com/docs/dbt-cloud/cloud-configuring-dbt-cloud/cloud-installing-the-github-application) and [Importing a project by git URL](/docs.getdbt.com/docs/dbt-cloud/cloud-configuring-dbt-cloud/cloud-import-a-project-by-git-url) for detailed setup instructions
- Your dbt project must be connected to a [data platform](/docs.getdbt.com/docs/dbt-cloud/cloud-configuring-dbt-cloud/connecting-your-database)
- You must have a [**development** environment](/docs/develop/develop-in-ide#set-up-the-cloud-ide) and **development** credentials set up.
- The environment must be on dbt version 1.0 or higher

**Start up process in the IDE**

There are three start-up states when using or launching the Cloud IDE:

- *Creation start* - This is the state in which you start the IDE for the first time. You can also view this as a *cold start* (see below), and you can expect this state to take longer because the git repository is being cloned.
- *Cold start -* This is the process of starting a new develop session, which will be available for you for three hours. The environment automatically turns off three hours after the last activity with the rpc server. This includes compile, preview, or any dbt invocation, however, it *does not* include editing and saving a file.
- *Hot start* -  This is the state of resuming an existing or active develop session within 3 hours of the last activity.

**Work retention in the IDE**

The Cloud IDE needs explicit action to save your changes and there are three ways your work is stored:

- **Unsaved, local code** -- Any code you write is automatically available from your browser’s storage. You can see your changes but will lose them if you switch branches or browsers (another device or browser).
- **Saved but uncommitted code** -- When you save a file, the data gets stored in your local storage (EFS storage). If you switch branches but don’t *commit* your saved changes, you will lose your changes.
- **Committed code** -- This is stored in the branch with git provider and you are able to check out other (remote) branches.

## Set up the **Cloud IDE**

:::📌 New to dbt? Check out our [Getting Started guide](https://docs.getdbt.com/guides/getting-started) to build your first dbt project in the Cloud IDE!

:::

To start developing in the Cloud IDE, you need to first set up your **Development environment** and **Development credentials.** If you’re new to dbt, you will automatically add this during the project setup. However, if you have an existing dbt Cloud account, you may need to create a Development Environment and credentials manually to use the Cloud IDE:

1. Create a development environment and choose **Deploy** > **Environments** from the top left. Then, click **Create Environment**.

![Creating a new environment for the Analytics project](https://docs.getdbt.com/img/docs/running-a-dbt-project/using-the-dbt-ide/empty-env-page.png)

Creating a new environment for the Analytics project

1. Enter an environment **Name** that would help you identify it among your other environments (for example, `Nate's Development Environment`). 
2. Choose **Development** as the **Environment Type**. 
3. You can also select which **dbt Version** to use at this time. For compatibility reasons, we recommend that you select the same dbt version that you plan to use in your deployment environment. 
4. Click **Save** to finish creating your **Development environment**.

![Creating a development environment](https://docs.getdbt.com/img/docs/running-a-dbt-project/using-the-dbt-ide/create-dev-env.png)

Creating a development environment

The IDE uses *developer credentials* to connect to your database. These developer credentials should be specific to your user. They should *not* be super user credentials or the same credentials that you use for your production deployment of dbt. 

1. To set up or manage your developer credentials, go to the [**Credentials](https://cloud.getdbt.com/next/settings/profile#credentials)** section. 
2. Select the relevant project in the list. 
3. Click **Edit** on the bottom right of the page
4. Enter your developer credentials and click **Save.** 

You should now be able to access the Cloud IDE by clicking **Develop** and start developing! 

![Configure developer credentials in your Profile.](https://docs.getdbt.com/img/docs/running-a-dbt-project/using-the-dbt-ide/dev-cred-edit-proj.png)

Configure developer credentials in your Profile.

## **Access the Cloud IDE**

To use the Cloud IDE:

1. Log in with your dbt Cloud account  
2. Click **Develop** at the top of the page
3. Use the below image guide to familiarize yourself with the Cloud IDE:
    
    ![Screenshot 2022-09-30 at 11.46.30.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/bd2fbb71-2ed6-4cac-907d-274c457b3cae/Screenshot_2022-09-30_at_11.46.30.png)
    

1. **File Tree -** The file tree allows you to organize your project and manage your files and folders. Click the three-dot menu associated with the file or folder to create, rename, or delete it. Note: This function is unavailable if you’re on the **Main** branch. 
2. **Editor -** This is where you edit your files. You can use the tab for each editor to position it exactly where you need it.
3. **IDE git button -** The git button in the IDE allows you to apply the concept of [version control](/docs/collaboration/version-control-basics) to your project and you can execute git commands directly in the IDE.
4. **Command bar -** You can enter and run commands from the command bar at the bottom of the IDE. Use the [rich model selection syntax](/docs.getdbt.com/reference/node-selection/syntax) to execute [dbt commands](/docs.getdbt.com/reference/dbt-commands) directly within dbt Cloud. You can also view the history, status, and logs of previous runs by clicking **History** on the left of the bar**.**
5. **Status ba**r - This area provides you with useful information about your IDE and project status. You also have additional options like restarting or [recloning your repo](/docs/collaboration/version-control-basics).
6. **Format/Preview/Compile/Build -** This is where you can format/preview/compile or build your dbt project, as well as see the DAG. The new **Format** feature format your file and is powered by [sqlfmt](http://sqlfmt.com/).
7. **Lineage tab -** You can see how models are used as building blocks from left to right to transform your data from raw sources, into cleaned-up modular derived pieces and final outputs on the far right of the DAG. You can access files in the **Lineage** tab by double-clicking on a particular model. Expand the DAG into fullscreen to view the DAG view differently. Note: Our default view is `+model+`, however, you can change it to `2+model+2`.
8. **Generating and viewing documentation -** Generate and view your [documentation](/docs/collaborate/build-and-view-your-docs) for your dbt project in real-time. You can inspect and verify what your project's documentation will look like before you deploy your changes to production. 
    1. Run the `dbt docs generate` command in the command bar to generate the docs for your dbt project as it exists in development in your IDE session. 
    2. Click the documentation menu icon on top of the file tree to see the latest version of your documentation rendered in a new browser window.

### Manage projects

You can *build*, *compile*, *run* *and test* dbt projects directly in the Cloud IDE using the **Build** feature or the command bar. The Cloud IDE will update in real time when you run models, tests, seeds, and operations. If a model or test fails, you can review the logs to find and fix the issue.

You can also use dbt's [rich model selection syntax](//docs.getdbt.com/reference/node-selection/syntax) to [run dbt commands](/docs.getdbt.com/reference/dbt-commands) directly within dbt Cloud.

![Preview, compile, or build your dbt project. Use the lineage tab to see your DAG.](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d3b5d4e4-9906-49e8-b43b-5979f631065e/ezgif.com-gif-maker.gif)

Preview, compile, or build your dbt project. Use the lineage tab to see your DAG.

![Build, run and test your dbt project.](https://docs.getdbt.com/img/docs/dbt-cloud/cloud-ide/build.png)

Build, run and test your dbt project.

**Related docs**

Refer to [Getting Started with dbt Cloud](/docs.getdbt.com/guides/getting-started) to build your first dbt project and perform some key tasks. For more information, see the following articles:

- [What is dbt?](/docs.getdbt.com/docs/introduction#what-else-can-dbt-do)
- [dbt Learn courses](https://courses.getdbt.com/collections)
- [Version control basics](/docs/collaboration/version-control-basics)
- [dbt Commands](/docs.getdbt.com/reference/dbt-commands)
- [Syntax overview](/docs.getdbt.com/reference/node-selection/syntax)

**Related questions**

- Is there a cost to using the Cloud IDE?
    
    Not at all! You can use dbt Cloud when you sign up for the Free [Developer plan](https://www.getdbt.com/pricing/), which comes with one developer seat. If you’d like to access more features or have more developer seats, you can upgrade your account to the Team or Enterprise plan. See dbt [Pricing plans](https://www.getdbt.com/pricing/) for more details.
    
- Can I be a contributor to dbt Cloud?
    
    Anyone can contribute to the dbt project. And whether it's a dbt package, a plugin, dbt-core, or this documentation site, contributing to the open source code that supports the dbt ecosystem is a great way to level yourself up as a developer, and give back to the community. See [Contributing](/docs.getdbt.com/docs/contributing/oss-expectations) for details on what to expect when contributing to the dbt open source software (OSS).
    
- What is the difference between developing on the Cloud IDE and on the CLI?
    
    There are two main ways to develop with dbt: using the web-based IDE in dbt Cloud or using the command-line interface (CLI) in dbt Core.
    
    - **dbt Cloud IDE** - dbt Cloud is a web-based application that allows you to develop dbt projects with the IDE, includes a purpose-built scheduler, and provides an easier way to share your dbt documentation with your team. The IDE is a faster and more reliable way to deploy your dbt models and provides a real-time editing and execution environment for your dbt project.
    - **dbt Core CLI** - The command line interface (CLI) uses [dbt Core](/docs.getdbt.com/docs/introduction), an [open-source](https://github.com/dbt-labs/dbt) software that’s freely available. You can build your dbt project in a code editor, like Jetbrains or VSCode, and run dbt commands from the command line.
- What type of support is provided with dbt Cloud?

The global dbt Support team is available to help dbt Cloud users by email or in-product live chat. Developer and Team accounts offer 24x5 support, while Enterprise customers have priority access and options for custom coverage.

If you have project-related or modeling questions, you can use our dedicated [GitHub Discussions](https://docs.getdbt.com/docs/contributing/long-lived-discussions-guidelines) or [dbt Community Slack](http://getdbt.slack.com/) to get help as well.