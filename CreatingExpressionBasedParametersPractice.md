# Creating Expression-Based Parameters

## Practice Duration

This practice will take 20 minutes to complete.

## Practice Objective

In this practice, you will create two expression-based parameters to dynamically set the minimum and maximum of a slider based on aggregations of a measure.

## Open an existing report

1. Open the **230_152_Creating Expression-Based Parameters** report from the **Courses/VISUAL** folder.

   <p><details>
   <summary>Click to expand/collapse for solution</summary>

   **Solution:**
   1. From the Desktop, open SAS Visual Analytics and sign in to SAS Viya.
   1. In the upper left corner, click ![ApplicationsMenu](/images/CDT-12533-10-image1.png) (**Show list of applications**) and select **Explore and Visualize**. SAS Visual Analytics appears.
   1. Click **SAS Content**.
   1. Navigate to the **Courses/VISUAL** folder.
   1. Double-click the **230_152_Creating Expression-Based Parameters** report to open it.
   1. Verify you are editing the report.
   </details></p>

1. What is the Range minimum and Range maximum of the slider?

   <p><details>
   <summary>Click to expand/collapse for solution</summary>

   **Solution:**
   1. Select the slider.
   1. On the right, click on **Options**.
   1. In the **Slider** group, view the **Range minimum** and **Range maximum**.

   **Answer:** The Range minimum is 400 and the Range maximum is 130,000.
   </details></p>

1. Using the treemap, what is the range of Quantity?

   <p><details>
   <summary>Click to expand/collapse for solution</summary>

   **Solution:**
   1. View the legend of the treemap.

   ![QuantityRangeTreemap](/images/CDT-12533-13-image1.png)

   **Answer:** The Quantity ranges from 478 to 127,765.
   </details></p>

1. Given that the slider should have the same range as the Quantity, what are potential problems with hardcoding the Range minimum and maximum? What can happen as the data gets updated?

   <p><details>
   <summary>Click to expand/collapse for solution</summary>

   **Solution:**
   As the data gets updated, the minimum or maximum of Quantity can change. In that case, the Range minimum and Range maximum of the slider need to be updated manually.
   </details></p>

   ## Create Expression-Based Parameters

1. Create a numeric expression-based parameter that calculates the minimum value of Quantity.

   <p><details>
   <summary>Click to expand/collapse for solution</summary>

   **Solution:**
   1. On the left, click on **Data**.
   1. Click on **New data item** and **Parameter**.
   1. For the Name, enter **Minimum Quantity**.
   1. For the Type, ensure that **Numeric** is selected.
   1. For the Format, select **COMMA12.**
      1. Next to the **Format** field, click ![Edit](/images/CDT-12533-13-image2.png) (**Edit**).
      1. For the **Format**, verify that **Comma** is specified.
      1. For the **Width** field, verify that **12** is specified.
      1. In the **Decimals** field, enter **0**.
      1. Click **OK**.
   1. Next to the Default value, select **Edit as expression**:

      ![EditAsExpression](/images/CDT-12533-13-image3.png).

   1. In the Edit Parameter Value, click on **Functions** and scroll down to the **Aggregated (tabular)** group to find the **AggregateTable** function:
   1. For the **Value** field, select **Quantity**.
   1. In **Aggregation 1**, for **Method**, ensure **\_Sum\_** is selected.
   1. For **Group context**, select **Fixed categories**.
   1. For **Categories**, click on the ![Edit](/images/CDT-12533-13-image2.png) **Edit** button. Double-click **Product Group** to select it and click on **OK**.
   1. For the **Final Aggregation**, for the **Method**, select **\_Min\_**.

      ![EditAggregateTableMin](/images/CDT-12533-13-image4.png)

   1. Click **OK**.
   1. The expression should look as follows:

      ```sas
      AggregateTable(_Min_, Table(_Sum_, Fixed('Product Group'n), Quantity))
      ```

   1. Click **OK** to close the Edit Parameter Value window.
   1. Click **OK** to close the New Parameter window.
   </details></p>

1. Create a numeric expression-based parameter that calculates the maximum value of Quantity.

   <p><details>
   <summary>Click to expand/collapse for solution</summary>

   **Solution:**
   1. In the data pane on the left, right-click on **Minimum Quantity** and select **Duplicate**.
   1. Right-click on the resulting **Minimum Quantity (1)** parameter and select **Edit Parameter**.
   1. For the name, enter **Maximum Quantity**.
   1. Next to the Default value, select **Edit as expression**:
   1. In the Edit Parameter Value window, right-click on **AggregateTable** and select **Edit**:
   1. In the **Edit AggregateTable** window, change the **Final Aggregation Method** to **\_Max\_**:

      ![EditAggregateTableMax](/images/CDT-12533-13-image5.png)

   1. Click **OK**.
   1. The expression should look as follows:

      ```sas
      AggregateTable(_Max_, Table(_Sum_, Fixed('Product Group'n), Quantity))
      ```

   1. Click **OK** to close the Edit Parameter Value window.
   1. Click **OK** to close the New Parameter window.
   </details></p>

1. Adapt the slider to use the parameters for its Range minimum and Range maximum.

   <p><details>
   <summary>Click to expand/collapse for solution</summary>

   **Solution:**
   1. Select the slider.
   1. On the right, click on **Options**.
   1. For the **Range minimum**, select the **Minimum Quantity** parameter:

      ![SelectParameterForRangeMinimum](/images/CDT-12533-13-image6.png).

   1. For the **Range maximum**, select the **Maximum Quantity** parameter:

      ![SelectParameterForRangeMaximum](/images/CDT-12533-13-image7.png).
   </details></p>

1. Save the report.
