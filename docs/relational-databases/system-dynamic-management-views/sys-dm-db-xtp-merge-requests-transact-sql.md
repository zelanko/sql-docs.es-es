---
title: Sys. dm_db_xtp_merge_requests (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/01/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
ms.assetid: c1224e88-af74-4c99-ae32-d5d2c552a1f5
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: f489b01655f3b6836c1360bc0e473747e62ca59e
ms.sourcegitcommit: 039fb38c583019b3fd06894160568387a19ba04e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/30/2020
ms.locfileid: "87442673"
---
# <a name="sysdm_db_xtp_merge_requests-transact-sql"></a>sys.dm_db_xtp_merge_requests (Transact-SQL)

[!INCLUDE[sqlserver](../../includes/applies-to-version/sqlserver.md)]

Realiza el seguimiento de las solicitudes de combinación de bases de datos. Es posible que la solicitud de combinación la haya generado SQL Server o que un usuario con [Sys. sp_xtp_merge_checkpoint_files (Transact-SQL)](../../relational-databases/system-stored-procedures/sys-sp-xtp-merge-checkpoint-files-transact-sql.md)haya realizado la solicitud.

> [!NOTE]
> Esta vista de administración dinámica (DMV), sys. dm_db_xtp_merge_requests, existe hasta Microsoft SQL Server 2014.
> Pero a partir de SQL Server 2016 ya no se aplica esta DMV.

## <a name="columns-in-the-report"></a>Columnas del informe

| Nombre de la columna | Tipo de datos | Descripción |
| :-- | :-- | :-- |
| request_state | TINYINT | Estado de la solicitud de combinación:<br/>0 = solicitada<br/>1 = pendiente<br/>2 = instalado<br/>3 = abandonada |
| request_state_desc | nvarchar(60) | Significados para el estado actual de la solicitud:<br/><br/>Solicitado: existe una solicitud Merge.<br/>Pending: la combinación se está procesando.<br/>Instalado: la combinación se ha completado.<br/>Abandonado: no se pudo completar la fusión mediante combinación, quizás debido a la falta de almacenamiento. |
| destination_file_id | GUID | Identificador único del archivo de destino para la combinación de los archivos de origen. |
| lower_bound_tsn | bigint | Marca de tiempo mínima del archivo de combinación de destino. Marca de tiempo de transacción mínima de todos los archivos de origen que se van a combinar. |
| upper_bound_tsn | bigint | Marca de tiempo máxima del archivo de combinación de destino. Marca de tiempo de transacción máxima de todos los archivos de origen que se van a combinar. |
| collection_tsn | bigint | Marca de tiempo en la que se puede recuperar la fila actual.<br/><br/>Se quita una fila con el estado instalado cuando checkpoint_tsn es mayor que collection_tsn.<br/><br/>Se quita una fila con el estado abandonado cuando checkpoint_tsn es menor que collection_tsn. |
| checkpoint_tsn | bigint | Hora a la que se inició el punto de comprobación.<br/><br/>Las eliminaciones realizadas por transacciones con una marca de tiempo menor que esta se tienen en cuenta en el nuevo archivo de datos. Las eliminaciones restantes se mueven al archivo delta de destino. |
| sourcenumber_file_id | GUID | Hasta 16 identificadores de archivo internos que identifican de forma única los archivos de origen en la combinación. |

## <a name="permissions"></a>Permisos

Requiere el permiso VIEW DATABASE STATE en la base de datos actual.

## <a name="see-also"></a>Consulta también

[Vistas de administración dinámica de tablas con optimización para memoria (Transact-SQL)](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)
