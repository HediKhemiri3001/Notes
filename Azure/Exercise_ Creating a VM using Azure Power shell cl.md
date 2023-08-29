# Create a vm:
The following are commandlets used in powershell to create an Azure VM resource:
> `New-AzVm -ResourceGroupName learn-97f16455-5c11-4fce-bbf7-a0b74717cd18 -Name "testvm-eus-01" -Credential (Get-Credential) -Location "eastus" -Image Canonical:0001-com-ubuntu-server-focal:20_04-lts:latest -OpenPorts 22 -PublicIpAddressName "testvm-eus-01"`

Get the vm as an object ( . accessible):
>`$vm = (Get-AzVM -Name "testvm-eus-01" -ResourceGroupName learn-97f16455-5c11-4fce-bbf7-a0b74717cd18)`
> Now we can access attributes using: `$vm.smthng`

Get the public Ip-Address of a vm :
> `Get-AzPublicIpAddress -ResourceGroupName learn-97f16455-5c11-4fce-bbf7-a0b74717cd18 -Name "testvm-eus-01"`

# Delete a vm:
First we stop it 
>`Stop-AzVM -Name $vm.Name -ResourceGroupName $vm.ResourceGroupName`

Then we remove it:
>`Remove-AzVM -Name $vm.Name -ResourceGroupName $vm.ResourceGroupName`

Although we removed the VM, all the other ressources created automatically for the VM won't be deleted, to check the list we do :
>`Get-AzResource -ResourceGroupName $vm.ResourceGroupName | Format-Table`

And so we have to delete the network interface like so :
>`$vm | Remove-AzNetworkInterface –Force`

And then the disk:
>`Get-AzDisk -ResourceGroupName $vm.ResourceGroupName -DiskName $vm.StorageProfile.OSDisk.Name | Remove-AzDisk -Force`

Next, delete the virtual network:
>`Get-AzVirtualNetwork -ResourceGroupName $vm.ResourceGroupName | Remove-AzVirtualNetwork -Force`

Delete the network security group:
>`Get-AzNetworkSecurityGroup -ResourceGroupName $vm.ResourceGroupName | Remove-AzNetworkSecurityGroup -Force`

And finally, delete the public IP address:
>`Get-AzPublicIpAddress -ResourceGroupName $vm.ResourceGroupName | Remove-AzPublicIpAddress -Force`
