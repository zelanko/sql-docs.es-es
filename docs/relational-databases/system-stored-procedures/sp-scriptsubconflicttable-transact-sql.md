---
title: sp_scriptsubconflicttable (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_scriptsubconflicttable
- sp_scriptsubconflicttable_TSQL
helpviewer_keywords:
- sp_scriptsubconflicttable
ms.assetid: 13867145-3dad-47a4-8d50-a65175418479
caps.latest.revision: 22
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 86a5b01b46aee8a08c0e490b0d59e3887211d51e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="spscriptsubconflicttable-transact-sql"></a>sp_scriptsubconflicttable (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Genera un script para crear una tabla de conflictos en el suscriptor de un determinado artículo de suscripción en cola. El script generado se ejecuta en el suscriptor de la base de datos de suscripciones. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_scriptsubconflicttable [@publication =] 'publication'    , [@article =] 'article'  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publication=**] **'***publicación***'**  
 Es el nombre de la publicación que contiene el artículo. El nombre debe ser único en la base de datos. *publicación* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@article=**] **'***artículo***'**  
 Es el nombre del artículo de suscripción. *artículo* es **sysname**, no tiene ningún valor predeterminado.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**cmdtext**|**nvarchar(4000)**|Devuelve el script de [!INCLUDE[tsql](../../includes/tsql-md.md)] para crear la tabla de conflictos en el suscriptor del artículo de suscripción en cola. Este script se ejecuta en el suscriptor de la base de datos de suscripciones.|  
  
## <a name="remarks"></a>Comentarios  
 **sp_scriptsubconflicttable** se utiliza para los suscriptores que tienen suscripciones donde se aplica manualmente la instantánea inicial. La tabla de conflictos es opcional en el suscriptor.  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de servidor o **db_owner** rol fijo de base de datos puede ejecutar **sp_scriptsubconflicttable**.  
  
## <a name="see-also"></a>Vea también  
 [Detección y resolución de conflictos de actualización en cola](../../relational-databases/replication/transactional/updatable-subscriptions-queued-updating-conflict-resolution.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
