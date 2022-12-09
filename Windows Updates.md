1) This will install the Windows Update module in PowerShell.

```Install-Module PSWindowsUpdate```

2) This command will check for updates.

```Get-WindowsUpdate```

3) This command will install the available updates (which were listed in step 2)

```Install-WindowsUpdate```


```
# This script will check for any pending Windows updates and install them automatically

# First, check for pending updates
$updates = Get-WindowsUpdate

# If there are no pending updates, display a message and exit the script
if ($updates.Count -eq 0) {
    Write-Output "No pending updates"
    exit
}

# If there are pending updates, install them automatically
Write-Output "Installing pending updates"
$updates | Install-WindowsUpdate

# Check for any failed updates and display a message if any were found
$failedUpdates = Get-WindowsUpdate -ErrorAction SilentlyContinue | Where-Object {$_.ResultCode -ne "Ok"}
if ($failedUpdates.Count -gt 0) {
    Write-Output "The following updates failed to install:"
    $failedUpdates | Select-Object -Property Title, ResultCode
} else {
    Write-Output "All updates were installed successfully"
}
```

This script can be run on a Windows system to check for any pending updates and install them automatically. It also checks for any failed updates and displays a message if any were found.
