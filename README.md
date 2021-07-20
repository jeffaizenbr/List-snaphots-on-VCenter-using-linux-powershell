# List-snaphots-on-VCenter-using-linux-powershell




# Adding repository on CentOS 7


```bash
curl https://packages.microsoft.com/config/rhel/7/prod.repo | sudo tee /etc/yum.repos.d/microsoft.repo
```

# Install PoweShell on Linux


```bash
sudo yum install -y powershell
```

# Install PowerCLI module


```bash
Install-Module -Name VMware.PowerCLI -Scope CurrentUser
```

# Connecting do vcenter server

Connect to powershell console
```bash
pwsh 
```
Ignore de SSL verification
```bash
Set-PowerCLIConfiguration -InvalidCertificateAction:ignore -Scope:User
```
Connect to VCenter
```bash
Connect-VIServer -Server 10.34.53.10 -Protocol https -User XXXXXXXX -Password XXXXXXXXX
```

# List Snapshots or export do TXT file on /tmp path


```bash
Get-VM | Get-Snapshot | select VM, Name, Created | Export-Csv /tmp/snap.txt
```
# Automate steps 

```bash
vim /opt/microsoft/powershell/7/listasnap.ps1
```

```bash
#!/usr/bin/pwsh -Command

Connect-VIServer -Server 10.34.53.10 -Protocol https -User XXXXXXXXXX -Password XXXXXXX

Get-VM | Get-Snapshot | select VM, Created | Export-Csv /opt/microsoft/powershell/7/snapshots.txt
```


```bash
chmod +x /opt/microsoft/powershell/7/listasnap.ps1
```

```bash
vim /etc/crontab
```
```bash
########Listar Snaphots no vcenter, e salvar no caminho /opt/microsoft/powershell/7/snapshots.txt######
30 08 * * * root /opt/microsoft/powershell/7/listasnap.ps1
```


