---
title: Actividad de registro | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- logging activity
ms.assetid: a777b3d9-2262-4e82-bc82-b62ad60d0e55
caps.latest.revision: 32
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d748bac061fdd4b76b1df0b9a6cf0a8101f21092
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="logging-activity"></a>Actividad de registro
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

De manera predeterminada, los errores y las advertencias generados por los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] no se registran. En este tema se describe cómo configurar la actividad de registro.  
  
## <a name="logging-activity-using-the-pdosqlsrv-driver"></a>Actividad de registro con el controlador PDO_SQLSRV  
La única configuración disponible para el controlador PDO_SQLSRV es la entrada pdo_sqlsrv.log_severity en el archivo php.ini.  
  
Agregue lo siguiente al final del archivo php.ini:  
  
```  
[pdo_sqlsrv]  
pdo_sqlsrv.log_severity = <number>  
```  
  
**log_severity** puede ser uno de los siguientes valores:  
  
|Valor|Descripción|  
|---------|---------------|  
|0|El registro está deshabilitado (se trata del valor predeterminado si no se define ninguno).|  
|-1|Especifica que se registrarán errores, advertencias y avisos.|  
|1|Especifica que se registrarán los errores.|  
|2|Especifica que se registrarán las advertencias.|  
|4|Especifica que se registrarán los avisos.|  
  
La información de registro se agregará al archivo phperrors.log.  
  
PHP lee el archivo de configuración durante la inicialización y almacena los datos en una memoria caché. Además, proporciona una API para actualizar estos valores de configuración y este uso inmediatamente, y se escribe en el archivo de configuración. Esta API permite que los scripts de la aplicación cambien la configuración, incluso después de la inicialización de PHP.  
  
## <a name="logging-activity-using-the-sqlsrv-driver"></a>Actividad de registro con el controlador SQLSRV  
Para activar el registro, puede utilizar la función [sqlsrv_configure](../../connect/php/sqlsrv-configure.md) o modificar el archivo php.ini. Puede registrar la actividad sobre inicializaciones, conexiones, instrucciones o funciones de error. También puede especificar si desea registrar los errores, las advertencias, los avisos o los tres tipos.  
  
> [!NOTE]  
> Puede configurar la ubicación del archivo de registro en el archivo php.ini.  
  
### <a name="turning-logging-on"></a>Activación del registro  
Puede activar el registro usando la función [sqlsrv_configure](../../connect/php/sqlsrv-configure.md) para especificar un valor para la configuración **LogSubsystems** . Por ejemplo, la siguiente línea de código configura el controlador para que registre la actividad de las conexiones:  
  
`sqlsrv_configure("LogSubsystems", SQLSRV_LOG_SYSTEM_CONN);`  
  
En la siguiente tabla se describen las constantes que se pueden utilizar como el valor de la configuración **LogSubsystems** :  
  
|Valor (equivalente entero entre paréntesis)|Description|  
|-----------------------------------------------|---------------|  
|SQLSRV_LOG_SYSTEM_ALL (-1)|Activa el registro de todos los subsistemas.|  
|SQLSRV_LOG_SYSTEM_OFF (0)|Desactiva el registro. Ésta es la opción predeterminada.|  
|SQLSRV_LOG_SYSTEM_INIT (1)|Activa el registro de la actividad de inicialización.|  
|SQLSRV_LOG_SYSTEM_CONN (2)|Activa el registro de la actividad de conexión.|  
|SQLSRV_LOG_SYSTEM_STMT (4)|Activa el registro de la actividad de instrucción.|  
|SQLSRV_LOG_SYSTEM_UTIL (8)|Activa el registro de la actividad de funciones de error (como handle_error y handle_warning).|  
  
Puede establecer más de un valor a la vez para la **LogSubsystems** usando el operador lógico OR (|). Por ejemplo, la siguiente línea de código activa el registro de actividad de las conexiones y las instrucciones:  
  
