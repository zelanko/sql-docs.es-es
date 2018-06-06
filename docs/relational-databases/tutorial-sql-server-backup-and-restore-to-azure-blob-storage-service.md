---
title: 'Tutorial: Copias de seguridad y restauración de SQL Server en el servicio Azure Blob Storage | Microsoft Docs'
ms.custom: ''
ms.date: 04/09/2018
ms.prod: sql
ms.prod_service: database-engine
ms.component: tutorial
ms.reviewer: ''
ms.suite: sql
ms.technology: performance
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- SQL Server 2016 Preview
ms.assetid: 9e1d94ce-2c93-45d1-ae2a-2a7d1fa094c4
caps.latest.revision: 11
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 1c070d081e622982bbead15826914b01a89179e7
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/04/2018
ms.locfileid: "34585627"
---
# <a name="tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service"></a>Tutorial: Copias de seguridad y restauración de SQL Server en el servicio Azure Blob Storage
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
Este tutorial le ayudará a entender cómo escribir copias de seguridad en el servicio Azure Blob Storage y cómo restaurar desde este.  
  
## <a name="what-you-will-learn"></a>Aprendizaje  
En este tutorial se muestra cómo crear una cuenta de Storage y un contenedor de blobs, cómo crear credenciales para acceder a la cuenta de almacenamiento, cómo escribir una copia de seguridad en el servicio de blobs y cómo realizar una restauración simple. El tutorial está compuesto por cuatro lecciones:  
  
[Lección 1: Crear objetos de Azure Storage](http://msdn.microsoft.com/library/74edd1fd-ab00-46f7-9e29-7ba3f1a446c5)  
En esta lección, creará una cuenta de Azure Storage y un contenedor de blobs.  
  
[Lección 2: Crear una credencial de SQL Server](http://msdn.microsoft.com/library/64f8805c-1ddc-4c96-a47c-22917d12e1ab)  
En esta lección, creará una credencial para almacenar la información de seguridad usada para acceder a la cuenta de Azure Storage.  
  
[Lección 3: Escribir una copia de seguridad completa de la base de datos en el servicio Azure Blob Storage](https://technet.microsoft.com/en-us/library/jj720552\(v=sql.110\).aspx)  
En esta lección, emitirá una instrucción T-SQL para escribir una copia de seguridad de la base de datos AdventureWorks2012 en el servicio Azure Blob Storage.  
  
[Lección 4: Realizar una restauración desde una copia de seguridad completa de la base de datos](http://msdn.microsoft.com/library/580f76e6-9802-4abc-9043-db6de592c733)  
En esta lección, emitirá una instrucción T-SQL para restaurar desde la copia de seguridad de la base de datos creada en la lección anterior.  
  
### <a name="requirements"></a>Requisitos  
Para completar este tutorial, debe estar familiarizado con los conceptos de copias de seguridad y restauración de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y con la sintaxis de T-SQL. Para usar este tutorial, el sistema debe cumplir los requisitos siguientes:  
  
-   Una instancia de [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] y la base de datos AdventureWorks2012 instalada.  
  
    La instancia de SQL Server puede ser local o residir en una máquina virtual de Azure.  
  
    Puede usar una base de datos de usuario en lugar de AdventureWorks2012 y modificar la sintaxis de tsql en consecuencia.  
  
-   La cuenta de usuario que se usa para emitir comandos BACKUP o RESTORE debe tener el rol de base de datos **operador de db_backup** con permisos **Modificar cualquier credencial**.  
  
### <a name="additional-reading"></a>Lecturas adicionales  
A continuación, se indican algunas lecturas recomendadas para entender los conceptos y los procedimientos recomendados al usar el servicio Azure Blob Storage para copias de seguridad de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
1.  [SQL Server Backup and Restore with Microsoft Azure Blob Storage Service](../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md) (Copia de seguridad y restauración de SQL Server con el servicio Microsoft Azure Blob Storage)  
  
2.  [SQL Server Backup to URL Best Practices and Troubleshooting](../relational-databases/backup-restore/sql-server-backup-to-url-best-practices-and-troubleshooting.md) (Procedimientos recomendados y solución de problemas de copia de seguridad en URL de SQL Server)  
  
## <a name="see-also"></a>Vea también  
[Copia de seguridad y restauración de SQL Server con el servicio de Almacenamiento de blobs de Microsoft Azure](../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)

