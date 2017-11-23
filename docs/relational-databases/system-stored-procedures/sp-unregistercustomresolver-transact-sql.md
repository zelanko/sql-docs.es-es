---
title: sp_unregistercustomresolver (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sp_unregistercustomresolver_TSQL
- sp_unregistercustomresolver
helpviewer_keywords: sp_unregistercustomresolver
ms.assetid: 08bd20c8-c6be-4be2-be9f-2b5e1d7bee43
caps.latest.revision: "30"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 831b1004df2d4c62f81e051fb4cdb95e48a97d35
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="spunregistercustomresolver-transact-sql"></a>sp_unregistercustomresolver (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Elimina del Registro un módulo de lógica de negocios registrado anteriormente. La lógica de negocios puede estar en formato de un componente COM o un ensamblado de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework. Este procedimiento almacenado se ejecuta en el distribuidor donde se ha registrado la lógica de negocios.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_unregistercustomresolver [ @article_resolver = ] 'article_resolver'   
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@article_resolver =** ] **'***article_resolver***'**  
 Especifica el nombre de la lógica de negocios personalizada cuyo registro se está cancelando. *article_resolver* es **nvarchar (255)**, no tiene ningún valor predeterminado. Si la lógica de negocios que se va a quitar es un componente COM, este parámetro es el nombre descriptivo del componente. Si la lógica de negocios es un ensamblado de .NET Framework, este parámetro es el nombre del ensamblado.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_unregistercustomresolver** se utiliza en la replicación de mezcla.  
  
 Use [sp_enumcustomresolvers](../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md) en cualquier servidor de la topología de replicación para devolver la lista de módulos de lógica de negocios personalizada registrado o solucionadores COM disponibles para la topología.  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de servidor o **db_owner** rol fijo de base de datos puede ejecutar **sp_unregistercustomresolver**.  
  
## <a name="see-also"></a>Vea también  
 [sp_lookupcustomresolver &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-lookupcustomresolver-transact-sql.md)   
 [sp_registercustomresolver &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-registercustomresolver-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
