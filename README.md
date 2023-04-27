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

Regarding with the functional use case, the assets we are going to develope simulates an expedient management solution for a financial institution, in which each expedient represents a financial operation for a customer, and the expedient is acting as an archive where a sort of documents related with the operation are managed as a whole. 
	
The expedient is represented into blockchain as a non fungible token (NFT), it means we can define the different kind of actions which can be executed against it, depending on the role of the user accessing to the expedient. And the documents themselves are stored into a child array of the archive NFT entity. 

<p align="center">
<img width="591" height="385" src="https://github.com/jvillenap/CMS-Secured-by-Blockchain/blob/main/images/2_documentWorkflow.png"/>
</p>
 
If the user who accesses to the expedient is its current owner (or custodian), the user will be able to update the documents on the expedient, and also will be granted to perform a transfer of the expedient to a different user/department.

In the other hand, if the user who accesses to the expedient, is not its current owner or custodian, the user will only be granted to review the existing documentation of the expedient.










Non-Fungible Tokens (NFT) are unique digital identifiers that cannot be copied, substituted, or subdivided, recorded in a blockchain, and that is used to certify authenticity and custodianship. NFT is the perfect digital twin for whatever kind of physical or digital asset which can be used to track any usage, event, status change, or any other kind of peculiarity which makes sense to be tracked. Blockchain will provide an easily accesible inmutable history of the asset, which will be really valuable for whatever entity or person interested in the tracking performed on the asset itself.

Using Oracle Blockchain we can create in minutes an Hyperledger Fabric network as a founder, or join whatever existing Hyperledger Fabric network as a participant. For the purpose of this HoL, we are going to create a new network in which there will be two participants:
- *Founder of the network*: ***eshop***, a shop which rent assets.
- *One Participant*: ***lessee1***, a lessee who rents assets from the eshop organization.

<p align="center">
<img width="371" height="392" src="https://github.com/jvillenap/Using-NFT-and-FT-Tokens-in-Oracle-Blockchain/blob/main/images/0-intro-2-1.png"/>
</p>

In this Hyperledger Fabric network we will create a dedicated channel to be used only for the smartcontracts related with our use case. This channel will be named ***rentalshop***, and obviously both existing participants of the network will join this channel:

<p align="center">
<img width="719" height="114" src="https://github.com/jvillenap/Using-NFT-and-FT-Tokens-in-Oracle-Blockchain/blob/main/images/0-intro-2-2.png"/>
</p>

All the administrative taks will be easily executed thanks to the Service Console present for any Oracle Blockchain instances, one for the founder, and the other for the participant:

<p align="center">
<img width="994" height="526" src="https://github.com/jvillenap/Using-NFT-and-FT-Tokens-in-Oracle-Blockchain/blob/main/images/0-intro-2-3.png"/>
</p>

In the other hand, App Builder is a toolset developed by Oracle which will help you to create your Smartcontracts abstracting you from all the intrinsic technical complexities, even more when you need to create NFT or FT tokens. So, leveraging Oracle Blockchain and AppBuilder you will reduce considerably the time to market for any idea in which NFTs and FTs would be the perfect fit.

<p align="center">
<img width="791" height="494" src="https://github.com/jvillenap/Using-NFT-and-FT-Tokens-in-Oracle-Blockchain/blob/main/images/0-intro-2-4.png"/>
</p>

AppBuilder will help you to reduce considerably the complexity of the development, packaging, testing, and deployment of Hyperledger Fabric chaincodes, giving you the option to create them in different languages (TypeScript or Go).

<p align="center">
<img width="814" height="392" src="https://github.com/jvillenap/Using-NFT-and-FT-Tokens-in-Oracle-Blockchain/blob/main/images/0-intro-2-5.png"/>
</p>

First of all we are going to create the smartcontract used to handle a cryptocurrency which will be represented as a Fungible Token (FT), and will be used to pay for the rented assets. Lessee will need to aquire tokens of this crypto to be able to rent the assets from the eshop. 

There will be a second smartcontract used to handle the Non-fungible token (NFT) which will be the digital representation in Blockchain of the real assets to be rented by the eShop company to the different lessees. 

Once each of the smartcontracts get created, we will install and deploy them into the different instances which compound the Blockchain Network created during the first lab.

Once all the tasks has been done, as Oracle Blockchain publishes all the smartcontract methods as REST APIs, we can execute a whole sample simulating the rental of an asset, just using Postman.

Here you have the links to each of the labs to fulfill this HoL:  

   [1. Create an Oracle Blockchain Network](../../blob/main/01-Create-The-Network/README.md)  
   [2. Preparation of Oracle App Builder development environment](../../blob/main/02-Prepare-Dev-Environment/README.md)  
   [3. Creation, Installation and Deployment of a SmartContract handling FTs](../../blob/main/03-Creation-and-Deployment-of-an-FT-SmartContract/README.md)  
   [4. Creation, Installation and Deployment of a SmartContract handling NFTs](../../blob/main/04-Creation-and-Deployment-of-an-NFT-SmartContract/README.md)   
   [5. Test the SmartContracts using Postman](../../blob/main/05-Test-Smartcontract-Using-Postman/README.md)  


Enjoy it!
