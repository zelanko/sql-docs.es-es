---
title: sp_addmergepartition (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addmergepartition
- sp_addmergepartition_TSQL
helpviewer_keywords:
- sp_addmergepartition
ms.assetid: 02a5f46b-e5ff-4932-a3ff-7f0fd82d0981
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5599370f892d174336411573883e2feffa27b886
ms.sourcegitcommit: 2db83830514d23691b914466a314dfeb49094b3c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2019
ms.locfileid: "58492658"
---
# <a name="spaddmergepartition-transact-sql"></a>sp_addmergepartition (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Crea una partición filtrada dinámicamente para una suscripción que se filtra por los valores de [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) o [SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md) en el suscriptor. Este procedimiento almacenado se ejecuta en el publicador en la base de datos que se está publicando y se utiliza para generar particiones manualmente.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_addmergepartition [ @publication = ] 'publication'  
        , [ @suser_sname = ] 'suser_sname'  
        , [ @host_name = ] 'host_name'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'` Es la publicación de combinación en el que se va a crear la partición. *publicación* es **sysname**, no tiene ningún valor predeterminado. Si *suser_sname* se especifica, el valor de *hostname* debe ser NULL.  
  
`[ @suser_sname = ] 'suser_sname'` Es el valor utilizado al crear la partición para una suscripción que está filtrada por el valor de la [SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md) función en el suscriptor. *SUSER_SNAME* es **sysname**, no tiene ningún valor predeterminado.  
  
`[ @host_name = ] 'host_name'` Es el valor utilizado al crear la partición para una suscripción que está filtrada por el valor de la [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) función en el suscriptor. *HOST_NAME* es **sysname**, no tiene ningún valor predeterminado.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_addmergepartition** se utiliza en la replicación de mezcla.  
  
## <a name="example"></a>Ejemplo  
 [!code-sql[HowTo#sp_MergeDynamicPubPlusPartition](../../relational-databases/replication/codesnippet/tsql/sp-addmergepartition-tra_1.sql)]  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor o **db_owner** rol fijo de base de datos se puede ejecutar **sp_addmergepartition**.  
  
## <a name="see-also"></a>Vea también  
 [Crear una instantánea para una publicación de mezcla con filtros con parámetros](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)   
 [Filtros de fila con parámetros](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)  
  
  
