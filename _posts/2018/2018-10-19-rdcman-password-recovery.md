---
layout: single
title: "Recovering Passwords from Remote Desktop Connection Manager"
date: 2018-10-19 22:24:17 -0400
categories: powershell
published: true
---

Microsoft’s Remote Desktop Connection Manager stores connection parameters - including credentials - in the .rdg file. The file itself is just an XML file but the passwords it contains are (rightfully) encrypted. With Powershell, we can pull those stored passwords out and decrypt them.

If you open an RDG file in a text editor, inside you’ll find entries that look like this:

{% highlight xml %}
<server>
    <properties>
        <displayName>My Server</displayName>
        <name>192.168.1.5</name>
    </properties>
    <logonCredentials inherit="None">
        <profileName scope="Local">Custom</profileName>
        <userName>MY-SERVER\Administrator</userName>
        <password>AQAAANCMnd8BFd51TsNoHsAYWFGAgdQzKDBK8jY=</password>
        <domain>MY-SERVER</domain>
    </logonCredentials>
</server>
{% endhighlight %}

The passwords are not stored in cleartext (which was actually an option in earlier versions of RDC Manager). They’re encrypted using [CryptProtectData](https://msdn.microsoft.com/en-us/library/aa380261.aspx) using the credentials of the user who created the RDG file. This is a good approach for protecting against offline attacks, but it means the following decryption method will only work when done under the user account that originally created it.

Using PowerShell, we can extract the encryption parameters from RDCMan by copying the executable and changing the extension to DLL:
{% highlight powershell %}
Copy-Item '{Path_to_RDCMan}\RDCMan.exe' 'C:\temp\rdcman.dll'
{% endhighlight %}

Next, import the DLL into the PowerShell session:
{% highlight powershell %}
Import-Module 'C:\temp\rdcman.dll'
{% endhighlight %}

Create a new object in the session to store the parameters we need:
{% highlight powershell %}
$settings = New-Object -TypeName RdcMan.EncryptionSettings
{% endhighlight %}

Now store the encrypted password that you want to decrypt
{% highlight powershell %}
$password = '{paste ciphertext here}'
{% endhighlight %}

Now decrypt:
{% highlight powershell %}
[RdcMan.Encryption]::DecryptString($password , $settings)
{% endhighlight %}