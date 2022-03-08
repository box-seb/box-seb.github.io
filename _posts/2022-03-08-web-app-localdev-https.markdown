---
layout: post
title:  "HTTPS for local Web development"
date:   2022-03-08 11:01:01 +1200
---

Very often http protocol for local web development is enough. However, there are situations where libraries used to perform tasks such as authentication or authorization need to reach out to your application and refuse to work without https.

One of the options is to solve the problem is to use locally generated certificates. This is good enough for local development but not acceptable for production environments.

## Let's register a certificate for domain `mylocal.machine.com`
### Parts that need attentions:
- Domain name `mylocal.machine.com`, this is quite obvious
- Certificate file `mylocal.machine.com.pfx` is stored in `$env:USERPROFILE` direcotry
- Password name for the certificate is `password` - it's just for local development

## The script below can be run using PowerShell
```
$cert = New-SelfSignedCertificate -DnsName @("mylocal.machine.com") -CertStoreLocation "cert:\LocalMachine\My"

$certKeyPath = "$env:USERPROFILE\.aspnet\https\mylocal.machine.com.pfx"
$password = ConvertTo-SecureString 'password' -AsPlainText -Force
$cert | Export-PfxCertificate -FilePath $certKeyPath -Password $password
$rootCert = $(Import-PfxCertificate -FilePath $certKeyPath -CertStoreLocation 'Cert:\LocalMachine\Root' -Password $password)
```

## Start web app in Docker
The nice feature of running the application as Docker means that we do not need to change the application to honor the certificate.

## The script below can be run using PowerShell
```
docker run `
	-p 4443:443 `
	-e ASPNETCORE_URLS="https://+" `
	-e ASPNETCORE_HTTPS_PORT=443 `
	-e ASPNETCORE_Kestrel__Certificates__Default__Password="password" `
	-e ASPNETCORE_Kestrel__Certificates__Default__Path=/https/mylocal.machine.com.pfx `
	-v $env:USERPROFILE\.aspnet\https:/https/ `
	--name mywebapp `
	mywebapp

```
A few words of explanation:
- `-p 4443:443` - port mapping: maps localhost port `4443` to container's `443` port
- `-e` - [environment variables](https://docs.microsoft.com/en-us/aspnet/core/fundamentals/configuration/?view=aspnetcore-6.0#environment-variables-set-in-generated-launchsettingsjson) like this one .net core 
- `ASPNETCORE_Kestrel__Certificates__Default__Password` - requires a password for the certificate, the same one used for certificate creation
- `ASPNETCORE_Kestrel__Certificates__Default__Path` - location of the certificate is `https` directory and file name is `mylocal.machine.com.pfx` - the same one used during certificate creation
- `-v $env:USERPROFILE\.aspnet\https:/https/` - volume mounted, local directory `$env:USERPROFILE\.aspnet\https` where certificate file was saved to is mounted as `/https/` directory in container
  
## dotnet dev-cert
There is a great tool for creating dev certificates but it only works with localhost domain. Like below:
```
dotnet dev-certs https -ep $env:USERPROFILE\.aspnet\https\aspnetapp.pfx -p crypticpassword
```
If there is a need for special domain name then PowerShell's `New-SelfSignedCertificate` tool does the job.

## Windows hosts file
Local domain needs to be registered in hosts file. 

#### hosts file location
```
c:\Windows\System32\Drivers\etc\hosts
```

#### hosts file sample content
```
127.0.0.1 		mylocal.machine.com
192.168.1.123	host.docker.internal
192.168.1.123	gateway.docker.internal
127.0.0.1 		kubernetes.docker.internal
```


### References
- [Docker with HTTPS](https://docs.microsoft.com/en-us/aspnet/core/security/docker-https?view=aspnetcore-6.0)
- [Self signed certificates](https://docs.microsoft.com/en-us/dotnet/core/additional-tools/self-signed-certificates-guide#with-powershell)