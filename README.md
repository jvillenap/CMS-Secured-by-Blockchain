# CMS-Secured-by-Blockchain

This HoL has been created to demonstrate how easily you can create a custom CMS enriched with a verification of non-tampering of the documents by using blockchain as a certifier of the integrity of the documents.

The whole solution is created using just three Oracle Cloud Services we depict in the following diagram:

<p align="center">
<img width="416" height="307" src="https://github.com/jvillenap/CMS-Secured-by-Blockchain/blob/main/images/0_WEDO_CMS_LogicalArchitecture.jpg"/>
</p>

As you can see in the picture, we are using two different persistence solutions, it is:
1. First of all [Oracle Blockchain](https://www.oracle.com/es/blockchain/ "Oracle Blockchain Cloud Service"), it is the core piece of the solution, here is where the metadata of the documents are stored, like its name, kind of file, URL to be able to locate the document, or a hash generated based on the binary content of the document.

2. We are also using [OCI Object Storage](https://www.oracle.com/es/cloud/storage/object-storage/ "Oracle Cloud Infrastructure (OCI) Object Storage"), where documents itself, are stored.
	This is probably the best choice for those who needs the cheapest and most reliable storage solution. 
	OCI Object Storage allows you to store thousands of documents at a negligible cost.

We are also using [Oracle Integration Cloud](https://www.oracle.com/es/integration/application-integration/ "Oracle Integration Cloud"), not only for its integration capabilities, also because its extremely powerful Web & Mobile Low-Code development environment embedded in it, it is: [Oracle Visual Builder](https://www.oracle.com/es/integration/application-integration/#rc30p3 "Oracle Visual Builder"). It makes possible the development of a web or mobile interface in hours instead of weeks!

As you will see during the HoL, Oracle Visual Builder does not need to be instantiated. We have used Oracle Visual Builder to develope the web application, but once developed, you can just deploy the provided web application in whatever compute instance which can execute Node.js, so not needing to create any instance of Visual Builder, because the web application is self-contained.

And finally, we are also using the Identity Management solution offered by OCI, it is [Identity Cloud Service (IDCS)](https://www.oracle.com/es/security/cloud-security/identity-cloud/ "Oracle Identity Cloud Service"), where all the users who need to access to the solution, have been created, and granted to access with the proper privileges depending on their role.

it is important to highlight that, among the information stored in blockchain for each document, there is a hash generated based on the binary content of the document, here we can see how this hash is included among the metadata information of each document to be Stored into the blockchain ledger:
<p align="center">
<img width="620" height="530" src="https://github.com/jvillenap/CMS-Secured-by-Blockchain/blob/main/images/1_PostmanDocHash2.png"/>
</p>

if someone modifies the document from its external location, in our case a bucket in OCI Storage, next time someone tries to retrieve the document, the verfication based on validity of the hash will fail, so the user will be notified for the tampering of the document.

Regarding with the functional use case, the assets we are going to develop simulates an expedient management solution for a financial institution, in which each expedient represents a financial operation for a customer, and the expedient is acting as an archive where a sort of documents related with the operation are managed as a whole. 
	
The expedient is represented into blockchain as a non fungible token (NFT), because this kind of tokens fit really well in situations where one key aspect is the ownership of the asset. It means we can define the different kind of actions which can be executed against it depending on the role of the user accessing to the expedient. And the documents themselves are stored into a child array of the archive NFT entity. 

<p align="center">
<img width="785" height="510" src="https://github.com/jvillenap/CMS-Secured-by-Blockchain/blob/main/images/2_documentWorkflow.png"/>
</p>

There will be two different roles to access to the documents through the application:
* ***Expedient Manager***: If the user who accesses to the expedient is its current owner (or custodian), the user will be able to update the documents on the expedient, and also will be granted to perform a transfer of the expedient to a different user/department.

* ***Document Reviewer***:In the other hand, if the user who accesses to the expedient, is not its current owner or custodian, the user will only be granted to review the existing documentation of the expedient.

If you are interested in know a little bit more about NFTs, check the [Using NFT and FT Tokens in Oracle Blockchain](https://github.com/jvillenap/Using-NFT-and-FT-Tokens-in-Oracle-Blockchain/blob/main/README.md "Using NFT and FT Tokens in Oracle Blockchain") HoL, in which you can deploy your first Smartcontract handling Fungible and Non-Fungible tokens on Hyperledger Fabric, and test them really easily.


Steps to execute the HoL
========================
To implement a solution like the one exposed in this HoL, there are three main areas to work:
   1. Blockchain infrastructure preparation.  
   2. Development and Deployment of the Smartcontract.  
   3. Creation of the application(s) which will make use of our Smartcontract.  
  <p align="center">
<img width="584" height="532" src="https://github.com/jvillenap/CMS-Secured-by-Blockchain/blob/main/images/8-bc-arquitecture.png"/>
</p>

First of all we will create an Hyperledger Fabric network, which initially will be composed of one single organization, but can be easily scaled to as many members as you can. You can follow the instructions in the first labs of the [Using NFT and FT Tokens in Oracle Blockchain](https://github.com/jvillenap/Using-NFT-and-FT-Tokens-in-Oracle-Blockchain/blob/main/README.md "Using NFT and FT Tokens in Oracle Blockchain") HoL to see how you can do it.

Then, we will proceed to create the smartcontract to handle the logic needed to persist and manage into blockchain the entities required by our business case. 

Once the smartcontract gets created, we will install and deploy it into our blockchain network, and create the enrolments, configure the accounts who can own the NFT token, and initialize the NFT token!!!

At this point, the smartcontract methods have already been published through the API Gateway of our Oracle Blockchain instance, so they are ready to be used by the client applications, in our case the Web Application we have already created with VBCS, and we will provide in this chapter.

Next to last step is the creation of the OCI Storage Bucket where the documents itself will be stored, and last step is reconfiguration of the VBCS application provided as interface to use our smartcontract, and deploy it into our tenancy.

Here you have the links to each of the labs to fulfill this HoL:  

   [1. Create an Oracle Blockchain Network](../../blob/main/1-create-network/README.md)  
   [2. Preparation of Oracle App Builder development environment](../../blob/main/2-install-AppBuilder/README.md)  
   [3. Creation, Installation, Deployment and Initialization of the SmartContract](../../blob/main/3-smartcontract/README.md)  
   [4. Creation and Configuration of the OCI Storage Bucket](../../blob/main/4-bucket/README.md)   
   [5. Configuration and Deployment of the Web Application](../../blob/main/5-webbApp/README.md)  
   [6. Test the Application](../../blob/main/6-test/README.md)  




What we are going to use to develop this HoL
============================================
Leveraging in Oracle Blockchain we can create in minutes an Hyperledger Fabric network as a founder, or join whatever existing Hyperledger Fabric network as a new participant. For the purpose of this HoL, we are going to create the most simple network where there is one single participant, obviously the founder of the network. This single organization network, does not have too much sense, but after the initial creation it can be easily extended by adding new organizations to the network. So, the topology of the network will be something like: 

<p align="center">
<img width="371" height="392" src="https://github.com/jvillenap/CMS-Secured-by-Blockchain/blob/main/images/3-bc_topology.png"/>
</p>


In this Hyperledger Fabric network we will create a dedicated channel to be used only for the smartcontracts related with our use case. In my case I've named the channel ***wedocms***, and obviously the only existing participant of the network will join this channel:

<p align="center">
<img width="834" height="153" src="https://github.com/jvillenap/CMS-Secured-by-Blockchain/blob/main/images/4-bc-channel.png"/>
</p>

All the administrative taks will be easily executed thanks to the Service Console present for any Oracle Blockchain instances, one for the founder, and the other for the participant:

<p align="center">
<img width="960" height="540" src="https://github.com/jvillenap/CMS-Secured-by-Blockchain/blob/main/images/5-bc-adminconsole.png"/>
</p>

In the other hand, Oracle App Builder is a toolset developed by Oracle which will help you to create your Smartcontracts abstracting you from all the intrinsic technical complexities, even more when you need to create a NFT token. So, leveraging Oracle Blockchain and Oracle AppBuilder you will reduce considerably the time to market for any project in which NFTs and/or FTs would be needed.

<p align="center">
<img width="960" height="540" src="https://github.com/jvillenap/CMS-Secured-by-Blockchain/blob/main/images/6-appbuilder1.png"/>
</p>

AppBuilder will help you to reduce considerably the complexity of the development, packaging, testing, and deployment of Hyperledger Fabric chaincodes, giving you the option to create them in different languages (TypeScript or Go).

<p align="center">
<img width="814" height="392" src="https://github.com/jvillenap/CMS-Secured-by-Blockchain/blob/main/images/7-appbuilder2.png"/>
</p>


Enjoy it!
