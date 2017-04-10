---
title: "El servicio CDC de Oracle | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 47759ddc-358d-405b-acb9-189ada76ea6d
caps.latest.revision: 8
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 8
---
# El servicio CDC de Oracle
  El servicio CDC de Oracle es un servicio de Windows que ejecuta el programa xdbcdcsvc.exe. El servicio CDC de Oracle se puede configurar para ejecutar varios servicios de Windows en el mismo equipo, cada uno de ellos con un nombre de servicio de Windows diferente. Se suelen crear varios servicios de Windows CDC de Oracle en un único equipo para obtener una mejor separación entre ellos o cuando cada uno de ellos debe trabajar con una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] diferente.  
  
 Un servicio CDC de Oracle se crea mediante la Consola de configuración del servicio CDC de Oracle o se define mediante la interfaz de línea de comandos integrada en el programa xdbcdcsvc.exe. En ambos casos, cada servicio CDC de Oracle creado está asociado a una única instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (que puede agruparse en clústeres o reflejarse con la instalación de **AlwaysOn**) y la información de conexión (cadena de conexión y credenciales de acceso) forma parte de la configuración del servicio.  
  
 Cuando se inicia un servicio CDC de Oracle, intenta conectarse a la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con la que está asociado, obtiene la lista de instancias CDC de Oracle que debe controlar y realiza una validación inicial del entorno. Los errores que se producen durante el inicio del servicio y cualquier información de inicio o detención se escriben siempre en el registro de eventos de aplicación de Windows. Cuando se establece una conexión con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], todos los errores y mensajes informativos se escriben en la tabla **dbo.xdbcdc_trace** de la base de datos MSXDBCDC de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Una de las comprobaciones realizadas durante el inicio consiste en comprobar que no hay ningún otro servicio CDC de Oracle con el mismo nombre funcionando en ese momento. Si un servicio con el mismo nombre está conectado actualmente desde un equipo diferente, el servicio CDC de Oracle entra en un bucle de espera, esperando a que el otro servicio se desconecte antes de controlar el trabajo de CDC de Oracle.  
  
 Cuando el servicio CDC de Oracle supera todas las comprobaciones de inicio, examina la tabla **dbo.xdbcdc_databases** de la base de datos MSXDBCDC para ver si hay alguna instancia CDC de Oracle habilitada. Para cada instancia CDC de Oracle habilitada, el servicio inicia un subproceso para controlar esa instancia CDC de Oracle.  
  
 Cuando una instancia CDC de Oracle se inicia, tiene acceso a la base de datos CDC de SQL Server que tiene el mismo nombre que la instancia CDC y recupera su estado de la ejecución anterior. También comprueba que todo funciona correctamente. Después, reanuda el procesamiento de cambios leyendo los registros de transacciones de Oracle y escribiendo cambios en la base de datos CDC.  
  
 El servicio CDC de Oracle supervisa periódicamente la tabla **dbo.xdbcdc_tables** de la base de datos MSXDBCDC para determinar si hay algún cambio en la configuración de alguna instancia CDC de Oracle. Si se encuentra algún cambio, el servicio CDC de Oracle notifica a la instancia CDC de Oracle que debe comprobar su configuración para ver los cambios. La mayoría de los cambios de configuración, como agregar y quitar instancias de captura, se pueden aplicar mientras la instancia CDC de Oracle está habilitada, mientras que otros necesitan que la instancia CDC de Oracle se reinicie.  
  
 Cuando se usa la Consola del diseñador CDC de Oracle, los cambios se detectan automáticamente. Al actualizar la configuración de CDC de Oracle directamente mediante SQL, se debe llamar al procedimiento siguiente para que el servicio CDC de Oracle detecte el cambio de configuración:  
  
```  
DECLARE @dbname nvarchar(128) = 'HRcdc'  
EXECUTE [MSXDBCDC].[dbo].[xdbcdc_update_config_version] @dbname  
GO  
  
```  
  
 El proceso de la instancia CDC de Oracle actualiza su estado en la tabla del sistema **cdc.xdbcdc_state** y escribe la información de error en la tabla **cdc.xdbcdc_trace**. La tabla **xdbcdc_state** es útil para supervisar el estado de la instancia CDC de Oracle. Proporciona el estado actualizado, varios contadores (como el número de cambios leídos de Oracle, el número de cambios escritos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el número de transacciones confirmadas escritas y el número actual de transacciones en curso) y la indicación de latencia.  
  
 La configuración de la instancia CDC de Oracle se guarda en la tabla **cdc.xdbcdc_config**, que es la tabla con la que trabaja la Consola del diseñador CDC de Oracle. Puesto que toda la configuración de una instancia CDC de Oracle se encuentra en la instancia y las bases de datos CDC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de destino, es posible crear scripts de implementación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para una instancia CDC de Oracle. Esto se realiza mediante las consolas de configuración del servicio CDC de Oracle y del Diseñador CDC de Oracle.  
  
## Consideraciones de seguridad  
 A continuación se describen los requisitos de seguridad necesarios para trabajar con el servicio CDC para Oracle.  
  
