---
title: sp_helptracertokens (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helptracertokens
- sp_helptracertokens_TSQL
helpviewer_keywords:
- sp_helptracertokens
ms.assetid: 61f27234-531d-4b37-8fa3-fe4c32e6f521
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: b04bf618bccb5d4d49724e0b62f03ba193dc0f2a
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/05/2020
ms.locfileid: "82826059"
---
# <a name="sp_helptracertokens-transact-sql"></a>sp_helptracertokens (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Devuelve una fila para cada testigo de seguimiento que se ha insertado en una publicación para determinar la latencia. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación o en el distribuidor de la base de datos de distribución.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_helptracertokens [ @publication = ] 'publication'   
    [ , [ @publisher = ] 'publisher' ]   
    [ , [ @publisher_db = ] 'publisher_db' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'`Es el nombre de la publicación en la que se insertaron los testigos de seguimiento. *Publication* es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
`[ @publisher = ] 'publisher'`Nombre del publicador. *Publisher* es de **tipo sysname y su**valor predeterminado es NULL.  
  
> [!NOTE]
>  Este parámetro solo debe especificarse para los publicadores que no sean de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
`[ @publisher_db = ] 'publisher_db'`Nombre de la base de datos de publicación. *publisher_db* es de **tipo sysname y su**valor predeterminado es NULL. Si el procedimiento almacenado se ejecuta en el publicador, se omite este parámetro.  
  
## <a name="result-set"></a>Tipo de cursor  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**tracer_id**|**int**|Identifica un registro de un token de seguimiento.|  
|**publisher_commit**|**datetime**|Fecha y hora a la que el registro de token se confirmó en el publicador de la base de datos de publicaciones.|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_helptracertokens** se utiliza en la replicación transaccional.  
  
 **sp_helptracertokens** se utiliza para obtener los identificadores de token de seguimiento al ejecutar [sp_helptracertokenhistory &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptracertokenhistory-transact-sql.md).  
  
## <a name="example"></a>Ejemplo  
 [!code-sql[HowTo#sp_tracertokens](../../relational-databases/replication/codesnippet/tsql/sp-helptracertokens-tran_1.sql)]  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros del rol fijo de servidor **sysadmin** , el rol fijo de base de datos **db_owner** en la base de datos de publicación, o **db_owner** roles fijos de base de datos o **replmonitor** en la base de datos de distribución pueden ejecutar **sp_helptracertokenhistory**.  
  
## <a name="see-also"></a>Consulte también  
 [Medir la latencia y validar las conexiones para la replicación transaccional](../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)   
 [sp_deletetracertokenhistory &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-deletetracertokenhistory-transact-sql.md)  
  
  
