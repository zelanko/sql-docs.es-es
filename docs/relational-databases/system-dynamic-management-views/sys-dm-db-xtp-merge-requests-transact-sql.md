---
title: sys.dm_db_xtp_merge_requests (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/01/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
ms.assetid: c1224e88-af74-4c99-ae32-d5d2c552a1f5
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f522fde05ce951575d3e02b3cdc4d3336056bd4e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68026806"
---
# <a name="sysdmdbxtpmergerequests-transact-sql"></a>sys.dm_db_xtp_merge_requests (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

Realiza el seguimiento de las solicitudes de combinación de bases de datos. La solicitud de combinación puede haber sido generada por SQL Server o la solicitud se ha realizado un usuario con [sys.sp_xtp_merge_checkpoint_files (Transact-SQL)](../../relational-databases/system-stored-procedures/sys-sp-xtp-merge-checkpoint-files-transact-sql.md).

> [!NOTE]
> Esta vista de administración dinámica (DMV), sys.dm_db_xtp_merge_requests, existe hasta que Microsoft SQL Server 2014.
> Pero a partir de SQL Server 2016, esta DMV ya no es aplicable.

## <a name="columns-in-the-report"></a>Columnas del informe

| Nombre de columna | Tipo de datos | Descripción |
| :-- | :-- | :-- |
| request_state | tinyint | Estado de la solicitud de combinación:<br/>0 = solicitada<br/>1 = pendiente<br/>2 = instalado<br/>3 = abandonada |
| request_state_desc | nvarchar(60) | Significado para el estado actual de la solicitud:<br/><br/>¿Solicitado: existe una solicitud de combinación.<br/>Pendiente: la combinación es que se va a procesar.<br/>Ha instalado, la fusión mediante combinación completada.<br/>Abandonado: la combinación no se pudo completar, quizás debido a falta de almacenamiento. |
| destination_file_id | GUID | Identificador único del archivo de destino para la combinación de los archivos de origen. |
| lower_bound_tsn | bigint | Marca de tiempo mínima del archivo de combinación de destino. Marca de tiempo de transacción mínima de todos los archivos de origen que se van a combinar. |
| upper_bound_tsn | bigint | Marca de tiempo máxima del archivo de combinación de destino. Marca de tiempo de transacción máxima de todos los archivos de origen que se van a combinar. |
| collection_tsn | bigint | Marca de tiempo en la que se puede recuperar la fila actual.<br/><br/>Se quita una fila con el estado instalado cuando checkpoint_tsn es mayor que collection_tsn.<br/><br/>Se quita una fila con el estado abandonado cuando checkpoint_tsn es menor que collection_tsn. |
| checkpoint_tsn | bigint | Hora a la que se inició el punto de comprobación.<br/><br/>Las eliminaciones realizadas por transacciones con una marca de tiempo menor que esta se tienen en cuenta en el nuevo archivo de datos. Las eliminaciones restantes se mueven al archivo delta de destino. |
| sourcenumber_file_id | GUID | Hasta 16 identificadores de archivo interno que identifican los archivos de origen en la combinación. |

## <a name="permissions"></a>Permisos

Requiere el permiso VIEW DATABASE STATE en la base de datos actual.

## <a name="see-also"></a>Vea también

[Vistas de administración dinámica de tabla optimizada para memoria (Transact-SQL)](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)
