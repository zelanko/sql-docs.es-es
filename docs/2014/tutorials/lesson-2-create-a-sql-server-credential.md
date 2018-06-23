---
title: 'Lección 2: Crear una credencial de SQL Server | Documentos de Microsoft'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 64f8805c-1ddc-4c96-a47c-22917d12e1ab
caps.latest.revision: 13
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: b16012ed7ff12783e69add14cf8e51011668845e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36202406"
---
# <a name="lesson-2-create-a-sql-server-credential"></a>Lección 2: Crear una credencial de SQL Server
  **Credencial:** una credencial de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] es un objeto que se usa para almacenar la información de autenticación necesaria para conectarse a un recurso fuera de SQL Server.  En este caso, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] procesos de copia de seguridad y restauración usan credenciales para autenticarse en el servicio de almacenamiento de blobs de Windows Azure. La credencial contiene los valores de nombre y la **clave de acceso** de la cuenta de almacenamiento. Una vez creada la credencial, se debe especificar en la opción WITH CREDENTIAL al emitir las instrucciones BACKUP y RESTORE. Para obtener más información sobre cómo ver, copiar o regenerar **access keys**de cuentas de almacenamiento, vea [Ver, copiar y regenerar las claves de acceso de una cuenta de almacenamiento de Windows Azure](http://msdn.microsoft.com/library/windowsazure/hh531566.aspx).  
  
 Para obtener información general sobre las credenciales, vea [Credenciales](http://msdn.microsoft.com/library/ms161950.aspx).  
  
 Para obtener información sobre otros ejemplos donde se usan credenciales, vea [Crear un proxy del Agente SQL Server](http://msdn.microsoft.com/library/ms175834.aspx).  
  
> [!IMPORTANT]  
>  Los requisitos para crear una credencial de SQL Server que se describe a continuación son específicos para procesos de copia de seguridad de SQL Server ([copias de seguridad de SQL Server a URL](../relational-databases/backup-restore/sql-server-backup-to-url.md), y [SQL Server Managed Backup to Windows Azure](../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md)). Cuando SQL Server obtiene acceso al Almacenamiento de Azure para escribir o leer copias de seguridad, usa el nombre de la cuenta de almacenamiento y la información de la clave de acceso.  Para obtener más información sobre cómo crear credenciales para almacenar archivos de base de datos de almacenamiento de Azure, consulte [lección 3: crear una credencial de SQL Server](../relational-databases/lesson-2-create-a-sql-server-credential-using-a-shared-access-signature.md)  
  
## <a name="create-a-sql-server-credential"></a>Crear una credencial de SQL Server  
 Para crear una credencial de SQL Server, siga estos pasos:  
  
1.  Conéctese a SQL Server Management Studio.  
  
2.  En el Explorador de objetos, conéctese a la instancia del motor de base de datos que tiene instalada la base de datos AdventureWorks2012 o use su propia base de datos para este tutorial.  
  
3.  En la barra de herramientas **Estándar** , haga clic en **Nueva consulta**.  
  
4.  Copie y pegue el ejemplo siguiente en la ventana de consulta, y modifíquelo como sea necesario.  
  
    ```  
    CREATE CREDENTIAL mycredential   
    WITH IDENTITY= 'mystorageaccount' – this is the name of the storage account you specified when creating a storage account (See Lesson 1)   
    , SECRET = '<storage account access key>' – this should be either the Primary or Secondary Access Key for the storage account (See Lesson 1)  
  
    ```  
  
     ![asignación de cuenta de almacenamiento de las credenciales sql](../../2014/tutorials/media/backuptocloud-storage-credential-mapping.gif "asignar la cuenta de almacenamiento a las credenciales de sql")  
  
5.  Compruebe la instrucción T-SQL y haga clic en **Ejecutar**.  
  
 Para obtener más información acerca del servicio de almacenamiento de blobs de Windows Azure para conceptos de copia de seguridad y los requisitos, consulte [SQL Server Backup and Restore con el servicio de almacenamiento de blobs de Windows Azure](../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md).  
  
### <a name="next-lesson"></a>Lección siguiente  
 [Lección 3: Escribir una copia de seguridad completa de la base de datos en el servicio de almacenamiento de Windows Azure Blob](../../2014/tutorials/lesson-3-write-a-full-database-backup-to-the-windows-azure-blob-storage-service.md).  
  
  