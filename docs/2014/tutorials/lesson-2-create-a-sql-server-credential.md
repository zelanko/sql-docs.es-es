---
title: 'Lección 2: Crear una credencial de SQL Server | Microsoft Docs'
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
ms.openlocfilehash: baa337d33173f292145d92b60d6192af2a716c5e
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2019
ms.locfileid: "70154328"
---
# <a name="lesson-2-create-a-sql-server-credential"></a>Lección 2: Crear una credencial de SQL Server
  **Credencial:** Una credencial de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] es un objeto que se usa para almacenar la información de autenticación necesaria para conectarse a un recurso fuera de SQL Server.  Aquí, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] los procesos de copia de seguridad y restauración usan credenciales para autenticarse en el servicio de almacenamiento de blobs de Azure. La credencial contiene los valores de nombre y la **clave de acceso** de la cuenta de almacenamiento. Una vez creada la credencial, se debe especificar en la opción WITH CREDENTIAL al emitir las instrucciones BACKUP y RESTORE. Para obtener más información sobre cómo ver, copiar o regenerar **access keys**de cuentas de almacenamiento, vea [Ver, copiar y regenerar las claves de acceso de una cuenta de almacenamiento de Windows Azure](https://msdn.microsoft.com/library/windowsazure/hh531566.aspx).  
  
 Para obtener información general sobre las credenciales, vea [Credenciales](../relational-databases/security/authentication-access/credentials-database-engine.md).  
  
 Para obtener información sobre otros ejemplos donde se usan credenciales, vea [Crear un proxy del Agente SQL Server](../ssms/agent/create-a-sql-server-agent-proxy.md).  
  
> [!IMPORTANT]  
>  Los requisitos para crear una SQL Server credenciales que se describen a continuación son específicos de SQL Server procesos de copia de seguridad ([SQL Server copia de seguridad en la dirección URL](../relational-databases/backup-restore/sql-server-backup-to-url.md)y [SQL Server copia de seguridad administrada en Azure](../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md)). Cuando SQL Server obtiene acceso al Almacenamiento de Azure para escribir o leer copias de seguridad, usa el nombre de la cuenta de almacenamiento y la información de la clave de acceso.  Para obtener más información sobre cómo crear credenciales para almacenar archivos de base de [datos en Azure Storage, vea la lección 3: Crear una credencial de SQL Server](../relational-databases/lesson-2-create-a-sql-server-credential-using-a-shared-access-signature.md)  
  
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
  
     ![asignación de la cuenta de almacenamiento a las credenciales de SQL](../../2014/tutorials/media/backuptocloud-storage-credential-mapping.gif "asignación de la cuenta de almacenamiento a las credenciales de SQL")  
  
5.  Compruebe la instrucción T-SQL y haga clic en **Ejecutar**.  
  
 Para obtener más información sobre el servicio Azure BLOB Storage para los conceptos y los requisitos de copia de seguridad, vea [SQL Server Backup and restore with Azure BLOB Storage Service](../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md).  
  
### <a name="next-lesson"></a>Lección siguiente  
 [Lección 3: Escriba una copia de seguridad completa de la base](../../2014/tutorials/lesson-3-write-a-full-database-backup-to-the-windows-azure-blob-storage-service.md)de datos en el servicio Azure BLOB Storage.  
  
  
