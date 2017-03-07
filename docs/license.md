# Frontuser API License
<p>Each API request is authenticated by an authentication token in the request header and use <code><b>application/json</b></code> for request and response data. The access [i.e. authorization] token and content type should be sent through request headers same as below:</p>
<code><strong>Authorization</strong>: Bearer ACCESS_TOKEN</code><br /><code><strong>Content-Type</strong>: application/json</code><br />
<p>Each authorized token is valid for <b>3600</b> <i>ms(milisecond)</i>, you can revoke expired token with the help of <b>refresh_token</b> through <b>Refresh Access Token</b> api call.</p>
