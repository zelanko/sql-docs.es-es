---
title: sp_helpmergedeleteconflictrows (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
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
- sp_helpmergedeleteconflictrows
- sp_helpmergedeleteconflictrows_TSQL
helpviewer_keywords:
- sp_helpmergedeleteconflictrows
ms.assetid: 222be651-5690-4341-9dfb-f9ec1d80c970
caps.latest.revision: 17
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e8bb0cf7dfa6b5eb44a7d30320f1beb0f90fbca7
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2018
ms.locfileid: "43025663"
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
 [  **@publication=**] **'***publicación***'**  
 Es el nombre de la publicación. *publicación* es **sysname**, su valor predeterminado es **%**. Si se especifica la publicación, se devuelven todos los conflictos calificados por la publicación.  
  
 [  **@source_object=**] **'***source_object***'**  
 Es el nombre del objeto de origen. *source_object* es **nvarchar (386)**, su valor predeterminado es null.  
  
 [  **@publisher=**] **'***publisher***'**  
 Es el nombre del publicador. *publisher* es **sysname**, su valor predeterminado es null.  
  
 [ **@publisher_db=**] **'***publisher_db***'**  
 Es el nombre de la base de datos del publicador. *publisher_db* es **sysname**, su valor predeterminado es null.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**source_object**|**nvarchar(386)**|Objeto de origen del conflicto de eliminación.|  
|**rowguid**|**uniqueidentifier**|Identificador de la fila del conflicto de eliminación.|  
|**conflict_type**|**int**|Código que indica el tipo de conflicto:<br /><br /> **1** = UpdateConflict: conflicto se detecta en el nivel de fila.<br /><br /> **2** = ColumnUpdateConflict: conflicto detectado en el nivel de columna.<br /><br /> **3** = UpdateDeleteWinsConflict: eliminación gana el conflicto.<br /><br /> **4** = UpdateWinsDeleteConflict: la columna rowguid eliminada que pierde el conflicto se registra en esta tabla.<br /><br /> **5** = UploadInsertFailed: inserción del suscriptor no pudo aplicarse en el publicador.<br /><br /> **6** = DownloadInsertFailed: inserción del publicador no pudo aplicarse en el suscriptor.<br /><br /> **7** = UploadDeleteFailed: no se pudo cargar la eliminación en el suscriptor en el publicador.<br /><br /> **8** = DownloadDeleteFailed: no se pudo descargar la eliminación en el publicador al suscriptor.<br /><br /> **9** = UploadUpdateFailed: actualización del suscriptor no pudo aplicarse en el publicador.<br /><br /> **10** = DownloadUpdateFailed: actualización en el publicador no pudo aplicarse al suscriptor.|  
|**reason_code**|**Int**|Código del error, que puede depender del contexto.|  
|**reason_text**|**varchar(720)**|Descripción del error, que puede depender del contexto.|  
|**origin_datasource**|**varchar (255)**|Origen del conflicto.|  
|**pubid**|**uniqueidentifier**|Identificador de la publicación.|  
|**MSrepl_create_time**|**datetime**|Hora en que Se ha agregado la información del conflicto.|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Notas  
 **sp_helpmergedeleteconflictrows** se utiliza en la replicación de mezcla.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor y el **db_owner** rol fijo de base de datos se puede ejecutar **sp_helpmergedeleteconflictrows**.  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
