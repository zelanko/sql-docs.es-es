---
title: sp_enumcustomresolvers (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_enumcustomresolvers
- sp_enumcustomresolvers_TSQL
helpviewer_keywords:
- sp_enumcustomresolvers
ms.assetid: 81bd0d3a-48dc-42b1-b662-c630f61fc630
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4e07931ebbecafdede044582ca06c2636ab195d8
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2019
ms.locfileid: "58526607"
---
# <a name="spenumcustomresolvers-transact-sql"></a>sp_enumcustomresolvers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve una lista de todos los controladores de lógica de negocios y solucionadores personalizados disponibles registrados en el distribuidor. Este procedimiento almacenado se ejecuta en el publicador de cualquier base de datos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_enumcustomresolvers [ [ @distributor =] 'distributor']  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @distributor = ] 'distributor'` Es el nombre del distribuidor donde se encuentra el solucionador personalizado. *distribuidor* es **sysname**, su valor predeterminado es null. *Este parámetro está en desuso y se quitará en futuras versiones.*  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**article_resolver**|**nvarchar(255)**|Nombre descriptivo del controlador de lógica de negocios o del solucionador de conflictos.|  
|**resolver_clsid**|**nvarchar(50)**|Identificador de clase (CLSID) del solucionador basado en COM. Para un controlador de lógica de negocios, esta columna devuelve un valor de CLSID de cero.|  
|**is_dotnet_assembly**|**bit**|Indica si el registro es para un controlador de lógica de negocios.<br /><br /> **0** = Solucionador de conflictos basado en COM<br /><br /> **1** = controlador de lógica de negocios|  
|**dotnet_assembly_name**|**nvarchar(255)**|Nombre del ensamblado de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework que implementa el controlador de la lógica de negocios.|  
|**dotnet_class_name**|**nvarchar(255)**|Es el nombre de la clase que reemplaza <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> para implementar el controlador de lógica de negocios.|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_enumcustomresolvers** se utiliza en la replicación de mezcla.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor y el **db_owner** rol fijo de base de datos se puede ejecutar **sp_enumcustomresolvers**.  
  
## <a name="see-also"></a>Vea también  
 [Implement a Business Logic Handler for a Merge Article](../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)  (Implementar un controlador de lógica de negocios para un artículo de mezcla)  
 [Implementar un solucionador de conflictos personalizado para un artículo de mezcla](../../relational-databases/replication/implement-a-custom-conflict-resolver-for-a-merge-article.md)   
 [sp_lookupcustomresolver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-lookupcustomresolver-transact-sql.md)   
 [sp_unregistercustomresolver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-unregistercustomresolver-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