### Protección de datos de Oracle de origen  
 El servicio CDC de Oracle no necesita acceso a los datos de origen de Oracle y está protegido asegurándose de que las credenciales de minería de registros no proporcionan el permiso SELECT para las tablas de Oracle de cliente.  
  
### Protección de datos modificados de Oracle de origen  
 El servicio CDC de Oracle se proporciona con credenciales de minería de registros que permiten al servicio capturar los cambios realizados en cualquier tabla de la base de datos de Oracle. Los datos modificados no tienen los permisos de acceso específicos que tienen las tablas normales, por lo que el acceso a los datos modificados elude los controles de acceso a datos integrados de Oracle.  
  
 Las tablas capturadas de Oracle de origen tienen tablas reflejadas vacías con el mismo nombre de esquema y de tabla que la base de datos CDC. Los datos capturados se almacena en instancias de captura de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y ofrecen la misma protección que se proporciona para los cambios capturados de la base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obtener acceso a los datos modificados asociados a una instancia de captura, se debe conceder al usuario acceso exclusivo a todas las columnas capturadas de la tabla reflejada asociada. Además, si se especifica un rol de acceso cuando se crea la instancia de captura, el autor de las llamadas también debe ser miembro del rol de acceso especificado. Otras funciones generales de captura de datos modificados para obtener acceso a los metadatos son accesibles para todos los usuarios de la base de datos a través del rol public, aunque el acceso a los metadatos devueltos también se suele conseguir mediante un acceso exclusivo a las tablas de origen subyacentes y por pertenencia a cualquier rol de acceso definido.  
  
 Esto significa que los usuarios que tienen el rol fijo de servidor **sysadmin** o el rol fijo de base de datos **db_owner** tienen (de forma predeterminada) acceso total a los datos capturados, y se puede conceder un acceso aún mayor mediante roles de acceso o concediendo acceso exclusivo a las columnas capturadas.  
  
### Protección de las credenciales de minería de registros de Oracle de origen  
 La configuración del servicio CDC de Oracle, almacenada en la base de datos CDC (en la tabla cdc.xdbcdc_config), incluye el nombre de usuario de minería de registros y su contraseña asociada.  
  
 La contraseña de minería de registros se almacena cifrada mediante una clave asimétrica con el nombre fijo `xdbcdc_asym_key` que se crea automáticamente con el comando siguiente:  
  
```  
USE [<cdc-database-name>]  
CREATE ASYMMETRIC KEY xdbcdc_asym_key  
    WITH ALGORITHM = RSA_1024  
    ENCRYPTION BY PASSWORD = '<cdc-database-name><asym-key-password>'  
  
```  
  
 Si se emplea un algoritmo diferente, se puede quitar esta clave y crear una nueva con el mismo nombre y cifrada con la misma contraseña.  
  
 La contraseña de clave asimétrica es la contraseña maestra que se guarda en el Registro, en la ruta **HKLM\Software\Microsoft\XDBCDCSVC\\<nombre-servicio>**. Esa clave solo está disponible para los administradores locales y la cuenta de servicio de Windows CDC de Oracle. La clave contiene un valor binario cifrado **AsymmetricKeyPassword** que almacena la contraseña de la clave asimétrica. Se necesita acceso a esta clave del Registro para poder obtener acceso a las credenciales de minería de registros de Oracle.  
  
 Para usar la cláusula ENCRYPTION BY PASSWORD, la contraseña debe cumplir los requisitos de la directiva de contraseñas de Windows para el equipo que ejecuta la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Esto se realiza seleccionando la contraseña de clave asimétrica según dicha directiva.  
  
 Si se pierde la contraseña de clave asimétrica, se deben especificar de nuevo las credenciales de minería de registros para cada instancia CDC de Oracle en el Diseñador del servicio CDC de Oracle.  
  
 La clave asimétrica se crea automáticamente en la base de datos CDC cuando el servicio CDC detecta una base de datos CDC de instancia de Oracle que no tiene esta clave asimétrica o cuando la clave existe pero la contraseña no coincide.  
  
### Cuenta de servicio de Windows CDC de Oracle  
 La cuenta de servicio usada con el servicio de Windows CDC de Oracle no necesita ningún privilegio adicional. Esta cuenta debe poder usar la API Oracle Native Client y la API ODBC de SQL Server Native Client. También necesita poder tener acceso a la clave de configuración del servicio en el Registro (la Consola de configuración del servicio CDC configura la ACL para ello).  
  
## En esta sección  
  
-   [Compatibilidad con alta disponibilidad](../../integration-services/change-data-capture/high-availability-support.md)  
  
-   [Permisos de conexión con SQL Server necesarios para el servicio CDC](../../integration-services/change-data-capture/sql-server-connection-required-permissions-for-the-cdc-service.md)  
  
-   [Roles de usuario](../../integration-services/change-data-capture/user-roles.md)  
  
-   [Trabajar con el servicio CDC de Oracle](../../integration-services/change-data-capture/working-with-the-oracle-cdc-service.md)  
  
## Vea también  
 [Cómo administrar un servicio CDC local](../../integration-services/change-data-capture/how-to-manage-a-local-cdc-service.md)   
 [Administrar un servicio CDC de Oracle](../../integration-services/change-data-capture/manage-an-oracle-cdc-service.md)  
  
  