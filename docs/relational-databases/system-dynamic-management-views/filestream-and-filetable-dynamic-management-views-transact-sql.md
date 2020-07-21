---
title: Vistas de administración dinámica de FileStream y FileTable (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- FileTables [SQL Server], dynamic management views
ms.assetid: e50a135d-6644-42a4-a0df-1c7a2b722051
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 782885ddccf486cb74b0b79b60422f1564d4ddbc
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2020
ms.locfileid: "85894680"
---
# <a name="filestream-and-filetable-dynamic-management-views-transact-sql"></a>Vistas de administración dinámica de secuencia de archivo y FileTable (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  En esta sección se describen las vistas de administración dinámica relacionadas con las características FILESTREAM y FileTable.  
  
## <a name="filestream-dynamic-management-views-and-functions"></a>Funciones y vistas de administración dinámica de Filestream  
 [sys.dm_filestream_file_io_handles &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-filestream-file-io-handles-transact-sql.md)  
 Muestra los identificadores de archivos transaccionales abiertos actualmente.  
  
 [sys.dm_filestream_file_io_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-filestream-file-io-requests-transact-sql.md)  
 Muestra las solicitudes de entrada y salida de archivos actuales.  
  
## <a name="filetable-dynamic-management-views-and-functions"></a>Funciones y vistas de administración dinámica de FileTable  
 [sys.dm_filestream_non_transacted_handles &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-filestream-non-transacted-handles-transact-sql.md)  
 Muestra los identificadores de archivos no transaccionales abiertos actualmente asociados a los datos de FileTable.  

## <a name="see-also"></a>Consulte también
[Secuencia de archivos](../../relational-databases/blob/filestream-sql-server.md)
<br>[Filetables](../../relational-databases/blob/filetables-sql-server.md)
<br>[Vistas de catálogo de secuencia de archivo y FileTable (Transact-SQL)](../system-catalog-views/filestream-and-filetable-catalog-views-transact-sql.md)
<br>[Procedimientos almacenados del sistema de Filestream y FileTable (Transact-SQL)](../system-stored-procedures/filestream-and-filetable-system-stored-procedures.md)
  
