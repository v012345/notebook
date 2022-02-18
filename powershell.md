## allow PowerShell execute unsigned script
### Step 1
> Start Windows PowerShell with the "Run as Administrator" option
### Step 2
> run the below command  
> `set-executionpolicy remotesigned`

## kill by process name
```powershell
taskkill /IM "nginx.exe" /F
```

