# Create an Oracle Blockchain Network

#### Table of Contents  
[Introduction](#Introduction)  
[Prerequisites](#Prerequisites)  
[Creation of the Founder instance](#createFounder)  
[Create a Channel](#channelCreate)  
[Set Anchor Peers](#setAnchorPeers)  
[Create User Accounts](#createAcconts)  
[Create Enrollments in the REST Proxy nodes](#createEnrollments)  

<a name="Introduction"/>

## Introduction

For the creation of an Hyperledger Fabric network based in Oracle Blockchain, you can use two different kinds of Oracle Blockchain instances:
- [Oracle Blockchain Cloud Service](https://www.oracle.com/es/blockchain/ "Oracle Blockchain Cloud Service")
- [Oracle Blockchain Platform Enterprise Edition](https://www.oracle.com/blockchain/blockchain-platform-enterprise-edition/ "Oracle Blockchain Platform Enterprise Edition")

For simplicity in this HoL we are going to use the first option, the Cloud Version. 

Also for simplicity, we are going to create a single instance HLF network, as per the use case we can show the functionality within one single organization belonging to the network. In case you want to extend the interchangeability of the expedients among departments from different organizations, you can add a new participant member to the network following the instructions in the following link:
- [How to create an HLF network with a founder instance, and a participant instance](https://github.com/jvillenap/Using-NFT-and-FT-Tokens-in-Oracle-Blockchain/blob/main/01-Create-The-Network/README.md "How to create an HLF network with a founder instance, and a participant instance").

As a preassembled PaaS, Oracle Blockchain Platform includes all the dependencies required to provision and manage a blockchain network: compute, storage, containers, identity services, event services, and management services. Oracle Blockchain Platform also includes the blockchain network console to support integrated operations. This helps you start developing applications within minutes.

<a name="Prerequisites"/>

## Prerequisites
- Access to an Oracle Cloud tenancy

<a name="createFounder"/>

## Creation of the Founder instance
1. In the OCI services menu, select ***Developer Services*** and click on ***Blockchain Platform***.
![Select Blockchain Service from the OCI console](https://github.com/jvillenap/CMS-Secured-by-Blockchain/blob/main/1-create-network/images/1-obp-2-1.png "Select Blockchain Service from the OCI console")

2. From the compartment combo selector located in the left side of the OCI Console, ensure the compartment where you want to create the instance is selected:
<p align="center"  alt="Select The compartment where the instance of the founder organization will be created">
<img width="283" height="257" src="https://github.com/jvillenap/CMS-Secured-by-Blockchain/blob/main/1-create-network/images/1-obp-2-2.png"/>
</p>

3. Press the button Create Blockchain Platform.
![Press the button Create Blockchain Platform](https://github.com/jvillenap/CMS-Secured-by-Blockchain/blob/main/1-create-network/images/1-obp-2-3.png "Press the button Create Blockchain Platform")

4. Give your platform a Display Name (e.g. 'eshop'), optionally add a Description, and keep the remaining default selections, as they are the settings to create a Founder instance, which will be the founder of a new Hyperledger Fabric Network, and using the standard shape, which has exactly the same functionality as the Enterprise shape but at a lower cost, but perfectly valid for development work. Click 'Create'.
<p align="center">
<img width="727" height="848" src="https://github.com/jvillenap/CMS-Secured-by-Blockchain/blob/main/1-create-network/images/1-obp-2-4.png"/>
</p>

5. Once pushed the 'Create' button, the creation of the instance for this Organization (e-shop) has been submited, and will be ready in a few minutes:
<p align="center">
<img width="834" height="415" src="https://github.com/jvillenap/CMS-Secured-by-Blockchain/blob/main/1-create-network/images/1-obp-2-5.png"/>
</p>

6. When the Founder instance gets created, you will be able to access to the Oracle Blockchain console for this instance by pushing the 'Service Console' button:
<p align="center">
<img width="833" height="417" src="https://github.com/jvillenap/CMS-Secured-by-Blockchain/blob/main/1-create-network/images/1-obp-2-6.png"/>
</p>


<a name="channelCreate"/>

## Create a Channel

We need to join the organizations at the channel level to allow communication between the founder and the participant.

1. From the founder ('e-shop') console, select the ***Channels*** tab. Click ***Create a New Channel***.
<p align="center">
<img width="641" height="271" src="https://github.com/jvillenap/CMS-Secured-by-Blockchain/blob/main/1-create-network/images/1-obp-2-20.png"/>
</p>

2. Fill out the form as shown and click ***Submit***.
- Set ***rentalshop*** as your Channel Name
- Check the boxes next to ***lessee1***
- Select both ***peer0*** and ***peer1*** under Peers to Join Channel
<p align="center">
<img width="956" height="578" src="https://github.com/jvillenap/CMS-Secured-by-Blockchain/blob/main/1-create-network/images/1-obp-2-21.png"/>
</p>

3. Confirm the creation by clicking ***Yes*** in the confirmation popup.
<p align="center">
<img width="956" height="572" src="https://github.com/jvillenap/CMS-Secured-by-Blockchain/blob/main/1-create-network/images/1-obp-2-22.png"/>
</p>

4. Check that the channel table displays the new channel. Click on 'rentalshop' to view channel details.
<p align="center">
<img width="948" height="308" src="https://github.com/jvillenap/CMS-Secured-by-Blockchain/blob/main/1-create-network/images/1-obp-2-23.png"/>
</p>

5. Note that both necessary organizations are listed.
<p align="center">
<img width="740" height="315" src="https://github.com/jvillenap/CMS-Secured-by-Blockchain/blob/main/1-create-network/images/1-obp-2-24.png"/>
</p>


<a name="setAnchorPeers"/>

## Set Anchor Peers

Each member using a channel (whether founder or participant) must designate at least one anchor peer. Anchor peers are primary network contact points, and are used to discover and communicate with other network peers on the channel.

1. Go to the founder ***eshop*** console and select the Channels tab. Click ***rentalshop*** under the channel table.
<p align="center">
<img width="786" height="309" src="https://github.com/jvillenap/CMS-Secured-by-Blockchain/blob/main/1-create-network/images/1-obp-2-27.png"/>
</p>

2. Click ***Peers*** in the left-hand pane.
<p align="center">
<img width="760" height="353" src="https://github.com/jvillenap/CMS-Secured-by-Blockchain/blob/main/1-create-network/images/1-obp-2-28.png"/>
</p>

3. Locate ***peer0*** and ensure that the ***Anchor Peer*** box is selected.
<p align="center">
<img width="758" height="322" src="https://github.com/jvillenap/CMS-Secured-by-Blockchain/blob/main/1-create-network/images/1-obp-2-29.png"/>
</p>

4. Click ***Set Anchor Peer*** to save changes.
<p align="center">
<img width="758" height="325" src="https://github.com/jvillenap/CMS-Secured-by-Blockchain/blob/main/1-create-network/images/1-obp-2-30.png"/>
</p>

Repeat for all these steps for the participant organization ***lessee1***.
<p align="center">
<img width="762" height="325" src="https://github.com/jvillenap/CMS-Secured-by-Blockchain/blob/main/1-create-network/images/1-obp-2-31.png"/>
</p>


<a name="createAcconts"/>

## Create Participant Accounts
We are going to use Oracle Identity Cloud (IDCS) to create at least one user in each organization to have the ownership of the FT and NFT tokens. To each of those users an account will be created to hold in it the tokens they own.

We are going to create the users ***eshop_manager*** and ***lessee1_manager***, and then assign them roles to control usage of their own OBP instances: 'eshop' for the eshop_manager user, and 'lessee1' for the lessee1_manager user.

1. From the OCI console, select the burger menu icon in the top left-hand corner and click on ***Identity & Security*** menu option, and into this option, select the ***Federation*** option from the ***Identity*** section.
<p align="center">
<img width="773" height="402" src="https://github.com/jvillenap/CMS-Secured-by-Blockchain/blob/main/1-create-network/images/1-obp-2-32.png"/>
</p>

2. Click in the link ***OracleIdentityCloudService***.
<p align="center">
<img width="770" height="345" src="https://github.com/jvillenap/CMS-Secured-by-Blockchain/blob/main/1-create-network/images/1-obp-2-33.png"/>
</p>

3. Push the button ***Create User***.
<p align="center">
<img width="958" height="378" src="https://github.com/jvillenap/CMS-Secured-by-Blockchain/blob/main/1-create-network/images/1-obp-2-34.png"/>
</p>

3. Set as username the value you want to use for login into the console or as the authorization username to execute the REST APIs of our smartcontract. In the email field set the email of your OCI account, so you will receive the email to reset the password for this user, and push the ***Create*** button:
<p align="center">
<img width="920" height="574" src="https://github.com/jvillenap/CMS-Secured-by-Blockchain/blob/main/1-create-network/images/1-obp-2-35.png"/>
</p>

4. In the next step you are asked to assign roles to recently created user, to do that push the ***Assign Roles*** Button.
<p align="center">
<img width="1148" height="324" src="https://github.com/jvillenap/CMS-Secured-by-Blockchain/blob/main/1-create-network/images/1-obp-2-36.png"/>
</p>

5. In the three dots of the ***AUTOBLKCHAIN*** Service, select the option to ***Manage Instance Access***:
<p align="center">
<img width="695" height="373" src="https://github.com/jvillenap/CMS-Secured-by-Blockchain/blob/main/1-create-network/images/1-obp-2-37.png"/>
</p>

6. Depending on the user you have just created, you will give to it grants based on the following table, and after assign the correct roles, push the ***Update Instance Settings***:

| username        | Instance      | Roles              |
| --------------- |:-------------:| ------------------ |
| eshop_manager   | eshop-....    | ADMIN, REST_CLIENT |
| lessee1_manager | lessee1-....  | ADMIN, REST_CLIENT |

<p align="center">
<img width="691" height="373" src="https://github.com/jvillenap/CMS-Secured-by-Blockchain/blob/main/1-create-network/images/1-obp-2-38.png"/>
</p>

7. You should see the roles properly assgined.
<p align="center">
<img width="695" height="371" src="https://github.com/jvillenap/CMS-Secured-by-Blockchain/blob/main/1-create-network/images/1-obp-2-39.png"/>
</p>

8. You will be asked to send an email to the email address to the user informing the roles for which has been granted. It's up to you sending or not the email
<p align="center">
<img width="691" height="357" src="https://github.com/jvillenap/CMS-Secured-by-Blockchain/blob/main/1-create-network/images/1-obp-2-40.png"/>
</p>

9. During the user creation process, you should receive to the email account associated with the recently created user, an email to reset the password for this user. Use the link provided to set the password of the user just created.
<p align="center">
<img width="610" height="900" src="https://github.com/jvillenap/CMS-Secured-by-Blockchain/blob/main/1-create-network/images/1-obp-2-41.png"/>
</p>


<a name="createEnrollments"/>

## Create Enrollments in the REST Proxy nodes
Oracle Blockchain Platform supports enrollments to the REST proxy. These enrollments are used in chaincodes where FT or NFT tokens exist, to ensure the identities of the user completing a transaction. To do this, when you add enrollments for token use cases, specify a user ID for each enrollment (founder ID in this case), and specify one and only one user for each enrollment.

Each enrollment must be created in the instance(s) where the user with such role are allowed to execute transactions trhough the REST Proxy on that Blockchain instance, so enrollment eshop_manager assigned to the user eshop_manager needs to be created in the REST Proxy node of the eshop (founder) instance, and the enrollment lessee1_manager assigned to the user lessee1_manager needs to be created in the REST Proxy node of the lessee1 (participant) instance.

1. While logged into the eshop founder instance, navigate to ***Nodes*** tab in the Blockchain console.

2. Click on the hamburger menu besides restproxy and select 'View or manage enrollments.'
<p align="center">
<img width="658" height="216" src="https://github.com/jvillenap/CMS-Secured-by-Blockchain/blob/main/1-create-network/images/1-obp-2-42.png"/>
</p>

3. Select ***Create New Enrollment***.
<p align="center">
<img width="501" height="243" src="https://github.com/jvillenap/CMS-Secured-by-Blockchain/blob/main/1-create-network/images/1-obp-2-43.png"/>
</p>

4. Set Enrollment ID as ***eshop_manager***, User ID as ***eshop_manager***, and push the ***Enroll*** button.
<p align="center">
<img width="502" height="335" src="https://github.com/jvillenap/CMS-Secured-by-Blockchain/blob/main/1-create-network/images/1-obp-2-44.png"/>
</p>

All this four steps must be repited to create the enrollment ***lessee1_manager*** for the user ***lessee1_manager*** but in the REST Proxy of the participant Blockchain instance (lessee1), so accessing to the Blockchain console of such instance. 
<p align="center">
<img width="985" height="532" src="https://github.com/jvillenap/CMS-Secured-by-Blockchain/blob/main/1-create-network/images/1-obp-2-45.png"/>
</p>
