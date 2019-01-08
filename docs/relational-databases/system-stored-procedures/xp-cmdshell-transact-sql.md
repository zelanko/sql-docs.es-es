---
title: xp_cmdshell (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- xp_cmdshell
- xp_cmdshell_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- xp_cmdshell
ms.assetid: 18935cf4-b320-4954-b6c1-e007fcefe358
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 533b096b11ded9c76db81e640c961449a2785330
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/11/2018
ms.locfileid: "53211524"
---
# <a name="xpcmdshell-transact-sql"></a>xp_cmdshell (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Genera un shell de comandos de Windows y lo pasa a una cadena para ejecutarlo. Los resultados se devuelven como filas de texto.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
xp_cmdshell { 'command_string' } [ , no_output ]  
```  
  
## <a name="arguments"></a>Argumentos  
 **'** *command_string* **'**  
 Es la cadena que contiene un comando que se pasa al sistema operativo. *command_string* es **varchar (8000)** o **nvarchar (4000)**, no tiene ningún valor predeterminado. *command_string* no puede contener más de un conjunto de comillas dobles. Es necesario un único par de comillas si están presentes en las rutas de acceso del archivo de espacios en blanco o hace referenciados en los nombres de programa *command_string*. Si tiene problemas con espacios incrustados, considere el uso de nombres de archivo de tipo FAT 8.3 como solución.  
  
 **no_output**  
 Es un parámetro opcional que especifica que no se devuelven resultados al cliente.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 La ejecución de la instrucción `xp_cmdshell` devuelve una lista de directorios del directorio actual.  
  
```  
EXEC xp_cmdshell 'dir *.exe';  
GO  
```  
  
 Las filas se devuelven en un **nvarchar (255)** columna. Si el **no_output** se utiliza la opción, se devolverá únicamente los siguientes elementos:  
  
```  
The command(s) completed successfully.  
```  
  
## <a name="remarks"></a>Comentarios  
 El proceso de Windows generados por **xp_cmdshell** tiene los mismos derechos de seguridad que la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cuenta de servicio.  
  
 **xp_cmdshell** funciona de forma sincrónica. No se devolverá el control al llamador hasta que el comando del shell de comandos esté completo.  
  
 **xp_cmdshell** pueden habilitar y deshabilitar mediante la administración basada en directivas o ejecutando **sp_configure**. Para obtener más información, consulte [Surface Area Configuration](../../relational-databases/security/surface-area-configuration.md) y [xp_cmdshell Server Configuration Option](../../database-engine/configure-windows/xp-cmdshell-server-configuration-option.md).  
  
> [!IMPORTANT]
>  Si **xp_cmdshell** se ejecuta dentro de un lote y devuelve un error, se producirá un error en el lote. Es un cambio de comportamiento. En versiones anteriores de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] el lote continuaría su ejecución.  
  
## <a name="xpcmdshell-proxy-account"></a>Cuenta de proxy xp_cmdshell  
 Cuando se llama a un usuario que no es un miembro de la **sysadmin** rol fijo de servidor **xp_cmdshell** se conecta a Windows mediante el nombre de cuenta y la contraseña almacenada en la credencial denominada **## #xp_cmdshell_proxy_account ##**. Si no existe esta credencial de proxy, **xp_cmdshell** se producirá un error.  
  
 Puede crear la credencial de cuenta de proxy ejecutando **sp_xp_cmdshell_proxy_account**. Como argumentos, este procedimiento almacenado utiliza un nombre de usuario y una contraseña de Windows. Por ejemplo, el siguiente comando crea una credencial de proxy para el usuario de dominio de Windows `SHIPPING\KobeR` que tiene la contraseña de Windows `sdfh%dkc93vcMt0`.  
  
```  
EXEC sp_xp_cmdshell_proxy_account 'SHIPPING\KobeR','sdfh%dkc93vcMt0';  
```  
  
 Para obtener más información, consulte [sp_xp_cmdshell_proxy_account &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-xp-cmdshell-proxy-account-transact-sql.md).  
  
## <a name="permissions"></a>Permisos  
 Dado que a veces, los usuarios malintencionados intentan elevar sus privilegios mediante el uso de **xp_cmdshell**, **xp_cmdshell** está deshabilitada de forma predeterminada. Use **sp_configure** o **administración basada en directivas** para habilitarla. Para más información, vea [xp_cmdshell (opción de configuración del servidor)](../../database-engine/configure-windows/xp-cmdshell-server-configuration-option.md).  
  
 Cuando se habilita por primera vez, **xp_cmdshell** requiere el permiso CONTROL SERVER para ejecutar y el proceso de Windows creado por **xp_cmdshell** tiene el mismo contexto de seguridad que la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cuenta de servicio. El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cuenta de servicio a menudo tiene más permisos que son necesarios para el trabajo realizado por el proceso creado por **xp_cmdshell**. Para mejorar la seguridad, el acceso a **xp_cmdshell** deben limitarse a los usuarios con privilegios elevados.  
  
 Para permitir que los usuarios usar **xp_cmdshell**y permiten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cree procesos secundarios con el token de seguridad de una cuenta con menos privilegios, siga estos pasos:  
  
1.  Cree y personalice una cuenta de usuario local de Windows o una cuenta de dominio con los permisos mínimos que los procesos requieran.  
  
2.  Utilice la **sp_xp_cmdshell_proxy_account** procedimiento del sistema para configurar **xp_cmdshell** utilizar esa cuenta con privilegios mínimos.  
  
    > [!NOTE]  
    >  También puede configurar esta cuenta de proxy mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] haciendo **propiedades** en el servidor, nombre en el Explorador de objetos y buscando en el **seguridad** la pestaña para el **Server cuenta de proxy** sección.  
  
3.  En [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], con la base de datos maestra, ejecute el `GRANT exec ON xp_cmdshell TO '<somelogin>'` instrucción para conceder a concretos que no sean**sysadmin** a los usuarios la capacidad de ejecutar **xp_cmdshell**. El inicio de sesión especificado debe asignarse a un usuario en la base de datos maestra.  
  
 Ahora que no sean administradores pueden iniciar los procesos del sistema operativo con **xp_cmdshell** y esos procesos se ejecutan con los permisos de la cuenta de proxy que ha configurado. Los usuarios con permiso CONTROL SERVER (los miembros de la **sysadmin** rol fijo de servidor) seguirán recibiendo los permisos de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cuenta de servicio de procesos secundarios iniciados por **xp_cmdshell** .  
  
 Para determinar la cuenta de Windows utilizada por **xp_cmdshell** al iniciar los procesos del sistema operativo, ejecute la instrucción siguiente:  
  
```  
xp_cmdshell 'whoami.exe'  
  
```  
  
 Para determinar el contexto de seguridad de otro inicio de sesión, ejecute lo siguiente:  
  
```  
EXECUTE AS LOGIN = '<other_login>' ;  
GO  
xp_cmdshell 'whoami.exe' ;  
REVERT ;  
  
```  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-returning-a-list-of-executable-files"></a>A. Devolver una lista de archivos ejecutables  
 En el siguiente ejemplo se muestra el procedimiento almacenado extendido `xp_cmdshell` ejecutando un comando de directorio.  
  
```  
EXEC master..xp_cmdshell 'dir *.exe''  
```  
  
### <a name="b-returning-no-output"></a>b. No devolver resultados  
 En el siguiente ejemplo se utiliza `xp_cmdshell` para ejecutar una cadena de comandos sin devolver los resultados al cliente.  
  
```  
USE master;  
  
EXEC xp_cmdshell 'copy c:\SQLbcks\AdvWorks.bck  
    \\server2\backups\SQLbcks, NO_OUTPUT';  
GO  
```  
  
### <a name="c-using-return-status"></a>C. Utilizar el estado de retorno  
 En el ejemplo siguiente, la `xp_cmdshell` procedimiento almacenado extendido también sugiere el estado de retorno. El valor del código de retorno se almacena en la variable `@result`.  
  
```  
DECLARE @result int;  
EXEC @result = xp_cmdshell 'dir *.exe';  
IF (@result = 0)  
   PRINT 'Success'  
ELSE  
   PRINT 'Failure';  
```  
  
### <a name="d-writing-variable-contents-to-a-file"></a>D. Escribir el contenido de variables en un archivo  
 En el siguiente ejemplo se escribe el contenido de la variable `@var` en un archivo denominado `var_out.txt` en el directorio actual del servidor.  
  
```  
DECLARE @cmd sysname, @var sysname;  
SET @var = 'Hello world';  
SET @cmd = 'echo ' + @var + ' > var_out.txt';  
EXEC master..xp_cmdshell @cmd;  
```  
  
### <a name="e-capturing-the-result-of-a-command-to-a-file"></a>E. Capturar el resultado de un comando en un archivo  
 En el siguiente ejemplo se escribe el contenido del directorio actual en un archivo denominado `dir_out.txt` en el directorio actual del servidor.  
  
```  
DECLARE @cmd sysname, @var sysname;  
SET @var = 'dir/p';  
SET @cmd = @var + ' > dir_out.txt';  
EXEC master..xp_cmdshell @cmd;  
```  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados extendidos generales &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)   
 [Opción de configuración del servidor xp_cmdshell](../../database-engine/configure-windows/xp-cmdshell-server-configuration-option.md)   
 [Configuración de Área expuesta](../../relational-databases/security/surface-area-configuration.md)   
 [sp_xp_cmdshell_proxy_account &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-xp-cmdshell-proxy-account-transact-sql.md)  
  
  
