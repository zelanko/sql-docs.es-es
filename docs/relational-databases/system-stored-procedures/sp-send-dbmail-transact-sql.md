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
ms.openlocfilehash: 52a89c0220bddde6944e759936dc22ad1f3e0ff2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68126301"
---
# <a name="sp_send_dbmail-transact-sql"></a>sp_send_dbmail (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Envía un mensaje de correo electrónico a los destinatarios especificados. El mensaje puede incluir un conjunto de resultados de una consulta, datos adjuntos o ambos elementos. Cuando se coloca correctamente en la cola de correo electrónico de base de datos, **sp_send_dbmail** devuelve el **mailitem_id** del mensaje. Este procedimiento almacenado se encuentra en la **msdb** base de datos.  
  
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
`[ @profile_name = ] 'profile_name'` Es el nombre del perfil para enviar el mensaje desde. El *profile_name* es de tipo **sysname**, su valor predeterminado es null. El *profile_name* debe ser el nombre de un perfil de correo electrónico de base de datos existente. Cuando no hay ninguna *profile_name* se especifica, **sp_send_dbmail** usa el perfil privado predeterminado para el usuario actual. Si el usuario no tiene un perfil privado predeterminado, **sp_send_dbmail** utiliza el perfil público predeterminado para el **msdb** base de datos. Si el usuario no tiene un perfil privado predeterminado y no hay ningún perfil público predeterminado para la base de datos, **@profile_name** debe especificarse.  
  
`[ @recipients = ] 'recipients'` Es una lista delimitada por punto y coma de direcciones de correo electrónico para enviar el mensaje. La lista de destinatarios es de tipo **varchar (max)** . Aunque este parámetro es opcional, al menos uno de **@recipients** , **@copy_recipients** , o **@blind_copy_recipients** debe especificarse o **sp_ send_dbmail** devuelve un error.  
  
`[ @copy_recipients = ] 'copy_recipients'` Es que una lista delimitada por punto y coma de correo electrónico direcciones para la copia del mensaje. La lista de destinatarios de copia es de tipo **varchar (max)** . Aunque este parámetro es opcional, al menos uno de **@recipients** , **@copy_recipients** , o **@blind_copy_recipients** debe especificarse o **sp_ send_dbmail** devuelve un error.  
  
`[ @blind_copy_recipients = ] 'blind_copy_recipients'` Es que una lista delimitada por punto y coma de correo electrónico direcciones a recibir copia oculta del mensaje. La lista de destinatarios de copia oculta es de tipo **varchar (max)** . Aunque este parámetro es opcional, al menos uno de **@recipients** , **@copy_recipients** , o **@blind_copy_recipients** debe especificarse o **sp_ send_dbmail** devuelve un error.  
  
`[ @from_address = ] 'from_address'` Es el valor de la 'from address' del mensaje de correo electrónico. Se trata de un parámetro opcional que se usa para invalidar la configuración del perfil de correo. Este parámetro es de tipo **varchar (max)** . La configuración de seguridad de SMTP determina si se aceptan estas invalidaciones. Si no se especifica ningún parámetro, el valor predeterminado es NULL.  
  
`[ @reply_to = ] 'reply_to'` Es el valor de la 'reply to address' del mensaje de correo electrónico. Solo acepta una dirección de correo electrónico como valor válido. Se trata de un parámetro opcional que se usa para invalidar la configuración del perfil de correo. Este parámetro es de tipo **varchar (max)** . La configuración de seguridad de SMTP determina si se aceptan estas invalidaciones. Si no se especifica ningún parámetro, el valor predeterminado es NULL.  
  
`[ @subject = ] 'subject'` Es el asunto del mensaje de correo electrónico. El asunto es de tipo **nvarchar (255)** . Si no se especifica ningún asunto, el valor predeterminado es 'Mensaje de SQL Server'.  
  
`[ @body = ] 'body'` Es el cuerpo del mensaje de correo electrónico. El cuerpo del mensaje es de tipo **nvarchar (max)** , su valor predeterminado es null.  
  
`[ @body_format = ] 'body_format'` Es el formato del cuerpo del mensaje. El parámetro es de tipo **varchar (20)** , su valor predeterminado es null. Si se especifica, los encabezados del mensaje saliente indican que el cuerpo del mensaje tiene el formato especificado. El parámetro puede contener uno de los siguientes valores:  
  
