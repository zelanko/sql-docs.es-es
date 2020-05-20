---
title: sp_requestpeerresponse (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_requestpeerresponse_TSQL
- sp_requestpeerresponse
helpviewer_keywords:
- sp_requestpeerresponse
ms.assetid: cbe13c22-4d7d-4a36-b194-7a13ce68ef27
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 82259f4293d821882f64e8162e0e5ec48e0548d1
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/05/2020
ms.locfileid: "82824380"
---
# <a name="sp_requestpeerresponse-transact-sql"></a>sp_requestpeerresponse (Transact-SQL)
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
`[ @publication = ] 'publication'`Es el nombre de la publicación en una topología punto a punto para la que se está comprobando el estado. *Publication* es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
`[ @description = ] 'description'`Información definida por el usuario que se puede utilizar para identificar solicitudes de estado individuales. la *Descripción* es de tipo **nvarchar (4000)** y su valor predeterminado es NULL.  
  
`[ @request_id = ] request_id`Devuelve el identificador de la nueva solicitud. *request_id* es de **tipo int** y es un parámetro de salida. Este valor se puede usar al ejecutar [sp_helppeerresponses &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-helppeerresponses-transact-sql.md) para ver todas las respuestas a una solicitud de estado.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_requestpeerresponse** se usa en la replicación transaccional punto a punto.  
  
 **sp_requestpeerresponse** se utiliza para asegurarse de que todos los demás nodos han recibido todos los comandos antes de restaurar una base de datos Publicada en una topología punto a punto. Se utiliza también al replicar cambios del lenguaje de definición de datos (DDL) realizados mientras un nodo estaba sin conexión para calcular cuándo llegan estos cambios a los otros nodos.  
  
 **sp_requestpeerresponse** no se puede ejecutar en una transacción definida por el usuario.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros del rol fijo de servidor **sysadmin** o del rol fijo de base de datos **db_owner** pueden ejecutar **sp_requestpeerresponse**.  
  
## <a name="see-also"></a>Consulte también  
 [sp_deletepeerrequesthistory &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-deletepeerrequesthistory-transact-sql.md)   
 [sp_helppeerrequests &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-helppeerrequests-transact-sql.md)  
  
  
