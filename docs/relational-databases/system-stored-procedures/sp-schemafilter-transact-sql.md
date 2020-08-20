---
description: sp_schemafilter (Transact-SQL)
title: sp_schemafilter (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_schemafilter_TSQL
- sp_schemafilter
helpviewer_keywords:
- sp_schemafilter
ms.assetid: 199e869b-2cd2-44ee-b2ee-69edb06a1bc4
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: ad023dd248b3849e4bb900e1891bd655087a51f7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88481108"
---
# <a name="sp_schemafilter-transact-sql"></a>sp_schemafilter (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Modifica y muestra la información del esquema que se excluye al incluir tablas de Oracle aptas para su publicación.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_schemafilter [ @publisher = ] 'publisher'   
   [ , [ @schema = ] 'schema' ]   
   [ , [ @operation = ] 'operation' ]   
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publisher = ] 'publisher'` Es el nombre del publicador que no es de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . *Publisher* es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
`[ @schema = ] 'schema'` Es el nombre del esquema. *Schema* es de **tipo sysname y su**valor predeterminado es NULL.  
  
`[ @operation = ] 'operation'` Es la acción que se va a realizar en este esquema. la *operación* es **nvarchar (4)** y puede tener uno de los valores siguientes.  
  
|Value|Descripción|  
|-----------|-----------------|  
|**add**|Agrega el esquema especificado a la lista de esquemas no aptos para su publicación.|  
|**drop**|Quita el esquema especificado de la lista de esquemas no aptos para su publicación.|  
|**help**|Devuelve la lista de esquemas no aptos para su publicación.|  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**equivale**|**sysname**|Es el nombre del esquema no apto para su publicación.|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Observaciones  
 **sp_schemafilter** solo se debe usar para publicadores heterogéneos.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros del rol fijo de servidor **sysadmin** en el distribuidor pueden ejecutar **sp_schemafilter**.  
  
## <a name="see-also"></a>Consulte también  
 [Procedimientos almacenados de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
