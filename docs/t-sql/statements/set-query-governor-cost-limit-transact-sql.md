---
title: SET QUERY_GOVERNOR_COST_LIMIT (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SET QUERY_GOVERNOR_COST_LIMIT
- SET_QUERY_GOVERNOR_COST_LIMIT_TSQL
- QUERY_GOVERNOR_COST_LIMIT
- QUERY_GOVERNOR_COST_LIMIT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- SET QUERY_GOVERNOR_COST_LIMIT statement
- connections [SQL Server], overriding
- QUERY_GOVERNOR_COST_LIMIT option
- overriding connection values
ms.assetid: 3424bb44-6915-462d-a8d7-fe834af81387
caps.latest.revision: 27
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 6090e52a9b3b2a701129e6cebeaa8460ab02fc43
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="set-querygovernorcostlimit-transact-sql"></a>SET QUERY_GOVERNOR_COST_LIMIT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Invalidaciones configuradas actualmente **opción query governor cost limit** valor para la conexión actual.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SET QUERY_GOVERNOR_COST_LIMIT value  
```  
  
## <a name="arguments"></a>Argumentos  
 *value*  
 Es un valor numérico o entero que especifica el tiempo máximo que puede durar la ejecución de una consulta. Los valores se redondean por defecto al entero más próximo. Los valores negativos se redondean a 0. El regulador de consultas no permite la ejecución de consultas que tengan un costo estimado superior a ese valor. Al especificar 0 (valor predeterminado) para esta opción desactiva el regulador de consultas, y todas las consultas se pueden ejecutar de forma indefinida.  
  
 El término "costo de consultas" hace referencia al tiempo estimado, en segundos, necesario para completar una consulta con una configuración de hardware específica.  
  
## <a name="remarks"></a>Comentarios  
 SET QUERY_GOVERNOR_COST_LIMIT solo se aplica a la conexión actual y solo está activo durante la conexión. Use la [configurar la opción de configuración del servidor de query governor cost limit](../../database-engine/configure-windows/configure-the-query-governor-cost-limit-server-configuration-option.md)opción de **sp_configure** para cambiar el regulador de consultas de todo el servidor de costo del valor de límite. Para obtener más información acerca de cómo configurar esta opción, vea [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) y [opciones de configuración de servidor &#40; SQL Server &#41; ](../../database-engine/configure-windows/server-configuration-options-sql-server.md).  
  
 La opción SET QUERY_GOVERNOR_COST_LIMIT se establece en tiempo de ejecución, no en tiempo de análisis.  
  
## <a name="permissions"></a>Permissions  
 Debe pertenecer al rol **public** .  
  
## <a name="see-also"></a>Vea también  
 [Instrucciones SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  
  
  

