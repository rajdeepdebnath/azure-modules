# azure-modules

Install-Module Az.Accounts `(To connect to azure)`

Install-Module Az.Advisor                

Install-Module Az.Aks                     

Install-Module Az.AnalysisServices        

Install-Module Az.ApiManagement          

Install-Module Az.ApplicationInsights     

Install-Module Az.Automation              

Install-Module Az.Batch                   

Install-Module Az.Billing                 

Install-Module Az.Cdn                     

Install-Module Az.CognitiveServices       

Install-Module Az.Compute          `(To create\manage vm)`        

Install-Module Az.ContainerInstance       

Install-Module Az.ContainerRegistry       

Install-Module Az.DataBoxEdge             

Install-Module Az.DataFactory             

Install-Module Az.DataLakeAnalytics       

Install-Module Az.DataLakeStore           

Install-Module Az.DataShare               

Install-Module Az.DesktopVirtualization   

Install-Module Az.DeploymentManager       

Install-Module Az.DevTestLabs             

Install-Module Az.Dns                     

Install-Module Az.EventGrid               

Install-Module Az.EventHub                

Install-Module Az.FrontDoor              

Install-Module Az.Functions            

Install-Module Az.HDInsight               

Install-Module Az.HealthcareApis          

Install-Module Az.IotHub                  

Install-Module Az.KeyVault                

Install-Module Az.LogicApp                

Install-Module Az.MachineLearning         

Install-Module Az.Maintenance             

Install-Module Az.ManagedServices         

Install-Module Az.MarketplaceOrdering     

Install-Module Az.Media             

Install-Module Az.Monitor                 

Install-Module Az.Network               

Install-Module Az.NotificationHubs        

Install-Module Az.OperationalInsights     

Install-Module Az.PolicyInsights          

Install-Module Az.PowerBIEmbedded         

Install-Module Az.PrivateDns              

Install-Module Az.RecoveryServices        

Install-Module Az.RedisCache           

Install-Module Az.Relay              

Install-Module Az.Resources         

Install-Module Az.ServiceBus          

Install-Module Az.ServiceFabric           

Install-Module Az.SignalR             

Install-Module Az.Sql             

Install-Module Az.SqlVirtualMachine       

Install-Module Az.Storage       

Install-Module Az.StorageSync     

Install-Module Az.StreamAnalytics   

Install-Module Az.Support       

Install-Module Az.TrafficManager   

Install-Module Az.Websites  



# Uninstall Azure modules

```
workflow Uninstall-AzureModules
{
    $Modules = (Get-Module -ListAvailable Az*).Name |Get-Unique
    Foreach -parallel ($Module in $Modules)
    { 
        Write-Output ("Uninstalling: $Module")
        Uninstall-Module $Module -Force
    }
}

Uninstall-AzureModules

Uninstall-AzureModules
```

[Thanks](https://stackoverflow.com/a/50297028/9648252)
