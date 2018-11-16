# NortheastDreamin 2018 
# Building Custom Apps with Lightning App Builder

Welcome to Northeast Dreamin 2018!  Here are links to the various resources needed to complete the hands-on Lightning App Builder workshop.

## Getting Started
Create your hands-on org & install project resources

1. Visit https://bit.ly/workshoplauncher

2. Select "Create Org" under the option titled "Automate A Business Process with Point And Click Tools"

3. When the message 'Your org is ready!' appears then click the 'Launch' button. 

4. Once logged into the demo org, copy the link below and paste it into the address bar while replacing everything after the initial "/"

Package Address: **/packagingSetupUI/ipLanding.app?apvId=04tf4000004MZI2**

Example: 
https://random-demo-org-dev-ed.lightning.force.com/lightning/setup/SetupOneHome/home becomes
https://random-demo-org-dev-ed.lightning.force.com/packagingSetupUI/ipLanding.app?apvId=04tf4000004MZI2


5. From the 'Install WorkshopDemo' screen, select the 'Install for Admins Only' option and press 'Install'.

6. Assign Permission Set. Setup > Users > Permission Sets > Demo Request User.  Click 'Manage Assignments'. Select 'USER' then 'Add'.

## Use Case #1 - Sales Users Need the Ability to Track Demo Requests in Salesforce
“XYZ Widgets has implemented Sale Cloud features that enable their team to perform account management and opportunity tracking in Salesforce. Sam, the Sales Manager, would like to extend the current functionality to allow the Reps to request demo equipment for customers via Salesforce.  

Working with her team, she has identified the following requirements:

The demo request feature should be accessible from the Opportunity 

Sales Reps should provide a reason for the eval request

The request should indicate the duration of the eval period

A Request Date should be provided in the new record

Requests should list the associated Account and Opportunity


### Solution Review - Demo Request Custom Object and Quick Action

The package installed earlier contains a custom object, fields, and other resources we will use to configure a solution to address the use case.  Use the steps below to add these 

Let's get started!

#### Review the Quick Action

1. Enter Setup. Navigate to Object Manager > Opportunity > Buttons, Links, and Actions

2. Click 'Demo Request' Quick Action from the list.

3. Click 'Edit Layout' and ensure that the **Request Date**, **Demo Duration**, and **Request Comments** fields are listed.

4. Return to the Quick Action page and note the list of fields in the **Predefined Values** section.

5. Click **'New'** to add an additional predefined value entry.  Set the values as follows and save the entry:

  Field: **Requested By**
  
  Formula Value: **$User.Id**

#### Add the Quick Action to the Page Layout
1. Add the 'Demo Request' quick action to the Opportunity Page Layout.

2. From Object Manager, Select Opportunity > Page Layouts > Opportunity Layout
  
3. Locate the **'Salesforce Mobile and Lightning Experience Actions'** section of the layout and click the wrench icon to override the default actions.
  
4. Select the **'Mobile & Lightning Actions'** section from the layout toolbar and drag the **'Demo Request'** action into the **Salesforce Mobile and Lightning Experience Actions'** section of the layout.

#### Add the Demo Requests related list to the Page Layout
1. Add the 'Demo Requests' related list to the Opportunity Page Layout.

2. Scroll down to the 'Related Lists' section from the layout toolbar and drag the 'Demo Requests' list onto the page layout.
 
3. Save the changes to the Opportunity Page Layout.

### Use the Quick Action to Create a Record

1. Click the 'App Launcher' icon and select the 'Sales' app.  Use the Search box at the top of the page to locate and open the **'Express Logistics Portable Truck Generator'** opportunity.  Add this opportunity to your Salesforce favorites for quick reference in future steps.

2. Click the **'Demo Request'** quick action from the action section of the Opportunity detail page and provide values for the required fields and Save to create the record.  Note that the new record will appear in the related list and include values for the fields on the quick action layout along with those listed in the predefined values section.

## Use Case #2 - Conditional Limits and Quick Actions


“Sam has received positive feedback from the Sales Reps regarding the new Quick Action.  This feature has made it very easy to create and follow-up on demo requests for customers. In fact, this feature is a bit too easy to use and demo requests are being submitted for Accounts and Customers that are not eligible for the demo equipment.  Sam states that the following conditions should be met before demo requests are created.

