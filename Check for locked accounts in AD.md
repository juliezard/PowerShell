```# Import the Active Directory module
# Import-Module ActiveDirectory

# Get a list of all locked user accounts
$lockedAccounts = Search-ADAccount -LockedOut

# Check if any accounts are locked
if ($lockedAccounts.Count -eq 0) {
    Write-Output "No accounts are locked"
} else {
    # Output the locked accounts
    foreach ($account in $lockedAccounts) {
        Write-Output "Account: $($account.Name) is locked"
    }
}```
