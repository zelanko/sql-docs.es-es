---
description: sp_xtp_flush_temporal_history (Transact-SQL)
title: sp_xtp_flush_temporal_history | Microsoft Docs
ms.custom: ''
ms.date: 02/21/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- sp_xtp_flush_temporal_history
- sp_xtp_flush_temporal_history_TSQL
- sys.sp_xtp_flush_temporal_history
- sys.sp_xtp_flush_temporal_history_TSQL
helpviewer_keywords:
- sp_xtp_flush_temporal_history
ms.assetid: 322e3170-93f8-468a-a123-104ce7bd7fad
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 7c22e02aba01530059357b709a0c72be350ec7de
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/08/2020
ms.locfileid: "89544702"
---
# <a name="sp_xtp_flush_temporal_history-transact-sql"></a>sp_xtp_flush_temporal_history (Transact-SQL)

[!INCLUDE [sqlserver2016-asdb-asdbmi](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi.md)]

  Invoca la tarea de vaciado de datos para trasladar todas las filas confirmadas de la tabla de almacenamiento provisional en memoria a la tabla de historial basada en disco.  

 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sys.sp_xtp_flush_temporal_history @schema_name, @object_name  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *\@schema_name*  
 Nombre del esquema de la tabla actual o temporal  
  
 *\@object_name*  
 Nombre de la tabla actual o temporal  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o >0 (error)  
  
## <a name="permissions"></a>Permisos  
 Requiere permisos de db_owner.  
  
## <a name="see-also"></a>Consulte también  
 [Consideraciones de rendimiento con tablas temporales con control de versiones con optimización para memoria](../../relational-databases/tables/memory-optimized-system-versioned-temporal-tables-performance.md)  
  
  
