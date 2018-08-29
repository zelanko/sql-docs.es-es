---
title: sp_script_synctran_commands (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
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
- sp_script_synctran_commands
- sp_script_synctran_commands_TSQL
helpviewer_keywords:
- sp_script_synctran_commands
ms.assetid: f132694a-dd05-405b-9d84-21acce9e564a
caps.latest.revision: 27
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b86c1064eb96174243ea15cba6f5f84a77e40a1f
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2018
ms.locfileid: "43031812"
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
 [ **@publication** =] **'***publicación***'**  
 Es el nombre de la publicación de la que se va a crear un script. *publicación* es **sysname**, no tiene ningún valor predeterminado.  
  
 [ **@article** =] **'***artículo***'**  
 Es el nombre del artículo que se va a agregar al script. *artículo* es **sysname**, su valor predeterminado es **todas**, que especifica todos los artículos se convertirá en script.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="results-set"></a>Conjunto de resultados  
 **sp_script_synctran_commands** devuelve un conjunto de resultados que consta de una sola **nvarchar (4000)** columna. El conjunto de resultados forma las secuencias de comandos completadas necesarios para crear tanto el **sp_addsynctrigger** y **sp_addqueued_artinfo** llamadas que se aplicará en los suscriptores.  
  
## <a name="remarks"></a>Notas  
 **sp_script_synctran_commands** se utiliza en la replicación de instantáneas y transaccional.  
  
 **sp_addqueued_artinfo** se utiliza para suscripciones actualizables en cola.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor o **db_owner** rol fijo de base de datos se puede ejecutar **sp_script_synctran_commands**.  
  
## <a name="see-also"></a>Vea también  
 [sp_addsynctriggers &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsynctriggers-transact-sql.md)   
 [sp_addqueued_artinfo &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addqueued-artinfo-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
