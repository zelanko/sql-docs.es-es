---
title: 'Tutorial: Copias de seguridad y restauración de SQL Server en el servicio Azure Blob Storage | Microsoft Docs'
ms.custom: ''
ms.date: 04/09/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: 9e1d94ce-2c93-45d1-ae2a-2a7d1fa094c4
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: a33c2bd47bae8bede7fa71e1654627c123e7cdbc
ms.sourcegitcommit: 8dccf20d48e8db8fe136c4de6b0a0b408191586b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/09/2018
ms.locfileid: "48874323"
---
# <a name="tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service"></a>Tutorial: Copias de seguridad y restauración de SQL Server en el servicio Azure Blob Storage
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
Con este tutorial, entenderá mejor cómo escribir copias de seguridad en el servicio Azure Blob Storage y cómo restaurar desde este servicio.  En este tutorial se explica cómo crear un contenedor de blobs de Azure, cómo crear credenciales para acceder a la cuenta de almacenamiento, cómo escribir una copia de seguridad en el servicio de blobs y cómo realizar una restauración simple.
  
### <a name="prerequisites"></a>Prerequisites  
Para completar este tutorial, debe estar familiarizado con los conceptos de copias de seguridad y restauración de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y con la sintaxis de T-SQL. Para hacer este tutorial, necesita una cuenta de almacenamiento de Azure, tener instalado SQL Server Management Studio (SSMS), tener acceso a un servidor que ejecute SQL Server y una base de datos de AdventureWorks. Además, la cuenta que se usa para emitir comandos BACKUP o RESTORE debe tener el rol de base de datos **db_backupoperator** con permisos **Modificar cualquier credencial**. 

