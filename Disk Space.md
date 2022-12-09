The 'Get-WmiObject' cmdlet is used to query the Windows Management Instrumentation (WMI) database on a remote computer, but it requires that the WMI service is running on the remote computer and that the user running the script has the necessary permissions to access the WMI database.

If the WMI service is not running on the remote computer, or if the user does not have the necessary permissions, the Get-WmiObject cmdlet will not be able to retrieve the disk usage information and will return zero values for the free and total space.

To fix this issue, you can try the following steps:

1. Make sure that the WMI service is running on the remote computer. To do this, you can log in to the remote computer and check the status of the WMI service in the Services management console (services.msc). The WMI service should be set to "Automatic" startup type and should be in the "Running" state.

2. Make sure that the user running the script has the necessary permissions to access the WMI database on the remote computer. To do this, you can grant the user the "Remote Enable" permission on the WMI namespace on the remote computer. You can use the wmic command-line tool to grant this permission, like this:

Copy code

```wmic /node:<remote computer name> /namespace:\\root\cimv2 path __SystemSecurity call PutACE 'user:<user name>','Remote Enable','allow'```

Replace <remote computer name> with the name of the remote computer, and <user name> with the name of the user who will be running the script. This will grant the "Remote Enable" permission on the WMI namespace to the specified user.
  
```
# Get the remote computer name from the user
$computer = Read-Host "Enter the name of the remote computer"

# Get the threshold for the minimum amount of free disk space (in GB)
$threshold = Read-Host "Enter the minimum amount of free disk space (in GB)"

# Get the current disk usage on the remote computer
$disk = Get-WmiObject -Class Win32_LogicalDisk -Filter "DeviceID='C:'" -ComputerName $computer

# Calculate the current free disk space in GB
$freeSpace = [Math]::Round(($disk.FreeSpace / 1GB), 2)

# Calculate the total disk space in GB
$totalSpace = [Math]::Round(($disk.Size / 1GB), 2)

# Display the free and total disk space
Write-Host "Free space on ${computer}: $freeSpace GB"
Write-Host "Total space on ${computer}: $totalSpace GB"


# Check if the free disk space is below the threshold
if ($freeSpace -lt $threshold)
{
    # If the free disk space is below the threshold, send an alert
    Write-Host "Low disk space alert! Free space on $computer is $freeSpace GB"
}
else
{
    # If the free disk space is above the threshold, display a message
    Write-Host "There is enough free space on $computer"
}
```
