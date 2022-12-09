# PowerShell


Get connected:
- ```Connect-EXOPSSession -UserPrincipalName user@domain.com```
- ```Connect-ExchangeOnline```

- ```Connect_AzureAD -Confirm```
- ``` $Credential = Get-CredentialConnect_AzureAD -Confirm``` 
disconnect
- ```Get-PSSession | Remove-PSSession```

o365 powershell calander
website with info ***https://theitbros.com/add-calendar-permissions-in-office-365-via-powershell/***

- ```Add-MailboxFolderPermission username:\calendar –user username –accessrights reviewer```
- ```Set-MailboxFolderPermission username:\calendar –user username –accessrights reviewer```
- ```Remove-MailboxFolderPermission user.name:\calendar –user user.name```



**Default for all users**

```$users = Get-Mailbox -Resultsize Unlimited
foreach ($user in $users) {
Write-Host -ForegroundColor green "Setting permission for $($user.alias)..."
Set-MailboxFolderPermission -Identity "$($user.alias):\calendar" -User Default -AccessRights Reviewer
}


Get connected:
Connect-EXOPSSession -UserPrincipalName user@domain.com

Export Rules:
Get-Mailbox -ResultSize Unlimited | % { Get-InboxRule -Mailbox $_.Alias | Select Enabled,Name,Priority,From,SentTo,CopyToFolder,DeleteMessage,ForwardTo,MarkAsRead,MoveToFolder,RedirectTo,@{Expression={$_.SendTextMessageNotificationTo};Label="SendTextMessageNotificationTo"},MailboxOwnerId } | Export-Csv C:\Users\username\Desktop\it\o365\forwards.csv -NoTypeInformation


Update user data
 $user_file | ForEach {Set-user $_.login_name -Title $_.title -Department $_.department -Office $_.office -Manager $_.manager}

set user data
$user_file | ForEach {Set-user $_.login_name -Title $_.title -Department $_.department -Manager $_.manager -StreetAddress $_.Address -StateOrProvince $_.State -City $_.City -PostalCode $_.Zip} 
$user_file | ForEach {Set-AzureADuser -ObjectId $_.login_name -TelephoneNumber $_.Work -Mobile $_.Mobile}

get list of blocked users...remove manager
Get-MsolUser -All | Where {$_.BlockCredential -eq $True} | Select UserPrincipalName | Export-CSV "C:\Users\username\Desktop\it\o365\blocked.csv"
$user_file | ForEach {Set-user -Identity $_.login_name -Manager $Null}
$user_file = Import-CSV "C:\Users\username\Desktop\it\o365\blocked.csv"

Update distro
Add-DistributionGroupMember -Identity "distrubutionlistname" -Member "user@domain.com"

$user_file = Import-CSV distroHouston.csv
$user_file | ForEach {Add-DistributionGroupMember -Identity "allhouston" -Member $_.member}

Unblock-File -Path C:\Downloads\script1.ps1
