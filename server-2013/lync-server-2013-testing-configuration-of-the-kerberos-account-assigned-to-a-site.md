﻿---
title: "Testing configuration of the Kerberos account assigned to a site"
TOCTitle: Testing configuration of the Kerberos account assigned to a site
ms:assetid: a087d77e-c59e-44f5-9caa-ccfd41be7276
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dn743837(v=OCS.15)
ms:contentKeyID: 62279286
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Testing configuration of the Kerberos account assigned to a site in Lync Server 2013

 

_**마지막으로 수정된 항목:** 2015-03-09_


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Verification schedule</p></td>
<td><p>Daily</p></td>
</tr>
<tr class="even">
<td><p>Testing tool</p></td>
<td><p>Windows PowerShell</p></td>
</tr>
<tr class="odd">
<td><p>Permissions required</p></td>
<td><p>When run locally using the Lync Server 관리 셸, users must be members of the RTCUniversalServerAdmins security group.</p>
<p>When run using a remote instance of Windows PowerShell, users must be assigned an RBAC role that has permission to run the Test-CsKerberosAccountAssignment cmdlet. To see a list of all RBAC roles that can use this cmdlet, run the following command from the Windows PowerShell prompt:</p>
<pre><code>Get-CsAdminRole | Where-Object {$_.Cmdlets -match &quot;Test-CsKerberosAccountAssignment&quot;}</code></pre></td>
</tr>
</tbody>
</table>


## Description

The Test-CsKerberosAccountAssignment cmdlet enables you to verify that a Kerberos account is associated with a given site, that this account is configured correctly, and that the account is working as expected. Kerberos accounts are computer accounts that can serve as the authentication principal for all the computers in a site that are running Internet Information Server (IIS). Because these accounts use the Kerberos authentication protocol, the accounts are known as Kerberos accounts, and the new authentication process is known as Kerberos web authentication. This enables you to manage all IIS servers by using a single account.

For more information, see the Help documentation for the [Test-CsKerberosAccountAssignment](https://docs.microsoft.com/en-us/powershell/module/skype/Test-CsKerberosAccountAssignment) cmdlet.

## Running the Test

By default, Test-CsKerberosAccountAssignment displays very little output on-screen. Instead, information returned by the cmdlet is written to an HTML file. Because of that, we recommend that you include the Verbose parameter and the Report parameter any time that you run Test-CsKerberosAccountAssignment. The Verbose parameter will provide slightly more detailed output on-screen while the cmdlet runs. The Report parameter allows you to specify a file path and file name for the HTML file generated by Test-CsKerberosAccountAssignment. If you do not include the Report parameter the HTML file will automatically be saved to your Users folder and be given a name similar to this: ce84964a-c4da-4622-ad34-c54ff3ed361f.html.

You must also specify a site Identity when you run Test-CsKerberosAccountAssignment. Kerberos accounts are assigned at the site scope.

The following command runs Test-CsKerberosAccountAssignment and saves the output to a file that is named C:\\Logs\\KerberosTest.html:

    Test-CsKerberosAccountAssignment -Identity "site:Redmond" -Report "C:\Logs\KerberosTest.html" -Verbose

For more information, see the Help documentation for the [Test-CsKerberosAccountAssignment](https://docs.microsoft.com/en-us/powershell/module/skype/Test-CsKerberosAccountAssignment) cmdlet.

## Determining Success or Failure

The Test-CsKerberosAccountAssignment cmdlet does not return a simple indication of success or failure. Instead, you must view the generated HTML file by using Internet Explorer.

## Reasons Why the Test Might Have Failed

Here are some common reasons why Test-CsKerberosAccountAssignment might fail:

  - You might have specified an incorrect site Identity. To return a list of valid site Identity, use this command:
    
        Get-CsSite | Select-Identity Identity
    
    A site Identity typically looks as follows:
    
    site:Redmond

  - The specified site might not have a Kerberos account assigned to it. You can determine whether or not a Kerberos account is assigned to a site by running a command similar to this:
    
        Get-CsKerberosAccountAssignment -Identity "site:Redmond"

  - Your Kerberos account might have a password that isn't valid. If you receive the following error message in report, you'll probably have to reset the Kerberos account password:
    
    InvalidKerberosConfiguration: The Kerberos configuration is invalid.
    
    InvalidKerberosConfiguration: The Kerberos configuration on atl-cs001.litwareinc.com is invalid. The expected assigned account is litwareinc\\kerberostest. Ensure that the account has not expired, and the configured password on the machine matches the Active Directory password of the account.
    
    You can set the password using the [Set-CsKerberosAccountPassword](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsKerberosAccountPassword) cmdlet.
