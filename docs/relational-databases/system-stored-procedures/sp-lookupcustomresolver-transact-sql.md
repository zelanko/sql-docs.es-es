---
title: sp_lookupcustomresolver (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
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
- sp_lookupcustomresolver_TSQL
- sp_lookupcustomresolver
helpviewer_keywords:
- sp_lookupcustomresolver
ms.assetid: 356a7b8a-ae53-4fb5-86ee-fcfddbf23ddd
caps.latest.revision: 20
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ad45f26fbd1c6b7f9488497333f5ba44a2b5fa8c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="splookupcustomresolver-transact-sql"></a>sp_lookupcustomresolver (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve información acerca de un controlador de lógica de negocios o el valor del identificador de clase (CLSID) de un componente de solucionador personalizado basado en COM registrado en el distribuidor. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_lookupcustomresolver [ @article_resolver = ] 'article_resolver'   
    [, [ @resolver_clsid = ] 'resolver_clsid' OUTPUT ]  
    [ , [ @is_dotnet_assembly = ] is_dotnet_assembly OUTPUT ]  
    [ , [ @dotnet_assembly_name = ] 'dotnet_assembly_name' OUTPUT ]  
    [ , [ @dotnet_class_name = ] 'dotnet_class_name' OUTPUT ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@article_resolver =** ] **'***article_resolver***'**  
 Especifica el nombre de la lógica de negocios personalizada cuyo registro se está cancelando. *article_resolver* es **nvarchar (255)**, no tiene ningún valor predeterminado. Si la lógica de negocios que se va a quitar es un componente COM, este parámetro es el nombre descriptivo del componente. Si la lógica de negocios es un ensamblado de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework, este parámetro es el nombre del ensamblado.  
  
 [ **@resolver_clsid**=] **'***resolver_clsid***'** salida  
 Es el valor CLSID del objeto COM asociado con el nombre de la lógica de negocios personalizada especificada en el *article_resolver* parámetro. *resolver_clsid* es **nvarchar (50)**, su valor predeterminado es null.  
  
 [  **@is_dotnet_assembly=** ] **'***is_dotnet_assembly***'** salida  
 Especifica el tipo de la lógica de negocios personalizada que se va a registrar. *is_dotnet_assembly* es **bits**, con un valor predeterminado es 0. **1** indica que la lógica de negocios personalizada que se va a registrar es un controlador de lógica de negocios ensamblado; **0** indica que es un componente COM.  
  
 [  **@dotnet_assembly_name=** ] **'***dotnet_assembly_name***'** salida  
 Es el nombre del ensamblado que implementa el controlador de lógica de negocios. *dotnet_assembly_name* es **nvarchar (255)**, su valor predeterminado es null.  
  
 [  **@dotnet_class_name=** ] **'***dotnet_class_name***'** salida  
 Es el nombre de la clase que reemplaza <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> para implementar el controlador de lógica de negocios. *dotnet_class_name* es **nvarchar (255)**, su valor predeterminado es null.  
  
 [  **@publisher=** ] **'***publisher***'**  
 Es el nombre del publicador. *Publisher* es **sysname**, su valor predeterminado es null. Utilice este parámetro si no se llama al procedimiento almacenado desde el publicador. Si no se especifica, se da por supuesto que el servidor local es el publicador.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_lookupcustomresolver** se utiliza en la replicación de mezcla.  
  
 **sp_lookupcustomresolver** devuelve un valor NULL para *resolver_clsid* cuando el componente no está registrado en la distribución y el valor "00000000-0000-0000-0000-000000000000" si el registro pertenece a un Ensamblado de .NET framework registrado como un controlador de lógica de negocios.  
  
 **sp_lookupcustomresolver** llama a [sp_addmergearticle](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) y [sp_changemergearticle](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md) para validar especificado *article_resolver*.  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **db_owner** rol fijo de base de datos en la base de datos de publicación puede ejecutar **sp_lookupcustomresolver**.  
  
## <a name="see-also"></a>Vea también  
 [Advanced Merge Replication Conflict Detection and Resolution](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [Ejecutar lógica de negocios durante la sincronización de mezcla](../../relational-databases/replication/merge/execute-business-logic-during-merge-synchronization.md)   
 [Implement a Business Logic Handler for a Merge Article](../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)  (Implementar un controlador de lógica de negocios para un artículo de mezcla)  
 [Especificar a un solucionador de artículos de mezcla](../../relational-databases/replication/publish/specify-a-merge-article-resolver.md)   
 [sp_registercustomresolver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-registercustomresolver-transact-sql.md)   
 [sp_unregistercustomresolver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-unregistercustomresolver-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
