---
title: sp_scriptpublicationcustomprocs (Transact-SQL) | Microsoft Docs
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
- sp_scriptpublicationcustomprocs
- sp_scriptpublicationcustomprocs_TSQL
helpviewer_keywords:
- sp_scriptpublicationcustomprocs
ms.assetid: b06102d5-4284-4834-b126-bc0baea49be5
caps.latest.revision: 20
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 15c841becf856af68e37273349cdb7b3fe578fdf
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2018
ms.locfileid: "43026864"
---
# <a name="spscriptpublicationcustomprocs-transact-sql"></a>sp_scriptpublicationcustomprocs (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Crea los scripts de los procedimientos INSERT, UPDATE y DELETE personalizados para todos los artículos de las tablas de una publicación en la que la opción de esquema de procedimiento personalizado de generación automática esté habilitada. **sp_scriptpublicationcustomprocs** es especialmente útil para configurar suscripciones en las que se aplica manualmente la instantánea.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_scriptpublicationcustomprocs [ @publication = ] 'publication_name'  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@publication**=] **'***publication_name***'**  
 Es el nombre de la publicación. *publication_name* es **sysname** no tiene ningún valor predeterminado.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Devuelve un conjunto de resultados que consta de una sola **nvarchar (4000)** columna. El conjunto de resultados forma toda la instrucción CREATE PROCEDURE que se necesita para crear el procedimiento almacenado personalizado.  
  
## <a name="remarks"></a>Notas  
 Los artículos sin la opción de esquema de procedimiento personalizado de generación automática (0x2) no se benefician de la creación de script de los procedimientos personalizados.  
  
 Los procedimientos siguientes se utilizan por **sp_scriptpublicationcustomprocs** para crear procedimientos en el suscriptor y no se debe ejecutar directamente:  
  
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
 Ejecutar permiso se concede a **pública**; se realiza una comprobación de seguridad dentro de este procedimiento almacenado para restringir el acceso a los miembros de la **sysadmin** rol fijo de servidor y **db_ propietario** rol fijo de base de datos en la base de datos actual.  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
