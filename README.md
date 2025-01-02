# **Guide to Using and Customizing the Workflow**

This guide explains how to use the workflow, what it does, and how you can customize it to suit your needs.

---

## **Overview**
This workflow is designed to:
1. Periodically fetch specific metrics from your monitoring system.
2. Identify custom devices that meet certain criteria.
3. Trigger problem events for these devices when conditions are met.

It’s set up to run automatically based on a scheduled trigger.

---

## **How It Works**

### **1. Importing Necessary Modules**
At the top of the script, you’ll find imports for the required SDK modules. These modules allow the script to interact with the monitoring system and process the data.

<img>

#### **Customization:**
No changes are typically needed here unless you're adding additional functionality.

---

### **2. Setting Up the Metric Selector**
The metric selector defines which devices and metrics the script should analyze.

<img>

#### **Explanation:**
- **`custom.db.query:filter(...)`**
  - Specifies a query to filter metrics data.
- **Filters in Use:**
  - **`or(in("dt.entity.custom_device", entityName))`**: Matches custom devices with specific identifiers (`entityName`).
  - **`entityName.contains("cipg")`**: Finds devices whose names include `"cipg"`.
  - **`eq(query_name, "Infinite Loop Check")`**: Looks for a specific query name.

#### **Customization:**
- Replace `"cipg"` with your desired substring.
- Change `"Infinite Loop Check"` to the appropriate query name for your use case.

---

### **3. Setting the Threshold**
The threshold defines the condition for selecting devices.

<img>

#### **Explanation:**
- Devices with metric values greater than or equal to the threshold will be processed.

#### **Customization:**
- Change `0` to the desired threshold value.

---

### **4. Fetching Metrics Data**
This section retrieves the metrics data based on the selector.

<img>

#### **Explanation:**
- **`metricsClient.query`**: Fetches the data.
- **`acceptType`**: Specifies the format of the response.

#### **Customization:**
- No changes needed unless you’re modifying the data structure or selector.

---

### **5. Evaluating Devices Against the Threshold**
The script evaluates the data and identifies devices meeting the threshold.

<img>

#### **Explanation:**
- Loops through the retrieved data.
- Checks if the metric value meets or exceeds the threshold.
- Maps matching devices by their IDs.

#### **Customization:**
- Adjust the loop logic if the data structure changes.

---

### **6. Creating the Problem Event**
If devices meet the threshold, a problem event is created for each.

<img>

#### **Explanation:**
- **Event Details:**
  - **`title`**: The title of the event.
  - **`entitySelector`**: Identifies which devices the event applies to.
  - **`properties`**: Additional details about the event.

#### **Customization:**
- Update the `title` and `description` to match your specific needs.

---

## **Key Points for Customization**
1. **Metric Selector:**
   - Update `"cipg"` and `"Infinite Loop Check"` to match your requirements.
2. **Threshold:**
   - Change the `threshold` value as needed.
3. **Event Details:**
   - Edit the `title` and `description` fields for clarity.

---

## **Example Use Case**
Let’s say you want to monitor devices with names containing `"error"` and trigger events for a query called `"Critical Error Check"` if the metric value exceeds `5`. You would:
1. Replace `"cipg"` with `"error"` in the metric selector.
2. Change `"Infinite Loop Check"` to `"Critical Error Check"`.
3. Update the `threshold` to `5`.
4. Modify the event `title` and `description` accordingly.

---

This guide should help you understand and customize the workflow even with minimal technical knowledge. If you encounter any issues or need clarification, feel free to ask!
