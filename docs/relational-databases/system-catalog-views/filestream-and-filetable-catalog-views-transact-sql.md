---
title: Vistas de catálogo de FileStream y FileTable (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- FileTables [SQL Server], catalog views
ms.assetid: 2c83a4a7-720b-4435-a3b5-788c29f56949
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: b0294cb76ad25e4c11038be59666892c270256bb
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/05/2020
ms.locfileid: "82829769"
---
# <a name="filestream-and-filetable-catalog-views-transact-sql"></a>Vistas de catálogo de secuencia de archivo y FileTable (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  En esta sección se describen las vistas de catálogo relacionadas con la característica FileTable.  
  
## <a name="filestream-and-filetable-catalog-views-transact-sql"></a>Vistas de catálogo de FileStream y filetable (Transact-SQL)
 [sys.database_filestream_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-filestream-options-transact-sql.md)  
 Muestra información sobre el nivel de acceso no transaccional a los datos de FILESTREAM en los objetos FileTable habilitados. Contiene una fila por cada base de datos de la instancia de SQL Server.  
  
 [sys.filetable_system_defined_objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-filetable-system-defined-objects-transact-sql.md)  
 Muestra una lista de los objetos definidos por el sistema relacionados con objetos FileTable. Contiene una fila por cada objeto definido por el sistema.  
  
 [sys.filetables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-filetables-transact-sql.md)  
 Devuelve una fila para cada objeto FileTable. Hereda de **Sys. Tables**.  

## <a name="see-also"></a>Consulte también
[FileStream](../../relational-databases/blob/filestream-sql-server.md)
<br>[Filetables](../../relational-databases/blob/filetables-sql-server.md)
<br>[Vistas de administración dinámica de secuencia de archivo y FileTable (Transact-SQL)](../system-dynamic-management-views/filestream-and-filetable-dynamic-management-views-transact-sql.md)
<br>[Procedimientos almacenados del sistema de Filestream y FileTable (Transact-SQL)](../system-stored-procedures/filestream-and-filetable-system-stored-procedures.md)
  
  
