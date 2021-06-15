# Business Context

  * To boost generalization of e-invoicing in Belgium, the Government decided to set up Hermes (hrms), an xml to pdf gateway that brings Belgian enterprises not yet equipped with inbound e-invoicing tools within the reach of Peppol BIS invoice senders.
  * A key component of hrms is HermeSMP (hsmp): this smp is dedicated to store only hrms receivers, ie all Belgian enterprises as long as they have not found a suitable Peppol Access Provider.
  * This API provides a 'machine friendly exit' for participant by providing Peppol access point to get the necessary migration key to start the standard SMP migration process, as defined in Peppol specifications.
  * Note that beside this API, there is also the possibility for an enterprise representative manually collects the migration key using a webform exposed by the Government. TODO : @Arnaud could you provide the url of the IWF


# API Documentation

This documentation describes the REST interface for the exchanges between the HSMP and a client wishing to retrieve a migration key in order to take over a Peppol participant.<br/>
This process is part of the <a href='https://github.com/OpenPEPPOL/documentation/blob/master/TransportInfrastructure/ICT-Transport-SML_Service_Specification-101.pdf'>Peppol SML specification</a>. But the actual exchange of the migration key part is left to specific implementation, as described in this extract of the SML specification:<br/><br/>
*Another set of steps relating to SMPs and the SML relates to the migration of the metadata about a participant from one SMP to another SMP (for example, the participant decides to change suppliers for this function). There are interfaces to the SML to support migrations of this kind, which imply following a sequence of steps along the lines shown in figure 4.
   In this sequence, the original SMP receives a request from a participant to migrate its metadata to a new SMP (a step that is done out-of-band: there are no interfaces defined in these specifications for this).
    The SMP generates a Migration Key which is a unique string containing characters and numbers only, with a maximum length of 24 characters.
    The original SMP invokes the PrepareToMigrate operation of the SML and then passes the migration key to the new SMP (the key passing is an out-of-band step not defined in these specifications).
    When the new SMP has created the relevant metadata for the participant, it signals that it is taking over by invoking the Migrate operation of the SML, which then causes the DNS record(s) for that participant ID to be updated to point at the new SMP.
    Once this switch is complete, the original SMP can remove the metadata which it holds for the participant.*


## Mutual TLS authentication
In order to call the API, the access point must use a valid Peppol certificate to perform a mutual TLS authentication:

* Production Access point certificate can be used for PROD and TEST Participants (SML and SMK)
* Test Access Point Certificate can only be used for TEST Participants (SMK)

Swagger is not able to specify security based on mutual TLS authentication, therefore the security part is left empty in the endpoint documentation.

## User blacklisting
HSMP allows a maximum of 1000 queries per day coming from a single certificate. If the limit is reached, the certificate is permanently baned. Access point may send a email request to BOSA support in order to to unblock the certificate.


## API DNS and IP's
The DNS entries are done for the following domains:

### TEST SMK : smp.acc-hermes-belgium.be

*  91.198.243.18
*  91.198.243.19

### PROD SML : smp.hermes-belgium.be

  *  91.198.243.20
  *  91.198.243.21


# Changes
## 1.0.0
The first release was done as parto f the initial development of the HSMP. Its purpose was to enable the BOSA intelligent web form to gather and distribute the migration key.
## 2.0.0beta
Following up on Access Points feedback, BOSA decided to provide a public API for Access Point to automate Participant migration.<br/>
Here is the list of changes:

  * The name of the API was changed to a more 'REST' friendly resource like name
  * The xml elements names were adapted to be closer to the one used in the SML documentation
  * The xml structure of the API request and response have been adapted in order to be fit in the capabilities of the swagger definition file.
  * Authentication was change to leverage the Peppol PKI
  * Error code were added. Note that due to swagger documentation, the error code are documented as x-000-HSMP-000. The API will respond a standard response code corresponding to the first 3 digits. The body of the response will contain the error code and message.

## 2.0.0CR
As part of the development few consistency changes were made.<br/>
Here is the list of changes:
  * Change prefix to URL : /hermes-rw/migrationKey
  * Few error codes (002 -> 012, 003 -> 013, 004 -> 811) were changed to insure consistency with Belgium SMP  
