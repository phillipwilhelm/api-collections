Thank you for using the Open Practice Solutions Interface (OPS) Platform Integration API! 

This version of the API is currently supported!

This API services healthcare data using the industry standard FHIR STU 3 specifications. Complete documentation for this specification can be found at http://hl7.org/fhir/STU3/. This API will allow implementations to programatically manipulate data in OpenPM.

Use of this API requires an understanding of the above specification and a working understanding of RESTful APIs. While this documentation will provide context specific references to the FHIR specification where appropriate, it will not explain or serve as a tutorial for the concepts covered in that specification or RESTful APIs in general.

This is a living document and will be updated with non-breaking changes. When breaking changes are made, new documentation and migration guides will be released. Older versions will no longer be supported.

<h2>Notable Exceptions:</h2>
<ul>
<li>This API only contains implementations for the Resources listed in this documentation. Special considerations to be aware of regarding this implementation of the FHIR specification can be found under each Resource heading. References or functionality dependent on a resource not present in this documentation may cause unexpected or breaking behaviors. A complete implementation of the FHIR specification is planned and in progress.</li>
<li>The only acceptable data format for use with this API is JSON. While FHIR supports XML and other various formats, this API does not currently intend on implementing them.</li>
<li>PATCH operations are currently not supported. In order to update a resource, the user must call for a complete PUT operation. Any fields not provided in that operation, will be removed from that resource. PATCH operations will be supported soon.
</ul>