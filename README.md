# SAML.Docs
SAML 2.0 Documentation with examples of ADFS, SimpleSAMLphp, etc... sample code and more


## Why is this documentation here?
Because when I started looking into implementing SAML in a product almost one and a half years ago. I really struggled to find **ANY** documentation on it or coding examples.
I hope that this documentation will be able to help someone else to use the madness that is SAML with more ease.

## What is **SAML** and **SAML 2.0**?
**[SAML](https://www.oasis-open.org/standards#samlv2.0)** is a specification for a SSO (Single Sign-On) method/process using XML, Certificates and Digital Signatures.

Here I will talk specifically about **[SAML 2.0](https://www.oasis-open.org/standards#samlv2.0)**


This also allows you to create a standard well known configuration file or endpoints on how to connect to your IDP (Identity Provider) or SP (Server Provider).
This standard configuration file is normally know as 'Metadata' some other services have sightly differing names for it e.g. **ADFS** (Active Directory Federation Services)
calls in 'FederationMetadata' for reasons I will not get into here (see **[ADFS](./ADFS.md)** for more).


## What SAML is not
It is not OAuth


## But...Wait how does it actually work?


## Hmm...So I sort of get it, but this will only work inside the clients network right?



## Examples

`An unsigned SamlRequest`
```xml
<?xml version="1.0"?>
<samlp:AuthnRequest xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion" xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol"
    Version="2.0"
    Destination="https://bad.netscalerserver.com/saml/login"
    ID="id8dcaa3c379d847a2880888d94c0e000d"
    IssueInstant="2017-07-13T23:18:35.360164Z"
    AssertionConsumerServiceURL="https://sp.example.com/saml/acs"
    ProtocolBinding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-POST"
    IsPassive="false">
    <saml:Issuer>https://sp.example.com</saml:Issuer>
    <samlp:NameIDPolicy AllowCreate="true" Format="urn:oasis:names:tc:SAML:2.0:nameid-format:persistent" />
    <saml:Conditions>
        <saml:AudienceRestriction>
            <saml:Audience>https://sp.example.com</saml:Audience>
        </saml:AudienceRestriction>
    </saml:Conditions>
</samlp:AuthnRequest>
```

`A Signed SamlRequest`
coming soon


`An unsigned SamlResponse`
```xml
<samlp:Response
    xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol"
    xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion"
    Consent="urn:oasis:names:tc:SAML:2.0:consent:obtained"
    Destination="https://sp.example.com/saml/acs"
    ID="id9qVeE-sBXDIf6aJihdhDqqp5nKU"
    InResponseTo="idb2722bf354da44eeb0882c77d9435c7a"
    IssueInstant="2017-06-20T03:54:22Z"
    Version="2.0">
    <saml:Issuer>https://login.example.com.au/nidp/saml2/metadata</saml:Issuer>
    <samlp:Status>
        <samlp:StatusCode Value="urn:oasis:names:tc:SAML:2.0:status:Success"/>
    </samlp:Status>
    <saml:Assertion ID="idYb0UJVMAqjaQZke2EnyRmRQDsNU" IssueInstant="2017-06-20T03:54:22Z" Version="2.0">
        <saml:Issuer>https://login.example.com.au/nidp/saml2/metadata</saml:Issuer>
        <saml:Subject>
            <saml:NameID Format="urn:oasis:names:tc:SAML:2.0:nameid-format:transient"
             NameQualifier="https://login.example.com.au/nidp/saml2/metadata"
             SPNameQualifier="https://sp.example.com"
             >jQ7h+CEcd3USah9OO24USTRvHUoyZhdJxA94wA==</saml:NameID>
            <saml:SubjectConfirmation Method="urn:oasis:names:tc:SAML:2.0:cm:bearer">
                <saml:SubjectConfirmationData InResponseTo="idb2722bf354da44eeb0882c77d9435c7a" NotOnOrAfter="2017-06-20T03:59:22Z" Recipient="https://sp.example.com/saml/acs"/>
            </saml:SubjectConfirmation>
        </saml:Subject>
        <saml:Conditions NotBefore="2017-06-20T03:49:22Z" NotOnOrAfter="2017-06-20T03:59:22Z">
            <saml:AudienceRestriction>
                <saml:Audience>https://sp.example.com</saml:Audience>
            </saml:AudienceRestriction>
        </saml:Conditions>
        <saml:AuthnStatement AuthnInstant="2017-06-20T03:54:22Z" SessionIndex="idYb0UJVMAqjaQZke2EnyRmRQDsNU">
            <saml:AuthnContext>
                <saml:AuthnContextClassRef>urn:oasis:names:tc:SAML:2.0:ac:classes:Kerberos</saml:AuthnContextClassRef>
                <saml:AuthnContextDeclRef>exampleserver/exampleKerberos</saml:AuthnContextDeclRef>
            </saml:AuthnContext>
        </saml:AuthnStatement>
        <saml:AttributeStatement>
            <saml:Attribute
                xmlns:xs="http://www.w3.org/2001/XMLSchema"
                xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Name="preferred_username" NameFormat="urn:oasis:names:tc:SAML:2.0:attrname-format:unspecified">
                <saml:AttributeValue xsi:type="xs:string">exampleUser</saml:AttributeValue>
            </saml:Attribute>
        </saml:AttributeStatement>
    </saml:Assertion>
</samlp:Response>
```


### Tools
[SAML Tool.com by onelogin](https://www.samltool.com/online_tools.php)



### GET(Redirect) vs POST

get
- sig as param
- inflate/deflate

post
- sig indoc
