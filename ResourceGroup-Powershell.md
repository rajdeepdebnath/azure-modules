# Resource group

```
New-AzResourceGroup -Name $NewResourceGroupName -Location $location

Get-AzResourceGroup -Name $ResourceGroupName

Remove-AzResourceGroup -Name $ResourceGroupName
```

### Resource lock
```
New-AzResourceLock -LockName $Lock_Name -LockLevel $Lock_Level -ResourceGroupName -$ResourceGroup_Name

Get-AzResourceLock

Remove-AzResourceLock -LockName $Lock_Name -ResourceGroupName $Resource_Group_Name
```

### Azure locations
```
centralus,eastasia,southeastasia,eastus,eastus2,westus,westus2,northcentralus,southcen
tralus,westcentralus,northeurope,westeurope,japaneast,japanwest,brazilsouth,australiasoutheast,australiaeast,westindia,southindia,centralindia,canadacentral,canadaeast,uksouth,ukwest,koreacentral,koreasou
th,francecentral,southafricanorth,uaenorth,australiacentral,switzerlandnorth,germanywestcentral,norwayeast
```

### Azure Subscription
```
Get-AzSubscription

$context = Get-AzSubscription -SubscriptionId [your_subscription_id]
Set-AzContext $context
```
