---
title: sp_helpmergeconflictrows (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpmergeconflictrows_TSQL
- sp_helpmergeconflictrows
helpviewer_keywords:
- sp_helpmergeconflictrows
ms.assetid: 131395a5-cb18-4795-a7ae-fa09d8ff347f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1de46c12b0e05b592489e557a80138996ad9767f
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2019
ms.locfileid: "58528797"
---
# <a name="sphelpmergeconflictrows-transact-sql"></a>sp_helpmergeconflictrows (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve las filas de la tabla de conflictos especificada. Este procedimiento almacenado se ejecuta en el equipo donde se almacena la tabla de conflictos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_helpmergeconflictrows [ [ @publication = ] 'publication' ]  
        , [ @conflict_table = ] 'conflict_table'  
    [ , [ @publisher = ] 'publisher' ]   
    [ , [ @publisher_db = ] 'publsher_db' ]   
    [ , [ @logical_record_conflicts = ] logical_record_conflicts ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'` Es el nombre de la publicación. *publicación* es **sysname**, su valor predeterminado es **%**. Si se especifica la publicación, se devuelven todos los conflictos calificados por la publicación. Por ejemplo, si la **MSmerge_conflict_Customers** tabla tiene filas de conflicto para la **WA** y **CA** publicaciones, pasando un nombre de publicación **CA**  recupera los conflictos que pertenecen a la **CA** publicación.  
  
`[ @conflict_table = ] 'conflict_table'` Es el nombre de la tabla de conflictos. *conflict_table* es **sysname**, no tiene ningún valor predeterminado. En [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y versiones posteriores, las tablas de conflictos se denominan utilizando los nombres de formato con **MSmerge_conflict\__publicación\_artículo_**, con una tabla para cada artículo publicado.  
  
`[ @publisher = ] 'publisher'` Es el nombre del publicador. *publicador* es **sysname**, su valor predeterminado es null.  
  
`[ @publisher_db = ] 'publisher_db'` Es el nombre de la base de datos del publicador. *publisher_db* es **sysname**, su valor predeterminado es null.  
  
`[ @logical_record_conflicts = ] logical_record_conflicts` Indica si el conjunto de resultados contiene información sobre los conflictos de registros lógicos. *logical_record_conflicts* es **int**, con un valor predeterminado de 0. **1** indica que se devuelve información de conflictos de registros lógicos.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 **sp_helpmergeconflictrows** devuelve un conjunto que consta de la estructura de tabla base y estas columnas adicionales de resultados.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**origin_datasource**|**varchar(255)**|Origen del conflicto.|  
|**conflict_type**|**int**|Código que indica el tipo de conflicto:<br /><br /> **1** = conflicto de actualización: El conflicto se detecta en el nivel de fila.<br /><br /> **2** = conflicto de actualización de columna: El conflicto se detecta en el nivel de columna.<br /><br /> **3** = conflicto entre actualización Delete: La eliminación gana el conflicto.<br /><br /> **4** = conflicto entre actualización Delete: La columna rowguid eliminada que pierde el conflicto se registra en esta tabla.<br /><br /> **5** = error de inserción en carga: La inserción desde el suscriptor no pudo aplicarse en el publicador.<br /><br /> **6** = error de inserción en descarga: La inserción desde el publicador no pudo aplicarse en el suscriptor.<br /><br /> **7** = error de eliminación en carga: No se pudo cargar la eliminación en el suscriptor al publicador.<br /><br /> **8** = error de eliminación en descarga: No se pudo descargar la eliminación en el publicador al suscriptor.<br /><br /> **9** = error de actualización de carga: La actualización en el suscriptor no pudo aplicarse en el publicador.<br /><br /> **10** = error de actualización de descarga: La actualización en el publicador no pudo aplicarse al suscriptor.<br /><br /> **12** = eliminación de Wins de actualización del registro lógico: El registro lógico eliminado que pierde el conflicto se registra en esta tabla.<br /><br /> **13** = actualización de inserción de conflicto de registros lógicos: Inserte un conflictos de registro lógico con una actualización.<br /><br /> **14** = conflicto de actualización de Wins de eliminación de registros lógicos: El registro lógico actualizado que pierde el conflicto se registra en esta tabla.|  
|**reason_code**|**int**|Código del error, que puede depender del contexto.|  
|**reason_text**|**varchar(720)**|Descripción del error, que puede depender del contexto.|  
|**pubid**|**uniqueidentifier**|Identificador de la publicación.|  
|**MSrepl_create_time**|**datetime**|Hora en que Se ha agregado la información del conflicto.|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_helpmergeconflictrows** se utiliza en la replicación de mezcla.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor, el **db_owner** fijo de base de datos y el **replmonitor** en la base de datos de distribución pueden ejecutar **sp_helpmergeconflictrows**.  
  
## <a name="see-also"></a>Vea también  
 [Ver información de conflictos para publicaciones de mezcla &#40;programación de Transact-SQL de replicación&#41;](../../relational-databases/replication/view-conflict-information-for-merge-publications.md)   
 [Procedimientos almacenados de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
