---
title: sp_helpmergedeleteconflictrows (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpmergedeleteconflictrows
- sp_helpmergedeleteconflictrows_TSQL
helpviewer_keywords:
- sp_helpmergedeleteconflictrows
ms.assetid: 222be651-5690-4341-9dfb-f9ec1d80c970
author: stevestein
ms.author: sstein
ms.openlocfilehash: 86e8d3d21246cbb308db5b698a29f2b02ce45ac3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68137747"
---
# <a name="sphelpmergedeleteconflictrows-transact-sql"></a>sp_helpmergedeleteconflictrows (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve información sobre las filas de datos que han perdido conflictos de eliminación. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicaciones o en el suscriptor de la base de datos de suscripciones cuando se utiliza el registro de conflictos no centralizado.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_helpmergedeleteconflictrows [ [ @publication = ] 'publication']  
    [ , [ @source_object = ] 'source_object']  
    [ , [ @publisher = ] 'publisher'  
    [ , [ @publisher_db = ] 'publsher_db'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'` Es el nombre de la publicación. *publicación* es **sysname**, su valor predeterminado es **%** . Si se especifica la publicación, se devuelven todos los conflictos calificados por la publicación.  
  
`[ @source_object = ] 'source_object'` Es el nombre del objeto de origen. *source_object* es **nvarchar (386)** , su valor predeterminado es null.  
  
`[ @publisher = ] 'publisher'` Es el nombre del publicador. *publisher* es **sysname**, su valor predeterminado es null.  
  
`[ @publisher_db = ] 'publisher_db'` Es el nombre de la base de datos del publicador. *publisher_db* es **sysname**, su valor predeterminado es null.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**source_object**|**nvarchar(386)**|Objeto de origen del conflicto de eliminación.|  
|**rowguid**|**uniqueidentifier**|Identificador de la fila del conflicto de eliminación.|  
|**conflict_type**|**int**|Código que indica el tipo de conflicto:<br /><br /> **1** = UpdateConflict: Conflicto se detecta en el nivel de fila.<br /><br /> **2** = ColumnUpdateConflict: Conflicto se detecta en el nivel de columna.<br /><br /> **3** = UpdateDeleteWinsConflict: Eliminación gana el conflicto.<br /><br /> **4** = UpdateWinsDeleteConflict: La columna rowguid eliminada que pierde el conflicto se registra en esta tabla.<br /><br /> **5** = UploadInsertFailed: Inserción del suscriptor no pudo aplicarse en el publicador.<br /><br /> **6** = DownloadInsertFailed: Inserción del publicador no pudo aplicarse en el suscriptor.<br /><br /> **7** = UploadDeleteFailed: No se pudo cargar la eliminación en el suscriptor en el publicador.<br /><br /> **8** = DownloadDeleteFailed: No se pudo descargar la eliminación en el publicador al suscriptor.<br /><br /> **9** = UploadUpdateFailed: Actualización del suscriptor no pudo aplicarse en el publicador.<br /><br /> **10** = DownloadUpdateFailed: Actualización en el publicador no pudo aplicarse al suscriptor.|  
|**reason_code**|**Int**|Código del error, que puede depender del contexto.|  
|**reason_text**|**varchar(720)**|Descripción del error, que puede depender del contexto.|  
|**origin_datasource**|**varchar(255)**|Origen del conflicto.|  
|**pubid**|**uniqueidentifier**|Identificador de la publicación.|  
|**MSrepl_create_time**|**datetime**|Hora en que Se ha agregado la información del conflicto.|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_helpmergedeleteconflictrows** se utiliza en la replicación de mezcla.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor y el **db_owner** rol fijo de base de datos se puede ejecutar **sp_helpmergedeleteconflictrows**.  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
