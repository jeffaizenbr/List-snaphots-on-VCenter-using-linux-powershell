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
pwsh 
```
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

# List Snapshots and export a TXT file on /tmp/snap.txt


```bash
Get-VM | Get-Snapshot | select VM, Name, Created | Export-Csv /tmp/snap.txt
```
# Automate steps 

Creating listasnap.ps1
```bash
vim /opt/microsoft/powershell/7/listasnap.ps1
```
Copy pwsh script
```bash
#!/usr/bin/pwsh -Command

Connect-VIServer -Server 10.34.53.10 -Protocol https -User XXXXXXXXXX -Password XXXXXXX

Get-VM | Get-Snapshot | select VM, Created | Export-Csv /opt/microsoft/powershell/7/snapshots.txt
```

giving permission the execution
```bash
chmod +x /opt/microsoft/powershell/7/listasnap.ps1
```
put the task on crontab
```bash
vim /etc/crontab
```
copy on crontab file
```bash
########Listar Snaphots no vcenter, e salvar no caminho /opt/microsoft/powershell/7/snapshots.txt######
30 08 * * * root /opt/microsoft/powershell/7/listasnap.ps1
```


