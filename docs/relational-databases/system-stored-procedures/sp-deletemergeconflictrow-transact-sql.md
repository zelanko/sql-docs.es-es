---
title: sp_deletemergeconflictrow (Transact-SQL) | Documentos de Microsoft
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
- sp_deletemergeconflictrow
- sp_deletemergeconflictrow_TSQL
helpviewer_keywords:
- sp_deletemergeconflictrow
ms.assetid: 64cf1186-28b8-4cd9-88f1-a7808a9c8d60
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 971d7dcce23ed908e5bd880da1f96681be6ad88c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32989554"
---
# <a name="spdeletemergeconflictrow-transact-sql"></a>sp_deletemergeconflictrow (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Elimina las filas de una tabla de conflictos o [MSmerge_conflicts_info &#40;Transact-SQL&#41; ](../../relational-databases/system-tables/msmerge-conflicts-info-transact-sql.md) tabla. Este procedimiento almacenado se ejecuta en el equipo donde está almacenada la tabla de conflictos, en cualquier base de datos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_deletemergeconflictrow [ [ @conflict_table = ] 'conflict_table' ]  
    [ , [ @source_object = ] 'source_object' ]  
    { , [ @rowguid = ] 'rowguid'  
        , [ @origin_datasource = ] 'origin_datasource' ] }  
    [ , [ @drop_table_if_empty = ] 'drop_table_if_empty' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@conflict_table=**] **'***conflict_table***'**  
 Es el nombre de la tabla de conflictos. *conflict_table* es **sysname**, su valor predeterminado es **%**. Si el *conflict_table* se especifica como NULL o **%**, el conflicto se supone que es un conflicto de eliminación y la fila que coincida con *rowguid* y *origin_datasource* y *source_object* se elimina de la [MSmerge_conflicts_info &#40;Transact-SQL&#41; ](../../relational-databases/system-tables/msmerge-conflicts-info-transact-sql.md) tabla.  
  
 [  **@source_object=**] **'***source_object***'**  
 Es el nombre de la tabla de origen. *source_object* es **nvarchar (386)**, su valor predeterminado es null.  
  
 [  **@rowguid =**] **'***rowguid***'**  
 Es el identificador de fila del conflicto de eliminación. *ROWGUID* es **uniqueidentifier**, no tiene ningún valor predeterminado.  
  
 [  **@origin_datasource=**] **'***origin_datasource***'**  
 Es el origen del conflicto. *origin_datasource* es **varchar (255)**, no tiene ningún valor predeterminado.  
  
 [  **@drop_table_if_empty=**] **'***drop_table_if_empty***'**  
 Es una marca que indica que la *conflict_table* es que se quitará si está vacía. *drop_table_if_empty* es **varchar (10)**, con un valor predeterminado es FALSE.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_deletemergeconflictrow** se utiliza en la replicación de mezcla.  
  
 [MSmerge_conflicts_info &#40;Transact-SQL&#41; ](../../relational-databases/system-tables/msmerge-conflicts-info-transact-sql.md) tabla es una tabla del sistema y no se elimina de la base de datos, incluso si está vacía.  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de servidor o **db_owner** rol fijo de base de datos puede ejecutar **sp_deletemergeconflictrow**.  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
