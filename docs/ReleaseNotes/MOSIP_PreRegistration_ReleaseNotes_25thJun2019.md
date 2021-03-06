**MOSIP Release Notes**
#### 1. Pre Registration

#### 1.1 Introduction : <br><sub>This document highlights features for Pre-Registration that are released for Technoforte.</sub></br>

#### 1.2 Release Summary : 
|         |          |
|----------|----------|
SubmittedBy|Ravi C Balaji
Date Raised | 27-Jun-2019
Jenkins Build #	|Min Version : 2235 [Any later version also]
Objective & Scope of Release| Pre-registration module
Acceptance Criteria	| Unit Testing and Code Coverage > 85%
Role/Job Title|Technical Lead
RFC(s) #|	NA


#### 1.3 Features Delivered : <br><sub>List of Features Delivered as part of this release should be listed here</sub></br>
Requirement ID | Requirement Type <br>(New\\Enhancement\\Defect)</br> | Description
-----|----------|-------------
MOS-25680|New|UI Enhancement - Padding & Alignment Fixes of current implemented UI. **Partially Done** For – Login Page,Demographic Page,File Upload Page. **In-progress** for other page


#### 1.4 Prerequisites 
1. MOSIP configuration has been separated from source code, and moved to a different repository. The same has been updated in Getting started here :

    https://github.com/mosip/mosip/wiki/Getting-Started#1-getting-the-source-code-

    To use this release, please make sure to mirror this new repository and update all configurations in this newly mirrored repository. And also make sure to use the same tag of mosip-configuration repository(i.e. 0.12.0)

2. Please make sure all required kernel service and external depency setup is done.
https://github.com/mosip/mosip/wiki/Kernel-Dependencies

3. Kernel KeyManager Auto Deployment (Non K8 cluster) - https://github.com/mosip/mosip/wiki/Getting-Started#67-steps-to-install-kernel-key-manager-service

4. HDFS security configuration - https://github.com/mosip/mosip/wiki/Steps-to-Install-and-configuration-HDFS

If security is not configured keep authentication-enabled false in application properties.
mosip.kernel.fsadapter.hdfs.authentication-enabled=false

Make user in all module specific properties hdfs.user-name is configured as per your hdfs cluster users. 
For ex. pre-registration-qa.properties mosip.kernel.fsadapter.hdfs.user-name=prereg  NOT   prereg-qa 
Same for registration-processor-qa.properties and id-repository-qa.properties


#### 1.5 Deployment

1. The existing schemas must be dropped and recreated. Scripts are there in Getting started page. </br>
2. Deploy the kernel module. 
https://github.com/mosip/mosip/blob/0.12.0/docs/ReleaseNotes/MOSIP_Kernel_Sprint12-ReleaseNotes.md </br>
3. In Kernel config server kubernetes yaml (deployment - confi-server-deployment-and-service.yml inside scripts/configuration), change git_url_env environment variable to the ssh URL of mosip-configuration repository that you have mirrored. <br/>
4. Deploy the Pre-registration module. 


#### 1.6 Prerequisites : <br><sub>Dependent module/component with their respective versions should be mentioned here</sub></br>
Module/Files|Component|Version|Description (If any)
-----|-------------|----------------|--------------
Java|JDK + JRE [Installed]|Main Version: Java 8 Min Version: 181|The Java Version is to be installed in the machine.
kernel-core|NA|0.12.13|Basic core kernel packages.
kernel-logger-logback|NA|0.12.13|Use for the logging.
kernel-dataaccess-hibernate|NA|0.12.13|Used for the communicating to the DB.
kernel-idgenerator-prid|NA|0.12.13|Used to generate the PRID format.
kernel-idvalidator-prid|NA|0.12.13|Used to validate the PRID format.
kernel-crypto-signature|NA|0.12.13|Used to validate the signature response from server.
kernel-templatemanager|NA|0.12.13|Used to generate the template manager.
kernel-qrcodegenerator-zxing|NA|0.12.13|Used to generate the QR code in acknowledgment page.
kernel-pdfgenerator-itext|NA|0.12.13|Used to scan the document in PDF format.
kernel-idobjectvalidator|NA|0.12.13|Used to validate the JSON.
kernel-fsadapter-hdfs|NA|0.12.13|DFS adaptor for HDFS.
kernel-virusscanner-clamav|NA|0.12.13|Used to communicate to the Antivirus Clam AV.
kernel-applicanttype-service|NA|0.12.13|Used to get the applicant types. 
kernel-masterdata-service|NA|0.12.13|Used to get the master data. 
kernel-emailnotification-service|NA|0.12.13|Used to notify the user through email. 
kernel-smsnotification-service|NA|0.12.13|Used to notify the user through sms. 
kernel-auditmanager-service|NA|0.12.13|Used to audit the reocrds into the DB.
kernel-cryptomanager-service|NA|0.12.13|Used to encrypt the pre-redistaion data information.

