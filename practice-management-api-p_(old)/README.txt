# Introduction
Provides information and functionality to assist the managers of the consulting company to manage the practices within the firm

# Overview
The following use case diagram shows how actors will interact with the API

<img src="https://yuml.me/bff6941d.jpg" alt="UML use case">

You can edit this use case diagram here https://yuml.me/edit/bff6941d


# Authentication
Authentication is managed by Open API Connect and Authorisiation is managed by OAUTH 2.  We are using Auth0 to provide thes services

# Response Codes


<div>
    <br/>
</div>
<div>
    <p>
        A number of codes are available for successful responses. However, the
        exact status in most cases can be inferred from the request, and
        multiple potential successful return codes encourage inconsistency and
        add an overhead for testing and debugging.
    </p>
    <p>
        A successful response code should be one of the following:
    </p>
    <table border="1" cellspacing="0" cellpadding="0">
        <thead>
            <tr>
                <td width="98">
                    <p align="center">
                        <strong>HTTP Status Code</strong>
                    </p>
                </td>
                <td width="364">
                    <p align="center">
                        <strong>When Used</strong>
                    </p>
                </td>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td width="98">
                    <p align="center">
                        200
                    </p>
                </td>
                <td width="364">
                    <p>
                        OK – used to indicate that the request was successfully
                        processed, and has returned data to the consumer of the
                        service.
                    </p>
                </td>
            </tr>
            <tr>
                <td width="98">
                    <p align="center">
                        201
                    </p>
                </td>
                <td width="364">
                    <p>
                        Created – used when a request has resulted in the
                        creation of a new resource, e.g. from a POST request.
                    </p>
                </td>
            </tr>
            <tr>
                <td width="98">
                    <p align="center">
                        202
                    </p>
                </td>
                <td width="364">
                    <p>
                        Accepted – used when a request has been received for
                        processing, but that processing hasn’t yet completed;
                        for example, an asynchronous request.
                    </p>
                </td>
            </tr>
            <tr>
                <td width="98">
                    <p align="center">
                        204
                    </p>
                </td>
                <td width="364">
                    <p>
                        No Content – used when a request has been successfully
                        processed but has resulted in a response containing an
                        empty body.
                    </p>
                </td>
            </tr>
        </tbody>
    </table>
    <br/>
