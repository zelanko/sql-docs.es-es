---
title: Cambiar tablas de captura de datos (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: a4372d0b-50ca-4e58-80f6-2ed3cb52a84a
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 680ccf7eb66d7a70b14432521e299a85f516b9b5
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="change-data-capture-tables-transact-sql"></a>Tablas de captura de datos de cambio (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  La captura de datos de cambio permite realizar un seguimiento de las tablas de tal manera que los cambios en el lenguaje de manipulación de datos (DML) y en el lenguaje de definición de datos (DDL) realizados en las tablas se puedan cargar incrementalmente en un almacenamiento de datos. Los temas de esta sección describen las tablas del sistema que almacenan las información que usan las operaciones de captura de datos modificados.  
  
## <a name="in-this-section"></a>En esta sección  
 [cdc.<capture_instance>_CT](../../relational-databases/system-tables/cdc-capture-instance-ct-transact-sql.md)  
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
  
 [dbo.cdc_jobs &#40; Transact-SQL &#41;](../../relational-databases/system-tables/dbo-cdc-jobs-transact-sql.md)  
 Devuelve los parámetros de configuración para los trabajos de agente de captura de datos del cambio.  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados de captura de datos modificados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/change-data-capture-stored-procedures-transact-sql.md)   
 [Cambiar las funciones de captura de datos &#40; Transact-SQL &#41;](../../relational-databases/system-functions/change-data-capture-functions-transact-sql.md)  
  
  
