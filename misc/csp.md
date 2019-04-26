### Content Security Policy
Its a Layer of security that helps in detecting and mitigating certain types of attach such as cross-site scripting(XSS), packet sniffing attacks and data injection attacts.

> Browser that doesnt support CSP still works with the servers which support it. If CSP headers not provided in the response then the browser use the same-origin-policy i.e. allows content from the same origin

#### Enabling CSP:
Configure your web server to return the Content-Security-Policy HTTP Headers (X-Content-Security-Policy headers as old name). Aleternatively, <meta> tags can be used to specify the poclicy:
`<meta http-equiv="Content-Security-Policy" contect="default-src 'self'; img-src https://*; child-src 'none';" >`

#### Threats:
1. Cross site scripting (XSS)
  - client site code injection attack.
  - running malicious JS code in client's web browser.
  - Site which let post commnet and does not sanitize the user comment input.
  Two types of XSS
  - reflected (The attack payload is included in a parameter when the victim follows a URL to the site.)
  - stored (The attack payload is stored in the site itself and when anyone visits the page, regardless of the URL followed, the attack executes.)

Allow scripts from the whitelisted trusted domain 

2. Packet Sniffing Attack:
 - allowing browser to interact to server using the secure channels eg. HTTPS
 - marking cookies with the secure flag
 - redireting HTTP to their HTTPS counterparts
 - sites may also use Strict-Transport-Policy header

#### Using CSP:
- Constructing the Contect-Security-Policy Header and adding values of the resources in it which are secure and allowed on the page, and then adding it to the page.
`Content-Security-Policy: {policy}`
- {polciy} -> is a string containing the policy directives.

- Policy directive: describe the policy for a certain resource type
1. default-src: policy directve it is the fallback for all those directives which are not specified in the poolicy
2. default-src/script-src blocks the inline scripts and the use of eval().
3. default-src/style-src block inline scripts or the style attribute.


USE CASES:

1. allow all content to come from own origin

`Content-Security-Policy: default-src 'self'`

2. Allow content from a trusted domain or its subdomain

`Content-Security-Policy: default-src 'self' *.trsuted.com`

3. Allow:
- images : from any origin
- audio/video: trusted provides
- script: trusted server

`Content-Security-Policy: default-src 'self'; img-src *; media-src media-1.com media2.com; script-src trsuted-script.com;`

4. Allows content is loaded using SSL

`Content-Security-Policy: default-src https://sometrsutedsite.com`

5. if script-src is from same then default-src 'self' only can be used. No need to specify the script-src in this case


#### Testing Policy:
CSP can be deployed in the report-only mode. In this case the policy is not enforced but any violations are reported to provided URI. A report-only header can be used to test the policy without deploying it.

- `Content-Security-Policy-Report-Only: {policy}`
Both Content-Security-Policy and Content-Security-Policy-Report-Only can be used together. Content-Security-Policy will be enforced while Content-Security-Policy-Report-Only will be used for reporting only.

##### Enabling reporting:
By providing report-uri policy directive in Content-Security-Policy

- `Content-Security-Policy: report-uri https://reportcollector.com`

Report JSON object:
```json
{
  "csp-report": {
    "document-uri": "the uri of the page/document where the violation occurred",
    "referrer": "the referrer of the document where the violation occurred",
    "blocked-uri": "the uri of the blocked resource",
    "violated-directive": "the name of the policy section which got violated",
    "original-policy": "the original policy as specified by the Content-Security-Policy HTTP header",
    "disposition": "enforce/reporting depending whether Content-Security-Policy-Report-Only was used",
    "effective-directive": "the directive use enforement caused the violation",
    "script-sample": "the first 40 chars of the violation script/style",
    "status-code": "the HTTP status code of the resource on which the global object was initialized"

  }
}
```
> In safari if Content-Security-Policy Header is set but not same-origin-policy header, it reports violation.

##### Using Nonces:
Nonce (number once), is a random string which is not predictable and generated using a secure function. Attacker can not know the number and every script without this particular nonce will be blocked. Nonce will be generated in every request.

`Content-Security-Policy: script-src 'self' "bmV0c3BhcmtlciBydWxlcyA7KQ=="`

```js
<script nonce="bmV0c3BhcmtlciBydWxlcyA7KQ==">
     var a = 'b';
</script>
```

##### Using Hashes:
Using the hashes of the scripts blocks.
