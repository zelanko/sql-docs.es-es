---
title: FileStream y vistas de administración dinámica de FileTable (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- FileTables [SQL Server], dynamic management views
ms.assetid: e50a135d-6644-42a4-a0df-1c7a2b722051
caps.latest.revision: 8
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 932638c7737529ec74168be238e84a9d573a53f1
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="filestream-and-filetable-dynamic-management-views-transact-sql"></a>Vistas de administración dinámica de secuencia de archivo y FileTable (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  En esta sección se describen las vistas de administración dinámica relacionadas con las características FILESTREAM y FileTable.  
  
## <a name="filestream-dynamic-management-views-and-functions"></a>Funciones y vistas de administración dinámica de Filestream  
 [sys.dm_filestream_file_io_handles &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-filestream-file-io-handles-transact-sql.md)  
 Muestra los identificadores de archivos transaccionales abiertos actualmente.  
  
 [sys.dm_filestream_file_io_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-filestream-file-io-requests-transact-sql.md)  
 Muestra las solicitudes de entrada y salida de archivos actuales.  
  
## <a name="filetable-dynamic-management-views-and-functions"></a>Funciones y vistas de administración dinámica de FileTable  
 [sys.dm_filestream_non_transacted_handles &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-filestream-non-transacted-handles-transact-sql.md)  
 Muestra los identificadores de archivos no transaccionales abiertos actualmente asociados a los datos de FileTable.  

## <a name="see-also"></a>Vea también
[FileStream](../../relational-databases/blob/filestream-sql-server.md)
<br>[Filetables](../../relational-databases/blob/filetables-sql-server.md)
<br>[FileStream y vistas de catálogo de FileTable (Transact-SQL)](../system-catalog-views/filestream-and-filetable-catalog-views-transact-sql.md)
<br>[FileStream y FileTable sistema procedimientos almacenan (Transact-SQL)](../system-stored-procedures/filestream-and-filetable-system-stored-procedures.md)
  
