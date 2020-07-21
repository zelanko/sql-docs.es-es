---
title: sp_scriptsubconflicttable (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_scriptsubconflicttable
- sp_scriptsubconflicttable_TSQL
helpviewer_keywords:
- sp_scriptsubconflicttable
ms.assetid: 13867145-3dad-47a4-8d50-a65175418479
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 93656ff6bec2acc3c3f6f7ee189b1c45db75a7d6
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2020
ms.locfileid: "85899190"
---
# <a name="sp_scriptsubconflicttable-transact-sql"></a>sp_scriptsubconflicttable (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Genera un script para crear una tabla de conflictos en el suscriptor de un determinado artículo de suscripción en cola. El script generado se ejecuta en el suscriptor de la base de datos de suscripciones. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_scriptsubconflicttable [@publication =] 'publication'    , [@article =] 'article'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'`Es el nombre de la publicación que contiene el artículo. El nombre debe ser único en la base de datos. *Publication* es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
`[ @article = ] 'article'`Es el nombre del artículo de suscripción. *article* es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**cmdtext**|**nvarchar(4000)**|Devuelve el script de [!INCLUDE[tsql](../../includes/tsql-md.md)] para crear la tabla de conflictos en el suscriptor del artículo de suscripción en cola. Este script se ejecuta en el suscriptor de la base de datos de suscripciones.|  
  
## <a name="remarks"></a>Comentarios  
 **sp_scriptsubconflicttable** se utiliza para los suscriptores que tienen suscripciones en las que la instantánea inicial se aplica manualmente. La tabla de conflictos es opcional en el suscriptor.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros del rol fijo de servidor **sysadmin** o del rol fijo de base de datos **db_owner** pueden ejecutar **sp_scriptsubconflicttable**.  
  
## <a name="see-also"></a>Consulte también  
 [Detección y resolución de conflictos de actualización en cola](../../relational-databases/replication/transactional/updatable-subscriptions-queued-updating-conflict-resolution.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
