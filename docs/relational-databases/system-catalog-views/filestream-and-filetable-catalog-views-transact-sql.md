---
title: FileStream y vistas de catálogo de FileTable (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- FileTables [SQL Server], catalog views
ms.assetid: 2c83a4a7-720b-4435-a3b5-788c29f56949
caps.latest.revision: 7
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a9bb68f29d40cab87ae8817e2a428a268c234bd2
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="filestream-and-filetable-catalog-views-transact-sql"></a>Vistas de catálogo de secuencia de archivo y FileTable (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  En esta sección se describen las vistas de catálogo relacionadas con la característica FileTable.  
  
## <a name="filestream-and-filetable-catalog-views-transact-sql"></a>FileStream y filetable vistas de catálogo (Transact-SQL)
 [sys.database_filestream_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-filestream-options-transact-sql.md)  
 Muestra información sobre el nivel de acceso no transaccional a los datos de FILESTREAM en los objetos FileTable habilitados. Contiene una fila por cada base de datos de la instancia de SQL Server.  
  
 [sys.filetable_system_defined_objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-filetable-system-defined-objects-transact-sql.md)  
 Muestra una lista de los objetos definidos por el sistema relacionados con objetos FileTable. Contiene una fila por cada objeto definido por el sistema.  
  
 [sys.filetables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-filetables-transact-sql.md)  
 Devuelve una fila para cada objeto FileTable. Hereda de **sys.tables**.  

## <a name="see-also"></a>Vea también
[FileStream](../../relational-databases/blob/filestream-sql-server.md)
<br>[Filetables](../../relational-databases/blob/filetables-sql-server.md)
<br>[FileStream y vistas de administración dinámica de FileTable (Transact-SQL)](../system-dynamic-management-views/filestream-and-filetable-dynamic-management-views-transact-sql.md)
<br>[FileStream y FileTable sistema procedimientos almacenan (Transact-SQL)](../system-stored-procedures/filestream-and-filetable-system-stored-procedures.md)
  
  
