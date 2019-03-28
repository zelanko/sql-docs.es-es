---
title: sp_script_synctran_commands (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_script_synctran_commands
- sp_script_synctran_commands_TSQL
helpviewer_keywords:
- sp_script_synctran_commands
ms.assetid: f132694a-dd05-405b-9d84-21acce9e564a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a9ee35eb4c5d67ff50f4f08c1cfa29596e27aec2
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2019
ms.locfileid: "58536187"
---
# <a name="spscriptsynctrancommands-transact-sql"></a>sp_script_synctran_commands (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Genera un script que contiene el **sp_addsynctrigger** llamadas que se aplicará en los suscriptores para las suscripciones actualizables. Hay un **sp_addsynctrigger** llamar para cada artículo de la publicación. El script generado también contiene el **sp_addqueued_artinfo** llamadas que crean la **MSsubsciption_articles** tabla que se necesita para procesar las publicaciones en cola. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_script_synctran_commands [@publication = ] 'publication'  
    [ , [@article = ] 'article']  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'` Es el nombre de la publicación que se convertirá en script. *publicación* es **sysname**, no tiene ningún valor predeterminado.  
  
`[ @article = ] 'article'` Es el nombre del artículo que se convertirá en script. *artículo* es **sysname**, su valor predeterminado es **todas**, que especifica todos los artículos se convertirá en script.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="results-set"></a>Conjunto de resultados  
 **sp_script_synctran_commands** devuelve un conjunto de resultados que consta de una sola **nvarchar (4000)** columna. El conjunto de resultados forma las secuencias de comandos completadas necesarios para crear tanto el **sp_addsynctrigger** y **sp_addqueued_artinfo** llamadas que se aplicará en los suscriptores.  
  
## <a name="remarks"></a>Comentarios  
 **sp_script_synctran_commands** se utiliza en la replicación de instantáneas y transaccional.  
  
 **sp_addqueued_artinfo** se utiliza para suscripciones actualizables en cola.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor o **db_owner** rol fijo de base de datos se puede ejecutar **sp_script_synctran_commands**.  
  
## <a name="see-also"></a>Vea también  
 [sp_addsynctriggers &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsynctriggers-transact-sql.md)   
 [sp_addqueued_artinfo &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addqueued-artinfo-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