</div>
# Error Codes
<div>
    <p>
        Error status codes are:
    </p>
    <table border="1" cellspacing="0" cellpadding="0" width="473">
        <thead>
            <tr>
                <td width="99">
                    <p align="center">
                        <strong>HTTP Status Code</strong>
                    </p>
                </td>
                <td width="374">
                    <p align="center">
                        <strong>Description</strong>
                    </p>
                </td>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td width="99">
                    <p align="center">
                        400
                    </p>
                </td>
                <td width="374">
                    <p>
                        Bad request – the incoming request does not conform to
                        the expected schema definition. The data sent may not
                        match the definition, or may be missing altogether.
                    </p>
                </td>
            </tr>
            <tr>
                <td width="99">
                    <p align="center">
                        401
                    </p>
                </td>
                <td width="374">
                    <p>
                        Unauthorised – the requesting client has not
                        authenticated successfully, or is attempting to access
                        a resource that is protected.
                    </p>
                </td>
            </tr>
            <tr>
                <td width="99">
                    <p align="center">
                        403
                    </p>
                </td>
                <td width="374">
                    <p>
                        Forbidden – the client is attempting to access a
                        resource to which access has not been granted
                    </p>
                </td>
            </tr>
            <tr>
                <td width="99">
                    <p align="center">
                        404
                    </p>
                </td>
                <td width="374">
                    <p>
                        Not Found – used when the requested resource cannot be
                        located.
                    </p>
                </td>
            </tr>
            <tr>
                <td width="99">
                    <p align="center">
                        406
                    </p>
                </td>
                <td width="374">
                    <p>
                        Not Acceptable – used when a request contains an Accept
                        header that the service does not support.
                        <strong>
                            For experience APIs, prefer Status Code 400
                        </strong>
                        .
                    </p>
                </td>
            </tr>
            <tr>
                <td width="99">
                    <p align="center">
                        409
                    </p>
                </td>
                <td width="374">
                    <p>
                        Conflict – typically used when two requests are
                        processed that request a PATCH on the same resource at
                        the same time, resulting in potentially two copies of
                        the same data.
                        <strong>
                            For experience APIs, prefer Status Code 400
                        </strong>
                        .
                    </p>
                </td>
            </tr>
            <tr>
                <td width="99">
                    <p align="center">
                        410
                    </p>
                </td>
                <td width="374">
                    <p>
                        Gone – this is used when a resource being requested has
                        been intentionally removed, for example by a DELETE
                        request.
                        <strong>
                            For experience APIs, prefer Status Code 400.
                        </strong>
                    </p>
                </td>
            </tr>
            <tr>
                <td width="99">
                    <p align="center">
                        415
                    </p>
                </td>
                <td width="374">
                    <p>
                        Unsupported Media Type – used when the client attempts
                        to access a resource using a media type that is not
                        supported by the server or resource.
                        <strong>
                            For experience APIs, prefer Status Code 400
                        </strong>
                        .
                    </p>
                </td>
            </tr>
            <tr>
                <td width="99">
                    <p align="center">
                        429
                    </p>
                </td>
                <td width="374">
                    <p>
                        Too Many Requests – this is used when a service
                        implements rate limiting, and indicates that the client
                        has exhausted the number of requests allocated to the
                        client for a given time interval.
                        <strong>
                            For experience APIs, prefer Status Code 400
                        </strong>
                        .
                    </p>
                </td>
            </tr>
        </tbody>
    </table>
</div>
<div>
    <br/>
</div>
<div>
    <br/>
</div>
<div>
    <br/>
</div>
# Fault Codes
<div>
    <p>
        Fault status codes are:
    </p>
    <table border="1" cellspacing="0" cellpadding="0" width="466">
        <thead>
            <tr>
                <td width="98">
                    <p align="center">
                        <strong>HTTP Status Code</strong>
                    </p>
                </td>
                <td width="368">
                    <p align="center">
                        <strong>Description</strong>
                    </p>
                </td>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td width="98">
                    <p align="center">
                        500
                    </p>
                </td>
                <td width="368">
                    <p>
                        Internal Server Error – an unexpected condition was
                        encountered. Details about the error must NOT be
                        returned to the client, as this has the potential to
                        reveal technical details about the implementation to
                        consumers of the service.
                    </p>
                </td>
            </tr>
            <tr>
                <td width="98">
                    <p align="center">
                        502
                    </p>
                </td>
                <td width="368">
                    <p>
                        Bad Gateway - the server, while acting as a gateway or
                        proxy, received an invalid response from the upstream
                        server it accessed in attempting to fulfil the request.
                    </p>
                </td>
            </tr>
        </tbody>
    </table>
</div>
<div>
    <br/>
</div>
<div>
    <br/>
    <div>
        <p>
            <strong>Good</strong>
        </p>
        <p align="left">
            HTTP/1.1 400 Bad Request
            <br/>
            {
        </p>
        <p align="left">
            "Errors": [
        </p>
        <p align="left">
            {
        </p>
        <p align="left">
            "Code": "ER-1-0002",
        </p>
        <p align="left">
            "Message": "Invalid request data",
        </p>
        <p align="left">
            "DeveloperMessage": “the SendDateTime must be provided in the
            request message",
        </p>
        <p align="left">
            "Links":[{
            <br/>
            "Rel": "",
            <br/>
            "Href": "http://codingstandards/errors/ER-1-0002",
            <br/>
            "Description": "Invalid data",
            <br/>
            "Type": "GET"
        </p>
        <p align="left">
            }
            <br/>
            ]
            <br/>
            }
        </p>
    </div>
</div>



# Rate limit
Is there a limit to the number of requests an user can send?