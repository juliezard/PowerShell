```# This script prompts the user for a computer name and then pings the computer to check if it is online. If the computer is online, it displays the IP address and the response time.

# Prompt the user for a computer name
$computer = Read-Host "Enter a computer name"

# Ping the computer and store the results in a variable
$ping = Test-Connection $computer -Count 1

# Check if the ping was successful
if ($ping.StatusCode -eq 0) {
  # Display the IP address and the response time
  "Computer is online. IP address: $($ping.IPV4Address) Response time: $($ping.ResponseTime) ms"
} else {
  # Display an error message
  "Unable to ping computer. Check the name and try again."
}
```
