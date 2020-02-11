---
title: 'Tutorial: Copias de seguridad y restauración de SQL Server en el servicio Azure Blob Storage | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: 9e1d94ce-2c93-45d1-ae2a-2a7d1fa094c4
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: b166930b5d077e7294fcdbc13449d40cab309425
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "70176115"
---
# <a name="tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service"></a>Tutorial: Copias de seguridad y restauración de SQL Server en el servicio Azure Blob Storage
  Este es el Introducción con SQL Server tutorial de copia de seguridad y restauración con Azure Blob Storage Service. Este tutorial le ayudará a entender cómo escribir copias de seguridad en el servicio Azure Blob Storage y cómo restaurar desde este.  
  
## <a name="what-you-will-learn"></a>Aprendizaje  
 Este tutorial muestra cómo crear una cuenta de almacenamiento de Windows, un contenedor de blobs, crear credenciales para tener acceso a la cuenta de almacenamiento, escribir una copia de seguridad en el servicio de blob y realizar una restauración simple. El tutorial está compuesto por cuatro lecciones:  
  
 [Lección 1: Creación de objetos de Azure Storage](../tutorials/lesson-1-create-windows-azure-storage-objects.md)  
 En esta lección, creará una cuenta de Azure Storage y un contenedor de blobs.  
  
 [Lección 2: Crear una credencial de SQL Server](../tutorials/lesson-2-create-a-sql-server-credential.md)  
 En esta lección, creará una credencial para almacenar la información de seguridad usada para acceder a la cuenta de Azure Storage.  
  
 [Lección 3: Escritura de una copia de seguridad completa de la base de datos en el servicio Azure Blob Storage](../tutorials/lesson-3-write-a-full-database-backup-to-the-windows-azure-blob-storage-service.md)  
 En esta lección, emitirá una instrucción T-SQL para escribir una copia de seguridad de la base de datos AdventureWorks2012 en el servicio Azure Blob Storage.  
  
 [Lección 4: Realizar una restauración desde una copia de seguridad completa de la base de datos](../tutorials/lesson-4-perform-a-restore-from-a-full-database-backup.md)  
 En esta lección, emitirá una instrucción T-SQL para restaurar desde la copia de seguridad de la base de datos creada en la lección anterior.  
  
### <a name="requirements"></a>Requisitos  
 Para completar este tutorial, debe estar familiarizado con los conceptos de copias de seguridad y restauración de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y con la sintaxis de T-SQL. Para usar este tutorial, el sistema debe cumplir los requisitos siguientes:  
  
-   Una instancia de [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] y la base de datos AdventureWorks2012 instalada.  
  
     La instancia de SQL Server puede ser local o residir en una máquina virtual de Azure.  
  
     Puede usar una base de datos de usuario en lugar de AdventureWorks2012 y modificar la sintaxis de tsql en consecuencia.  
  
-   La cuenta de usuario que se usa para emitir comandos BACKUP o RESTORE debe tener el rol de base de datos **operador de db_backup** con permisos **Modificar cualquier credencial** .  
  
### <a name="additional-reading"></a>Lecturas adicionales  
 A continuación, se indican algunas lecturas recomendadas para entender los conceptos y los procedimientos recomendados al usar el servicio Azure Blob Storage para copias de seguridad de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
1.  [Copia de seguridad y restauración de SQL Server con el servicio Azure Blob Storage](backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)  
  
2.  [Procedimientos recomendados y solución de problemas de Copia de seguridad en URL de SQL Server](backup-restore/sql-server-backup-to-url-best-practices-and-troubleshooting.md)  
  
  
