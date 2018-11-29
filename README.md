
# Anypoint Template: API Led Connectivity System API for Salesforce

+ [License Agreement](#licenseagreement)
+ [Use Case](#usecase)
+ [Considerations](#considerations)
	* [Salesforce Considerations](#sfdcconsiderations)
+ [Run it!](#runit)
	* [Running on premise](#runonopremise)
	* [Running on Studio](#runonstudio)
	* [Running on Mule ESB stand alone](#runonmuleesbstandalone)
	* [Running on CloudHub](#runoncloudhub)
	* [Deploying your template on CloudHub](#deployingyouranypointtemplateoncloudhub)
	* [Properties to be configured (With examples)](#propertiestobeconfigured)
+ [Customize It!](#customizeit)
	* [system-api.xml](#systemapisfdc)



# License Agreement <a name="licenseagreement"/>
Note that using this template is subject to the conditions of this [License Agreement](AnypointTemplateLicense.pdf).
Please review the terms of the license before downloading and using this template. In short, you are allowed to use the template for free with Mule ESB Enterprise Edition, CloudHub, or as a trial in Anypoint Studio.

# Use Case <a name="usecase"/>
This Anypoint template serves as a foundation for API Led Connectivity approach of running an enterprise.
The template is a System API to underlying Salesforce system.

This template is a REST API implemented using APIkit and RAML definition. The basic CRUD operations are implemented for Account object (Customer). The API uses JSON as an exchange format. Included are example requests and responses.

Below are the endpoints that are implemented.

### GET /accounts
Retrieves accounts from Salesforce based on the combination of query parameters. At least one of `modifiedAfter` or `name` should be set to retrieve results. Look at the included RAML definition to learn more about the implemented query parameters.

### POST /accounts
Inserts new Account to Salesforce

### GET /accounts/{id}
Retrieves an Account based on the given Salesforce native identifier.

### PUT /accounts/{id}
Updates an Account with the data in the HTTP request. All fields are overwritten.

### DELETE /accounts/{id}
Deletes specific Account based on the given Salesforce native identifier.


Look at the included self-descriptive RAML definition and the corresponding flows to learn more about the flows.

# Considerations <a name="considerations"/>

To make this template run, there are certain preconditions that must be considered. All of them deal with the preparations, that must be made for the template to run smoothly.
**Failing to do so could lead to unexpected behavior of the template.**

## Salesforce Considerations <a name="salesforceconsiderations"/>

There may be a few things that you need to know regarding Salesforce, in order for this template to work.

In order to have this template working as expected, you should be aware of your own Salesforce field configuration.

### FAQ

 - Where can I check that the field configuration for my Salesforce instance is the right one?

    [Salesforce: Checking Field Accessibility for a Particular Field][1]

- Can I modify the Field Access Settings? How?

    [Salesforce: Modifying Field Access Settings][2]


[1]: https://help.salesforce.com/HTViewHelpDoc?id=checking_field_accessibility_for_a_particular_field.htm&language=en_US
[2]: https://help.salesforce.com/HTViewHelpDoc?id=modifying_field_access_settings.htm&language=en_US

If the user configured in the template for the source system does not have at least *read only* permissions for the fields that are fetched, then a *InvalidFieldFault* API fault will show up.

```
java.lang.RuntimeException: [InvalidFieldFault [ApiQueryFault [ApiFault  exceptionCode='INVALID_FIELD'
exceptionMessage='
Account.Phone, Account.Rating, Account.RecordTypeId, Account.ShippingCity
^
ERROR at Row:1:Column:486
No such column 'RecordTypeId' on entity 'Account'. If you are attempting to use a custom field, be sure to append the '__c' after the custom field name. Please reference your WSDL or the describe call for the appropriate names.'
]
row='1'
column='486'
]
]
```



# Run it! <a name="runit"/>
Simple steps to get API Led Connectivity System API for Salesforce running.


## Running on premise <a name="runonopremise"/>
In this section we detail the way you should run your template on your computer.


### Where to Download Mule Studio and Mule ESB
First thing to know if you are a newcomer to Mule is where to get the tools.

+ You can download Mule Studio from this [Location](http://www.mulesoft.com/platform/mule-studio)
+ You can download Mule ESB from this [Location](http://www.mulesoft.com/platform/soa/mule-esb-open-source-esb)


### Importing a template into Studio
Mule Studio offers several ways to import a project into the workspace, for instance:

+ Anypoint Studio generated Deployable Archive (.jar)
+ Anypoint Studio Project from External Location

You can find a detailed description on how to do so in this [Documentation Page](http://www.mulesoft.org/documentation/display/current/Importing+and+Exporting+in+Studio).


### Running on Studio <a name="runonstudio"/>
Once you have imported you template into Anypoint Studio you need to follow these steps to run it:

+ Locate the properties file `mule.dev.properties`, in src/main/resources
+ Complete all the properties required as per the examples in the section [Properties to be configured](#propertiestobeconfigured)
+ Once that is done, right click on you template project folder
+ Hover you mouse over `"Run as"`
+ Click on  `"Mule Application"`


### Running on Mule ESB stand alone <a name="runonmuleesbstandalone"/>
Complete all properties in one of the property files, for example in [mule.prod.properties](../master/src/main/resources/mule.prod.properties) and run your app with the corresponding environment variable to use it. To follow the example, this will be `mule.env=prod`.


## Running on CloudHub <a name="runoncloudhub"/>
While [creating your application on CloudHub](http://www.mulesoft.org/documentation/display/current/Hello+World+on+CloudHub) (Or you can do it later as a next step), you need to go to Deployment > Advanced to set all environment variables detailed in **Properties to be configured** as well as the **mule.env**.


### Deploying your template on CloudHub <a name="deployingyouranypointtemplateoncloudhub"/>
Mule Studio provides you with really easy way to deploy your Template directly to CloudHub, for the specific steps to do so please check this [link](http://www.mulesoft.org/documentation/display/current/Deploying+Mule+Applications#DeployingMuleApplications-DeploytoCloudHub)


## Properties to be configured (With examples) <a name="propertiestobeconfigured"/>
In order to use this Mule template you need to configure properties (Credentials, configurations, etc.) either in properties file or in CloudHub as Environment Variables. Detail list with examples:

### Application configuration
**Common Configuration**

+ http.port `9090`

**Salesforce Connector Configuration**

+ sfdc.username `user@company.com`
+ sfdc.password `secret`
+ sfdc.securityToken `h0fcC2Y7dnuH7ELk9BhoW0xu`

**API Configuration**

+ api.domain `your-sfdc-api.cloudhub.io`
+ api.basePath `/api`


# Customize It!<a name="customizeit"/>
This brief guide intends to give a high level idea of how this template is built and how you can change it according to your needs.
As mule applications are based on XML files, this page will be organized by describing all the XML that conform the template.
Of course more files will be found such as Test Classes and [Mule Application Files](http://www.mulesoft.org/documentation/display/current/Application+Format), but to keep it simple we will focus on the XMLs.

Here is a list of the main XML files you'll find in this application:

* [system-api.xml](#systemapisfdc)

## system-api.xml<a name="systemapisfdc"/>

A functional aspect of this template implemented in this XML is to create or update objects in the destination system for a represented use case. You can customize and extend the logic of this template in this XML to more specifically meet your needs.

Configuration for Connectors and [Properties Place Holders](http://www.mulesoft.org/documentation/display/current/Configuring+Properties) are also set in this file. **Even though you can change the configuration here, all parameters that can be modified here are in properties file, and this is the recommended place to do it so.** Of course if you want to do core changes to the logic you will probably need to modify this file.

In the visual editor they can be found on the *Global Element* tab.
