---
title: sp_dropmergepartition (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_dropmergepartition_TSQL
- sp_dropmergepartition
helpviewer_keywords:
- sp_dropmergepartition
ms.assetid: 1be511c1-79ff-4947-9379-78d83b7b8945
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 73526621bcd2925b863feb45566ed652484a6d57
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/09/2019
ms.locfileid: "54131745"
---
# <a name="spdropmergepartition-transact-sql"></a>sp_dropmergepartition (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Quita una partición para un filtro de fila con parámetros de una publicación. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación. Este procedimiento almacenado quita también el trabajo de instantáneas y los archivos de instantáneas correspondientes de la partición.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_dropmergepartition [ @publication = ] 'publication'  
        , [ @suser_sname = ] 'suser_sname'  
        , [ @host_name = ] 'host_name'  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@publication**] = **'**_publicación_**'**  
 Es el nombre de la publicación. *publicación* es **sysname**, no tiene ningún valor predeterminado.  
  
 [ **@suser_sname**=] **'**_suser_sname_**'**  
 Es el valor de la [SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md) función en el suscriptor utilizado para definir la partición. *SUSER_SNAME* es **sysname**, no tiene ningún valor predeterminado.  
  
 [ **@host_name** =] **'**_host_name_**'**  
 Es el valor de la [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) función en el suscriptor utilizado para definir la partición. *HOST_NAME* es **sysname**, no tiene ningún valor predeterminado.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_dropmergepartition** se utiliza en la replicación de mezcla.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor o **db_owner** rol fijo de base de datos se puede ejecutar **sp_dropmergepartition**.  
  
## <a name="see-also"></a>Vea también  
 [Administrar particiones para una publicación de mezcla mediante filtros con parámetros](../../relational-databases/replication/publish/manage-partitions-for-a-merge-publication-with-parameterized-filters.md)  
  
  
