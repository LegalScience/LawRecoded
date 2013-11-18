 
The OAuth 2.0 Authorization Framework, and Bearer Token Usage
 
# [https://github.com/LegalScience/LawRecoded/blob/master/brief-ietf-oauth2.md#problem-1](Problem)
# Proposed Solution
# Method of Implementation
# Possible Issues
# Ways to Mitigate Possible Issues
# Further Considerations

# Briefing 

The OAuth 2.0 Authorization Framework, and Bearer Token Usage are IETF specifications for user authorized access to protected resources. 

Authoritative Source: 


# Problem
* In the traditional client-server authentication model, the client requests an access-restricted resource (protected resource) on the server by authenticating with the server using the resource owner's credentials.  In order to provide third-party applications access to restricted resources, the resource owner shares its credentials with the third party.  This creates several problems and limitations:
 
   * Third-party applications are required to store the resource
  	owner's credentials for future use, typically a password in
  	clear-text.
 
   *  Servers are required to support password authentication, despite
  	the security weaknesses inherent in passwords.
 
   *  Third-party applications gain overly broad access to the resource
  	owner's protected resources, leaving resource owners without any
  	ability to restrict duration or access to a limited subset of
  	resources.
 
   *  Resource owners cannot revoke access to an individual third party
  	without revoking access to all third parties, and must do so by
  	changing the third party's password.
 
   * Compromise of any third-party application results in compromise of
  	the end-user's password and all of the data protected by that
  	password.
 
# Proposed Solution
*OAuth introduces authorization layer and separates the role of the client from that of the resource owner.  In OAuth, the client requests access to resources controlled by the resource owner and hosted by the resource server, and is issued a different set of credentials than those of the resource owner.
 
  * Instead of using the resource owner's credentials to access protected resources, the client obtains an access token -- a string denoting a specific scope, lifetime, and other access attributes.  Access tokens are issued to third-party clients by an authorization server with the approval of the resource owner.  The client uses the access token to access the protected resources hosted by the resource server.
 
# Method of Implementation
* OAuth steps:
 
   (A)  The client requests authorization from the resource owner.  The
    	authorization request can be made directly to the resource owner , or preferably indirectly via the authorization server as an intermediary.
 
   (B)  The client receives an authorization grant, which is a credential representing the resource owner's authorization. The authorization grant type depends on the method used by the client to request authorization and the types supported by the authorization server.
 
   (C)  The client requests an access token by authenticating with the authorization server and presenting the authorization grant.
 
   (D)  The authorization server authenticates the client and validates the authorization grant, and if valid, issues an access token.
 
   (E)  The client requests the protected resource from the resource server and authenticates by presenting the access token.
 
   (F)  The resource server validates the access token, and if valid, serves the request.
 
# Possible Issues 
 (source: The OAuth 2.0 Authorization Framework: Bearer Token Usage)
 
* Token manufacture/modification:  An attacker may generate a bogustoken or modify the token contents (such as the authentication or attribute statements) of an existing token, causing the resource server to grant inappropriate access to the client.  For example, an attacker may modify the token to extend the validity period; a malicious client may modify the assertion to gain access to information that they should not be able to view.
 
 *  Token disclosure:  Tokens may contain authentication and attribute statements that include sensitive information.
 
  * Token redirect:  An attacker uses a token generated for consumption by one resource server to gain access to a different resource server that mistakenly believes the token to be for it.
 
 *  Token replay:  An attacker attempts to use a token that has already been used with that resource server in the past.
 
# Ways to Mitigate Possible Issues
* A large range of threats can be mitigated by protecting the contents
   of the token by using a digital signature or a Message Authentication
   Code (MAC).  Alternatively, a bearer token can contain a reference to
   authorization information, rather than encoding the information
   directly.
* Safeguard bearer tokens by ensuring that bearer tokens are not leaked to unintended parties,
* Validate TLS certificate chains, and always use TLS (https) when making requests with bearer tokens. 
*Don't store bearer tokens in cookies: 
*Issue short-lived (one hour or less) bearer tokens, particularly when
  	issuing tokens to clients that run within a web browser or other
  	environments where information leakage may occur
* Issue scoped bearer tokens that contain an audience restriction, scoping their use to to intended relying party or set of relying parties.
* Don't pass bearer tokens in page URLs
 
# Further Considerations
* How will this be manageable from the individual user’s point of view?
*Are there administrability issues with respect to implementation and widespread use?
 

 
 