`sqlsrv_configure("LogSubsystems", SQLSRV_LOG_SYSTEM_CONN | SQLSRV_LOG_SYSTEM_STMT);`  
  
También puede activar el registro especificando un valor entero para la configuración **LogSubsystems** en el archivo php.ini. Por ejemplo, al agregar la siguiente línea a la sección `[sqlsrv]` del archivo php.ini, se activará el registro de la actividad de conexión:  
  
`sqlsrv.LogSubsystems = 2`  
  
Puede especificar más de una opción a la vez agregando valores enteros juntos. Por ejemplo, si agrega la siguiente línea a la sección `[sqlsrv]` del archivo php.ini, se activará el registro de la actividad de conexión y de instrucción:  
  
`sqlsrv.LogSubsystems = 6`  
  
### <a name="logging-errors-warnings-and-notices"></a>Registro de errores, advertencias y avisos  
Tras activar el registro, debe especificar qué desea registrar. Puede registrar uno o más de los siguientes elementos: errores, advertencias y avisos. Por ejemplo, la siguiente línea de código especifica que se registrarán solo advertencias:  
  
`sqlsrv_configure("LogSeverity", SQLSRV_LOG_SEVERITY_WARNING);`  
  
> [!NOTE]  
> El valor predeterminado de **LogSeverity** es **SQLSRV_LOG_SEVERITY_ERROR**. Si se activa el registro y no se especifica ningún valor para **LogSeverity** , solo se registran errores.  
  
En la tabla siguiente se describen las constantes que se pueden utilizar como el valor de la configuración **LogSeverity** :  
  
|Valor (equivalente entero entre paréntesis)|Description|  
|-----------------------------------------------|---------------|  
|SQLSRV_LOG_SEVERITY_ALL (-1)|Especifica que se registrarán errores, advertencias y avisos.|  
|SQLSRV_LOG_SEVERITY_ERROR (1)|Especifica que se registrarán los errores. Ésta es la opción predeterminada.|  
|SQLSRV_LOG_SEVERITY_WARNING (2)|Especifica que se registrarán las advertencias.|  
|SQLSRV_LOG_SEVERITY_NOTICE (4)|Especifica que se registrarán los avisos.|  
  
Puede establecer más de un valor a la vez para la **LogSeverity** usando el operador lógico OR (|). Por ejemplo, la siguiente línea de código especifica que se deben registrar errores y advertencias:  
  
`sqlsrv_configure("LogSeverity", SQLSRV_LOG_SEVERITY_ERROR | SQLSRV_LOG_SEVERITY_WARNING);`  
  
> [!NOTE]  
> Al especificar un valor para la configuración **LogSeverity** , no se activa el registro. Debe activar el registro especificando un valor para la configuración **LogSubsystems** y, luego, especificar la gravedad de lo que se registra definiendo un valor para **LogSeverity**.  
  
También puede especificar un valor para la configuración **LogSeverity** usando valores enteros en el archivo php.ini. Por ejemplo, al agregar la siguiente línea a la sección `[sqlsrv]` del archivo php.ini, se activa el registro solo de advertencias:  
  
`sqlsrv.LogSeverity = 2`  
  
Puede especificar más de una opción a la vez agregando valores enteros juntos. Por ejemplo, al agregar la siguiente línea a la sección `[sqlsrv]` del archivo php.ini, se habilitará el registro de errores y advertencias:  
  
`sqlsrv.LogSeverity = 3`  
  
## <a name="see-also"></a>Vea también  
[Guía de programación para el controlador SQL para PHP](../../connect/php/programming-guide-for-php-sql-driver.md)
[constantes &#40; Controladores de Microsoft para PHP para SQL Server &#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)  
[sqlsrv_configure](../../connect/php/sqlsrv-configure.md)  
[sqlsrv_get_config](../../connect/php/sqlsrv-get-config.md)  
[Referencia de API del controlador SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)  
  

