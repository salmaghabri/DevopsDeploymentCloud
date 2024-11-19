__Work done by: Mohamed Aziz Bellaaj, Louay Badri , Sandra Mourali and Salma Ghabri__
# TASK1

### 1. 2. Files uploaded and RG created
![](TP-1.png)


### 3. VMs provisioned
![](TP-2.png)

### 4. 5. `vnet00_to_vnet01` Peering created
![](TP-3.png)
### 6. 7. Peerings  `vnet00_to_vnet02 ` and  `vnet00_to_vnet02`
![](TP-4.png)
![](TP-5.png)

### 8. 9. 10.  Connection from `vm00` to `vm01` and to `vm02` successful
![](TP-7.png)


### 11.  Connection from  `vm01`  to `vm02` successful
![](TP-8.png)

---
# Task2
### 1. 2. Files uploded and RG created
![](TP-9.png)
### 3. Virtual Network and VMs deployed

![](TP-10.png)

 
### 4. The Network Watcher extension installed
```shell
$location = (Get-AzResourceGroup -ResourceGroupName $rgName).location $vmNames = (Get-AzVM -ResourceGroupName $rgName).Name
foreach ($vmName in $vmNames){
Set-AzVMExtension ` -ResourceGroupName $rgName ` 
-Location $location ` -VMName $vmName `
-Name 'networkWatcherAgent' ` -Publisher 'Microsoft.Azure.NetworkWatcher' `
-Type 'NetworkWatcherAgentWindows' ` 
-TypeHandlerVersion '1.4' }

```

### 5. 6. Resource ID of the virtual networks recorded
![](TP-12.png)

- **vnet01**: `/subscriptions/377d4f37-1b5e-430b-8267-ba81301d4065/resourceGroups/tp2-rg2/providers/Microsoft.Network/virtualNetworks/vnet01`
- **vnet02**: `/subscriptions/377d4f37-1b5e-430b-8267-ba81301d4065/resourceGroups/tp2-rg2/providers/Microsoft.Network/virtualNetworks/vnet02`

### 7. 8. `vnet00` Peerings added
![](TP-14.png)

![](TP-15.png)
![](TP-16.png)

### 9. 10. Network Watcher connectivity checks successful
#### vm01 (`10.61.0.4`) is reachable from vm00

![](TP-17.png)

#### vm02 (`10.62.0.4`) is reachable from vm00
![](TP-18.png)

### 11. Network Watcher vm01 and vm2 connectivity checks unsuccessful
![](TP-19.png)

### 12. nic0 IP forwarding enabled
![](TP-20.png)
### 13.`Remote Access Windows Server `role installed
![](TP-21.png)

### 14. `Routing`role service installed
![](TP-22.png)

### 15. 16 `route12`Route table created
![](TP-23.png)
### 17. `route-vnet1-to-vnet2` route added
![](TP-24.png)

### 18. Subnet associated to the new route
![](TP-25.png)

### 19. `route21`Route table created
![](TP-26.png)

### 20. `route-vnet2-to-vnet1` route added
![](TP-27.png)

### 21. Subnet associated to the new route

![](TP-28.png)

### 22. Connection is now successful between vm01 and vm02

![](TP-29.png)