---
title: sp_send_dbmail (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sendmail_sp_TSQL
- sendmail_sp
- SP_SEND_DBMAIL_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_send_dbmail
ms.assetid: f1d7a795-a3fd-4043-ac4b-c781e76dab47
author: stevestein
ms.author: sstein
ms.openlocfilehash: 23fe27611e0a3ec329d37d46ea2de5e9d97bf681
ms.sourcegitcommit: 3de1fb410de2515e5a00a5dbf6dd442d888713ba
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/02/2019
ms.locfileid: "70211227"
---
# <a name="sp_send_dbmail-transact-sql"></a>sp_send_dbmail (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  Envía un mensaje de correo electrónico a los destinatarios especificados. El mensaje puede incluir un conjunto de resultados de una consulta, datos adjuntos o ambos elementos. Cuando mail se coloca correctamente en la cola de Correo electrónico de base de datos, **sp_send_dbmail** devuelve el **mailitem_id** del mensaje. Este procedimiento almacenado está en la base de datos **msdb** .  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_send_dbmail [ [ @profile_name = ] 'profile_name' ]  
    [ , [ @recipients = ] 'recipients [ ; ...n ]' ]  
    [ , [ @copy_recipients = ] 'copy_recipient [ ; ...n ]' ]  
    [ , [ @blind_copy_recipients = ] 'blind_copy_recipient [ ; ...n ]' ]  
    [ , [ @from_address = ] 'from_address' ]  
    [ , [ @reply_to = ] 'reply_to' ]   
    [ , [ @subject = ] 'subject' ]   
    [ , [ @body = ] 'body' ]   
    [ , [ @body_format = ] 'body_format' ]  
    [ , [ @importance = ] 'importance' ]  
    [ , [ @sensitivity = ] 'sensitivity' ]  
    [ , [ @file_attachments = ] 'attachment [ ; ...n ]' ]  
    [ , [ @query = ] 'query' ]  
    [ , [ @execute_query_database = ] 'execute_query_database' ]  
    [ , [ @attach_query_result_as_file = ] attach_query_result_as_file ]  
    [ , [ @query_attachment_filename = ] query_attachment_filename ]  
    [ , [ @query_result_header = ] query_result_header ]  
    [ , [ @query_result_width = ] query_result_width ]  
    [ , [ @query_result_separator = ] 'query_result_separator' ]  
    [ , [ @exclude_query_output = ] exclude_query_output ]  
    [ , [ @append_query_error = ] append_query_error ]  
    [ , [ @query_no_truncate = ] query_no_truncate ]   
    [ , [ @query_result_no_padding = ] @query_result_no_padding ]   
    [ , [ @mailitem_id = ] mailitem_id ] [ OUTPUT ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @profile_name = ] 'profile_name'`Es el nombre del perfil del que se va a enviar el mensaje. *Profile_name* es de tipo **sysname y su**valor predeterminado es NULL. *Profile_name* debe ser el nombre de un perfil de correo electrónico de base de datos existente. Cuando no se especifica ningún valor de *profile_name* , **sp_send_dbmail** usa el perfil privado predeterminado para el usuario actual. Si el usuario no tiene un perfil privado predeterminado, **sp_send_dbmail** utiliza el perfil público predeterminado para la base de datos **msdb** . Si el usuario no tiene un perfil privado predeterminado y no hay ningún perfil público predeterminado para la base de datos **@profile_name** , se debe especificar.  
  
`[ @recipients = ] 'recipients'`Es una lista delimitada por puntos y coma de direcciones de correo electrónico a las que se va a enviar el mensaje. La lista de destinatarios es de tipo **VARCHAR (Max)** . Aunque este parámetro es opcional, se **@recipients** **@blind_copy_recipients** debe especificar al menos **@copy_recipients** uno de los parámetros, o, o **sp_send_dbmail** devuelve un error.  
  
`[ @copy_recipients = ] 'copy_recipients'`Es una lista delimitada por signos de punto y coma de direcciones de correo electrónico en las que se copia el mensaje. La lista de destinatarios de copia es de tipo **VARCHAR (Max)** . Aunque este parámetro es opcional, se **@recipients** **@blind_copy_recipients** debe especificar al menos **@copy_recipients** uno de los parámetros, o, o **sp_send_dbmail** devuelve un error.  
  
`[ @blind_copy_recipients = ] 'blind_copy_recipients'`Es una lista delimitada por signos de punto y coma de direcciones de correo electrónico a las que se debe copiar el mensaje en una copia oculta. La lista de destinatarios de copia oculta es de tipo **VARCHAR (Max)** . Aunque este parámetro es opcional, se **@recipients** **@blind_copy_recipients** debe especificar al menos **@copy_recipients** uno de los parámetros, o, o **sp_send_dbmail** devuelve un error.  
  
`[ @from_address = ] 'from_address'`Es el valor de la dirección "from" del mensaje de correo electrónico. Se trata de un parámetro opcional que se usa para invalidar la configuración del perfil de correo. Este parámetro es de tipo **VARCHAR (Max)** . La configuración de seguridad de SMTP determina si se aceptan estas invalidaciones. Si no se especifica ningún parámetro, el valor predeterminado es NULL.  
  
`[ @reply_to = ] 'reply_to'`Es el valor de ' Reply to address ' del mensaje de correo electrónico. Solo acepta una dirección de correo electrónico como valor válido. Se trata de un parámetro opcional que se usa para invalidar la configuración del perfil de correo. Este parámetro es de tipo **VARCHAR (Max)** . La configuración de seguridad de SMTP determina si se aceptan estas invalidaciones. Si no se especifica ningún parámetro, el valor predeterminado es NULL.  
  
`[ @subject = ] 'subject'`Es el asunto del mensaje de correo electrónico. El asunto es de tipo **nvarchar (255)** . Si no se especifica ningún asunto, el valor predeterminado es 'Mensaje de SQL Server'.  
  
`[ @body = ] 'body'`Es el cuerpo del mensaje de correo electrónico. El cuerpo del mensaje es de tipo **nvarchar (Max)** y su valor predeterminado es NULL.  
  
`[ @body_format = ] 'body_format'`Es el formato del cuerpo del mensaje. El parámetro es de tipo **VARCHAR (20)** y su valor predeterminado es NULL. Si se especifica, los encabezados del mensaje saliente indican que el cuerpo del mensaje tiene el formato especificado. El parámetro puede contener uno de los siguientes valores:  
  
-   TEXT  
  
-   HTML  
  
 El valor predeterminado es TEXT.  
  
`[ @importance = ] 'importance'`Es la importancia del mensaje. El parámetro es de tipo **VARCHAR (6)** . El parámetro puede contener uno de los siguientes valores:  
  
-   Bajo  
  
-   Normal  
  
-   Alto  
  
 El valor predeterminado es Normal.  
  
`[ @sensitivity = ] 'sensitivity'`Es la confidencialidad del mensaje. El parámetro es de tipo **VARCHAR (12)** . El parámetro puede contener uno de los siguientes valores:  
  
-   Normal  
  
-   Personal  
  
-   Privada  
  
-   Confidential  
  
 El valor predeterminado es Normal.  
  
`[ @file_attachments = ] 'file_attachments'`Es una lista delimitada por signos de punto y coma de nombres de archivo que se van a adjuntar al mensaje de correo electrónico. Especifique los archivos de la lista como rutas de acceso absolutas. La lista de datos adjuntos es de tipo **nvarchar (Max)** . De forma predeterminada, Correo electrónico de base de datos limita los datos adjuntos a 1 MB por archivo.  
 
 > [!IMPORTANT]
 > Este parámetro no está disponible en Azure SQL Instancia administrada porque no puede acceder al sistema de archivos local.
  
`[ @query = ] 'query'`Es una consulta que se va a ejecutar. Los resultados de la consulta pueden adjuntarse como archivo o incluirse en el cuerpo del mensaje de correo electrónico. La consulta es de tipo **nvarchar (Max)** y puede contener cualquier instrucción válida [!INCLUDE[tsql](../../includes/tsql-md.md)] . Tenga en cuenta que la consulta se ejecuta en una sesión independiente, por lo que las variables locales del script que llaman a **sp_send_dbmail** no están disponibles para la consulta.  
  
`[ @execute_query_database = ] 'execute_query_database'`Es el contexto de la base de datos en el que el procedimiento almacenado ejecuta la consulta. El parámetro es de tipo **sysname**y su valor predeterminado es la base de datos actual. Este parámetro solo es aplicable si **@query** se especifica.  
  
`[ @attach_query_result_as_file = ] attach_query_result_as_file`Especifica si el conjunto de resultados de la consulta se devuelve como un archivo adjunto. *attach_query_result_as_file* es de tipo **bit**y su valor predeterminado es 0.  
  
 Cuando el valor es 0, los resultados de la consulta se incluyen en el cuerpo del mensaje de correo electrónico, después del **@body** contenido del parámetro. Si el valor es 1, los resultados se devuelven como dato adjunto. Este parámetro solo es aplicable si **@query** se especifica.  
  
`[ @query_attachment_filename = ] query_attachment_filename`Especifica el nombre de archivo que se va a utilizar para el conjunto de resultados de los datos adjuntos de la consulta. *query_attachment_filename* es de tipo **nvarchar (255)** y su valor predeterminado es NULL. Este parámetro se omite cuando *attach_query_result* es 0. Cuando *attach_query_result* es 1 y este parámetro es NULL, correo electrónico de base de datos crea un nombre de archivo arbitrario.  
  
`[ @query_result_header = ] query_result_header`Especifica si los resultados de la consulta incluyen encabezados de columna. El valor de query_result_header es de tipo **bit**. Si el valor es 1, los resultados de la consulta contienen encabezados de columna. Si el valor es 0, los resultados de la consulta no contienen encabezados de columna. El valor predeterminado de este parámetro es **1**. Este parámetro solo es aplicable si **@query** se especifica.  
 
   >[!NOTE]
   > El siguiente error puede producirse cuando @query_result_header se establece en 0 @query_no_truncate y se establece en 1:
   > <br> Mensaje 22050, nivel 16, estado 1, línea 12: No se pudo inicializar la biblioteca SQLCMD con el número de error 2147024809.
  
`[ @query_result_width = ] query_result_width`Es el ancho de línea, en caracteres, que se va a utilizar para dar formato a los resultados de la consulta. *Query_result_width* es de tipo **int**y su valor predeterminado es 256. El valor proporcionado debe estar entre 10 y 32767. Este parámetro solo es aplicable si **@query** se especifica.  
  
`[ @query_result_separator = ] 'query_result_separator'`Es el carácter que se usa para separar las columnas en el resultado de la consulta. El separador es de tipo **Char (1)** . El valor predeterminado es ' ' (espacio).  
  
`[ @exclude_query_output = ] exclude_query_output`Especifica si se debe devolver la salida de la ejecución de la consulta en el mensaje de correo electrónico. **exclude_query_output** es de bit y su valor predeterminado es 0. Cuando este parámetro es 0, la ejecución del procedimiento almacenado **sp_send_dbmail** imprime el mensaje devuelto como resultado de la ejecución de la consulta en la consola. Cuando este parámetro es 1, la ejecución del procedimiento almacenado **sp_send_dbmail** no imprime ninguno de los mensajes de ejecución de la consulta en la consola.  
  
`[ @append_query_error = ] append_query_error`Especifica si se debe enviar el mensaje de correo electrónico cuando se devuelve un error desde **@query** la consulta especificada en el argumento. **append_query_error** es de **bit**y su valor predeterminado es 0. Cuando este parámetro es 1, el Correo electrónico de base de datos envía el mensaje de correo electrónico e incluye en el cuerpo del mismo el mensaje de error de la consulta. Cuando este parámetro es 0, Correo electrónico de base de datos no envía el mensaje de correo electrónico y **sp_send_dbmail** finaliza con el código de retorno 1, lo que indica un error.  
  
`[ @query_no_truncate = ] query_no_truncate`Especifica si se va a ejecutar la consulta con la opción que evita el truncamiento de tipos de datos de longitud variable grande (**VARCHAR (Max)** , **nvarchar (Max)** , **varbinary (Max)** , **XML**, **Text**, **ntext**, **Image** y los tipos de datos definidos por el usuario). Si el establece, los resultados de la consulta no contienen encabezados de columna. El valor de *query_no_truncate* es de tipo **bit**. Si el valor es 0 o no se especifica, las columnas de la consulta se truncan a 256 caracteres. Si el valor es 1, las columnas de la consulta no se truncan. El valor predeterminado de este parámetro es 0.  
  
> [!NOTE]  
>  Cuando se usa con grandes cantidades de datos, la opción @**query_no_truncate** consume recursos adicionales y puede reducir el rendimiento del servidor.  
  
`[ @query_result_no_padding ] @query_result_no_padding`El tipo es bit. El valor predeterminado es 0. Cuando se establece en 1, los resultados de la consulta no se rellenan, lo que puede reducir el tamaño del archivo. Si establece @query_result_no_padding en 1 y establece el @query_result_width parámetro, el @query_result_no_padding parámetro sobrescribe el @query_result_width parámetro.  
  
 En este caso no se producen errores.  
 
  >[!NOTE]
  > El siguiente error puede producirse cuando @query_result_no_padding se establece en 1 y se proporciona un parámetro para@query_no_truncate:
  > <br> Mensaje 22050, nivel 16, estado 1, línea 0: No se pudo ejecutar la consulta porque @query_result_no_append las @query_no_truncate opciones y son mutuamente excluyentes. 
  
 Si establece @query_result_no_padding en 1 y establece el @query_no_truncate parámetro, se produce un error.  
  
`[ @mailitem_id = ] mailitem_id [ OUTPUT ]`El parámetro de salida opcional devuelve el *mailitem_id* del mensaje. *Mailitem_id* es de tipo **int**.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 Un código de retorno de 0 significa éxito. Cualquier otro valor significa error. El código de error de la instrucción en la que se produjo el@ERROR error se almacena en la variable @.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Si se ejecuta correctamente, devuelve el mensaje "Correo en cola".  
  
## <a name="remarks"></a>Comentarios  
 Antes de su uso, Correo electrónico de base de datos se debe habilitar mediante el Asistente para configuración de Correo electrónico de base de datos o **sp_configure**.  
  
 **sysmail_stop_sp** detiene correo electrónico de base de datos deteniendo los objetos Service Broker que usa el programa externo. **sp_send_dbmail** sigue aceptando correo cuando se detiene correo electrónico de base de datos con **sysmail_stop_sp**. Para iniciar Correo electrónico de base de datos, use **sysmail_start_sp**.  
  
 Cuando **@profile** no se especifica, **sp_send_dbmail** utiliza un perfil predeterminado. Si el usuario que envía el mensaje de correo electrónico tiene un perfil privado predeterminado, el Correo electrónico de base de datos utilizará dicho perfil. Si el usuario no tiene un perfil privado predeterminado, **sp_send_dbmail** utiliza el perfil público predeterminado. Si no hay ningún perfil privado predeterminado para el usuario y ningún perfil público predeterminado, **sp_send_dbmail** devuelve un error.  
  
 **sp_send_dbmail** no admite mensajes de correo electrónico sin contenido. Para enviar un mensaje de correo electrónico, debe especificar al menos uno **@body** de **@query** los **@file_attachments** de, **@subject** , o. De lo contrario, **sp_send_dbmail** devuelve un error.  
  
 El Correo electrónico de base de datos utiliza el contexto de seguridad de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows del usuario actual para controlar el acceso a los archivos. Por lo tanto, los usuarios que se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autentican con autenticación no **@file_attachments** pueden adjuntar archivos mediante. Tenga en cuenta que Windows no permite que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proporcione credenciales desde un equipo remoto a otro. Por lo tanto, es posible que el Correo electrónico de base de datos no pueda adjuntar archivos desde un recurso compartido de red en aquellos casos en los que el comando se ejecuta desde un equipo que no sea el equipo donde se ejecuta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Si se especifican **@file_attachmentsyy** no se encuentra el archivo, la consulta se sigue ejecutando pero no se envía el correo electrónico. **@query**  
  
 Cuando se especifica una consulta, el conjunto de resultados se formatea como texto insertado. Los datos binarios del conjunto de resultados se envían en formato hexadecimal.  
  
 Los parámetros **@recipients** , **@copy_recipients** y **@blind_copy_recipients** son listas delimitadas por punto y coma de direcciones de correo electrónico. Se debe proporcionar al menos uno de estos parámetros, o **sp_send_dbmail** devuelve un error.  
  
 Al ejecutar **sp_send_dbmail** sin un contexto de transacción, correo electrónico de base de datos inicia y confirma una transacción implícita. Al ejecutar **sp_send_dbmail** desde una transacción existente, correo electrónico de base de datos se basa en el usuario para confirmar o revertir los cambios. No inicia ninguna transacción interna.  
  
## <a name="permissions"></a>Permisos  
 De forma predeterminada, los permisos de ejecución de **sp_send_dbmail** para todos los miembros del rol de base de datos **DatabaseMailUser** en la base de datos **msdb** . Sin embargo, cuando el usuario que envía el mensaje no tiene permiso para usar el perfil para la solicitud, **sp_send_dbmail** devuelve un error y no envía el mensaje.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-sending-an-e-mail-message"></a>A. Enviar un mensaje de correo electrónico  
 En este ejemplo se envía un mensaje de correo electrónico a su amigo `myfriend@Adventure-Works.com`mediante la dirección de correo electrónico. El asunto del mensaje es `Automated Success Message`. El cuerpo del mensaje contiene la frase `'The stored procedure finished successfully'`.  
  
```  
EXEC msdb.dbo.sp_send_dbmail  
    @profile_name = 'Adventure Works Administrator',  
    @recipients = 'yourfriend@Adventure-Works.com',  
    @body = 'The stored procedure finished successfully.',  
    @subject = 'Automated Success Message' ;  
```  
  
### <a name="b-sending-an-e-mail-message-with-the-results-of-a-query"></a>b. Enviar un mensaje de correo electrónico con los resultados de una consulta  
 En este ejemplo se envía un mensaje de correo electrónico a su amigo `yourfriend@Adventure-Works.com`mediante la dirección de correo electrónico. El asunto del mensaje es `Work Order Count`, y ejecuta una consulta que muestra el número de órdenes de trabajo con un valor de `DueDate` inferior a dos días después del 30 de abril de 2004. El Correo electrónico de base de datos adjunta el resultado como archivo de texto.  
  
```  
EXEC msdb.dbo.sp_send_dbmail  
    @profile_name = 'Adventure Works Administrator',  
    @recipients = 'yourfriend@Adventure-Works.com',  
    @query = 'SELECT COUNT(*) FROM AdventureWorks2012.Production.WorkOrder  
                  WHERE DueDate > ''2004-04-30''  
                  AND  DATEDIFF(dd, ''2004-04-30'', DueDate) < 2' ,  
    @subject = 'Work Order Count',  
    @attach_query_result_as_file = 1 ;  
```  
  
### <a name="c-sending-an-html-e-mail-message"></a>C. Enviar un mensaje de correo electrónico HTML  
 En este ejemplo se envía un mensaje de correo electrónico a su amigo `yourfriend@Adventure-Works.com`mediante la dirección de correo electrónico. El asunto del mensaje es `Work Order List` y contiene un documento HTML que muestra las órdenes de trabajo con un valor de `DueDate` inferior a dos días después del 30 de abril de 2004. El Correo electrónico de base de datos envía el mensaje en formato HTML.  
  
```  
DECLARE @tableHTML  NVARCHAR(MAX) ;  
  
SET @tableHTML =  
    N'<H1>Work Order Report</H1>' +  
    N'<table border="1">' +  
    N'<tr><th>Work Order ID</th><th>Product ID</th>' +  
    N'<th>Name</th><th>Order Qty</th><th>Due Date</th>' +  
    N'<th>Expected Revenue</th></tr>' +  
    CAST ( ( SELECT td = wo.WorkOrderID,       '',  
                    td = p.ProductID, '',  
                    td = p.Name, '',  
                    td = wo.OrderQty, '',  
                    td = wo.DueDate, '',  
                    td = (p.ListPrice - p.StandardCost) * wo.OrderQty  
              FROM AdventureWorks.Production.WorkOrder as wo  
              JOIN AdventureWorks.Production.Product AS p  
              ON wo.ProductID = p.ProductID  
              WHERE DueDate > '2004-04-30'  
                AND DATEDIFF(dd, '2004-04-30', DueDate) < 2   
              ORDER BY DueDate ASC,  
                       (p.ListPrice - p.StandardCost) * wo.OrderQty DESC  
              FOR XML PATH('tr'), TYPE   
    ) AS NVARCHAR(MAX) ) +  
    N'</table>' ;  
  
EXEC msdb.dbo.sp_send_dbmail @recipients='yourfriend@Adventure-Works.com',  
    @subject = 'Work Order List',  
    @body = @tableHTML,  
    @body_format = 'HTML' ;  
```  
  
## <a name="see-also"></a>Vea también  
 [Correo electrónico de base de datos](../../relational-databases/database-mail/database-mail.md)   
 [Correo electrónico de base de datos objetos de configuración](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [Procedimientos &#40;almacenados de correo electrónico de base de datos TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)   
 [sp_addrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)  
  
  
