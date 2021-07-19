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

```bash
pwsh 
```

```bash
Connect-VIServer -Server vcenter01 -User admin -Password pass
```

# List Snapshots or export do TXT file on /tmp path


```bash
get-vm -location “My lab” | get-snapshot | format-list
```

or

```bash
Get-Datacenter "YOURDATACENTERNAMEONVCENTER" |Get-VM |Get-Snapshot | Select vm, Name, Description, PowerState | Export-Csv /tmp/snapshot.txt
```
