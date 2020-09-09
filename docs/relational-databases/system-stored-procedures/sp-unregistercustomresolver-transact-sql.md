---
description: sp_unregistercustomresolver (Transact-SQL)
title: sp_unregistercustomresolver (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_unregistercustomresolver_TSQL
- sp_unregistercustomresolver
helpviewer_keywords:
- sp_unregistercustomresolver
ms.assetid: 08bd20c8-c6be-4be2-be9f-2b5e1d7bee43
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 54d4b4ff0b08f0cd5a2a1275c0f1bc65d462137e
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/08/2020
ms.locfileid: "89547326"
---
# <a name="sp_unregistercustomresolver-transact-sql"></a>sp_unregistercustomresolver (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Elimina del Registro un módulo de lógica de negocios registrado anteriormente. La lógica de negocios puede estar en formato de un componente COM o un ensamblado de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework. Este procedimiento almacenado se ejecuta en el distribuidor donde se ha registrado la lógica de negocios.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_unregistercustomresolver [ @article_resolver = ] 'article_resolver'   
```  
  
## <a name="arguments"></a>Argumentos  
`[ @article_resolver = ] 'article_resolver'` Especifica el nombre de la lógica de negocios personalizada que se va a eliminar del registro. *article_resolver* es de tipo **nvarchar (255)** y no tiene ningún valor predeterminado. Si la lógica de negocios que se va a quitar es un componente COM, este parámetro es el nombre descriptivo del componente. Si la lógica de negocios es un ensamblado de .NET Framework, este parámetro es el nombre del ensamblado.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Observaciones  
 **sp_unregistercustomresolver** se utiliza en la replicación de mezcla.  
  
 Utilice [sp_enumcustomresolvers](../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md) en cualquier servidor de la topología de replicación para devolver la lista de módulos de lógica de negocios personalizados registrados o los solucionadores com disponibles para la topología.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros del rol fijo de servidor **sysadmin** o del rol fijo de base de datos **db_owner** pueden ejecutar **sp_unregistercustomresolver**.  
  
## <a name="see-also"></a>Consulte también  
 [sp_lookupcustomresolver &#40;&#41;de Transact-SQL ](../../relational-databases/system-stored-procedures/sp-lookupcustomresolver-transact-sql.md)   
 [sp_registercustomresolver &#40;&#41;de Transact-SQL ](../../relational-databases/system-stored-procedures/sp-registercustomresolver-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