#### Note:
If you want to access rest apis, access token is required from authmanager.
1.Authenticate through clientId/Secret or UserId/Password haveing respective roles assigned.
2.After successful authentication access token will set as Autherization cookies.
3.Access API through postman by passing the access token in cookies.
NOTE: Swagger UI sends cookies automatically through browser.

1. Admin Token

    url- https://dev.mosip.io/v1/authmanager/authenticate/useridPwd

    ```
    {
    "id": "string",
    "metadata": {},
    "request": {
        "appId": "admin",
        "password": "preregadmin",
        "userName": "preregadmin"
    },
    "requesttime": "2018-12-10T06:12:52.994Z",
    "version": "string"
    }
    ```


2. Individual Token

    i. Send otp 
    url -   https://dev.mosip.io/preregistration/v1/login/sendOtp

    ### Request-
    ```
    {
    "id": "mosip.pre-registration.login.sendotp",
    "version": "1.0",
    "requesttime": "2019-05-14T07:24:47.605Z",
    "request": {
        "userId": "8907654778"
    }
    }
    ```

    ii. Validate Otp 

    url - https://dev.mosip.io/preregistration/v1/login/validateOtp

    ```
    Request-
    {
    "id": "mosip.pre-registration.login.useridotp",
    "version": "1.0",
    "requesttime": "2019-06-03T08:28:04.783Z",
    "request": {
        "otp": "345674",
        "userId": "8907654778"
    }
    }
    ```

After hitting validateOtp() api with proper request having otp and userid you will get the token in the header with the name Cookie.

### 1.7 IVV Closed Defects list :
Defect JIRA ID|Status|Availabilty in the branch
---------------|-------------|------------------
MOS-26095|Closed|Yes
MOS-25713|Closed|Yes
MOS-25687|Closed|Yes
MOS-25686|Closed|Yes
MOS-25613|Closed|Yes
MOS-25586|Closed|Yes
MOS-25584|Closed|Yes
MOS-25575|Closed|Yes
MOS-25574|Closed|Yes
MOS-25567|Closed|Yes
MOS-25563|Closed|Yes
MOS-25557|Closed|Yes
MOS-25556|Closed|Yes
MOS-25549|Closed|Yes
MOS-25546|Closed|Yes
MOS-25535|Closed|Yes

### 1.8 Ready for IVV Defects list :
Defect JIRA ID|Status|Availabilty in the branch
---------------|-------------|------------------
MOS-26109|Ready for ivv|Yes
MOS-26086|Ready for ivv|Yes
MOS-25734|Ready for ivv|Yes
MOS-25716|Ready for ivv|Yes
MOS-25632|Ready for ivv|Yes
MOS-25524|Ready for ivv|Yes
MOS-25520|Ready for ivv|Yes
MOS-25513|Ready for ivv|Yes

### 1.9 Known Defects list : Fixed and will be available in code drop 12.14
Defect JIRA ID|Status
---------------|-------------
MOS-26396|Fixed
MOS-26383|Fixed
MOS-26382|Fixed
MOS-26381|Fixed
MOS-26372|Fixed
MOS-26371|Fixed
MOS-26260|Fixed
MOS-26259|Fixed
MOS-26081|Fixed
