---
title: sysmail_help_profile_sp (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_help_profile_sp_TSQL
- sysmail_help_profile_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_help_profile_sp
ms.assetid: d7169a8e-92b1-49eb-9124-3b2f69755ddb
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 95660c293ef8a5efcca132407cd930ab0b721d89
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/05/2020
ms.locfileid: "82827429"
---
# <a name="sysmail_help_profile_sp-transact-sql"></a>sysmail_help_profile_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Muestra información acerca de uno o más perfiles de correo.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sysmail_help_profile_sp  [   [ @profile_id = ] profile_id | [ @profile_name = ] 'profile_name' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @profile_id = ] profile_id`Identificador de perfil para el que se va a devolver información. *profile_id* es de **tipo int**y su valor predeterminado es NULL.  
  
`[ @profile_name = ] 'profile_name'`Nombre del perfil para el que se va a devolver información. *profile_name* es de **tipo sysname y su**valor predeterminado es NULL.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Devuelve un conjunto de resultados con las columnas siguientes:  
  
||||  
|-|-|-|  
|Nombre de la columna|Tipo de datos|Descripción|  
|**profile_id**|**int**|Id. del perfil.|  
|**name**|**sysname**|Nombre del perfil.|  
|**denominación**|**nvarchar(256)**|La descripción del perfil.|  
  
## <a name="remarks"></a>Comentarios  
 Cuando se especifica un nombre de perfil o un identificador de perfil, **sysmail_help_profile_sp** devuelve información acerca de ese perfil. De lo contrario, **sysmail_help_profile_sp** devuelve información sobre cada perfil de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instancia.  
  
 El procedimiento almacenado **sysmail_help_profile_sp** está en la base de datos **msdb** y pertenece al esquema **DBO** . El procedimiento se debe ejecutar con un nombre de tres partes si la base de datos actual no es **msdb**.  
  
## <a name="permissions"></a>Permisos  
 Los permisos de ejecución para este procedimiento tienen como valor predeterminado los miembros del rol fijo de servidor **sysadmin** .  
  
## <a name="examples"></a>Ejemplos  
 **A. Mostrar una lista de todos los perfiles**  
  
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
  
## <a name="see-also"></a>Consulte también  
 [Correo electrónico de base de datos](../../relational-databases/database-mail/database-mail.md)   
 [Correo electrónico de base de datos procedimientos almacenados &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
