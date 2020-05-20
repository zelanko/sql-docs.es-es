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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 395a7c2227fb23a177cb1b3980b26014f0651c0c
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/05/2020
ms.locfileid: "82817756"
---
# <a name="sp_helpreplicationoption-transact-sql"></a>sp_helpreplicationoption (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Muestra los tipos de opciones de replicación habilitados para un servidor. Este procedimiento almacenado se ejecuta en cualquier servidor de cualquier base de datos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_helpreplicationoption [ [ @optname =] 'option_name' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @optname = ] 'option_name'`Es el nombre de la opción de replicación que se va a consultar. *option_name* es de **tipo sysname y su**valor predeterminado es NULL.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**transaccional**|Se devuelve un conjunto de resultados cuando se habilita la replicación transaccional.|  
|**sin**|Se devuelve un conjunto de resultados cuando se habilita la replicación de mezcla.|  
|NULL (predeterminado)|No se devuelve ningún conjunto de resultados.|  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**optname**|**sysname**|Es el nombre de la opción de replicación y puede ser uno de los valores siguientes:<br /><br /> **transaccional**<br /><br /> **sin**|  
|**value**|**bit**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**major_version**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**minor_version**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**revision**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**install_failures**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_helpreplicationoption** se usa para obtener información sobre las opciones de replicación habilitadas en un servidor determinado. Para obtener información sobre una base de datos determinada, use **sp_helpreplicationdboption**.  
  
## <a name="permissions"></a>Permisos  
 De forma predeterminada, los permisos de ejecución corresponden al rol **public** .  
  
## <a name="see-also"></a>Consulte también  
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
