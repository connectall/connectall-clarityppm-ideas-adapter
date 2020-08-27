# ConnectALL Clarity PPM Ideas Adapter

ConnectALL Clarity PPM Ideas Adapter is developed as an extension to the Universal adapter capability of ConnectALL. This adapter specifications will let the user use Clarity PPM Ideas with Webhooks to read and write the data in to Clarity PPM Ideas.

Please refere https://wiki.connectall.com/ca/latest/user-guide/adapters/custom-application-adapter for more information

# Usecase

As a user of Clarity PPM I would like to synchronize Ideas to Rally, VersionOne or similar Product and Portfolio management systems for planning and implementation process.

# How to use

> In order to use the Clarity PPM Ideas adapter you will need to get the license from ConnectALL sales team. Please reach out to sales@connectall.com for licenses and quotes.

## Import specifications
* Import *-adapter-descriptor.json in to ConnectALL using "Install custom adapter" feature. Customize the descriptor after importing to fit your personal projects
* View the transformation specs and open the transformation spec page
* Choose the operation, adapter type and create draft specifications
* Import the transformation specs of {adaptertype}-{operation}-[request|response]-[groovy|jolt].[groovy|json] into ConnectALL
* Test the specifications and save them as Active

> Note: You can also directly import the zip from dist directory in to ConnectALL directly.

## Define application links
* Create an application link in ConnectALL between Clarity PPM Ideas and a destination application of your choice
* Navigate to `Configuration -> Connections` screen and create a new connection to Clarity PPM Ideas like `https://connectall.clarityppm.com` as the endpoint
* In the Entity mapping tab under Advanced Properties choose "Sync Type" as POLL
* Use the below REST API templates for each operation

|Operation|API Method|Template|
|--- | --- | ---|
|QUERY MODIFIED RECORDS|GET|/ppm/rest/v1/${issueType}?filter=(lastUpdatedDate%20%3E%20'${last-modified-time}')&fields=lastUpdatedDate,code,name,description,estimatedFinishDate,estimatedStartDate,impact,description,estimatedCost,priority,objective,isFastTrack,regulatoryCompliance,estimateType,projectCategory,businessUnitPriority,corporatePriority,ideaPriority,workStatus|
|READ RECORD BY ID|GET|/ppm/rest/v1/ideas/${recordId}|
|CREATE RECORD|POST|/ppm/rest/v1/ideas|
|UPDATE RECORD|PUT|/ppm/rest/v1/ideas/${recordId}|
