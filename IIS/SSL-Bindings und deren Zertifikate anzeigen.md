Um eine Liste der SSL-Bindings inklusiver der konfigurierten Zertfifikate zu erhalten geht das über die Powershell:

```console
Import-Module -Name WebAdministration

Get-ChildItem -Path IIS:SSLBindings | ForEach-Object -Process `
{
    if ($_.Sites)
    {
        $certificate = Get-ChildItem -Path CERT:LocalMachine/My |
            Where-Object -Property Thumbprint -EQ -Value $_.Thumbprint

        [PsCustomObject]@{
            Sites                        = $_.Sites.Value
            Hostname                     = $_.Host
            CertificateFriendlyName      = $certificate.FriendlyName
            CertificateDnsNameList       = $certificate.DnsNameList
            CertificateNotAfter          = $certificate.NotAfter
            CertificateIssuer            = $certificate.Issuer
        }
    }
}
```

Dann gibt es eine schöne Liste 😄

Quelle: https://techstronghold.com/scripting/@rudolfvesely/powershell-script-to-get-all-iis-bindings-and-ssl-certificates/
