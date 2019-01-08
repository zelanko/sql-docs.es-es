---
title: sysmail_help_principalprofile_sp (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/02/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_help_principalprofile_sp_TSQL
- sysmail_help_principalprofile_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_help_principalprofile_sp
ms.assetid: 0cfd6464-09c7-4f03-9d25-58001c096a9e
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d96a4c72996ab34b03706cc71f6b406344164685
ms.sourcegitcommit: 37310da0565c2792aae43b3855bd3948fd13e044
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/18/2018
ms.locfileid: "53591629"
---
# <a name="sysmailhelpprincipalprofilesp-transact-sql"></a>sysmail_help_principalprofile_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Muestra información acerca de las asociaciones entre los perfiles del Correo electrónico de base de datos y las entidades de seguridad de la base de datos.  
  
 
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sysmail_help_principalprofile_sp [ {   [ @principal_id = ] principal_id | [ @principal_name = ] 'principal_name' } ]  
    [ [ , ] {   [ @profile_id = ] profile_id | [ @profile_name = ] 'profile_name' } ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@principal_id=** ] *principal_id*  
 Es el identificador de usuario de base de datos o del rol en el **msdb** base de datos para la asociación a la lista. *principal_id* es **int**, su valor predeterminado es null. Cualquier *principal_id* o *principal_name* se puede especificar.  
  
 [  **@principal_name=** ] **'**_principal_name_**'**  
 Es el nombre de usuario de base de datos o del rol en el **msdb** base de datos para la asociación a la lista. *principal_name* es **sysname**, su valor predeterminado es null. Cualquier *principal_id* o *principal_name* se puede especificar.  
  
 [  **@profile_id=** ] *profile_id*  
 Es el identificador del perfil para la asociación que se va a mostrar. *profile_id* es **int**, su valor predeterminado es null. Cualquier *profile_id* o *profile_name* se puede especificar.  
  
 [  **@profile_name=** ] **'**_profile_name_**'**  
 Es el nombre del perfil para la asociación que se va a mostrar. *nombre_perfil* es **sysname**, su valor predeterminado es null. Cualquier *profile_id* o *profile_name* se puede especificar.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Devuelve un conjunto de resultados que contiene las columnas que se indican en la siguiente tabla.  
  
||||  
|-|-|-|  
|Nombre de columna|Tipo de datos|Descripción|  
|**principal_id**|**int**|Id. del usuario de la base de datos.|  
|**principal_name**|**sysname**|El nombre del usuario de base de datos.|  
|**profile_id**|**int**|Número de Id. del perfil de Correo electrónico de base de datos.|  
|**nombre_perfil**|**sysname**|Nombre del perfil de Correo electrónico de base de datos.|  
|**is_default**|**bit**|Marca que indica si el perfil es el perfil predeterminado del usuario.|  
  
## <a name="remarks"></a>Comentarios  
 Si **sysmail_help_principalprofile_sp** se invoca sin parámetros, el conjunto de resultados devuelto muestran todas las asociaciones en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. En caso contrario, el conjunto de resultados contiene información para las asociaciones que coincidan con los parámetros suministrados. Por ejemplo, en el procedimiento se muestran todas las asociaciones para un perfil cuando se proporciona el nombre del perfil.  
  
 **sysmail_help_principalprofile_sp** está en el **msdb** de base de datos y que pertenece el **dbo** esquema. El procedimiento debe ejecutarse con un nombre de tres partes si la base de datos actual no es **msdb**.  
  
## <a name="permissions"></a>Permisos  
 Requiere la pertenencia al rol fijo de servidor **sysadmin** .  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-listing-information-for-a-specific-association"></a>A. Mostrar información para una asociación específica  
 En el ejemplo siguiente se indica cómo mostrar información para todas las asociaciones entre el perfil `AdventureWorks Administrator` y la entidad de seguridad `ApplicationLogin` en la base de datos `msdb`.  
  
```  
EXECUTE msdb.dbo.sysmail_help_principalprofile_sp  
    @principal_name = 'danw',  
    @profile_name = 'AdventureWorks Administrator' ;  
```  
  
 A continuación se muestra un conjunto de resultados de ejemplo con el formato cambiado para la longitud de línea.  
  
```  
principal_id principal_name     profile_id  profile_name                   is_default  
------------ ------------------ ----------- ------------------------------ ----------  
5            danw               9           AdventureWorks Administrator   1  
```  
  
### <a name="b-listing-information-for-all-associations"></a>b. Mostrar información para todas las asociaciones  
 En el ejemplo siguiente se indica cómo mostrar la información de todas las asociaciones en la instancia.  
  
```  
EXECUTE msdb.dbo.sysmail_help_principalprofile_sp ;  
```  
  
 A continuación se muestra un conjunto de resultados de ejemplo con el formato cambiado para la longitud de línea.  
  
```  
principal_id principal_name     profile_id  profile_name                   is_default  
------------ ------------------ ----------- ------------------------------ ----------  
6            terrid             3           Product Update Profile         1  
5            danw               9           AdventureWorks Administrator   1  
```  
  
## <a name="see-also"></a>Vea también  
 [Correo electrónico de base de datos](../../relational-databases/database-mail/database-mail.md)   
 [Procedimientos almacenados de correo electrónico de base de datos &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
