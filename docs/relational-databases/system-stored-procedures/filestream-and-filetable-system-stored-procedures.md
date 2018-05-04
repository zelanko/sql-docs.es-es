---
title: FileStream y FileTable sistema procedimientos almacenan (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- FileTables [SQL Server], catalog views
ms.assetid: 2c83a4a7-720b-4435-a3b5-788c29f56949
caps.latest.revision: 7
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 854593c3ee467502e19ae7b07ae3ff9979e4397a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="filestream-and-filetable-system-stored-procedures-transact-sql"></a>(Transact-SQL) de procedimientos almacenados del sistema de FileStream y FileTable
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Esta sección describen los procedimientos almacenados del sistema para la característica FileTable y Filestream.  

## <a name="filestream-and-filetable-system-stored-procedures"></a>Procedimientos almacenados del sistema de FileStream y Filetable
  [sp_filestream_force_garbage_collection (Transact-SQL)](filestream-and-filetable-sp-filestream-force-garbage-collection.md)

   Fuerza la ejecución del recolector de elementos no utilizados de FILESTREAM eliminando los archivos FILESTREAM innecesarios.

  [sp_kill_filestream_non_transacted_handles (Transact-SQL)](filestream-and-filetable-sp-kill-filestream-non-transacted-handles.md)

  Cierra los identificadores de archivos no transaccionales para datos de FileTable.


## <a name="see-also"></a>Vea también
[FileStream](../../relational-databases/blob/filestream-sql-server.md)
<br>[Filetables](../../relational-databases/blob/filetables-sql-server.md)
<br>[FileStream y vistas de administración dinámica de FileTable (Transact-SQL)](../system-dynamic-management-views/filestream-and-filetable-dynamic-management-views-transact-sql.md)
<br>[FileStream y vistas de catálogo de FileTable (Transact-SQL)](../system-catalog-views/filestream-and-filetable-catalog-views-transact-sql.md)
  
  
