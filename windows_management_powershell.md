## CMD tips:

``` 
wmic useraccount where name="UID" get SID

wmic product where "name like'%%office%%'" get name,version
``````
 

List logged in users: 
```
query session
```

 

```
C:\Users\user>query session

SESSIONNAME       USERNAME                 ID  STATE   TYPE        DEVICE

services                                    0  Disc

>console           user                  1  Active


…    logoff 1  (number is query )
```

Change cmd prompt look:
 
```
C:\Users\user>prompt $D$S$T$_$V$_$P$_$G

Fri 08/04/2023  8:05:02.82
Microsoft Windows [Version 10.0.19044.3208]

C:\Users\user
>prompt

 C:\Users\user>

```

## File Management with Powershell:

Get permissions of the file or directory:
```
$permissions = Get-Acl "<file or folder>"

$permissions | format-list

$permissions.Access

``` 

Set permissions to file or directory:
``` 
$acl = Get-Acl "<file or folder>"

$permission = "Administrator","FullControl","Allow"

$accessRule = New-Object System.Security.AccessControl.FileSystemAccessRule $permission

$acl.SetAccessRule($accessRule)

Set-Acl "<file or folder>" $acl
``` 
```
Content management:

Create content:

Set-content -Path “<path>” -Value “Value”
```
List content:
```
Get-content -Path “<path>”
```
Add content:
```
Add-content -Path “<path>”
```


## System Management:


Systeminformation:

```
$computerinfo = Get-ComputerInfo

$computerinfo.OsArchitecture
```
 
Processes:
 
Find the process:
``` 
Get-Process -Name taskmgr | Format-List

Get-Process | Where-Object -Property "ProcessName" -EQ "taskmgr"
```
 
Find process if you are not sure about exact name:
```
Get-Process | Where-Object -Property "ProcessName" -Like "t*"
```

List only specific properties:
```
Get-Process | Format-Table -Property Name, ID
```

Start the process:
```
Start-Process -FilePath "C:\Windows\System32\notepad.exe"
```

Start process with working directory:
```
Start-Process -FilePath "C:\Windows\System32\notepad.exe" -WorkingDirectory "C:\Users\adambiro\Desktop\ccctestfolder\"
```

Stop process:
```
Stop-Process -Name "notepad"
```

Service management:

Find service with exact name:
``` 
Get-Service -Name "PrintNotify"
```

Format the output :
```
Get-Service | Format-Table -Property DisplayName, Status
```

List running services:
```
Get-Service | Where-Object -Property Status -EQ "Running"
```

Stopping services:
```
Stop-Service -Name “service name”
```

Start-service:
```
Start-service -Name “service name”
``` 

Restart-service:
```
Restart-service -Name “service name”
```
 
Volume management:

List volumes:
```
Get-Volume
```
 
Info about specific volume:

```
Get-Volume -DriveLetter C | Format-List

$cdrive = Get-Volume -DriveLetter C

$cdrive.SizeRemaining

$cdrive.SizeRemaining/1GB
```

delete stuff in recycle bin: 
```
Clear-recyclebin
```