---
title: Solución de problemas de implementación del modo de Active Directory
titleSuffix: SQL Server Big Data Cluster
description: Solucione problemas de implementación de un clúster de macrodatos de SQL Server en un dominio de Active Directory.
author: rl-msft
ms.author: rafidl
ms.reviewer: mikeray
ms.date: 03/12/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 5d887eadd021641241516a1478c6ac13e0d0bdec
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "79191216"
---
# <a name="troubleshoot-sql-server-big-data-cluster-active-directory-mode-deployment"></a>Solución de problemas de implementación del modo de Active Directory de un clúster de macrodatos de SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En este artículo se explica cómo solucionar problemas de implementación de un clúster de macrodatos de SQL Server en el modo de Active Directory.

## <a name="check-deployment-progress"></a>Comprobación del progreso de la implementación

La implementación puede tardar varios minutos. Si el clúster no está listo después de 15 minutos, compruebe los registros del controlador para obtener más detalles.

Mientras se implementa el clúster, compruebe los pods.

```console
kubectl get pods -n mssql-cluster
```

Compruebe que la lista de pods que se devuelve incluye lo siguiente:

- `compute-`$
- `data-`
- `storage-`

Si no se crean los pods de proceso, datos y almacenamiento, compruebe los registros para identificar el motivo.

## <a name="check-logs"></a>Compruebe los registros

Para identificar por qué se ha salido de la implementación sin crear los pods de proceso, de datos o de almacenamiento, compruebe los registros siguientes: 

- Compruebe `controller.log` (`<folderOfDebugCopyLog>\debuglogs-mssql-cluster-20200219-093941\mssql-cluster\control-<suffix>\controller\controller\<date>\controller.log`). Busque la entrada siguiente:

  `WARN | StatefulSet master is not ready with 0 ready pods and 3 unready pods `

- Comprobación de `master-0` `provisioner.log` (`<folderOfDebugCopyLog>\debuglogs-mssql-cluster-20200219-093941\mssql-cluster\master-0\mssql-server\provisioner\provisioner.log`)

  ```
  ERROR | Failed to create sql login for domain user [<domain>.<top-level-domain>\<domain-group>]
    Traceback (most recent call last):
      File "/opt/provisioner/bin/scripts/provisioningpool.py", line 214, in executeNonQueries
        connection.execute_non_query(command)
      File "src/_mssql.pyx", line 1033, in _mssql.MSSQLConnection.execute_non_query
      File "src/_mssql.pyx", line 1061, in _mssql.MSSQLConnection.execute_non_query
      File "src/_mssql.pyx", line 1634, in _mssql.check_and_raise
      File "src/_mssql.pyx", line 1683, in _mssql.maybe_raise_MSSQLDatabaseException
    _mssql.MSSQLDatabaseException: (15401, b"Windows NT user or group '<domain>.<top-level-domain>\\<domain-group>' not found. Check the name again.DB-Lib error message 20018, severity 16:\nGeneral SQL Server error: Check messages from the SQL Server\n")
  WARNING | [3/3] Provisioning exception occurred during provisioning step: ProvisioningMasterPool.
  WARNING | Failed to create sql login for domain user [<domain>.<top-level-domain>\<domain-group>]
  WARNING | Retrying.
  ```

  En el ejemplo anterior, se produce un error en la implementación al crear un inicio de sesión para el usuario del dominio porque el ámbito del grupo de dominio es el dominio local. Use grupos con ámbito de dominio global o universal. En [Implementación de [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] en modo de Active Directory](deploy-active-directory.md) se explican los requisitos de ámbito de los grupo de AD.

## <a name="check-the-scope-of-domain-groups"></a>Compruebe el ámbito de los grupos de dominio.

Compruebe el ámbito del grupo de dominio (<`domain-group`>). Use [get-adgroup](/powershell/module/addsadministration/get-adgroup/).

Si el ámbito de grupo `<domain-group>` es dominio local (`DomainLocal`), se produce un error en la implementación. 

El script de PowerShell siguiente comprueba el ámbito de dos grupos de AD denominados `bdcadmins` y `bdcusers`. Reemplace los nombres por los nombres de los grupos. 

