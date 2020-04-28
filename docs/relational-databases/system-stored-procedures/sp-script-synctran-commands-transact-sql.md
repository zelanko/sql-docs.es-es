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
ms.openlocfilehash: d7caca72f684dfb6428361a4550860b3bea3f273
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "68126410"
---
# <a name="sp_script_synctran_commands-transact-sql"></a>sp_script_synctran_commands (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Genera un script que contiene las llamadas **sp_addsynctrigger** que se van a aplicar en los suscriptores para las suscripciones actualizables. Hay una **sp_addsynctrigger** llamada para cada artículo de la publicación. El script generado también contiene las llamadas **sp_addqueued_artinfo** que crean la tabla **MSsubsciption_articles** necesaria para procesar las publicaciones en cola. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_script_synctran_commands [@publication = ] 'publication'  
    [ , [@article = ] 'article']  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'`Es el nombre de la publicación que se va a incluir en el script. *Publication* es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
`[ @article = ] 'article'`Es el nombre del artículo que se va a incluir en el script. *article* es de **tipo sysname y su**valor predeterminado es **All**, que especifica que todos los artículos se incluyen en el script.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="results-set"></a>Conjunto de resultados  
 **sp_script_synctran_commands** devuelve un conjunto de resultados que consta de una única columna **nvarchar (4000)** . El conjunto de resultados forma los scripts completos necesarios para crear las llamadas **sp_addsynctrigger** y **sp_addqueued_artinfo** que se van a aplicar en los suscriptores.  
  
## <a name="remarks"></a>Observaciones  
 **sp_script_synctran_commands** se utiliza en la replicación de instantáneas y transaccional.  
  
 **sp_addqueued_artinfo** se utiliza para las suscripciones actualizables en cola.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros del rol fijo de servidor **sysadmin** o del rol fijo de base de datos **db_owner** pueden ejecutar **sp_script_synctran_commands**.  
  
## <a name="see-also"></a>Consulte también  
 [sp_addsynctriggers &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-addsynctriggers-transact-sql.md)   
 [sp_addqueued_artinfo &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-addqueued-artinfo-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