**Demo Requests should only be made for accounts rated as ‘Hot’**

**The Opportunity stage should be ‘Value Proposition’**


### Lightning Flow + Quick Actions + Conditional Visibility

At present, there is no configurable feature that provides Admins & App Builders the ability to conditionally hide or show quick actions.  However, Lightning App builder does include this capability and we can combine the powers of App Builder, Lightning Flow, and Quick Actions to dynamically display a flow in the Opportunity record page.

#### Review the Flow:

1. Navigate to Setup > Process Automation > Flows

2. Click the **Demo Request Screen Flow** to open the flow details.

3. Note that this flow contains 4 elements as detailed below:

Item #1 - Screen Element with instructions

Item #2 - Screen Element - User Input for the Demo Request record

Item #3 - Quick Action - Uses the quick action previously defined to create the record 

Item #4 - Screen Element - Confirmation message displayed after record is created.




### Include the Flow in the Opportunity Record Page using Lightning App Builder

1. Open the **'Express Logistics Portable Truck Generator'** opportunity.

2. Click the **'Setup'** gear at the top of the page and select **'Edit Page'** to launch Lightning App Builder.

3. Drag the **Flow** component from the list on the left and drop it at the top of the right side bar.

4. Configure the Flow component options as follows:
  Flow = **'Demo Request Screen Flow'**
  Layout = **'One Column'**
  Pass record ID into this variable = **Checked**

5. Set Component Visibility values for the flow component.  To start, click **'Add Filter'**

#### **Filter 1:**

Filter Type = **Advanced**

Field = **Record > Account Name > Rating**

Operator = **Equal**

Value = **Hot**

Click **Done** to save.



#### **Filter 2**

Click **Add Filter**

Filter Type = **Record Field**

Field = **Stage**

Operator = **Equal**

Value = **Value Proposition**

Click **Done** to save.

Click **Save** to Save the changes to the App Builder page.

#### Test the Lightning Record Page Changes

1. Open the **Express Logistics Portable Truck Generator** opportunity and notice that the Lightning Flow isn't visible (as expected).

2. Now, open the 'Express Logistics and Transport' account and press 'Edit'.  Change the 'Rating' value to 'Hot' and save the changes.

3. Reopen the **Express Logistics Portable Truck Generators** opportunity and you'll see that the Lightning Flow **IS** now visible for use by the reps as this record now meets the conditions defined by the visibility filters.

4. Use the Screen Flow to create a new Demo Request record -- be sure to complete the flow to trigger the related list refresh.

## Customizing the Demo Request Detail Page

Let's look at ways to highligh the status values associated with the Demo Request records.  Open one of the new Demo Request records from the **Express Logistics Portable Truck Generators** opportunity.  

1. Click the **Setup** gear at the top and then **'Edit Page'** to lauch **Lightning App Builder**.

2. Drag the **Path** component from the left to just under the Highlights panel on the screen

3. Configure Path options using the menu on the right.  Set the values as follows:

  Format: **Linear**
  
  Hide path update button: **Checked**
  
  
4. Click **'Set up Path'**.  The Path Settings page will appear -- and press the **'Enable'** button to activate the feature.

5. Return to Lightning App Builder tab and click **Save** then **Back** to see the Path component on the page.

Note how the path feature is configured to use the values defined in the Status field and how well this highlights the current status for the selected record.  


# Wrap-Up

Leverage Quick Actions to simplify related record creation or updates.

Consider Conditional Visibility as a way to create dynamic content based on record, related record, or user settings

Be Consistent - Lightning App Builder Customizations Tools are very powerful but work to establish some general guidelines and apply those consitently to ensure a clean user experience.



### Learn More with these Trailhead Modules

**Lightning Flow** - https://trailhead.salesforce.com/content/learn/modules/business_process_automation

**Lightning App Builder** - https://trailhead.salesforce.com/en/content/learn/modules/lightning_app_builder

**Lightning Experience Customization** - https://trailhead.salesforce.com/content/learn/modules/lex_customization

