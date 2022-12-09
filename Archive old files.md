```# This script will find all files in the current directory that have not been modified in the last 30 days, and then move them to an "Archived" folder:

$date = (Get-Date).AddDays(-30)
$files = Get-ChildItem | Where-Object {$_.LastWriteTime -lt $date}

if ($files.Count -gt 0) {
  if (!(Test-Path "./Archived")) {
    New-Item -ItemType Directory -Path "./Archived"
  }

  foreach ($file in $files) {
    Move-Item $file.FullName "./Archived"
  }
}
```

To use this script, simply save it as a '.ps1' file and run it in the desired directory using the PowerShell command line. The script will find all files in the current directory that have not been modified in the last 30 days and move them to an "Archived" folder. You can change the number of days to adjust the time frame for which the script will consider files to be "old".
