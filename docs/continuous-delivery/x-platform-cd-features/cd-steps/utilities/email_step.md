---
title: Email step
description: Send emails using pipelines
sidebar_position: 5
---

This topic describes the settings for the Email step available in Continuous Delivery (CD) and custom stages.

The Email step lets you easily send emails to users and teams during a pipeline execution.

![picture 1](./static/email-step.png)

The Email step has the following features:

- Send emails during pipeline executions.
- You can use the Harness SMTP Server included with your Harness account.
- Use your own SMTP server by adding it to Harness. For more information, go to [add SMTP configuration](/docs/platform/notifications/add-smtp-configuration).
- You can use this step as a [step template](/docs/platform/templates/run-step-template-quickstart) or as part of a [stage template](/docs/platform/templates/add-a-stage-template).
- You can manage this step's configuration via [Harness Git Experience](/docs/platform/git-experience/git-experience-overview).
- You can send emails to Harness users and users outside of Harness using the SMTP server in your Harness
- Use input variables in the email step to customize the subject, body, and recipient list dynamically based on pipeline variables and context.

## Visual summary

<DocVideo src="https://youtu.be/1oa-1xifsmE" />

## YAML example

```YAML
           steps:
              - step:
                  type: Email
                  name: Update Status
                  identifier: Update_Status
                  spec:
                    to: rohan.gupta@harness.io
                    cc: srinivas@harness.io
                    subject: Deployment Status
                    body: "Pipeline: <+pipeline.name> is complete. Harness deployed service <+service.name> into environment <+env.name>"
                  timeout: 10m
```

## To

The email address(es) where you want this Harness pipeline to send an email.

This setting can use be a comma-separated string of addresses. For example, `john.doe@harness.io, bill.smith@harness.io`.

You can set **To** as a runtime input.

You can pass in the email as a Harness expression, such as `<+pipeline.triggeredBy>`.

For more information on runtime inputs and expressions, go to [fixed values, runtime inputs, and expressions](/docs/platform/variables-and-expressions/runtime-inputs).

## CC

You can add email addresses to the **CC** section to carbon copy addresses on the email that will be sent with the pipeline execution.

## Subject

You can provide a subject for the email.

This subject can be a fixed string (for example, `Prod Deployment Notification`), a string with expressions (for example, `<+env.name> Deployment Notification`), or a runtime input.

For more information on runtime inputs and expressions, go to [fixed values, runtime inputs, and expressions](/docs/platform/variables-and-expressions/runtime-inputs).

## Body

The **Body** is a string field. You can enter in text and Harness expressions. Harness will resolve the expressions before sending the email.

- You can use HTML formatting in **Body**, such as `<br>` tags, for line breaks in the email body.
- If the `CDS_EMAIL_USE_DEFAULT_FORMATTING` feature flag is enabled, new lines will not be auto-detected. Instead, you must explicitly define new lines using `<br>` tags or similar HTML formatting.

For more information on runtime inputs and expressions, go to [fixed values, runtime inputs, and expressions](/docs/platform/variables-and-expressions/runtime-inputs).

<details>
<summary>Example of using `<br>` tag in the email body.</summary>

Below is an illustration of how you can insert `<br>` tags within the **Email Step** body:

![](./static/email-step-example.png)

**Pipeline YAML Example**:

```yaml
pipeline:
  name: Email-test
  identifier: emailtest
  projectIdentifier: PROJECT_ID
  orgIdentifier: default
  tags: {}
  stages:
    - stage:
        name: s1
        identifier: s1
        description: ""
        type: Custom
        spec:
          execution:
            steps:
              - step:
                  type: Email
                  name: Email_1
                  identifier: Email_1
                  spec:
                    to: RECIPIENT_EMAIL
                    cc: ""
                    subject: Pipeline status
                    body: |-
                      These are the pipeline details <br> <br>
                      Pipeline name: <+pipeline.name> <br>
                      Pipeline status: <+pipeline.status>. <br>
                      Pipeline step identifier: <+step.identifier>
                    inputVariables: []
                  timeout: 10m
        tags: {}

```


</details>

## Using Input Variables

You can use input variables in the Email Step to customize the subject, body, and recipient list with dynamic values from your pipeline.

- **Subject**: Personalize the subject line using placeholders like `${pipeline.buildNumber}` or `${deployment.status}`.
- **Body**: Insert dynamic content in the email body using pipeline variables.
- **Recipients**: Define the recipient list dynamically with pipeline variables, such as sending emails to team members based on environment or role.

You can use both predefined and custom pipeline variables in your emails. The Email Step also supports condition-based customization, allowing you to modify the email content based on pipeline states like success, failure, or approval.

## Sending emails to non-Harness users

By default, the Email step can only send emails to Harness users.

To send emails to non-Harness users, you must configure your own SMTP server and enable the **Enable Emails to be sent to non-Harness Users** default setting.

:::note Notes

- The Harness internal SMTP server included in your account is not used to email non-Harness users.
- Only users belonging to a user group with the **Default Setting** permission set to **Edit** can configure the **Enable Emails to be sent to non-Harness Users** default setting.

:::

To send emails to non-Harness users, do the following:

1. Add your own SMTP server. For details, go to [Add SMTP configuration](/docs/platform/notifications/add-smtp-configuration/).
2. In **Default Settings** (at the account, organization, or project level), select **Continuous Deployment**, and then set **Enable Emails to be sent to non-Harness Users** to **true**.

<DocImage path={require('./static/de6a52a680b74f1dd5535a5e2fed34ef8ed9be4f2af244a29636a0c497cda016.png')} width="60%" height="60%" title="Click to view full size image" />

Enable **Allow Overrides** to allow a project to override the setting of its org, or an org to override its account setting.

## Advanced settings

In **Advanced**, you can use the following options:

- [Delegate Selector](/docs/platform/delegates/manage-delegates/select-delegates-with-selectors)
- [Conditional Execution](/docs/platform/pipelines/step-skip-condition-settings)
- [Failure Strategy](/docs/platform/pipelines/failure-handling/define-a-failure-strategy-on-stages-and-steps)
- [Looping Strategy](/docs/platform/pipelines/looping-strategies/looping-strategies-matrix-repeat-and-parallelism)
- [Policy Enforcement](/docs/platform/governance/policy-as-code/harness-governance-overview)

## Options

You can send emails using your own SMTP Server. For more information, go to [add SMTP configuration](/docs/platform/notifications/add-smtp-configuration).

## Email delivery failures

Currently, Harness is unable to check whether the emails sent using the Email step are delivered successfully.

If you are encountering issues with email delivery, please open a Harness support ticket.

If you are using a custom email provider (as described in [Add SMTP configuration](/docs/platform/notifications/add-smtp-configuration/)) Harness will not have access to your emails. Please check your email provider and server log to determine the cause of the error.
