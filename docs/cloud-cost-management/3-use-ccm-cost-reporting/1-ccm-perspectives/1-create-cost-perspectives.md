---
title: Overview
description: Perspectives allow you to group your resources in ways that are more meaningful to your business needs.
sidebar_position: 1
helpdocs_topic_id: dvspc6ub0v
helpdocs_category_id: e7k0qds7tw
helpdocs_is_private: false
helpdocs_is_published: true
---

import Tabs from '@theme/Tabs';

import TabItem from '@theme/TabItem';


:::tip Latest Features Released in 1.50.2
<Tabs>
  <TabItem value="Label V2" label="Label V2">We’re moving from the older `Label` to `Label V2`. This will improve the load time of the Perspective or Cost Category which are powered by `Label V2`. `Label V2` can be used in place of `Label` in filter in perspectives, as a GROUP BY operand in perspectives graph and in specifying rules when creating a Perspective and Cost Categories. The main goal of `Label V2` is to give you full visibility into your original cloud tag keys, exactly as they appear in your AWS, Azure, GCP or Cluster environments.
  For Perspectives and Cost Categories using `Label`, **[migration to `Label V2` is REQUIRED for AWS compulsorily](/docs/cloud-cost-management/use-ccm-cost-reporting/ccm-perspectives/create-cost-perspectives#important-migration-from-label-to-labelv2)**. For new Perspectives and Cost Categories, **use `Label V2` and not `Label`**.</TabItem>

</Tabs>
:::


You can add business context to your Harness Cloud Cost Management (CCM) data using perspectives. Perspectives allow you to group your resources in ways that are more meaningful to your business needs.

### Before You Begin

* [Set Up Cloud Cost Management for your cloud service provider](https://developer.harness.io/docs/category/onboarding-guide-for-ccm)
* [Use Cost Categories](../2-ccm-cost-categories/1-ccm-cost-categories.md)

## Cloud Costs Perspective Concepts

This section describes Perspective concepts.

### Perspectives

Perspectives allow you to group your resources in ways that are more meaningful to your business needs.

For example, you can group and filter by Account, Environment, Service, Region, Product, Label, Namespace, Workload, etc., and create a Perspective for your business, finance, and engineering teams.

Here are some examples where you could use Perspectives:

* Build your own visual interface using flexible rules and filters. With Perspectives, business units can create views that align with their business needs based on groups of resources determined by different rules and filters.
* Create Perspectives broken down by project, team, department, or business unit to gain granular visibility into all your cloud environments. Perspectives provide a single-pane view of different products, for example, clusters, applications, AWS, GCP, and Azure.
* Schedule and share the reports with the key stakeholders for maximum business impact.
* Estimate costs consumed by specific teams, groups, departments, BUs, LOBs, cost centers, etc.

### Rule-based Engine

Perspectives use a rule-based engine to organize and display your cloud costs. Each Perspective has a set of rules and each rule can have multiple conditions. The following operators are supported for each condition:

* **IN**: The exact match operation is used to filter for the exact value specified.
* **NOT IN**: The exact match operation is used to filter for all values except the one specified.
* **NULL**: Null means the selected filter has no value. If you select NULL for your filter, then the cost of the selected filter isn't included in the Perspective.  
For example, in **Rules for Perspective**, if you select `Label: kubernetes.io/name` as `NULL`, then your Perspective won't include the cost for the selected label (`kubernetes.io/name`). It will include the cost of all the other resources.

  ![](./static/create-cost-perspectives-16.png)
* **NOT NULL**: Not null means that the selected filter has a value. If you choose NOT NULL for your filter, then only the cost of the selected filter is included in the perspective.  
  
For example, in **Rules for Perspective**, if you select `Label: kubernetes.io/name` as `NOT_NULL`, then your Perspective will list the cost of the selected label only (`kubernetes.io/name`). It won't include the cost of any other resource.

  ![](./static/create-cost-perspectives-17.png)
* **LIKE**: The Like operator uses `REGEXP_CONTAINS` provided by the BigQuery at the backend. This function is used to check if a given value partially matches a specified regular expression. 

  - Retrieves result even if the value partially matches the regular expression. 
  - To search for a full match (the entire value matches the regular expression), use `^` at the beginning of the regular expression and `$` at the end of the regular expression. These symbols signify the beginning and end of the text, respectively.

  For example, `AWS Account ID LIKE ‘abc’`. This means REGEXP_CONTAINS(aws_account_id, r'abc). User input is 'abc' in this example.

### Filters

You can create a Perspective for your resources using rules and filters. The filters are used to group the resources. The following are the supported filters:

* **Cost Categories**: You can create a perspective by filtering based on the cost categories you have created. To create cost categories, see [Use Cost Categories](../2-ccm-cost-categories/1-ccm-cost-categories.md).
* **AWS**: CCM allows you to view your AWS costs at a glance, understand what is costing the most, and analyze cost trends. CE displays the data for all your Amazon Web Services (ECS, EC2, and so on). For more information, see [Analyze Cost for AWS Using Perspectives](../3-root-cost-analysis/analyze-cost-for-aws.md).
* **GCP**: CCM allows you to view your Google Cloud Platform (GCP) costs, understand what is costing the most, and analyze cost trends. CE displays data for all your GCP products (such as Compute Engine, Cloud Storage, BigQuery, and so on), projects, SKUs, and location. For more information, see [Analyze Cost for GCP ​Using Perspectives](../3-root-cost-analysis/analyze-cost-for-gcp-using-perspectives.md).
* **Azure**: CCM allows you to view your Azure costs at a glance, understand what is costing the most, and analyze cost trends. CE displays the data for all your Azure services (Storage accounts, Virtual machines, Containers, and so on). For more information, see [Analyze Cost for Azure Using Perspectives](../3-root-cost-analysis/analyze-cost-for-azure.md).
* **Cluster**: Total cost, Cost trend, Idle cost, and Unallocated cost for each cluster.
* **Region**: Each AWS, GCP, or Azure region you're currently running services in.
* **Product**: Each of your active products with its cloud costs.
* **Label** and **Label V2**: Costs organized by the cloud and K8s labels that you are using to organize your Cloud instances.


### Preview

As you add your resources in the **Perspective Builder**, a **Preview** of your Perspective is displayed.

![](./static/create-cost-perspectives-18.png)

The following are the key advantages of preview:

* Provides a quick visual representation of your resources in the Perspective without saving them.
* Allows you to group resources in the preview mode itself. You can group by **Common**, **Custom** (if Custom Fields are available), **Cluster**, **AWS**, **GCP**, and **Azure**.
* Helps you to review your changes faster.


:::note
**Grouped by** Product in Preview.
:::

## Create a Perspective

You can create a Perspective by grouping your resources the way you wish. For example, if you want to create a perspective for your CFO, first add default or custom filters and then further group by Service, Account, Workload, Namespace, etc. that you would want to include in your Perspective.


:::note
You can create up to 10,000 Perspectives.
:::

Perform the following steps to create a Perspective:

1. In **Cloud Costs**, click **Perspectives**.
2. In **Perspectives**, click **New Perspective**.
3. In **Perspective Builder**, enter a name for your perspective. By default, a unique name is entered in the field. You can edit the pre-populated name of the perspective.

:::note
   Perspective names mustn't include any special characters.
:::

4. In **Perspective Builder**, in **Rules for Perspective**, click **+** **Add rule**.
5. Select one of the following:
   * Common
   * Cost Categories
   * Cluster
   * AWS
   * GCP
   * Azure
   * Region
   * Product
      
   As you add your resources in the Perspective Builder, a preview of your Perspective is displayed.
6. Select the operator. See the **Rule-based Engine** section for more information.
7. Select the value for your filter. You can select multiple values. You can also filter and customize your result using the search option.
   
     ![](./static/create-cost-perspectives-22.png)
8. After adding all the filters, click **Next** to add a report-sharing schedule and budget.


:::note
- When you create a new Perspective, data across all cloud service providers and clusters are displayed. If you want to restrict the data to a particular cloud service provider, you must apply a filter in the Cloud Provider field.

:::


:::note
If you've added labels and cluster rules in the perspective builder section, it's considered a cluster perspective, hence all cluster labels are considered. In this case, data from cloud service providers such as GCP, Azure, and AWS are not considered. However, if you have applied a label that belongs to the cloud provider data, and you want to view the cluster data as well, then you have to add a Cloud Provider filter.
:::

## View Perspectives

You can view any perspective by clicking on it. The perspective overview page provides a comprehensive dashboard with the following information:

### Key Metrics
- **[Total Cost](https://developer.harness.io/docs/cloud-cost-management/get-started/key-concepts#total-cost)**: Current accumulated cost for the selected time period
- **[Forecasted Cost](https://developer.harness.io/docs/cloud-cost-management/get-started/key-concepts#forecasted-cost)**: Projected spending based on current usage patterns
- **[Cost Recommendations](https://developer.harness.io/docs/cloud-cost-management/use-ccm-cost-optimization/ccm-recommendations/home-recommendations)**: Suggestions for optimizing your cloud spending
- **Budget Status**: Visual indicators of budget utilization (if budgets are configured)

### Cost Visualization
The interactive cost graph allows you to organize and segment your cost data using the **Group By** function. This grouping functionality determines how your costs are categorized and displayed in the visualization. You can group your data by any of the following dimensions:

- **[Cost Categories](https://developer.harness.io/docs/cloud-cost-management/use-ccm-cost-reporting/ccm-cost-categories/ccm-cost-categories)**: Group costs by your defined cost categories
- **Cloud Provider**: View costs by cloud service provider (AWS, Azure, GCP) with provider-specific options
- **Region**: Break down costs by geographical regions
- **Product**: Analyze costs by specific cloud products and services
- **Label**: Group by GCP, Azure, Cluster tags and (Harness-normalized) AWS tags 
- **Label V2**: Group by same labels exactly as they appear in your AWS, Azure, or GCP environments
- **None**: View aggregated costs without grouping

:::info
### Understanding the Difference: Label vs. Label V2

- **`Label` (Legacy)**: Normalizes AWS tags. GCP, Azure and Clusters tags are not normalized.
- **`Label V2` (New)**: Preserves the original structure from AWS similar to how GCP, Azure and Cluster tags are stored.

**Key Benefits of `Label V2`:**
- **Original tags**: Displays your original cloud tag keys exactly as they appear in AWS, Azure, or GCP
- **Improved Performance**: Enhanced data processing and query performance

`Label` is a label that you assign to your AWS resources. See how [AWS labels are created](https://developer.harness.io/docs/cloud-cost-management/use-ccm-cost-reporting/root-cost-analysis/analyze-cost-for-aws/). 

After `Label V2`, AWS labels are stored as-is without any normalization.

**Harness CCM is transitioning from the traditional `Label` system to the enhanced `Label V2` system. Support for the legacy `Label` system will be discontinued in the coming months.**

Please [see the steps here](/docs/cloud-cost-management/use-ccm-cost-reporting/ccm-perspectives/create-cost-perspectives#important-migration-from-label-to-labelv2) to migrate labels from `Label` to `Label V2`.
:::

### General Preferences

You can customize your perspective view with the following display preferences:

- **Show Others**: The graph displayed in a Perspective shows the top 12 costs only. Enable this setting to include the remaining costs as an **Others** item in the graph.

- **Show Anomalies**: Highlights unusual spending patterns or sudden cost changes in your visualization. This feature helps you quickly identify potential issues or unexpected charges that may require investigation.

- **Show Negative Cost**: Displays instances where discounts exceed the actual billing amount, resulting in negative cost values in your reports.

## Budgets, Reports, and Alerts
For details on adding Budgets, Reports, and Alerts go to:

* [Create a Budget for Your Perspective](../../3-use-ccm-cost-reporting/1-ccm-perspectives/3-create-a-budget-perspective.md)
* [Share Your Cost Perspective Report](../../3-use-ccm-cost-reporting/1-ccm-perspectives/4-share-cost-perspective-report.md)

## Perspective Preferences

Go to [Perspective Preferences](perspective-preferences.md) to learn about these settings.

### Review: No Account/Project/etc

It's important to understand the difference between the **Others** and **No Account/Project/etc** categories.

When a Perspective includes multiple data sources (for example, AWS, GCP, and Cluster) and you select one data source in a Perspective **Group By**, such as **AWS: Account**, the costs for the AWS data source are displayed individually. The costs for the other data sources (GCP, Cluster) are grouped under **No Account**.

In other words, a row with **No** followed by the selected `Group by` is displayed for costs that don’t have any relation with the selected `Group by`. For example, **No SKUs** is displayed for costs (AWS, clusters, etc.) that don’t have any GCP SKUs associated with it.

Another example is if the **Group By** is **Project**. For example, if you selected GCP: Project, then the **No Project** item in the graph represents the AWS and Cluster project costs.

Essentially, `No GroupBy` represents the null values for that `Group By` grouping. To work with these null values either in perspective filters or rules, you need to use the "IS NULL" function on that field. Since Perspectives don't explicitly provide a `No GroupBy` value in the filters, the "IS NULL" field serves as the way to handle these `No GroupBy` items. 

  For example, if your perspective includes both GCP and AWS cloud providers, and you intend to categorize costs by AWS accounts using the `GroupBy` function, any costs associated with GCP will be classified under the label `No Account`. In case you wish to view only the GCP costs, you can apply a filter with the condition `AWS > Account` IS NULL.


## Edit a Perspective

To edit a Perspective, do the following:

1. Select the Perspective that you want to edit, and click **Edit**.
   
2. The **Perspective Builder** appears. Follow the steps in **Create Cost Perspectives** to edit the Perspective.

## Clone a Perspective

When you clone a Perspective, all its settings are cloned. You simply add a new name. After it is cloned, you can edit it just as you would edit any perspective. To clone a Perspective, do the following:

Select the more actions icon on the Perspective tile that you want to clone, and select **Clone**.
   
  ![](./static/clone-delete-perspective.png)
    
  The cloned Perspective appears. 

## Delete a Perspective

To delete a Perspective, do the following:

Select the more actions icon on the Perspective tile that you want to delete, and select **Delete**.  
  
The Perspective is deleted and no longer appears in the Perspective dashboard.

## Organize Perspectives using Folders

You can organize Perspectives by adding them to folders.

Click **New folder**, name the folder, and then select the Perspectives you want to add.

![](./static/create-cost-perspectives-28.png)

You can also add a Perspective to a folder when you create it or move it to a folder when you edit it.

![](./static/create-cost-perspectives-29.png)

You can also move a Perspective to a folder from its more options (⋮) setting.

![](./static/create-cost-perspectives-30.png)

:::important note
The maximum number of folders that can be created is limited to 500.
:::


## Important: Migration from `Label` to `Label V2`

Harness CCM is transitioning from the traditional Label system to the enhanced Label V2 system. **Support for the legacy Label system will be discontinued in the coming months**.

### Required Action

- **AWS Labels**: Immediate migration required. You must update all AWS `Label` references to use `Label V2`.
- **GCP, Azure, and Cluster Labels**: After AWS label migration is complete, Harness CCM will automatically handle these migrations.

### How to Migrate

#### **Via UI:**

1. **Identify affected components**:
   - Review all Perspectives that use AWS Label-based grouping or filtering

2. **Update each component**:
   - Edit each Perspective
   - Locate all instances where you've defined rules, filters, or grouping using AWS Labels
   - Change the selection from "Label" to "Label V2"
   - Save your changes

3. **Verify your updates**:
   - After updating the Perspective, confirm that your cost data appears correctly
   - Ensure all previously configured label-based filters work as expected

Kindly follow the steps below: 
  <iframe 
     src="https://app.tango.us/app/embed/44d091fd-3177-44a1-b575-1a5a8febf36d" 
     title="Migrating Label to Label V2" 
     style={{minHeight:'480px'}}
     width="100%" 
     height="100%" 
     referrerpolicy="strict-origin-when-cross-origin" 
     frameborder="0" 
     webkitallowfullscreen="webkitallowfullscreen" 
     mozallowfullscreen="mozallowfullscreen" 
     allowfullscreen="allowfullscreen"></iframe>    

#### **Via API:**

Earlier every request had the Label field as:


```json
                {
                    field": {
                        "fieldId": "labels.value",
                        "fieldName": "key1",
                        "identifier": "LABEL",
                        "identifierName": "Label"
                    },
                    "operator": "IN",
                    "values": [
                        "value1"
                    ]
                } 
```

Now the request has the Label V2 field as:

```json
                {
                    field": {
                        "fieldId": "labels.value",
                        "fieldName": "key1",
                        "identifier": "LABEL_V2",
                        "identifierName": "Label v2"
                    },
                    "operator": "IN",
                    "values": [
                        "value1"
                    ]
                }
```
Similarly, for `labels.key`:

Earlier:

```json
 "idFilter": {
                    "field": {
                        "fieldId": "labels.key",
                        "fieldName": "",
                        "identifier": "LABEL",
                        "identifierName": "Label V2"
                    },
                    "operator": "IN",
                    "values": []
                }
```

Now:

```json
 "idFilter": {
                    "field": {
                        "fieldId": "labels.key",
                        "fieldName": "",
                        "identifier": "LABEL_V2",
                        "identifierName": "Label V2"
                    },
                    "operator": "IN",
                    "values": []
                }
```

In short, wherever you see `LABEL` in "identifier", replace it with `LABEL_V2` alongwith "identifierName" .

Please refer the following API docs for details:
- [Create a Perspective](https://apidocs.harness.io/tag/Cloud-Cost-Perspectives#operation/createPerspective)
- [Update a Perspective](https://apidocs.harness.io/tag/Cloud-Cost-Perspectives#operation/updatePerspective)
