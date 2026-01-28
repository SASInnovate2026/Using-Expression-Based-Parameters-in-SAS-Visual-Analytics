# Working with Expression Based Parameters

## Demo Duration

This demo will take 20 minutes to complete.

## Demo Objective

In this demo you create an expression-based parameter, and use the parameter to demonstrate calculating percent of total.

## Open the Report

1. From the Desktop, open SAS Visual Analytics and sign in to SAS Viya.

1. Enter the following to log in:
    - User ID:  ***Designer***
    - Password: ***Student1***

1. Click **Sign In**.

1. Navigate to the **SAS Content/Courses/VISUAL** folder.

1. Double click the **230_151_Working with Expression Based Parameters** report to open it.

1. If necessary, ensure that the report is in **Edit** mode.

1. Examine the report, which was created using the **CUSTOMERS** table.

   ![List table](/images/230_151_001_ListTable.png)

   It contains a list table displaying the number of sales in each country. Notice that there is also a page control that allows the user to select a particular continent and view only those countries.

   ## Add Percent of Total Using a Calculated Item

1. To make this report more useful to the viewer, we are going to add a new column to the list table that displays the percent of overall sales that each country represents. One way to do this is to use a calculated item.

1. In the left pane, click **Data**.

1. Select **New data item** > **Calculated item**.

1. In the **Name** field, enter **% of Total Sales**.

1. In the expression editor, click the **Operators** tab and select the **Division** operator.

1. Select the first term in the division expression.

1. Click the **Functions** button and select the **Sum** function in the **Aggregated (simple)** section.

   ![Sum function](/images/230_151_002_SumFunction.png)

1. Select **ByGroup** for the context and **Number of Sales** for the measure.

1. Select the second term in the division expression.

1. Click the **Functions** button and select the **Sum** function in the **Aggregated (simple)** section.

1. Select **ForAll** for the context and **Number of Sales** for the measure.

1. In the **Format** field, choose  **PERCENT12.2**.

   ![Expression](/images/230_151_003_Expression.png)

1. Click **OK** to create the new data item.

1. Select the list table.

1. In the right pane, click the **Data Roles** tab.

1. Click the **Add** button next to the **Columns** role and select the newly-created **% of Total Sales**.

   ![Add data item](/images/230_151_004_AddDataItem.png)

1. Click **Apply** to add the calculated item to the list table.

1. Now, let's test the report. The **% of Total Sales** column tells the report viewer what percentage of the total sales each individual country represents. What percent of total sales happen in Belgium?

   ![Results](/images/230_151_005_Results.png)

   Answer: 2.62%

1. Use the page control to select **Europe** and examine how the report changes. What percent of sales does the list table say take place in Belgium now?

   ![Results](/images/230_151_006_Results.png)

   Answer: 3.82%. This is because the calculated item **% of Total Sales** is being evaluated based on the data returned by the page control. While Belgium represents 2.62% of global sales, it also represents 3.82% of European sales.

   ## Create an Expression-Based Parameter

1. To allow the percent of total results to remain constant no matter what filters are applied, we can use an expression-based parameter.

1. In the left pane, click **New data item** and select **Parameter**.

1. In the name field, enter **TotalSales**.

1. In the **Type** field, verify that **Numeric** is selected.

1. Next to the **Default value** field, click the **Edit as expression** button.

   This opens an expression editor where you can define the value of the parameter, rather than defining the value using a control object.

1. We need to create a parameter that stores the total number of sales globally. Click the **Functions** button and select **Sum** from the **Aggregated (simple)** group.

   ![Sum function](/images/230_151_007_SumFunction.png)

1. For the **Context** field, select **ForAll**.

1. For the **measure** field, select **Number of Sales**.

   ![New sum](/images/230_151_008_NewSum.png)

1. Click **OK**.

1. Click **OK** to finish defining the parameter value.

   ![New parameter](/images/230_151_009_NewParameter.png)

1. Click **OK** to create the parameter.

1. In the left pane, click the **Data** tab and scroll down to the **Parameter** section.

1. Hover over the **TotalSales** parameter.

   ![Current value](/images/230_151_010_CurrentValue.png)

   Notice that the current value is displayed.

   ## Apply the Parameter

1. Next, we can use the **TotalSales** parameter to calculate the percent of total sales.

1. In the left pane, click **Data**.

1. Select **New data item** > **Calculated item**.

1. In the **Name** field, enter **% of Total Sales (Parameter)**.

1. In the expression editor, click the **Operators** tab and select the **Division** operator.

1. Select the first term in the division expression.

1. Click the **Functions** button and select the **Sum** function in the **Aggregated (simple)** section.

   ![Sum function](/images/230_151_002_SumFunction.png)

1. Select **ByGroup** for the context and **Number of Sales** for the measure.

1. Select the second term in the division expression.

1. Click the **Data** tab and select the **TotalSales** parameter in the **Parameters** group.

1. For the **Format** field, select **PERCENT12.2**.

   ![New calculated item](/images/230_151_011_NewCalculatedItem.png)

1. Click **OK** to finish creating the calculated item.

   ## Update Report

1. Next, we need to add the new calculated item to the list table in the report.

1. Select the list table.

1. In the right pane, click the **Data roles** tab.

1. Click the **Add** button next to the **Columns** role and select the newly-created **% of Total Sales (Parameter)**.

1. Click **Apply** to add the calculated item to the list table.

   ![Data roles](/images/230_151_012_DataRoles.png)

   ## Test the Updated Report

1. Finally, let's test the updated report.

1. Click the page control and select **Clear filter**.

1. In the top left of the report, click the **View report** button to enter viewing mode.

1. Compare the **% of Total Sales** and the **% of Total Sales (Parameter)** columns for France. Are they the same?

   ![France results](/images/230_151_013_FranceResults.png)

   Answer: Yes, both columns say 11.74% for France.

1. Use the page control to select **Europe**. Again, compare the **% of Total Sales** and the **% of Total Sales (Parameter)** columns for France. Are they the same?

   ![France results 2](/images/230_151_014_FranceResults2.png)

   Answer: Once the page control has been used to filter the list table, the two columns are not the same. The **% of Total Sales** column now contains the percent of total sales in Europe, whereas the **% of Total Sales (Parameter)** column still contains the percent of all global sales, because the parameter value is not affected by the page control.

1. The current column names were chosen to help us remember how they were calculated.  Now that we have seen how these measures are calculated, let's rename them to fit the context of the report.

1. Click the **Edit report** button to enter editing mode

1. In the left pane, click the **Data** tab.

1. Scroll down to the **Aggregated Measure** section.

1. Rename **% of Total Sales** to **% of Regional Sales**.

1. Rename **% of Total Sales (parameter)** to **% of Global Sales**.

   ![Rename](/images/230_151_015_Rename.png)

1. Save the report.

