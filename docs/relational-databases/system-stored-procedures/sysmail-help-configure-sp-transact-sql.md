---
title: sysmail_help_configure_sp (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sysmail_help_configure_sp
- sysmail_help_configure_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_help_configure_sp
ms.assetid: e598d4c8-3041-4965-b046-dce3a8e3d3e0
caps.latest.revision: 34
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 823d7549fdf6f2f4e452c5b46f3c914d24528647
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sysmailhelpconfiguresp-transact-sql"></a>sysmail_help_configure_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Muestra la configuración del Correo electrónico de base de datos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sysmail_help_configure_sp  [ [ @parameter_name = ] 'parameter_name' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [**@parameter_name** =] **'***parameter_name***'**  
 Nombre del parámetro de configuración que se va a recuperar. Cuando se especifica, se devuelve el valor de la opción de configuración en el **@parameter_value** parámetro de salida. Si no **@parameter_name** se especifica, este procedimiento almacenado devuelve un conjunto que contiene todos los valores de configuración de correo electrónico de base de datos en la instancia de resultados.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Si no **@parameter_name** se especifica, se devuelve un conjunto de resultados con las siguientes columnas.  
  
||||  
|-|-|-|  
|Nombre de columna|Tipo de datos|Description|  
|**paramName**|**nvarchar(256)**|El nombre del parámetro de configuración.|  
|**ParamValue**|**nvarchar(256)**|Valor del parámetro de configuración.|  
|**Descripción**|**nvarchar(256)**|Descripción del parámetro de configuración.|  
  
## <a name="remarks"></a>Comentarios  
 El procedimiento almacenado **sysmail_help_configure_sp** enumera los valores de configuración de correo electrónico de base de datos actuales para la instancia.  
  
 Cuando un **@parameter_name** se especifica, pero no se proporciona ningún parámetro de salida para **@parameter_value**, este procedimiento almacenado no genera ningún resultado.  
  
 El procedimiento almacenado **sysmail_help_configure_sp** está en el **msdb** la base de datos y es propiedad de la **dbo** esquema. Debe llamar al procedimiento con un nombre de tres partes si la base de datos actual no es **msdb**.  
  
## <a name="permissions"></a>Permissions  
 Permisos de ejecución para este procedimiento de forma predeterminada a los miembros de la **sysadmin** rol fijo de servidor.  
  
## <a name="examples"></a>Ejemplos  
 En este ejemplo se muestra la lista de parámetros de configuración del Correo electrónico de base de datos de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```  
EXECUTE msdb.dbo.sysmail_help_configure_sp ;  
```  
  
 El siguiente es un conjunto de resultados de ejemplo con la longitud de línea editada:  
  
```  
paramname                       paramvalue      description  
------------------------------- --------------- -----------------------------------------------------------------------------  
AccountRetryAttempts            1               Number of retry attempts for a mail server  
AccountRetryDelay               5000            Delay between each retry attempt to mail server  
DatabaseMailExeMinimumLifeTime  600             Minimum process lifetime in seconds  
DefaultAttachmentEncoding       MIME            Default attachment encoding  
LoggingLevel                    2               Database Mail logging level: normal - 1, extended - 2 (default), verbose - 3  
MaxFileSize                     1000000         Default maximum file size  
ProhibitedExtensions            exe,dll,vbs,js  Extensions not allowed in outgoing mails  
  
```  
  
## <a name="see-also"></a>Vea también  
 [Correo electrónico de base de datos](../../relational-databases/database-mail/database-mail.md)   
 [Procedimientos almacenados de correo electrónico de base de datos &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
