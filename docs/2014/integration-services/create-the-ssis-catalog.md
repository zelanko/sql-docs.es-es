---
title: Crear el catálogo de SSIS | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 6ed56d36-18d9-40c2-b51f-f2a4c71d1e73
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f8db507966f9b3323e415ca7f2abfe4a12601c1c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "72798018"
---
# <a name="create-the-ssis-catalog"></a>Crear el catálogo de SSIS
  Después de diseñar y probar paquetes en [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], puede implementar los proyectos que contienen los paquetes en un servidor de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . Para poder implementar los proyectos en el servidor de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], el servidor debe contener el catálogo de `SSISDB`. El programa de instalación de [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] no crea automáticamente el catálogo; es necesario crear manualmente el catálogo usando las instrucciones siguientes.  
  
 Puede crear el catálogo de SSISDB en [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. También crea el catálogo mediante programación con Windows PowerShell.  
  
### <a name="to-create-the-ssisdb-catalog-in-sql-server-management-studio"></a>Para crear un catálogo de SSISDB en SQL Server Management Studio  
  
1.  Abra [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
2.  Conéctese al motor de base de datos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
3.  En el Explorador de objetos, expanda el nodo del servidor, haga clic con el botón derecho en el nodo **Catálogos de Integration Services** y, después, haga clic en **Crear catálogo**.  
  
4.  Haga clic en **Habilitar integración con CLR**.  
  
     El catálogo usar los procedimientos almacenados de CLR.  
  
5.  Haga clic en **Habilitar la ejecución automática del procedimiento almacenado de Integration Services al iniciar SQL Server** para permitir que el procedimiento almacenado [catalog.startup](/sql/integration-services/system-stored-procedures/catalog-startup) se ejecute cada vez que se reinicie la instancia del servidor de [!INCLUDE[ssIS](../includes/ssis-md.md)] .  
  
     El procedimiento almacenado realiza el mantenimiento del estado de las operaciones del catálogo de SSISDB. Corrige el estado de los paquetes que estaban en ejecución si y cuando la instancia del servidor de [!INCLUDE[ssIS](../includes/ssis-md.md)] se bloquea.  
  
6.  Escriba una contraseña y haga clic en **Aceptar**.  
  
     La contraseña protege la clave maestra de la base de datos que se usar para cifrar los datos del catálogo. Guarde la contraseña en un lugar seguro. Se recomienda que haga también una copia de seguridad de la clave maestra de la base de datos. Para más información, consulte [Back Up a Database Master Key](../relational-databases/security/encryption/back-up-a-database-master-key.md).  
  
### <a name="to-create-the-ssisdb-catalog-programmatically"></a>Para crear el catálogo de SSISDB mediante programación  
  
1.  Ejecute el siguiente script de PowerShell:  
  
    ```powershell
    # Load the IntegrationServices Assembly  
    [Reflection.Assembly]::LoadWithPartialName("Microsoft.SqlServer.Management.IntegrationServices")  
  
    # Store the IntegrationServices Assembly namespace to avoid typing it every time  
    $ISNamespace = "Microsoft.SqlServer.Management.IntegrationServices"  
  
    Write-Host "Connecting to server ..."  
  
    # Create a connection to the server  
    $sqlConnectionString = "Data Source=localhost;Initial Catalog=master;Integrated Security=SSPI;"  
    $sqlConnection = New-Object System.Data.SqlClient.SqlConnection $sqlConnectionString  
  
    # Create the Integration Services object  
    $integrationServices = New-Object $ISNamespace".IntegrationServices" $sqlConnection  
  
    # Provision a new SSIS Catalog  
    $catalog = New-Object $ISNamespace".Catalog" ($integrationServices, "SSISDB", "P@assword1")  
    $catalog.Create()
    ```  
  
     Para obtener más ejemplos de cómo usar Windows PowerShell y el espacio de nombres <xref:Microsoft.SqlServer.Management.IntegrationServices>, vea la entrada del blog [SSIS and PowerShell in SQL Server 2012](https://go.microsoft.com/fwlink/?LinkId=242539) (SSIS y PowerShell en SQL Server 2012), en blogs.msdn.com. Para obtener información general sobre el espacio de nombres y ejemplos de código, vea la entrada del blog sobre el [Modelo de objetos administrados del catálogo de SSIS](https://go.microsoft.com/fwlink/?LinkId=254267)en blogs.msdn.com.  
  
## <a name="see-also"></a>Consulte también  
 [Catálogo de SSIS](catalog/ssis-catalog.md)   
 [Copia de seguridad, restauración y traslado del catálogo de SSIS](../../2014/integration-services/backup-restore-and-move-the-ssis-catalog.md)  