```powershell
#Administrators and users AD groups
$Cluster_admins_group='bdcadmins'
$Cluster_users_group='bdcusers'

#Performing AD Group Checks...

#AD admin group Check
$ClusterAdminGroupScope_Result = New-Object System.Collections.ArrayList
try {
    $GroupScope = Get-ADgroup -Identity $Cluster_admins_group | Select-Object -ExpandProperty GroupScope
    
    if ($GroupScope -eq 'DomainLocal') {
        [void]$ClusterAdminGroupScope_Result.Add("Misconfiguration - $Cluster_admins_group Group scope is $GroupScope, this scope is not supported, Please change group scope to either Global or Univesal") 
    }
    else {
        [void]$ClusterAdminGroupScope_Result.Add("OK - $Cluster_admins_group Group scope is $GroupScope")
    }
}
catch {
    [void]$ClusterAdminGroupScope_Result.Add("Error - " + $_.exception.message)
}
#Ad users group check
$ClusterUsersGroupScope_Result = New-Object System.Collections.ArrayList
$GroupScope = ''
try {
    $GroupScope = Get-ADgroup -Identity $Cluster_users_group | Select-Object -ExpandProperty GroupScope
    
    if ($GroupScope -eq 'DomainLocal') {
        [void]$ClusterUsersGroupScope_Result.Add("Misconfiguration - $Cluster_users_group Group scope is $GroupScope, this scope is not supported, Please change group scope to either Global or Univesal")
    } 
    else 
    { [void]$ClusterUsersGroupScope_Result.Add("OK - $Cluster_users_group Group scope is $GroupScope") }
}
catch {
    [void]$ClusterUsersGroupScope_Result.Add("Error - " + $_.exception.message)
}

#Display the results
$ClusterUsersGroupScope_Result
```

## <a name="check-security-support-container"></a>Comprobación del contenedor de compatibilidad de seguridad 

Revise los registros de contenedor de compatibilidad de seguridad.

El comando siguiente recopila los registros de compatibilidad de seguridad en un clúster en el espacio de nombres `mssql-cluster`.

```console
azdata bdc debug copy-logs -n mssql-cluster -c security-support
```

Extraiga los registros y busque `\mssql-cluster\control-<identifier>\controller\control-rts5t-controller-stdout.log`.

Busque las entradas siguientes en el registro:

```
ERROR    | Failed to create AD user account 'cntrl-controller'. Error code: 53. Message: Failed to create user object: Failed to add object 'CN=cntrl-controller,OU=bdc, DC=CONTOSO, DC=com' to '  <domain>.<top-level-domain>  ': Server is unwilling to perform. 
ERROR | Failed to create AD user account 'ldap-user'. Error code: 53. Message: Failed to create user object: Failed to add object 'CN=ldap-user,OU=bdc, DC=CONTOSO, DC=com' to '  <domain>.<top-level-domain>  ': Server is unwilling to perform. 
ERROR | Failed to create AD user account 'nginx-mgmtproxy'. Error code: 53. Message: Failed to create user object: Failed to add object 'CN=nginx-mgmtproxy,OU=bdc, DC=CONTOSO, DC=com' to '  <domain>.<top-level-domain>  ': Server is unwilling to perform.
```

Estas entradas se pueden producir cuando en el servidor DNS del controlador de dominio falta la entrada de DNS inverso (registro PTR).

## <a name="verify-reverse-lookup-ptr-record"></a>Comprobación de la búsqueda inversa (registro PTR)
    
Ejecute el script de PowerShell siguiente para confirmar si tiene configurada una entrada de DNS inverso (registro PTR).

```powershell
#Domain Controller FQDN 'DCserver01.contoso.local'
$Domain_controller_FQDN = 'DCserver01.contoso.local'

#Performing Domain Controller DNS record, reverse PTR Checks...
$DcControllerDnsPtr_Result = New-Object System.Collections.ArrayList
try {
    $Domain_controller_DNS_Record = Resolve-DnsName $Domain_controller_FQDN -Type A -Server $Domain_DNS_IP_address -ErrorAction Stop
    foreach ($ip in $Domain_controller_DNS_Record.IPAddress) {
        #resolving hostname by IP address to make sure we have reverse PTR record 
        if ((Resolve-DnsName $ip).NameHost -eq $Domain_controller_FQDN) {
            [void]$DcControllerDnsPtr_Result.add("OK - $Domain_controller_FQDN has an A record with an IP $ip, Reverse PTR record is in place") 
        }
        else {
            [void]$DcControllerDnsPtr_Result.add("Missing - $Domain_controller_FQDN has an A record with an IP $ip, But no reverse PTR record was found for the host")
        }
    }
}
catch {
    [void]$DcControllerDnsPtr_Result.add("Error - " + $_.exception.message)
}

#show the results 
$DcControllerDnsPtr_Result
```

[Comprobación de la entrada de DNS inverso (registro PTR) para el controlador de dominio](deploy-active-directory.md#verify-reverse-dns-entry-for-domain-controller).