---
title: sp_requestpeerresponse (Transact-SQL) | Microsoft Docs
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
- sp_requestpeerresponse_TSQL
- sp_requestpeerresponse
helpviewer_keywords:
- sp_requestpeerresponse
ms.assetid: cbe13c22-4d7d-4a36-b194-7a13ce68ef27
caps.latest.revision: 26
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b722bac6727e6d64bb0c2c475ca900ea78c8fc1d
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2018
ms.locfileid: "43024377"
---
# <a name="sprequestpeerresponse-transact-sql"></a>sp_requestpeerresponse (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cuando se ejecuta desde un nodo en una topología punto a punto, este procedimiento solicita una respuesta de todos los demás nodos de la topología. Ejecutando este procedimiento y revisando las respuestas correspondientes, puede garantizar que todos los comandos anteriores se han entregado a los nodos que responden. Este procedimiento almacenado se ejecuta en el nodo que lo solicita de cualquier base de datos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_requestpeerresponse [ @publication = ] 'publication'  
    [ , [ @description = ] 'description'  
    [ , [ @request_id = ] request_id OUTPUT ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@publication**=] **'***publicación***'**  
 Es el nombre de la publicación en una topología punto a punto de la que se está comprobando el estado. *publicación* es **sysname**, no tiene ningún valor predeterminado.  
  
 [ **@description**=] **'***descripción***'**  
 Información definida por el usuario que se puede utilizar para identificar solicitudes de estado individuales. *descripción* es **nvarchar (4000)**, su valor predeterminado es null.  
  
 [ **@request_id** =] *request_id*  
 Devuelve el identificador de la nueva solicitud. *request_id* es **int** y es un parámetro de salida. Este valor puede usarse al ejecutar [sp_helppeerresponses &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-helppeerresponses-transact-sql.md) para ver todas las respuestas a una solicitud de estado.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Notas  
 **sp_requestpeerresponse** se utiliza en la replicación transaccional punto a punto.  
  
 **sp_requestpeerresponse** se utiliza para garantizar que todos los comandos han sido recibidos por todos los demás nodos antes de restaurar una base de datos publicada en una topología punto a punto. Se utiliza también al replicar cambios del lenguaje de definición de datos (DDL) realizados mientras un nodo estaba sin conexión para calcular cuándo llegan estos cambios a los otros nodos.  
  
 **sp_requestpeerresponse** no se puede ejecutar dentro de una transacción definida por el usuario.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor o el **db_owner** rol fijo de base de datos se puede ejecutar **sp_requestpeerresponse**.  
  
## <a name="see-also"></a>Vea también  
 [sp_deletepeerrequesthistory &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-deletepeerrequesthistory-transact-sql.md)   
 [sp_helppeerrequests &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppeerrequests-transact-sql.md)  
  
  
