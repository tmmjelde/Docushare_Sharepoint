# Docushare_Sharepoint
A script I wrote with Dag Ove Valsgaard to handle document migration from Docushare to Office 365 Sharepoint.

IMPORTANT NOTE:
The Docushare login website obfuscates the password before submitting to the site for login.
I have not converted this obfuscation into PowerShell, 
and therefore this script will send the password in clear text
to a website running JavaScript that will return an obfuscated version.
Therefore, it's not ideal, and should be improved upon.
It should be possible to convert the javascript code to Powershell.

I am not including that site in the code as I don't want any passwords getting sniffed :)
You'll have to set this up yourself and change the script to reference your own obfuscation site in the meanwhile.

<!DOCTYPE html>
<html>
<body>
<p id="demo"></p>
<script>
    function obscure_string(pwd, challenge) {
      var obscured = "";
      var i;
      for (i=0; i < pwd.length; i++) {
    var c = pwd.charCodeAt(i);
    var j = ((i) % challenge.length);
    var k = challenge.charCodeAt(j);
    var x = (c ^ k);
    var x16 = x.toString(16);
    if (x16.length == 1) {
      x16 = "0" + x16;
    }
    obscured += x16;
      }
      return obscured;
    }
var responsevalue = obscure_string("","");
</script>
<a href = ""><script>document.write(responsevalue);</script></a>
</body>
</html>
