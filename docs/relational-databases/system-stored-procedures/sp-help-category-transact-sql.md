---
title: sp_help_category (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_help_category
- sp_help_category_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_category
ms.assetid: 8cad1dcc-b43e-43bd-bea0-cb0055c84169
caps.latest.revision: 18
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a84cde301cf3c3db39f8df1999b9e4c39416c324
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/16/2018
ms.locfileid: "40395592"
---
# <a name="sphelpcategory-transact-sql"></a>sp_help_category (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Proporciona información acerca de las clases especificadas de trabajos, alertas u operadores.  
   
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_help_category [ [ @class = ] 'class' ]   
     [ , [ @type = ] 'type' ]   
     [ , [ @name = ] 'name' ]   
     [ , [ @suffix = ] suffix ]   
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@class=**] **'***clase***'**  
 La clase sobre la que se solicita información. *clase* es **varchar (8)**, con un valor predeterminado de **trabajo**. *clase* puede ser uno de estos valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**TRABAJO**|Proporciona información acerca de una categoría de trabajo.|  
|**ALERTA**|Proporciona información acerca de una categoría de alerta.|  
|**OPERADOR**|Proporciona información acerca de una categoría de operador.|  
  
 [  **@type=** ] **'***tipo***'**  
 Tipo de categoría cuya información se solicita. *tipo* es **varchar (12)**, su valor predeterminado es null, y puede tener uno de estos valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**LOCAL**|Categoría de trabajo local.|  
|**MULTI-SERVIDOR**|Categoría de trabajo multiservidor.|  
|**NONE**|Categoría para una clase distinta **trabajo**.|  
  
 [  **@name=** ] **'***nombre***'**  
 Nombre de la categoría cuya información se solicita. *nombre* es **sysname**, su valor predeterminado es null.  
  
 [  **@suffix=** ] *sufijo*  
 Especifica si el **category_type** columna del conjunto de resultados es un identificador o un nombre. *sufijo* es **bit**, su valor predeterminado es **0**. **1** muestra el **category_type** como un nombre, y **0** lo muestra como un identificador.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Cuando **@suffix** es **0**, **sp_help_category** devuelve el conjunto de resultados siguientes:  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**category_id**|**int**|Id. de categoría|  
|**category_type**|**tinyint**|Tipo de categoría:<br /><br /> **1** = local<br /><br /> **2** = multiservidor<br /><br /> **3** = ninguno|  
|**Nombre**|**sysname**|Nombre de la categoría|  
  
 Cuando **@suffix** es **1**, **sp_help_category** devuelve el conjunto de resultados siguientes:  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**category_id**|**int**|Id. de categoría|  
|**category_type**|**sysname**|Tipo de categoría. Uno de **LOCAL**, **MULTISERVIDOR**, o **NONE**|  
|**Nombre**|**sysname**|Nombre de la categoría|  
  
## <a name="remarks"></a>Notas  
 **sp_help_category** se debe ejecutar desde la **msdb** base de datos.  
  
 Si no se especifica ningún parámetro, el conjunto de resultados proporciona información acerca de todas las categorías de trabajo.  
  
## <a name="permissions"></a>Permisos  
 De forma predeterminada, los miembros del rol fijo de servidor **sysadmin** pueden ejecutar este procedimiento almacenado. Al resto de usuarios se les debe conceder uno de los siguientes roles fijos de base de datos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la base de datos **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Para detalles sobre los permisos de estos roles, consulte [Roles fijos de base de datos del Agente SQL Server](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-returning-local-job-information"></a>A. Devolver información de un trabajo local  
 Este ejemplo devuelve información acerca de los trabajos que se administran localmente.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_category  
    @type = N'LOCAL' ;  
GO  
```  
  
### <a name="b-returning-alert-information"></a>B. Devolver información de alertas  
 Este ejemplo devuelve información acerca de la categoría de alertas de replicación.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_category  
    @class = N'ALERT',  
    @name = N'Replication' ;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [sp_add_category &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-category-transact-sql.md)   
 [sp_delete_category &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-category-transact-sql.md)   
 [sp_update_category &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-category-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
