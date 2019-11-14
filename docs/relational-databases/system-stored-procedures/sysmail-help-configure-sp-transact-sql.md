---
title: sysmail_help_configure_sp (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_help_configure_sp
- sysmail_help_configure_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_help_configure_sp
ms.assetid: e598d4c8-3041-4965-b046-dce3a8e3d3e0
author: stevestein
ms.author: sstein
ms.openlocfilehash: 3d07f77c468bb14b28cd003f599bebd636d6f862
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056158"
---
# <a name="sysmail_help_configure_sp-transact-sql"></a>sysmail_help_configure_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Muestra la configuración del Correo electrónico de base de datos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo a temas") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sysmail_help_configure_sp  [ [ @parameter_name = ] 'parameter_name' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @parameter_name = ] 'parameter_name'` el nombre de la opción de configuración que se va a recuperar. Cuando se especifica, el valor de la opción de configuración se devuelve en el **\@parameter_value** parámetro de salida. Cuando no se especifica ningún **parameter_name de\@** , este procedimiento almacenado devuelve un conjunto de resultados que contiene todos los valores de configuración de correo electrónico de base de datos de la instancia.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Cuando no se especifica ningún **parameter_name de\@** , devuelve un conjunto de resultados con las columnas siguientes.  
  
||||  
|-|-|-|  
|Nombre de columna|Tipo de datos|Descripción|  
|**paramName**|**nvarchar(256)**|Nombre del parámetro de configuración.|  
|**parámetro ParamValue**|**nvarchar(256)**|Valor del parámetro de configuración.|  
|**description**|**nvarchar(256)**|Descripción del parámetro de configuración.|  
  
## <a name="remarks"></a>Remarks  
 En el procedimiento almacenado **sysmail_help_configure_sp** se enumeran los valores de configuración correo electrónico de base de datos actuales para la instancia.  
  
 Cuando se especifica un **parameter_name de\@** , pero no se proporciona ningún parámetro de salida para **\@parameter_value**, este procedimiento almacenado no genera ningún resultado.  
  
 El procedimiento almacenado **sysmail_help_configure_sp** está en la base de datos **msdb** y pertenece al esquema **DBO** . El procedimiento se debe invocar con un nombre de tres partes si la base de datos actual no es **msdb**.  
  
## <a name="permissions"></a>Permisos  
 Los permisos de ejecución para este procedimiento tienen como valor predeterminado los miembros del rol fijo de servidor **sysadmin** .  
  
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
 [Procedimientos &#40;almacenados de correo electrónico de base de datos TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