-   TEXT  
  
-   HTML  
  
 El valor predeterminado es TEXT.  
  
`[ @importance = ] 'importance'` Es la importancia del mensaje. El parámetro es de tipo **varchar(6)** . El parámetro puede contener uno de los siguientes valores:  
  
-   Bajo  
  
-   Normal  
  
-   Alto  
  
 El valor predeterminado es Normal.  
  
`[ @sensitivity = ] 'sensitivity'` Es la confidencialidad del mensaje. El parámetro es de tipo **varchar (12)** . El parámetro puede contener uno de los siguientes valores:  
  
-   Normal  
  
-   Personal  
  
-   Privada  
  
-   Confidential  
  
 El valor predeterminado es Normal.  
  
`[ @file_attachments = ] 'file_attachments'` Es una lista delimitada por punto y coma de nombres de archivo para adjuntar al mensaje de correo electrónico. Especifique los archivos de la lista como rutas de acceso absolutas. La lista de los datos adjuntos es de tipo **nvarchar (max)** . De forma predeterminada, Correo electrónico de base de datos limita los datos adjuntos a 1 MB por archivo.  
  
`[ @query = ] 'query'` Es una consulta para ejecutarla. Los resultados de la consulta pueden adjuntarse como archivo o incluirse en el cuerpo del mensaje de correo electrónico. La consulta es de tipo **nvarchar (max)** y puede contener cualquier [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucciones. Tenga en cuenta que la consulta se ejecuta en una sesión independiente, las variables locales por lo que en el script que llama a **sp_send_dbmail** no están disponibles para la consulta.  
  
`[ @execute_query_database = ] 'execute_query_database'` Es el contexto de base de datos dentro del cual el procedimiento almacenado ejecuta la consulta. El parámetro es de tipo **sysname**, su valor predeterminado de la base de datos actual. Este parámetro solo es aplicable si **@query** se especifica.  
  
`[ @attach_query_result_as_file = ] attach_query_result_as_file` Especifica si el conjunto de resultados de la consulta se devuelve como un archivo adjunto. *attach_query_result_as_file* es de tipo **bit**, su valor predeterminado es 0.  
  
 Cuando el valor es 0, los resultados de consulta se incluyen en el cuerpo del mensaje de correo electrónico, después del contenido de la **@body** parámetro. Si el valor es 1, los resultados se devuelven como dato adjunto. Este parámetro solo es aplicable si **@query** se especifica.  
  
`[ @query_attachment_filename = ] query_attachment_filename` Especifica el nombre de archivo que se usará para el conjunto de resultados de los datos adjuntos de la consulta. *query_attachment_filename* es de tipo **nvarchar (255)** , su valor predeterminado es null. Este parámetro se omite cuando *attach_query_result* es 0. Cuando *attach_query_result* es 1 y este parámetro es NULL, correo electrónico de base de datos crea un nombre de archivo arbitrario.  
  
`[ @query_result_header = ] query_result_header` Especifica si los resultados de consulta incluyen encabezados de columna. El valor de query_result_header es de tipo **bits**. Si el valor es 1, los resultados de la consulta contienen encabezados de columna. Si el valor es 0, los resultados de la consulta no contienen encabezados de columna. Este parámetro tiene como valor predeterminado **1**. Este parámetro solo es aplicable si **@query** se especifica.  
 
   >[!NOTE]
   > Puede producirse el siguiente error al establecer @query_result_header a 0 y estableciendo @query_no_truncate en 1:
   > <br> Msg 22050, nivel 16, estado 1, línea 12: No se pudo inicializar la biblioteca sqlcmd con el número de error -2147024809.
  
`[ @query_result_width = ] query_result_width` Es el ancho de línea, en caracteres, que se usan para dar formato a los resultados de la consulta. El *query_result_width* es de tipo **int**, su valor predeterminado es 256. El valor proporcionado debe estar entre 10 y 32767. Este parámetro solo es aplicable si **@query** se especifica.  
  
`[ @query_result_separator = ] 'query_result_separator'` Es el carácter utilizado para separar las columnas en la salida de la consulta. El separador es de tipo **char (1)** . El valor predeterminado es ' ' (espacio).  
  
`[ @exclude_query_output = ] exclude_query_output` Especifica si se devuelve el resultado de la ejecución de consultas en el mensaje de correo electrónico. **exclude_query_output** es bit y su valor predeterminado es 0. Si este parámetro es 0, la ejecución de la **sp_send_dbmail** procedimiento almacenado imprime el mensaje devuelto como resultado de la ejecución de consultas en la consola. Si este parámetro es 1, la ejecución de la **sp_send_dbmail** procedimiento almacenado imprimir cualquiera de los mensajes de ejecución de consulta en la consola.  
  
`[ @append_query_error = ] append_query_error` Especifica si se debe enviar el correo electrónico cuando se devuelve un error de la consulta especificada en el **@query** argumento. **append_query_error** es **bit**, su valor predeterminado es 0. Cuando este parámetro es 1, el Correo electrónico de base de datos envía el mensaje de correo electrónico e incluye en el cuerpo del mismo el mensaje de error de la consulta. Cuando este parámetro es 0, correo electrónico de base de datos no envía el mensaje de correo electrónico, y **sp_send_dbmail** termina con el código de retorno 1, que indica un error.  
  
`[ @query_no_truncate = ] query_no_truncate` Especifica si se debe ejecutar la consulta con la opción que evita el truncamiento de tipos de datos de longitud variable grande (**varchar (max)** , **nvarchar (max)** , **varbinary (max)** **xml**, **texto**, **ntext**, **imagen**y los tipos de datos definido por el usuario). Si el establece, los resultados de la consulta no contienen encabezados de columna. El *@query_no_truncate* es el valor de tipo **bits**. Si el valor es 0 o no se especifica, las columnas de la consulta se truncan a 256 caracteres. Si el valor es 1, las columnas de la consulta no se truncan. El valor predeterminado de este parámetro es 0.  
  
> [!NOTE]  
>  Cuando se usa con grandes cantidades de datos, el @ **@query_no_truncate** opción consume recursos adicionales y puede ralentizar el rendimiento del servidor.  
  
`[ @query_result_no_padding ] @query_result_no_padding` El tipo es bit. El valor predeterminado es 0. Cuando se establece en 1, no se rellenan los resultados de consulta, posiblemente, reducirá el tamaño del archivo. Si establece @query_result_no_padding en 1 y establezca el @query_result_width parámetro, el @query_result_no_padding parámetro sobrescribe el @query_result_width parámetro.  
  
 En este caso no se producen errores.  
 
  >[!NOTE]
  > Puede producirse el siguiente error al establecer @query_result_no_padding a 1 y que proporciona un parámetro para @query_no_truncate:
  > <br> Msg 22050, nivel 16, estado 1, línea 0: No se pudo ejecutar la consulta porque el @query_result_no_append y @query_no_truncate opciones son mutuamente excluyentes. 
  
 Si establece la @query_result_no_padding en 1 y establezca el @query_no_truncate parámetro, un error se genera.  
  
`[ @mailitem_id = ] mailitem_id [ OUTPUT ]` Parámetro de salida opcional devuelve el *mailitem_id* del mensaje. El *mailitem_id* es de tipo **int**.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 Un código de retorno de 0 significa éxito. Cualquier otro valor significa error. El código de error para la instrucción que no se pudo se almacena en el @@ERROR variable.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Si se ejecuta correctamente, devuelve el mensaje "Correo en cola".  
  
## <a name="remarks"></a>Comentarios  
 Antes de usarse, correo electrónico de base de datos debe habilitarse utilizando el Asistente para configuración de correo electrónico de base de datos, o **sp_configure**.  
  
 **sysmail_stop_sp** detiene el correo electrónico de base de datos deteniendo los objetos de Service Broker que usa el programa externo. **sp_send_dbmail** sigue aceptando correo de correo electrónico de base de datos se haya detenido mediante **sysmail_stop_sp**. Para iniciar el correo electrónico de base de datos, use **sysmail_start_sp**.  
  
 Cuando **@profile** no se especifica, **sp_send_dbmail** utiliza un perfil predeterminado. Si el usuario que envía el mensaje de correo electrónico tiene un perfil privado predeterminado, el Correo electrónico de base de datos utilizará dicho perfil. Si el usuario no tiene ningún perfil privado predeterminado, **sp_send_dbmail** usa el perfil público predeterminado. Si no hay ningún perfil privado predeterminado para el usuario y ningún perfil público predeterminado, **sp_send_dbmail** devuelve un error.  
  
 **sp_send_dbmail** no admite mensajes de correo electrónico sin contenido. Para enviar un mensaje de correo electrónico, debe especificar al menos uno de **@body** , **@query** , **@file_attachments** , o **@subject** . En caso contrario, **sp_send_dbmail** devuelve un error.  
  
 El Correo electrónico de base de datos utiliza el contexto de seguridad de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows del usuario actual para controlar el acceso a los archivos. Por lo tanto, los usuarios se autentican con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticación no puede adjuntar archivos utilizando **@file_attachments** . Tenga en cuenta que Windows no permite que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proporcione credenciales desde un equipo remoto a otro. Por lo tanto, es posible que el Correo electrónico de base de datos no pueda adjuntar archivos desde un recurso compartido de red en aquellos casos en los que el comando se ejecuta desde un equipo que no sea el equipo donde se ejecuta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Si ambos **@query** y **@file_attachments** se especifican y no se encuentra el archivo, la consulta se ejecuta pero no se envía el correo electrónico.  
  
 Cuando se especifica una consulta, el conjunto de resultados se formatea como texto insertado. Los datos binarios del conjunto de resultados se envían en formato hexadecimal.  
  
 Los parámetros **@recipients** , **@copy_recipients** , y **@blind_copy_recipients** son listas delimitada por punto y coma de direcciones de correo electrónico. Debe proporcionarse al menos uno de estos parámetros, o **sp_send_dbmail** devuelve un error.  
  
 Al ejecutar **sp_send_dbmail** sin un contexto de transacción, el correo electrónico de base de datos se inicia y confirma una transacción implícita. Al ejecutar **sp_send_dbmail** desde dentro de una transacción existente, correo electrónico de base de datos se basa en el usuario para confirmar o revertir los cambios. No inicia ninguna transacción interna.  
  
## <a name="permissions"></a>Permisos  
 Permisos de ejecución de **sp_send_dbmail** predeterminada a todos los miembros de la **DatabaseMailUser** rol de base de datos en el **msdb** base de datos. Sin embargo, cuando el usuario que envía el mensaje no tiene permiso para utilizar el perfil para la solicitud, **sp_send_dbmail** devuelve un error y no envía el mensaje.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-sending-an-e-mail-message"></a>A. Enviar un mensaje de correo electrónico  
 Este ejemplo envía un mensaje de correo electrónico a su amigo utilizando la dirección de correo electrónico `myfriend@Adventure-Works.com`. El asunto del mensaje es `Automated Success Message`. El cuerpo del mensaje contiene la frase `'The stored procedure finished successfully'`.  
  
```  
EXEC msdb.dbo.sp_send_dbmail  
    @profile_name = 'Adventure Works Administrator',  
    @recipients = 'yourfriend@Adventure-Works.com',  
    @body = 'The stored procedure finished successfully.',  
    @subject = 'Automated Success Message' ;  
```  
  
### <a name="b-sending-an-e-mail-message-with-the-results-of-a-query"></a>b. Enviar un mensaje de correo electrónico con los resultados de una consulta  
 Este ejemplo envía un mensaje de correo electrónico a su amigo utilizando la dirección de correo electrónico `yourfriend@Adventure-Works.com`. El asunto del mensaje es `Work Order Count`, y ejecuta una consulta que muestra el número de órdenes de trabajo con un valor de `DueDate` inferior a dos días después del 30 de abril de 2004. El Correo electrónico de base de datos adjunta el resultado como archivo de texto.  
  
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
 Este ejemplo envía un mensaje de correo electrónico a su amigo utilizando la dirección de correo electrónico `yourfriend@Adventure-Works.com`. El asunto del mensaje es `Work Order List` y contiene un documento HTML que muestra las órdenes de trabajo con un valor de `DueDate` inferior a dos días después del 30 de abril de 2004. El Correo electrónico de base de datos envía el mensaje en formato HTML.  
  
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
 [Objetos de configuración de correo electrónico de base de datos](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [Procedimientos almacenados de correo electrónico de base de datos &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)   
 [sp_addrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)  
  
  
