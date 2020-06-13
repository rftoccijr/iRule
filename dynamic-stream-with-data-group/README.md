This iRule dynamically rewrites content on response if the request URI matches an entry in a data group.

Sets flag called dynamicStream to 0 (intial set)
Looks at the URI and sees if it exists in a data group caqlled "stream_url"
If it does, then set the dynamicStream flag to 1
We also set another variable to the URI so we can pass it to the HTTP_RESPONSE event

In HTTP_RESPONSE, disable STREAM 
Is the flag set?
If so, then look up the Content-Type header
If it matches the types listed in the switch statement
  Then pull the value associated with the URI in the data group. This will be a STREAM expression, in the form of @old@new@
    old is the string you need to replace
    new is the string you need to replace the old one with
  STREAM::max_matchsize is set to cover large JavaScript that sometimes gets sent to a client
  Set the STREAM expression
  Enable STREAM

Any logging lines can be removed or remarked out

