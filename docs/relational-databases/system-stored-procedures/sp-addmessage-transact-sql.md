---
title: sp_addmessage (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/16/2017
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
- sp_addmessage
- sp_addmessage_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addmessage
ms.assetid: 54746d30-f944-40e5-a707-f2d9be0fb9eb
caps.latest.revision: 25
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: b9ccc8c9b51de0b2c6c4d86acc107c9073efbfb1
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="spaddmessage-transact-sql"></a>sp_addmessage (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Almacena un nuevo mensaje de error definido por el usuario en una instancia del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. Los mensajes almacenados mediante el uso de **sp_addmessage** puede verse mediante la **sys.messages** vista de catálogo.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_addmessage [ @msgnum= ] msg_id , [ @severity= ] severity , [ @msgtext= ] 'msg'   
     [ , [ @lang= ] 'language' ]   
     [ , [ @with_log= ] { 'TRUE' | 'FALSE' } ]   
     [ , [ @replace= ] 'replace' ]   
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@msgnum*** =** ] *msg_id*  
 Es el identificador del mensaje de error. *msg_id* es **int** con un valor predeterminado es NULL. *msg_id* de error definidos por el usuario mensajes pueden ser un entero entre 50.001 y 2.147.483.647. La combinación de *msg_id* y *lenguaje* debe ser única; se devuelve un error si el identificador ya existe para el idioma especificado.  
  
 [  **@severity =** ]*gravedad*  
 Es el nivel de gravedad del error. *gravedad* es **smallint** con un valor predeterminado es NULL. Los niveles válidos son de 1 a 25. Para obtener más información sobre los niveles de gravedad, vea [Niveles de gravedad de error del motor de base de datos](../../relational-databases/errors-events/database-engine-error-severities.md).  
  
 [  **@msgtext =** ] **'***msg***'**  
 Es el texto del mensaje de error. *msg* es **nvarchar (255)** con un valor predeterminado es NULL.  
  
 [  **@lang =** ] **'***lenguaje***'**  
 Es el idioma de este mensaje. *idioma* es **sysname** con un valor predeterminado es NULL. Dado que se pueden instalar varios idiomas en el mismo servidor, *lenguaje* especifica el idioma en que está escrito cada mensaje. Cuando *lenguaje* es se omite, el idioma es el idioma predeterminado para la sesión.  
  
 [  **@with_log =** ] { **'**TRUE**'** | **'FALSE'** }  
 Especifica si el mensaje debe escribirse en el registro de aplicación Windows cuando se produzca. **@with_log** es **varchar (5)** con un valor predeterminado es FALSE. Si es TRUE, el error siempre se escribe en el registro de aplicación Windows. Si es FALSE, el error no siempre se escribe en el registro de aplicación Windows, pero se puede escribir, dependiendo de cómo se haya producido el error. Solo los miembros de la **sysadmin** rol de servidor puede usar esta opción.  
  
> [!NOTE]  
>  Si se escribe un mensaje en el registro de aplicación Windows, también se escribe en el archivo de registro de errores del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
 [ **@replace** *=* ] **'***reemplazar***'**  
 Si se especifica como la cadena *reemplazar*, mensajes de error existentes se sobrescriben con el nuevo nivel de gravedad y el texto del mensaje. *Reemplace* es **varchar(7)** con un valor predeterminado es NULL. Esta opción debe especificarse si *msg_id* ya existe. Si se sustituye un mensaje en inglés de EE.UU., Se reemplaza el mensaje en inglés, el nivel de gravedad para todos los mensajes en los demás idiomas que tienen el mismo *msg_id*.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="remarks"></a>Comentarios  
 Para las versiones no inglesas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], la versión en inglés de EE.UU. de un mensaje deberá existir para que pueda agregarse el mensaje en otro idioma. La gravedad de las dos versiones del mensaje debe coincidir.  
  
 Para traducir mensajes que contienen parámetros, utilice los números de parámetro que corresponden a los parámetros del mensaje original. Inserte un signo de exclamación (!) detrás de cada número de parámetro.  
  
|Mensaje original|Mensaje traducido|  
|----------------------|-----------------------|  
|‘Parámetro 1 del mensaje original: %s, <br /><br /> parámetro 2: %d'|‘Parámetro 1 del mensaje traducido: %1!, <br /><br /> parámetro 2: %2!'|  
  
 Debido a las diferencias sintácticas que existen entre los idiomas, puede que los números de los parámetros del mensaje traducido no aparezcan en la misma secuencia que en el mensaje original.  
  
## <a name="permissions"></a>Permissions  
Debe pertenecer a la **sysadmin** o **serveradmin** roles fijos de servidor.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-defining-a-custom-message"></a>A. Definir un mensaje personalizado  
 En el ejemplo siguiente se agrega un mensaje personalizado para **sys.messages**.  
  
```  
USE master;  
GO  
EXEC sp_addmessage 50001, 16,   
   N'Percentage expects a value between 20 and 100.   
   Please reexecute with a more appropriate value.';  
GO  
```  
  
### <a name="b-adding-a-message-in-two-languages"></a>B. Agregar un mensaje en dos idiomas  
 En el ejemplo siguiente se agrega primero un mensaje en inglés de EE.UU. y luego se agrega el mismo mensaje en francés`.`  
  
```  
USE master;  
GO  
EXEC sp_addmessage @msgnum = 60000, @severity = 16,   
   @msgtext = N'The item named %s already exists in %s.',   
   @lang = 'us_english';  
  
EXEC sp_addmessage @msgnum = 60000, @severity = 16,   
   @msgtext = N'L''élément nommé %1! existe déjà dans %2!',   
   @lang = 'French';  
GO  
```  
  
### <a name="c-changing-the-order-of-parameters"></a>C. Cambiar el orden de parámetros  
 En el ejemplo siguiente se agrega primero un mensaje en inglés de EE.UU. y luego se agrega un mensaje traducido con el orden de los parámetros cambiado.  
  
```  
USE master;  
GO  
  
EXEC sp_addmessage   
    @msgnum = 60000,   
    @severity = 16,  
    @msgtext =   
        N'This is a test message with one numeric  
        parameter (%d), one string parameter (%s),   
        and another string parameter (%s).',  
    @lang = 'us_english';  
  
EXEC sp_addmessage   
    @msgnum = 60000,   
    @severity = 16,  
    @msgtext =   
        -- In the localized version of the message,  
        -- the parameter order has changed. The   
        -- string parameters are first and second  
        -- place in the message, and the numeric   
        -- parameter is third place.  
        N'Dies ist eine Testmeldung mit einem   
        Zeichenfolgenparameter (%3!),  
        einem weiteren Zeichenfolgenparameter (%2!),   
        und einem numerischen Parameter (%1!).',  
    @lang = 'German';  
GO    
  
-- Changing the session language to use the U.S. English  
-- version of the error message.  
SET LANGUAGE us_english;  
GO  
  
RAISERROR(60000,1,1,15,'param1','param2') -- error, severity, state,  
GO                                       -- parameters.  
  
-- Changing the session language to use the German  
-- version of the error message.  
SET LANGUAGE German;  
GO  
  
RAISERROR(60000,1,1,15,'param1','param2'); -- error, severity, state,   
GO                                       -- parameters.  
```  
  
## <a name="see-also"></a>Vea también  
 [RAISERROR &#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md)   
 [sp_altermessage &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-altermessage-transact-sql.md)   
 [sp_dropmessage &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmessage-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
