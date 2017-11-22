---
title: Sys.sp_xtp_unbind_db_resource_pool (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_xtp_unbind_db_resource_pool_TSQL
- sp_xtp_unbind_db_resource_pool
- sys.sp_xtp_unbind_db_resource_pool_TSQL
- sys.sp_xtp_unbind_db_resource_pool
dev_langs: TSQL
helpviewer_keywords:
- sp_xtp_unbind_db_resource_pool
- sys.sp_xtp_unbind_db_resource_pool
ms.assetid: 695a796d-087e-4bc8-99d0-ddc342604c75
caps.latest.revision: "7"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6da5bc97801329871d6b433ecf8f049f4b0eb742
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="sysspxtpunbinddbresourcepool-transact-sql"></a>sys.sp_xtp_unbind_db_resource_pool (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  Este procedimiento del sistema quita un enlace existente entre una base de datos y un grupo de recursos con el fin de llevar un seguimiento del uso de la memoria de [!INCLUDE[hek_2](../../includes/hek-2-md.md)].  Si no hay ningún grupo actualmente enlazado a la base de datos especificada, la operación se realizará correctamente. Cuando la base de datos no está enlazada, la memoria previamente asignada para los objetos optimizados para memoria se mantiene para el grupo de recursos de servidor anterior. Debe reiniciar la base de datos para liberar la memoria asignada. Una vez que se haya quitado el enlace de una base de datos al grupo de recursos de servidor, el enlace recurre al grupo de recursos de servidor DEFAULT.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
||  
|-|  
|**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] a través de la [versión actual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
## <a name="syntax"></a>Sintaxis  
  
```tsql  
sys.sp_xtp_unbind_db_resource_pool 'database_name'  
```  
  
## <a name="arguments"></a>Argumentos  
 database_name  
 Nombre de una base de datos de [!INCLUDE[hek_2](../../includes/hek-2-md.md)] existente habilitada.  
  
#### <a name="parameters"></a>Parámetros  
  
## <a name="messages"></a>Mensajes  
 Si la base de datos se ha enlazado a un grupo de recursos de servidor con nombre, el procedimiento se realiza correctamente. Sin embargo, debe reiniciar la base de datos para que surta efecto la eliminación del enlace.  
 Si no hay enlaces para la base de datos especificada, `sp_xtp_unbind_db_resource_pool` se ejecuta correctamente, pero genera el mensaje informativo:  
  
```  
Msg 41374, Level 16, State 1, Procedure sp_xtp_unbind_db_resource_pool_internal, Line 140.  
Database 'Hekaton_DB' does not have a binding to a resource pool.  
  
```  
  
## <a name="example"></a>Ejemplo  
 El código siguiente elimina el enlace de la base de datos Hekaton_DB del grupo de recursos de servidor de [!INCLUDE[hek_2](../../includes/hek-2-md.md)] al que estaba enlazada.  Si Hekaton_DB no está enlazado actualmente a un grupo de recursos de servidor de [!INCLUDE[hek_2](../../includes/hek-2-md.md)], aparece un mensaje. Se debe reiniciar la base de datos para que surta efecto la eliminación del enlace.  
  
```tsql  
sys.sp_xtp_unbind_db_resource_pool 'Hekaton_DB'  
```  
  
## <a name="requirements"></a>Requisitos  
  
-   La base de datos que especificó `database_name` debe tener un enlace a un grupo de recursos de servidor de [!INCLUDE[hek_2](../../includes/hek-2-md.md)].  
  
-   Requiere el permiso CONTROL SERVER.  
  
## <a name="see-also"></a>Vea también  
 [Enlazar una base de datos con tablas con optimización para memoria a un grupo de recursos de servidor](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md)   
 [Sys.sp_xtp_bind_db_resource_pool &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sys-sp-xtp-bind-db-resource-pool-transact-sql.md)  
  
  
