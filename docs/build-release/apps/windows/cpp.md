---
title: Build your C++ app
description: Build your C++ app in Team Foundation Server and Visual Team Services
ms.prod: vs-devops-alm
ms.technology: vs-devops-build
ms.assetid: 49886DF3-3689-48B3-8F1C-CA99DAFD1E49
ms.manager: douge
ms.author: alewis
ms.date: 12/15/2016
ms.topic: get-started-article
---

# Build your C++ app for Windows

**VSTS | TFS 2017 Update 2**

Visual Studio Team Services (VSTS) and Team Foundation Server (TFS) provide a highly customizable continuous integration (CI) process to automatically build your C++ application whenever your team pushes or checks in code. In this quickstart you learn how to define your CI process for a C++ application developed using Visual Studio IDE.

## Prerequisites

[!INCLUDE [include](../../_shared/ci-cd-prerequisites-vsts.md)]

* While the simplest way to try this quickstart is to use a VSTS account, you can also use a TFS server instead of a VSTS account. Make sure that you have [configured a build agent](../../actions/agents/v2-windows.md) for your team project, and that you have a version of Visual Studio matching your development machine installed on the agent machine.

## Get sample app code

[!INCLUDE [include](../_shared/get-sample-code-intro.md)]

```
https://github.com/adventworks/cpp-sample
```

# [VSTS or TFS repo](#tab/vsts)

[!INCLUDE [include](../_shared/get-sample-code-vsts-tfs-2017-update-2.md)]

# [GitHub repo](#tab/github)

[!INCLUDE [include](../_shared/get-sample-code-github.md)]

---

## Set up continuous integration

[!INCLUDE [include](../../_shared/ci-quickstart-intro.md)]

[//]: # (TODO: Restore use of includes when we get support for using them in a list.)

1. Create a new build definition.

 # [VSTS or TFS repo](#tab/vsts)

 Navigate to the **Files** tab of the **Code** hub, and then click **Set up build**.

 ![Screenshot showing button to set up build for a repository](../_shared/_img/set-up-first-build-from-code-hub.png)

 You are taken to the **Build & Release** hub and asked to **Select a template** for the new build definition.

 # [GitHub repo](#tab/github)

 Navigate to the **Builds** tab of the **Build and Release** hub in VSTS or TFS, and then click **+ New**. You are asked to **Select a template** for the new build definition.

 ---

1. In the right panel, select **.NET Desktop**, and then click **Apply**. This template is useful in building most of the Visual Studio solutions including those that contain classic C++ projects.

 You now see all the tasks that were automatically added to the build definition by the template. These are the steps that will automatically run every time you check in code.

1. For the **Default agent queue**:

 * **VSTS:** Select _Hosted VS2017_. This is how you can use our pool of agents that have the software you need to build your app.

 * **TFS:** Select a queue that includes a [Windows build agent](../../actions/agents/v2-windows.md).

1. Click **Get sources** and then:

 # [VSTS or TFS repo](#tab/vsts)

 Observe that the new build definition is automatically linked to your repository.

 # [GitHub repo](#tab/github)

 Select your version control repository. You'll need to authorize access to your repo.

 [//]: # (TODO:> [!TIP])
 [//]: # (TODO:> To learn more about GitHub CI builds, see [Define CI build process for your Git repo](#)

 ---

1. Click the **Copy Files** task. Specify the following arguments:

 * **Contents:** `**\$(BuildConfiguration)\**\?(*.exe|*.dll|*.pdb)`

1. Click the **Variables** tab and modify these variables:

 * `BuildConfiguration` = `debug, release`

 * `BuildPlatform` = `x86, x64`

1. Click the **Triggers** tab and enable the **Continuous Integration** trigger. This will ensure that the build process is automatically triggered every time you commit a change to your repository.

1. Click the **Options** tab and then:

 * Select **Multi-configuration**.

 * Specify **Multipliers:** `BuildConfiguration, BuildPlatform`

1. Select **Parallel** if you have multiple build agents and want to build your configuration/platform pairings in parallel.

1. Click **Save and queue** to kick off your first build. On the **Queue build** dialog box, click **Queue**.

1. A new build is started. You'll see a link to the new build on the top of the page. Click the link to watch the new build as it happens.

## View the build summary

[!INCLUDE [include](../_shared/view-build-summary.md)]

## Next steps

[!INCLUDE [include](../_shared/ci-web-app-next-steps.md)]