- Obtenga una [cuenta de Azure](https://azure.microsoft.com/offers/ms-azr-0044p/) gratis.
- Cree una [cuenta de Azure Storage](https://docs.microsoft.com/azure/storage/common/storage-quickstart-create-account?tabs=portal).
- Instale [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).
- Instale [SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads).
- Descargue las [bases de datos de ejemplo de AdventureWorks2016](https://docs.microsoft.com/sql/samples/adventureworks-install-configure).
- Asigne la cuenta de usuario al rol [db_backupoperator](https://docs.microsoft.com/sql/relational-databases/security/authentication-access/database-level-roles) y conceda permisos [Modificar cualquier credencial](https://docs.microsoft.com/sql/t-sql/statements/alter-credential-transact-sql). 


## <a name="create-azure-blob-container"></a>Crear un contenedor de blobs de Azure
Los contenedores proporcionan una agrupación de un conjunto de blobs. Todos los blobs deben estar en un contenedor. Una cuenta puede contener un número ilimitado de contenedores, pero debe tener al menos un contenedor. Un contenedor puede almacenar un número ilimitado de blobs. 

Para crear un contenedor, siga estos pasos:

1. Abra Azure Portal. 
1. Navegue a la cuenta de almacenamiento. 
   1. Seleccione la cuenta de almacenamiento y baje hasta **Blob Services** (Servicios de blob).
   1. Seleccione **Blobs** y después +**Contenedor** para agregar un nuevo contenedor. 
   1. Escriba el nombre del contenedor y tome nota del nombre de contenedor especificado. Esta información se usa en la dirección URL (ruta de acceso al archivo de copia de seguridad) en las instrucciones T-SQL más adelante en este tutorial. 
   1. Seleccione **Aceptar**. 
    
    ![Nuevo contenedor](media/tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service/new-container.png)


  >[!NOTE]
  >La autenticación en la cuenta de almacenamiento es necesaria para las copias de seguridad y la restauración de SQL Server, incluso aunque elija crear un contenedor público. También puede crear un contenedor mediante programación con las API REST. Para más información, vea [Create container](https://docs.microsoft.com/rest/api/storageservices/Create-Container) (Creación de contenedor)


## <a name="create-a-sql-server-credential"></a>Crear una credencial de SQL Server
Una credencial de SQL Server es un objeto que se usa para almacenar la información de autenticación necesaria para conectarse a un recurso fuera de SQL Server. Aquí, los procesos de copia de seguridad y restauración de SQL Server usan credenciales para autenticarse en el servicio Windows Azure Blob Storage. La credencial contiene los valores de nombre y la **clave de acceso** de la cuenta de almacenamiento. Una vez creada la credencial, se debe especificar en la opción WITH CREDENTIAL al emitir las instrucciones BACKUP y RESTORE. Para más información sobre las credenciales, vea [Credenciales (motor de base de datos)](https://docs.microsoft.com/sql/relational-databases/security/authentication-access/credentials-database-engine). 

  >[!IMPORTANT]
  >Los requisitos para crear una credencial de SQL Server que se describen más adelante son específicos para procesos de copia de seguridad de SQL Server ([Copia de seguridad en URL de SQL Server](backup-restore/sql-server-backup-to-url.md) y [Copia de seguridad administrada de SQL Server en Microsoft Azure](backup-restore/sql-server-managed-backup-to-microsoft-azure.md)). SQL Server usa el nombre de la cuenta de almacenamiento y la información de la clave de acceso cuando accede a Azure Storage para escribir o leer copias de seguridad.

### <a name="access-keys"></a>Claves de acceso
Puesto que Azure Portal todavía está abierto, guarde las claves de acceso necesarias para crear la credencial. 

1. Navegue hasta **Cuenta de almacenamiento** en Azure Portal. 
1. Baje hasta **Configuración** y seleccione **Claves de acceso**. 
1. Guarde la clave y la cadena de conexión para usarlas más adelante en este tutorial. 

   ![Claves de acceso](media/tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service/access-keys.png)

### <a name="create-a-sql-server-credential"></a>Crear una credencial de SQL Server
Con la clave de acceso que guardó, cree la credencial de SQL Server siguiendo estos pasos. 

1. Conéctese a SQL Server mediante SQL Server Management Studio. 
1. Seleccione la base de datos **AdventureWorks2016** y abra una ventana **Nueva consulta**. 
1. Copie, pegue y ejecute el ejemplo siguiente en la ventana de consulta, y modifíquelo según sea necesario: 

  ```sql
  CREATE CREDENTIAL mycredential   
  WITH IDENTITY= 'msftutorialstorage', -- this is the name of the storage account you specified when creating a storage account   
  SECRET = '<storage account access key>' -- this should be either the Primary or Secondary Access Key for the storage account 
  ```
1. Ejecute la instrucción para crear la credencial. 

## <a name="backup-database-to-the-windows-azure-blob-storage-service"></a>Hacer copia de seguridad de la base de datos en el servicio Windows Azure Blob Storage
En esta sección, usará una instrucción T-SQL para realizar una copia de seguridad completa de la base de datos en el servicio Windows Azure Blob Storage. 

1. Conéctese a SQL Server mediante SQL Server Management Studio. 
1. Seleccione la base de datos **AdventureWorks2016** y abra una ventana **Nueva consulta**. 
1. Copie y pegue el ejemplo siguiente en la ventana de consulta y modifíquelo según sea necesario: 

 ```sql
 BACKUP DATABASE [AdventureWorks2016] 
 TO URL = 'https://msftutorialstorage.blob.core.windows.net/sql-backup/AdventureWorks2016.bak' 
 /* URL includes the endpoint for the BLOB service, followed by the container name, and the name of the backup file*/ 
 WITH CREDENTIAL = 'mycredential';
 /* name of the credential you created in the previous step */ 
 GO
 ```
1. Ejecute la instrucción para realizar una copia de seguridad de la base de datos AdventureWorks2016 en la URL. 

 
## <a name="restore-database-from-windows-azure-blob-storage-service"></a>Restaurar base de datos desde el servicio Windows Azure Blob Storage
En esta sección, usará una instrucción T-SQL para restaurar la copia de seguridad de base de datos completa. 

1. Conéctese a SQL Server mediante SQL Server Management Studio. 
1. Abra una ventana de **nueva consulta**. 
1. Copie y pegue el ejemplo siguiente en la ventana de consulta y modifíquelo según sea necesario: 

 ```sql
 RESTORE DATABASE AdventureWorks2016 
 FROM URL = 'https://msftutorialstorage.blob.core.windows.net/sql-backup/AdventureWorks2016.bak' 
 WITH CREDENTIAL = 'mycredential',
 STATS = 5 -- use this to see monitor the progress
 GO
 ``` 

## <a name="see-also"></a>Vea también 
Estas son algunas lecturas recomendadas para comprender mejor los conceptos y los procedimientos recomendados al usar el servicio Azure Blob Storage para copias de seguridad de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
-   [Copia de seguridad y restauración de SQL Server con el servicio de Almacenamiento de blobs de Microsoft Azure](../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)   
-   [Prácticas recomendadas y solución de problemas de Copia de seguridad en URL de SQL Server](../relational-databases/backup-restore/sql-server-backup-to-url-best-practices-and-troubleshooting.md)  
  
