---
title: sp_helpreplicationoption (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpreplicationoption
- sp_helpreplicationoption_TSQL
helpviewer_keywords:
- sp_helpreplicationoption
ms.assetid: ef988dbc-dd0b-4132-80ab-81eebec1cffe
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b125eeaab0ea833a801123ea4540f076696894d0
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2019
ms.locfileid: "58535897"
---
# <a name="sphelpreplicationoption-transact-sql"></a>sp_helpreplicationoption (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Muestra los tipos de opciones de replicación habilitados para un servidor. Este procedimiento almacenado se ejecuta en cualquier servidor de cualquier base de datos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_helpreplicationoption [ [ @optname =] 'option_name' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @optname = ] 'option_name'` Es el nombre de la opción de replicación para consultar. *option_name* es **sysname**, su valor predeterminado es null.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**transactional**|Se devuelve un conjunto de resultados cuando se habilita la replicación transaccional.|  
|**merge**|Se devuelve un conjunto de resultados cuando se habilita la replicación de mezcla.|  
|NULL (predeterminado)|No se devuelve ningún conjunto de resultados.|  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**optname**|**sysname**|Es el nombre de la opción de replicación y puede ser uno de los valores siguientes:<br /><br /> **transactional**<br /><br /> **merge**|  
|**value**|**bit**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**major_version**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**minor_version**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**revision**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**install_failures**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_helpreplicationoption** se utiliza para obtener información acerca de las opciones de replicación habilitada en un servidor determinado. Para obtener información sobre una determinada base de datos, use **sp_helpreplicationdboption**.  
  
## <a name="permissions"></a>Permisos  
 De forma predeterminada, los permisos de ejecución corresponden al rol **public** .  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
