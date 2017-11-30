---
title: sysmail_help_profile_sp (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sysmail_help_profile_sp_TSQL
- sysmail_help_profile_sp
dev_langs: TSQL
helpviewer_keywords: sysmail_help_profile_sp
ms.assetid: d7169a8e-92b1-49eb-9124-3b2f69755ddb
caps.latest.revision: "41"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6b2e503789cf2ad564132f34af4e9ab61464332a
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/27/2017
---
# <a name="sysmailhelpprofilesp-transact-sql"></a>sysmail_help_profile_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Muestra información acerca de uno o más perfiles de correo.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sysmail_help_profile_sp  [   [ @profile_id = ] profile_id | [ @profile_name = ] 'profile_name' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@profile_id**  =] *profile_id*  
 Identificador de perfil para el que se devuelve información. *profile_id* es **int**, su valor predeterminado es null.  
  
 [  **@profile_name**  =] **'***profile_name***'**  
 Nombre del perfil para el que se devuelve información. *profile_name* es **sysname**, su valor predeterminado es null.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Devuelve un conjunto de resultados con las columnas siguientes:  
  
||||  
|-|-|-|  
|Nombre de columna|Tipo de datos|Description|  
|**profile_id**|**int**|Id. del perfil.|  
|**Nombre**|**sysname**|Nombre del perfil.|  
|**Descripción**|**nvarchar(256)**|La descripción para el perfil.|  
  
## <a name="remarks"></a>Comentarios  
 Cuando se especifica un nombre de perfil o el identificador de perfil, **sysmail_help_profile_sp** devuelve información acerca de dicho perfil. En caso contrario, **sysmail_help_profile_sp** devuelve información acerca de todos los perfiles de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instancia.  
  
 El procedimiento almacenado **sysmail_help_profile_sp** está en el **msdb** la base de datos y es propiedad de la **dbo** esquema. El procedimiento se debe ejecutar con un nombre de tres partes si la base de datos actual no es **msdb**.  
  
## <a name="permissions"></a>Permissions  
 Permisos de ejecución para este procedimiento de forma predeterminada a los miembros de la **sysadmin** rol fijo de servidor.  
  
## <a name="examples"></a>Ejemplos  
 **A. Enumerar todos los perfiles**  
  
 En el ejemplo siguiente se muestra una lista de todos los perfiles de una instancia.  
  
```  
EXECUTE msdb.dbo.sysmail_help_profile_sp;  
```  
  
 El siguiente es un conjunto de resultados de ejemplo con la longitud de línea ajustada:  
  
```  
profile_id  name                          description  
----------- ----------------------------- ------------------------------  
56          AdventureWorks Administrator  Administrative mail profile.    
57          AdventureWorks Operator       Operator mail profile.          
```  
  
 **B. Mostrar un perfil específico**  
  
 En el ejemplo siguiente se muestra una lista de información del perfil `AdventureWorks Administrator`.  
  
```  
EXECUTE msdb.dbo.sysmail_help_profile_sp  
    @profile_name = 'AdventureWorks Administrator' ;  
```  
  
 El siguiente es un conjunto de resultados de ejemplo con la longitud de línea ajustada:  
  
```  
profile_id  name                          description  
----------- ----------------------------- ------------------------------  
56          AdventureWorks Administrator  Administrative mail profile.    
```  
  
## <a name="see-also"></a>Vea también  
 [Correo electrónico de base de datos](../../relational-databases/database-mail/database-mail.md)   
 [Correo electrónico de base de datos almacenados procedimientos &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
