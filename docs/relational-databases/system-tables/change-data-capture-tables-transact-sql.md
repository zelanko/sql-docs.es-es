---
title: Tablas de captura de datos modificados (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: a4372d0b-50ca-4e58-80f6-2ed3cb52a84a
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 4d23c366cab021fa04a5e651abd0b51276c2788d
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85764260"
---
# <a name="change-data-capture-tables-transact-sql"></a>Tablas de captura de datos de cambio (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  La captura de datos de cambio permite realizar un seguimiento de las tablas de tal manera que los cambios en el lenguaje de manipulación de datos (DML) y en el lenguaje de definición de datos (DDL) realizados en las tablas se puedan cargar incrementalmente en un almacenamiento de datos. Los temas de esta sección describen las tablas del sistema que almacenan las información que usan las operaciones de captura de datos modificados.  
  
## <a name="in-this-section"></a>En esta sección  
 [capture_instance CDC. <>_CT](../../relational-databases/system-tables/cdc-capture-instance-ct-transact-sql.md)  
 Devuelve una fila para cada cambio realizado en una columna capturada en la tabla de origen asociada.  
  
 [cdc.captured_columns](../../relational-databases/system-tables/cdc-captured-columns-transact-sql.md)  
 Devuelve una fila para cada columna de la que se ha realizado un seguimiento en una instancia de captura.  
  
 [cdc.change_tables](../../relational-databases/system-tables/cdc-change-tables-transact-sql.md)  
 Devuelve una fila por cada tabla de cambios en la base de datos.  
  
 [cdc.ddl_history](../../relational-databases/system-tables/cdc-ddl-history-transact-sql.md)  
 Devuelve una fila para cada cambio del lenguaje de definición de datos (DDL) realizado en las tablas que se habilitan para la captura de datos de cambio.  
  
 [cdc.lsn_time_mapping](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md)  
 Devuelve una fila para cada transacción que tiene filas en una tabla de cambios. Esta tabla se utiliza para las asignaciones entre los valores de confirmación de número de secuencia de registro (LSN) y la hora de confirmación de la transacción.  
  
 [cdc.index_columns](../../relational-databases/system-tables/cdc-index-columns-transact-sql.md)  
 Devuelve una fila para cada columna de índice asociada a una tabla de cambios.  
  
 [DBO. cdc_jobs &#40;Transact-SQL&#41;](../../relational-databases/system-tables/dbo-cdc-jobs-transact-sql.md)  
 Devuelve los parámetros de configuración para los trabajos de agente de captura de datos del cambio.  
  
## <a name="see-also"></a>Consulte también  
 [Procedimientos almacenados de captura de datos modificados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/change-data-capture-stored-procedures-transact-sql.md)   
 [Funciones de captura de datos modificados &#40;Transact-SQL&#41;](../../relational-databases/system-functions/change-data-capture-functions-transact-sql.md)  
  
  
