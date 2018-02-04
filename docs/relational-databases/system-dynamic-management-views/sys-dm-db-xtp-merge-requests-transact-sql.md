---
title: sys.dm_db_xtp_merge_requests (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 02/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c1224e88-af74-4c99-ae32-d5d2c552a1f5
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4e08d9df86f8b389e3a2811c4b63a35ab0945dd0
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/03/2018
---
# <a name="sysdmdbxtpmergerequests-transact-sql"></a>sys.dm_db_xtp_merge_requests (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]


Realiza el seguimiento de las solicitudes de combinación de bases de datos. La solicitud de combinación puede haber sido generada por SQL Server o la solicitud pudo haber realizado por un usuario con [sys.sp_xtp_merge_checkpoint_files (Transact-SQL)](../../relational-databases/system-stored-procedures/sys-sp-xtp-merge-checkpoint-files-transact-sql.md).

> [!NOTE]
> Esta vista de administración dinámica (DMV), sys.dm_db_xtp_merge_requests, existe hasta que Microsoft SQL Server 2014.
> 
> Pero a partir de SQL Server 2016 Esta DMV ya no es aplicable.

## <a name="columns-in-the-report"></a>Columnas del informe

| Nombre de columna | Tipo de datos | Description |
| :-- | :-- | :-- |
| request_state | tinyint | Estado de la solicitud de combinación:<br/>0 = solicitada<br/>1 = pendiente<br/>2 = instalado<br/>3 = abandonada |
| request_state_desc | nvarchar(60) | Significados para el estado actual de la solicitud:<br/><br/>Solicita - existe una solicitud de combinación.<br/>Pendiente: la combinación es que se va a procesar.<br/>Ha instalado, la combinación está completa.<br/>Abandone - la mezcla no se pudo completar, quizás debido a falta de almacenamiento. |
| destination_file_id | GUID | Identificador único del archivo de destino para la combinación de los archivos de origen. |
| lower_bound_tsn | bigint | Marca de tiempo mínima del archivo de combinación de destino. Marca de tiempo de transacción mínima de todos los archivos de origen que se van a combinar. |
| upper_bound_tsn | bigint | Marca de tiempo máxima del archivo de combinación de destino. Marca de tiempo de transacción máxima de todos los archivos de origen que se van a combinar. |
| collection_tsn | bigint | Marca de tiempo en la que se puede recuperar la fila actual.<br/><br/>Se quita una fila con el estado instalado cuando checkpoint_tsn es mayor que collection_tsn.<br/><br/>Se quita una fila con el estado abandonado cuando checkpoint_tsn es menor que collection_tsn. |
| checkpoint_tsn | bigint | Hora a la que se inició el punto de comprobación.<br/><br/>Las eliminaciones realizadas por transacciones con una marca de tiempo menor que esta se tienen en cuenta en el nuevo archivo de datos. Las eliminaciones restantes se mueven al archivo delta de destino. |
| sourcenumber_file_id | GUID | Hasta 16 identificadores de archivo interno que identifican de forma única los archivos de origen en la combinación. |

## <a name="permissions"></a>Permissions

Requiere el permiso VIEW DATABASE STATE en la base de datos actual.

## <a name="see-also"></a>Vea también

[Vistas de administración dinámica de tabla optimizada en memoria (Transact-SQL)](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)


