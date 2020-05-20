---
title: sp_dbmmonitorchangemonitoring (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_dbmmonitorchangemonitoring
- sp_dbmmonitorchangemonitoring_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dbmmonitorchangemonitoring
- database mirroring [SQL Server], monitoring
ms.assetid: 17be755b-673d-4cd4-9544-6ecb4220bed3
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: eaabc73c78b16a2babac681c87504da8d38a935a
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/05/2020
ms.locfileid: "82826211"
---
# <a name="sp_dbmmonitorchangemonitoring-transact-sql"></a>sp_dbmmonitorchangemonitoring (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cambia el valor de un parámetro de supervisión de la creación de reflejo de la base de datos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_dbmmonitorchangemonitoring parameter  
    , value   
```  
  
## <a name="arguments"></a>Argumentos  
 *parámetro*  
 Especifica el identificador del parámetro cuyo valor se va a cambiar. Actualmente, solo está disponible el siguiente parámetro:  
  
 1 = Período de actualización  
  
 Número de minutos entre actualizaciones de la tabla de estado de la creación de reflejo de la base de datos. El intervalo predeterminado es 1 minuto.  
  
 *value*  
 Especifica el nuevo valor del parámetro que se está cambiando.  
  
|Parámetro|Descripción del valor|  
|---------------|--------------------------|  
|1|Entero entre 1 y 120 que especifica un nuevo período de actualización en minutos.|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 None  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="permissions"></a>Permisos  
 Requiere la pertenencia al rol fijo de servidor **sysadmin** .  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se cambia el período de actualización a 5 minutos.  
  
```  
EXEC sp_dbmmonitorchangemonitoring 1, 5 ;  
```  
  
## <a name="see-also"></a>Consulte también  
 [Supervisar la creación de reflejo de la base de datos &#40;SQL Server&#41;](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)   
 [sp_dbmmonitoraddmonitoring &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-dbmmonitoraddmonitoring-transact-sql.md)   
 [sp_dbmmonitordropmonitoring &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-dbmmonitordropmonitoring-transact-sql.md)   
 [sp_dbmmonitorhelpmonitoring &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-dbmmonitorhelpmonitoring-transact-sql.md)   
 [sp_dbmmonitorresults &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorresults-transact-sql.md)  
  
  
