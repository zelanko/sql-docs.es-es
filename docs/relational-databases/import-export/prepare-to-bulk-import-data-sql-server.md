---
title: Preparación para importar datos de forma masiva (SQL Server) | Microsoft Docs
description: Puede usar el comando bcp, la instrucción BULK INSERT o la función OPENROWSET(BULK) para la importación en bloque de datos solo desde un archivo de datos.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- bulk importing [SQL Server], about bulk importing
- BULK INSERT statement, guidelines
- BULK INSERT statement, restrictions
- bcp utility [SQL Server], guidelines
- bcp utility [SQL Server], restrictions
- hidden characters
- OPENROWSET function, BCP guidelines
ms.assetid: a82ef43c-d006-4c71-bfca-f001a3ba1ba0
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: e80c94b8198b3564e76d67e5a632a4791d9c64e1
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2020
ms.locfileid: "80980637"
---
# <a name="prepare-to-bulk-import-data-sql-server"></a>Prepararse para importar datos de forma masiva (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Puede usar el comando **bcp** , la instrucción BULK INSERT o la función OPENROWSET(BULK) para la importación masiva de datos solo desde un archivo de datos.  
  
> [!NOTE]  
>  Es posible escribir una aplicación personalizada que importe de forma masiva datos desde objetos que no sean un archivo de texto. Para realizar la importación en bloque de datos desde búferes de memoria, use las extensiones de bcp a la interfaz de programación de aplicaciones (API) cliente nativa (ODBC) de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o la interfaz **IRowsetFastLoad** de OLE DB.  Para realizar la importación en bloque de datos desde una tabla de datos de C#, use la API de copia masiva de ADO.NET, **SqlBulkCopy**.  
  
> [!NOTE]  
>  No se admite la importación masiva de datos en una tabla remota.  
  
 Use las siguientes directrices cuando importe en bloque datos de un archivo de datos a una instancia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   Obtenga los permisos necesarios para la cuenta de usuario.  
  
     La cuenta de usuario en que use la utilidad **bcp**, la instrucción BULK INSERT o la instrucción INSERT ... SELECT * FROM OPENROWSET(BULK...) debe tener los permisos necesarios sobre la tabla, que son asignados por el propietario de la tabla. Para obtener más información sobre los permisos necesarios en cada método, vea [bcp (utilidad)](../../tools/bcp-utility.md), [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md), y [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md).  
  
-   Use el modelo de recuperación optimizado para cargas masivas de registros.  
  
     Esta indicación es para bases de datos que utilizan el modelo de recuperación completa. El modelo de recuperación optimizado para cargas masivas de registros resulta útil al realizar operaciones masivas en una tabla sin indexar (un *montón*). El uso de la recuperación por medio de registros de operaciones masivas ayuda a evitar que el registro de transacciones se quede sin espacio, ya que este tipo de recuperación no realiza la inserción de filas del registro. Para obtener más información sobre el modelo de recuperación optimizado para cargas masivas de registros, vea [Modelos de recuperación &#40;SQL Server&#41;](../../relational-databases/backup-restore/recovery-models-sql-server.md).  
  
     Se recomienda cambiar la base de datos para que use el modelo de recuperación optimizado para cargas masivas de registros inmediatamente antes de la operación de importación masiva. Inmediatamente después, debe restablecer la base de datos al modelo de recuperación completa. Para obtener más información, vea [Ver o cambiar el modelo de recuperación de una base de datos &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server.md).  
  
    > [!NOTE]  
    >  más información sobre cómo minimizar el registro durante las operaciones de importación en bloque, vea [Requisitos previos para el registro mínimo durante la importación en bloque](../../relational-databases/import-export/prerequisites-for-minimal-logging-in-bulk-import.md).  
  
-   Realice una copia de seguridad después de la importación masiva de datos.  
  
     Para una base de datos que utilice el modelo de recuperación simple, se recomienda realizar una copia de seguridad completa o diferencial cuando finalice la operación de importación masiva. Para obtener más información, vea [Crear una copia de seguridad completa de una base de datos &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md) o [Crear una copia de seguridad diferencial de una base de datos &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-differential-database-backup-sql-server.md).  
  
     Si se utiliza el modelo de recuperación optimizado para cargas masivas de registros o de recuperación completa, basta con una copia de seguridad de registros. Para obtener más información, vea [Copias de seguridad del registro de transacciones &#40;SQL Server&#41;](../../relational-databases/backup-restore/transaction-log-backups-sql-server.md).  
  
-   Elimine los índices de las tablas para mejorar el rendimiento de las importaciones masivas de gran tamaño.  
  
     Esta indicación es adecuada cuando vaya a importar una gran cantidad de datos en comparación con la cantidad de datos que ya tiene la tabla. En este caso, la eliminación de los índices de la tabla antes de realizar la operación de importación masiva puede aumentar el rendimiento considerablemente.  
  
    > [!NOTE]  
    >  Sin embargo, si va a cargar una cantidad pequeña de datos en comparición con la cantidad de datos ya incluidos en la tabla, quitar los índices es contraproducente. El tiempo necesario para volver a crear los índices puede ser mayor que el tiempo que se ahorra durante la operación de importación masiva.  
  
-   Busque y quite los caracteres ocultos del archivo de datos.  
  
     Muchas herramientas y editores de texto muestran los caracteres ocultos que suelen encontrarse al final del archivo de datos. Durante una operación de importación masiva, los caracteres ocultos en un archivo de datos ASCII pueden producir  problemas que den como resultado un error de tipo "se encontró un valor nulo inesperado". La búsqueda y eliminación de todos los caracteres ocultos debería solucionar el problema.  
  
## <a name="see-also"></a>Consulte también  
 [Importar y exportar datos en bloque con la utilidad bcp &#40;SQL Server&#41;](../../relational-databases/import-export/import-and-export-bulk-data-by-using-the-bcp-utility-sql-server.md)   
 [Importación en bloque de datos mediante las instrucciones BULK INSERT u OPENROWSET&#40;BULK...&#41; &#40;SQL Server&#41;](../../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)   
 [bcp (utilidad)](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [Formatos de datos para importación en bloque o exportación masiva &#40;SQL Server&#41;](../../relational-databases/import-export/data-formats-for-bulk-import-or-bulk-export-sql-server.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)  
  
  
