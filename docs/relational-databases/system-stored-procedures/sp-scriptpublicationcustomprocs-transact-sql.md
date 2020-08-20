---
description: sp_scriptpublicationcustomprocs (Transact-SQL)
title: sp_scriptpublicationcustomprocs (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_scriptpublicationcustomprocs
- sp_scriptpublicationcustomprocs_TSQL
helpviewer_keywords:
- sp_scriptpublicationcustomprocs
ms.assetid: b06102d5-4284-4834-b126-bc0baea49be5
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: d31a6f58b62d242fd6fe056eaac198fb0a7b7738
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88481067"
---
# <a name="sp_scriptpublicationcustomprocs-transact-sql"></a>sp_scriptpublicationcustomprocs (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  Crea los scripts de los procedimientos INSERT, UPDATE y DELETE personalizados para todos los artículos de las tablas de una publicación en la que la opción de esquema de procedimiento personalizado de generación automática esté habilitada. **sp_scriptpublicationcustomprocs** es especialmente útil para configurar suscripciones para las que la instantánea se aplica manualmente.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_scriptpublicationcustomprocs [ @publication = ] 'publication_name'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication_name'` Es el nombre de la publicación. *publication_name* es de **tipo sysname** y no tiene ningún valor predeterminado.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Devuelve un conjunto de resultados que consta de una única columna **nvarchar (4000)** . El conjunto de resultados forma toda la instrucción CREATE PROCEDURE que se necesita para crear el procedimiento almacenado personalizado.  
  
## <a name="remarks"></a>Observaciones  
 Los artículos sin la opción de esquema de procedimiento personalizado de generación automática (0x2) no se benefician de la creación de script de los procedimientos personalizados.  
  
 Los procedimientos siguientes se usan en **sp_scriptpublicationcustomprocs** para crear procedimientos en el suscriptor y no deben ejecutarse directamente:  
  
 **sp_script_reconciliation_delproc**  
  
 **sp_script_reconciliation_insproc**  
  
 **sp_script_reconciliation_vdelproc**  
  
 **sp_script_reconciliation_xdelproc**  
  
 **sp_scriptdelproc**  
  
 **sp_scriptinsproc**  
  
 **sp_scriptmappedupdproc**  
  
 **sp_scriptupdproc**  
  
 **sp_scriptvdelproc**  
  
 **sp_scriptvupdproc**  
  
 **sp_scriptxdelproc**  
  
 **sp_scriptxupdproc**  
  
## <a name="permissions"></a>Permisos  
 El permiso de ejecución se concede a **Public**; dentro de este procedimiento almacenado se realiza una comprobación de seguridad de procedimiento para restringir el acceso a los miembros del rol fijo de servidor **sysadmin** y **db_owner** rol fijo de base de datos en la base de datos actual.  
  
## <a name="see-also"></a>Consulte también  
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
