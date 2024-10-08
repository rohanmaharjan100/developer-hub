---
title: Sync GitOps applications
description: This topic describes how to sync GitOps applications.
sidebar_position: 30
redirect_from:
  - /docs/continuous-delivery/gitops/sync-gitops-applications
---

Sync is a process that ensures that the live state of a system matches its desired state by applying a declarative description. This process involves synchronizing the desired Git state with the live cluster state. 

To sync applications from the **Applications** page: 

1. In your GitOps project, go to **Deployments** > **GitOps** > **Applications**, and then select your application.
   
   ![](./static/sync-applications-3.png)

2. To sync the selected application: 
   * Select the more options icon, and then select **Sync**.
   
     ![](./static/sync-applications-1.png)
   * Select the application, and then select **SYNC**. 

     ![](./static/sync-applications-2.png)
3. Configure the sync options, and then select **Synchronize**.

   When synchronizing the application, you have the option to apply a specific revision. By default, target revision of the application is selected.
   
   The Branch and Tag options display a list of available branches and tags, allowing you to make a selection. Additionally, the Ref option enables synchronization of branches, tags, and commit hashes.
   
   ![](./static/sync-applications-4.png)

To sync applications using the **GitOpsSync** step: 

1. Select a pipeline and go to the **Execution** tab of a deploy stage.
   
   :::info

   Make sure that the service, environment, and cluster selected in the pipeline matches the service, environment, and cluster in the application.

   ::: 
   
2. Select **Add Step**, and then select the **GitOpsSync** step.
3. Select the GitOpsSync step to configure step parameters.
4. Optionally, click on the **Wait until healthy** checkbox, if you would like the step to run until the application reaches it's **Healthy** state.
5. In **Advanced Configuration**, select the application you want to sync and configure the sync options.
      You can either can either choose an application or applications manually, or you can match up to 1000 applications using a regex filter.

    ![](./static/gitopssync-step-regex.png)    
 
6. Select **Apply Changes**.

Here is how the resources would look in Harness after the sync process is complete.

![](./static/harness-git-ops-application-set-tutorial-40.png)

## Terminate sync

To terminate an in-progress sync, go to the application for the syncing app and locate the **Terminate Sync** button in the top right corner of the UI. Replace the **Sync** button when a sync is in progress.

![](./static/terminate_sync.png)