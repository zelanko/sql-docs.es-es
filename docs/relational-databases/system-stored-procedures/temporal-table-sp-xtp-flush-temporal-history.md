---
title: sp_xtp_flush_temporal_history | Documentos de Microsoft
ms.custom: 
ms.date: 02/21/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server (starting with 2016 CTP3)
f1_keywords:
- sp_xtp_flush_temporal_history
- sp_xtp_flush_temporal_history_TSQL
- sys.sp_xtp_flush_temporal_history
- sys.sp_xtp_flush_temporal_history_TSQL
helpviewer_keywords: sp_xtp_flush_temporal_history
ms.assetid: 322e3170-93f8-468a-a123-104ce7bd7fad
caps.latest.revision: "7"
author: CarlRabeler
ms.author: carlrab
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 75a2394e72a0990a9f5108af6b77feb1fb3c44d6
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="temporal-table---spxtpflushtemporalhistory"></a>Tabla temporal - sp_xtp_flush_temporal_history
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Se invoca la tarea de vaciado de datos para mover confirmadas todas las filas de tabla de almacenamiento provisional en memoria a la tabla de historial basadas en disco.  

 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sys.sp_xtp_flush_temporal_history @schema_name, @object_name  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *@schema_name*  
 El nombre del esquema de la tabla temporal o actual  
  
 *@object_name*  
 El nombre de la tabla temporal o actual  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o >0 (error)  
  
## <a name="permissions"></a>Permissions  
 Se requieren permisos db_owner.  
  
## <a name="see-also"></a>Vea también  
 [Consideraciones de rendimiento con tablas temporales con control de versiones del sistema con optimización para memoria](../../relational-databases/tables/memory-optimized-system-versioned-temporal-tables-performance.md)  
  
  
