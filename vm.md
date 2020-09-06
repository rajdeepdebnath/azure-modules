## Virtual Network

```
$vnet = New-AzVirtualNetwork -Name vnet1 -ResourceGroupName test1 -Location 'East US' -AddressPrefix 10.0.0.0/24

$subnet = Add-AzVirtualNetworkSubnetConfig -Name default -VirtualNetwork $vnet -AddressPrefix 10.0.0.0/27

$vnet | Set-AzVirtualNetwork
```

## VM Image
```
Get-AzVMImagePublisher -Location 'East US' | Select PublisherName

Get-AzVMImageOffer -Location 'East US' -PublisherName Canonical

Get-AzVMImageSku -Location 'East US' -PublisherName Canonical -Offer UbuntuServer

Get-AzVMImage -Location 'East US' -PublisherName Canonical -Offer UbuntuServer -Skus 18.04-LTS | Select Version
```

## VM
```
$usr = 'admin1234'
$pwd = ConvertTo-SecureString -String 'Admin@12345678' -AsPlainText -Force
$cred = New-Object System.Management.Automation.PSCredential -ArgumentList $usr,$pwd

$vnet = Get-AzVirtualNetwork -Name vnet1

$subnet = $vnet.Subnets

$publicip = New-AzPublicIpAddress -Name publicip1 -ResourceGroupName test1 -Location 'East US' -Sku Basic -AllocationMethod Dynamic

$nsg = New-AzNetworkSecurityGroup -Name nsg1 -ResourceGroupName test1 -Location 'East US'
$nsg = Add-AzNetworkSecurityRuleConfig -Name rule1 -NetworkSecurityGroup $nsg -Protocol Tcp -SourcePortRange * -SourceAddressPrefix * -DestinationPortRange 80 -DestinationAddressPrefix * `
-Access Allow -Priority 301 -Direction Inbound 
$nsg = Add-AzNetworkSecurityRuleConfig -Name rule2 -NetworkSecurityGroup $nsg -Protocol * -SourcePortRange * -SourceAddressPrefix * -DestinationPortRange 22 -DestinationAddressPrefix * `
-Access Allow -Priority 311 -Direction Inbound 
$nsg | Set-AzNetworkSecurityGroup


$nic = New-AzNetworkInterface -Name nic1 -ResourceGroupName test1 -Location 'East US' -SubnetId $subnet.Id -PublicIpAddressId $publicip.Id
$nic.NetworkSecurityGroup = $nsg
$nic | Set-AzNetworkInterface

$vm = New-AzVMConfig -VMName testvm1 -VMSize 'Standard_B1ls'
$vm = Add-AzVMNetworkInterface -VM $vm -NetworkInterface $nic
$vm = Set-AzVMOperatingSystem -VM $vm -Linux -ComputerName ctest1 -Credential $cred
$vm = Set-AzVMSourceImage -VM $vm -PublisherName Canonical -Offer UbuntuServer -Skus 19.04 -Version 19.04.201908140
$vm = Set-AzVMOSDisk -VM $vm -Name osdisk1 -Caching ReadWrite -CreateOption FromImage -StorageAccountType Standard_LRS

New-AzVM -ResourceGroupName test1 -Location 'East US' -VM $vm

```

## Netwrok Security Group
```
$nsg = New-AzNetworkSecurityGroup -Name nsg1 -ResourceGroupName test1 -Location 'East US'
$nsg = Add-AzNetworkSecurityRuleConfig -Name rule1 -NetworkSecurityGroup $nsg -Protocol Tcp -SourcePortRange * -SourceAddressPrefix * -DestinationPortRange 80 -DestinationAddressPrefix * `
-Access Allow -Priority 301 -Direction Inbound 
$nsg = Add-AzNetworkSecurityRuleConfig -Name rule2 -NetworkSecurityGroup $nsg -Protocol * -SourcePortRange * -SourceAddressPrefix * -DestinationPortRange 22 -DestinationAddressPrefix * `
-Access Allow -Priority 311 -Direction Inbound 
$nsg | Set-AzNetworkSecurityGroup
```

## Subnet
```
$vnet = Get-AzVirtualNetwork -Name vnet1

$subnet = $vnet.Subnets

$subnet
```

## Loab balancer
```
$publicip = Get-AzPublicIpAddress -Name publicip1

$front = New-AzLoadBalancerFrontendIpConfig -Name front1 -PublicIpAddress $publicip

$bp = New-AzLoadBalancerBackendAddressPoolConfig -Name bpool1

$probe = New-AzLoadBalancerProbeConfig -Name hrpobe1 -Protocol Http -Port 80 -RequestPath / -IntervalInSeconds 360 -ProbeCount 5

$rule = New-AzLoadBalancerRuleConfig -Name rule1 -Protocol Tcp -FrontendPort 80 -Probe $probe -BackendPort 80 -FrontendIpConfiguration $front -BackendAddressPool $bp

New-AzLoadBalancer -ResourceGroupName test1 -Name az1 -Sku Basic -Location 'East US' -FrontendIpConfiguration $front -BackendAddressPool $bp -LoadBalancingRule $rule -Probe $probe
```
