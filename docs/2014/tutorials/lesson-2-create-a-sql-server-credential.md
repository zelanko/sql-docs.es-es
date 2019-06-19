---
title: 'Lección 2: Crear una credencial SQL Server | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
ms.assetid: 64f8805c-1ddc-4c96-a47c-22917d12e1ab
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: fbea11b0500c075105bff885cdb1cd8264b320d6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62931635"
---
# <a name="lesson-2-create-a-sql-server-credential"></a>Lección 2: Crear una credencial de SQL Server
  **Credencial:** Una credencial de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] es un objeto que se usa para almacenar la información de autenticación necesaria para conectarse a un recurso fuera de SQL Server.  Aquí, los procesos de copia de seguridad y restauración de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usan credenciales para autenticarse en el servicio de almacenamiento Blob de Windows Azure. La credencial contiene los valores de nombre y la **clave de acceso** de la cuenta de almacenamiento. Una vez creada la credencial, se debe especificar en la opción WITH CREDENTIAL al emitir las instrucciones BACKUP y RESTORE. Para obtener más información sobre cómo ver, copiar o regenerar **access keys**de cuentas de almacenamiento, vea [Ver, copiar y regenerar las claves de acceso de una cuenta de almacenamiento de Windows Azure](https://msdn.microsoft.com/library/windowsazure/hh531566.aspx).  
  
 Para obtener información general sobre las credenciales, vea [Credenciales](../relational-databases/security/authentication-access/credentials-database-engine.md).  
  
 Para obtener información sobre otros ejemplos donde se usan credenciales, vea [Crear un proxy del Agente SQL Server](../ssms/agent/create-a-sql-server-agent-proxy.md).  
  
> [!IMPORTANT]  
>  Los requisitos para crear una credencial de SQL Server que se describe a continuación son específicos para procesos de copia de seguridad de SQL Server ([copias de seguridad de SQL Server a URL](../relational-databases/backup-restore/sql-server-backup-to-url.md), y [Copia de seguridad administrada de SQL Server en Windows Azure](../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md)). Cuando SQL Server obtiene acceso al Almacenamiento de Azure para escribir o leer copias de seguridad, usa el nombre de la cuenta de almacenamiento y la información de la clave de acceso.  Para obtener más información sobre cómo crear credenciales para almacenar archivos de base de datos de almacenamiento de Azure, consulte [lección 3: Crear una credencial SQL Server](../relational-databases/lesson-2-create-a-sql-server-credential-using-a-shared-access-signature.md)  
  
## <a name="create-a-sql-server-credential"></a>Crear una credencial de SQL Server  
 Para crear una credencial de SQL Server, siga estos pasos:  
  
1.  Conéctese a SQL Server Management Studio.  
  
2.  En el Explorador de objetos, conéctese a la instancia del motor de base de datos que tiene instalada la base de datos AdventureWorks2012 o use su propia base de datos para este tutorial.  
  
3.  En la barra de herramientas **Estándar** , haga clic en **Nueva consulta**.  
  
4.  Copie y pegue el ejemplo siguiente en la ventana de consulta, y modifíquelo como sea necesario.  
  
    ```  
    CREATE CREDENTIAL mycredential   
    WITH IDENTITY= 'mystorageaccount' - this is the name of the storage account you specified when creating a storage account (See Lesson 1)   
    , SECRET = '<storage account access key>' - this should be either the Primary or Secondary Access Key for the storage account (See Lesson 1)  
  
    ```  
  
     ![asignación de cuenta de almacenamiento a las credenciales de sql](../../2014/tutorials/media/backuptocloud-storage-credential-mapping.gif "asignar la cuenta de almacenamiento a las credenciales de sql")  
  
5.  Compruebe la instrucción T-SQL y haga clic en **Ejecutar**.  
  
 Para obtener más información sobre el servicio de almacenamiento Blob de Windows Azure para conceptos de copia de seguridad y los requisitos, consulte [Copia de seguridad y restauración de SQL Server con el servicio de almacenamiento Blob de Windows Azure](../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md).  
  
### <a name="next-lesson"></a>Lección siguiente  
 [Lección 3: Escribir una copia de seguridad de base de datos completa en el servicio de Windows Azure Blob Storage](../../2014/tutorials/lesson-3-write-a-full-database-backup-to-the-windows-azure-blob-storage-service.md).  
  
  
