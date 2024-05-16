# Power BI

Microsoft Power BI is a complete reporting solution that offers data preparation, data visualization, distribution, and management through development tools and an online platform.

Power BI can scale from simple reports using a single data source to reports requiring complex data modeling and consistent themes. Use Power BI to create visually stunning, interactive reports to serve as the analytics and decision engine behind group projects, divisions, or entire organizations.

There are three primary components to Power BI:
* Power BI Desktop (desktop application)
* Power BI service (online platform)
* Power BI Mobile (cross-platform mobile app)

## Flow of BI
There's a common flow when creating reports with Power BI. First, you start with Power BI Desktop to connect to data and create the report. Then you publish the report to the Power BI service and distribute to consumers.

The flow of Power BI is:

1. Connect to data with Power BI Desktop.
2. Transform and model data with Power BI Desktop.
3. Create visualizations and reports with Power BI Desktop.
4. Publish report to Power BI service.
5. Distribute and manage reports in the Power BI service.

## Building Blocks of Power BI

The building blocks of Power BI are semantic models and visualizations. Create a semantic model and then use visualizations to make a compelling report.

### Create the Semantic model

A semantic model consists of all the data connections, transformations, relationships and calculations. First connect to the data, transform the data, create relationships and calculations to create the semantic model.

First, connect to as many data sources you need. Then clean and transform the data to your needs. Add relationships between tables and calculations to extend the semantic model. After all of that, now you can create a report.

### Create visualizations in the report

In Power BI Desktop, when you create a visualization (also called visual), you add it to the canvas for a report page. Choose your visualizations to build pages in your report. It's ideal to keep each page simple with related data, so consumers can easily see the insights.

One of the most valuable features of Power BI reports is the interactivity between visuals. Consumers can select different data points in the visual and see how that affects the other visuals. Depending on your design, they can also drillthrough from one visual to more detail or filter based on different fields in the report.

### Create Dashboards

In the Power BI service, you can also create dashboards after you've published a report. Dashboards consist of a single page made up of tiles. Add tiles to a dashboard by pinning a visual in a report to the dashboard. Tiles aren't interactive like visuals, so when a user interacts with the tile, they go to the underlying report for more information.

## Power BI service

### Workspaces
Workspaces are the foundation of the Power BI service. When publishing any report, you must choose a workspace. By default, every user has access to My workspace, which is ideal only for testing. When you want to share content with others, always create and use a shared workspace.

### Apps
In a workspace, you can create an app, which provides consumers a simplified interface to access reports and dashboards. In the app configuration, you set up the app, select the content to include (limited to the current workspace), and choose your audience.

Apps are the ideal sharing solution within any organization. While you can grant access to the workspace, workspace permissions may grant users access to more content than desired. Sharing individual items also presents a problem if you make changes you don't want consumers to see yet.

### Refresh a sematic model
In order to support your ever-changing data, you can configure scheduled refreshes of your semantic models in the Power BI service. On-demand refreshes are also available.