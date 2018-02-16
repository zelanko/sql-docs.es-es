---
title: Roles de usuario | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: change-data-capture
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: be0ec384-e03b-4483-96ca-02b289804d6a
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0abefa916dda5690d033bc9cd74ac5f75245d408
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/15/2018
---
# <a name="user-roles"></a>Roles de usuario
  En esta sección se describen los roles de usuario para el Servicio de captura de datos modificados para Oracle de Attunity. Los roles descritos son roles de base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , roles de Windows o roles de base de datos de Oracle.  
  
## <a name="windows-user-roles"></a>Roles de usuario de Windows  
 A continuación se describen los roles de usuario de Windows que el servicio CDC de Oracle emplea.  
  
### <a name="computer-administrator-oracle-cdc-service"></a>Administrador del equipo: Servicio CDC de Oracle  
 El administrador del equipo es un usuario de Windows responsable de crear y mantener el servicio CDC en el equipo. Este usuario debe pertenecer al grupo Administradores del equipo local.  
  
 Entre las tareas realizadas por el administrador del equipo del servicio CDC de Oracle se incluyen:  
  
-   Instalar el software del servicio CDC para Oracle  
  
-   Crear un servicio de Windows CDC de Oracle  
  
-   Configurar la conexión del servicio CDC con la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de destino (cadena de conexión y credenciales)  
  
-   Asegurarse de que la contraseña maestra del servicio CDC con las credenciales de minería de registros de Oracle está protegida  
  
-   Eliminar un servicio de Windows de servicio CDC  
  
-   Desinstalar el software del servicio CDC para Oracle  
  
-   Mantener el software del servicio CDC para Oracle (por ejemplo, instalando actualizaciones)  
  
-   Iniciar y detener un servicio de Windows de servicio CDC  
  
 Al trabajar con configuraciones de alta disponibilidad, como clústeres de conmutación por error de Microsoft, el administrador del equipo debe tener responsabilidades y permisos adicionales como:  
  
-   Instalar y mantener el software del servicio CDC para Oracle en todos los nodos del clúster.  
  
-   Definir los recursos genéricos del servicio de clúster para el servicio de Windows de servicio CDC en los distintos nodos del clúster.  
  
-   Actuar como administrador del equipo autorizado como administrador en el equipo donde está instalado el servicio CDC para Oracle. Esta persona instala el servicio CDC para Oracle y emplea la Consola de configuración del servicio CDC para configurar un servicio CDC para Oracle en un equipo local.  
  
### <a name="service-account-oracle-cdc-service"></a>Cuenta de servicio: Servicio CDC de Oracle  
 Esta cuenta de servicio de Windows de servicio CDC de Oracle es una cuenta de Windows que se usa para ejecutar el servicio CDC de Oracle (la cuenta de servicio).  
  
 El único privilegio necesario para la cuenta de servicio es poder usar el cliente de Oracle y el proveedor ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client. Esta cuenta no necesita tener acceso a archivos, a menos que lo necesiten determinados proveedores (por ejemplo, si la cadena de conexión de cliente de Oracle hace referencia a instancias de base de datos de Oracle en un archivo **tnsnames.ora** , la cuenta de servicio necesita tener acceso de lectura a ese archivo).  
  
 Al crear un servicio CDC de Oracle en Windows Vista o Windows Server 2008, la cuenta de servicio predeterminada es SERVICIO DE RED.  
  
 En Windows 7, Windows Server 2008 R2 y versiones posteriores, la cuenta de servicio predeterminada es Servicio NT\\<nombre-servicio>.  
  
 Cuando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se ejecuta en otro equipo o es una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en clúster y el servicio necesita conectar con el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de destino usando la autenticación de Windows, la cuenta de servicio debe ser una cuenta de dominio.  
  
## <a name="sql-server-user-roles"></a>Roles de usuario de SQL Server  
 A continuación se describen los roles de usuario de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que el servicio CDC de Oracle emplea.  
  
### <a name="oracle-cdc-service-administrator"></a>Administrador del servicio CDC de Oracle  
 El administrador del servicio CDC es un usuario de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con control total sobre los artefactos del servicio CDC de Oracle en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de destino. El administrador del servicio CDC usa la Consola del diseñador CDC de Oracle para diseñar instancias CDC de Oracle.  
  
 El administrador del servicio CDC debe conceder los roles fijos de servidor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] public **y** dbcreator **de**.  
  
 Entre las tareas realizadas por el administrador del servicio CDC se incluyen:  
  
-   Preparar una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para hospedar instancias CDC de Oracle (que son bases de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ). En esta tarea, se crea una base de datos especial denominada MSXDBCDC en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Crear una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de la instancia CDC de Oracle. La tarea incluye habilitar la nueva base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para CDC, para la que se necesita un administrador del sistema de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (**sysadmin**).  
  
-   Diseñar una instancia CDC de Oracle. Esta tarea incluye proporcionar información acerca de la base de datos de Oracle de origen y las tablas capturadas, lo que necesita un administrador de bases de datos de Oracle.  
  
-   Mantener la instancia CDC de Oracle a lo largo del tiempo, lo que incluye agregar y quitar instancias de captura y actualizar la configuración.  
  
-   Habilitar o deshabilitar una instancia CDC de Oracle.  
  
-   Supervisar el estado de una instancia CDC de Oracle.  
  
-   Solucionar problemas que afectan a la instancia CDC de Oracle.  
  
 El administrador del servicio CDC tiene, al menos inicialmente, el rol fijo de base de datos **db_owner** para la base de datos CDC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] asociada a la instancia CDC de Oracle. Esto proporciona al administrador del servicio CDC acceso a los datos modificados almacenados en la base de datos CDC. Una vez creado, el rol **db_owner** de la base de datos CDC se puede asignar a otro usuario, que puede realizar todas las tareas indicadas anteriormente, excepto preparar una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y crear otra instancia CDC de Oracle.  
  
 El administrador del servicio CDC no necesita conocer la contraseña maestra especificada al crear el servicio de Windows CDC de Oracle.  
  
### <a name="system-administrator"></a>Administrador del sistema  
 El administrador del sistema de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es un usuario de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y necesita tener concedido el rol fijo de servidor **sysadmin** en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] asociada a los servicios CDC de Oracle.  
  
 Solo hay una tarea específica de CDC de Oracle que se realiza con el rol administrador del sistema de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y es habilitar la base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para una instancia CDC de Oracle para CDC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Esta tarea se realiza mediante la Consola del diseñador CDC de Oracle al crear una nueva instancia CDC de Oracle.  
  
### <a name="oracle-cdc-service-user"></a>Usuario del servicio CDC de Oracle  
 El usuario del servicio CDC de Oracle de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que el servicio CDC de Oracle emplea para realizar su trabajo en la base de datos MSXDBCDC y en todas las instancias CDC de Oracle (bases de datos CDC) administradas por este servicio.  
  
 El usuario del servicio CDC de Oracle de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe ser lo siguiente:  
  
-   Miembro de los roles fijos de base de datos **db_dlladmin**, **db_datareader**y **db_datawriter** para todas las bases de datos CDC controladas por el servidor.  
  
-   Miembro de los roles fijos de base de datos **db_datareader** y **db_datawriter** para la base de datos MSXDBCDC.  
  
 Puesto que el servicio CDC de Oracle usa un único inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para trabajar con todas las bases de datos CDC y la base de datos MSXDBCDC, este inicio de sesión se debe asignar en todas las bases de datos.  
  
### <a name="oracle-cdc-change-consumer"></a>Consumidor de cambios CDC de Oracle  
 El consumidor de cambios CDC de Oracle es un usuario de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que usa los cambios almacenados en las tablas CDC de la base de datos de la instancia CDC de Oracle de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Este usuario determina el rol de usuario necesario para tener acceso a cada una de las tablas CDC mediante las funciones CDC generadas por la infraestructura CDC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Si no se especifica ningún rol de usuario al especificar una instancia de captura, el acceso a los cambios está limitado al miembro del rol fijo de base de datos **db_owner** de la base de datos CDC.  
  
## <a name="oracle-user-roles"></a>Roles de usuario de Oracle  
 A continuación se describen los roles de usuario de Oracle que el servicio CDC de Oracle emplea.  
  
### <a name="database-administrator-dba"></a>Administrador de base de datos (DBA)  
 El administrador de base de datos (DBA) de Oracle es un usuario de bases de datos de Oracle. Entre las tareas realizadas por el DBA de Oracle se incluyen:  
  
-   Configurar la base de datos de Oracle de origen para que funcione en modo ARCHIVELOG.  
  
-   Configurar un usuario de minería de registros con los permisos necesarios.  
  
-   Configurar el registro complementario para las tablas capturadas.  
  
-   Ayudar a restaurar los archivos de registro de transacciones almacenados que ya no están disponibles para que se puedan procesar.  
  
 El administrador de bases de datos de Oracle puede obtener scripts SQL de Oracle que hay que ejecutar para que se puedan evaluar antes de ejecutarlos. El administrador de base de datos de Oracle también puede ejecutar directamente scripts SQL de Oracle desde la Consola del diseñador CDC de Oracle.  
  
 Si el administrador de base de datos de Oracle elige usar la Consola del diseñador CDC de Oracle, las credenciales del administrador no se conservan, a excepción del contexto (diálogo) en el que se usaron.  
  
 El administrador de base de datos de Oracle trabaja en coordinación con el administrador del servicio CDC de Oracle en la configuración de las instancias CDC de Oracle de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
### <a name="log-mining-user"></a>Usuario de minería de registros  
 El usuario extractor de registros de Oracle es un usuario especial de base de datos de Oracle al que se conceden los privilegios necesarios para obtener acceso a los registros de transacciones de Oracle y procesarlos.  
  
 Las credenciales de este usuario se almacenan en la base de datos de la instancia CDC de Oracle de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante el cifrado de claves asimétricas. Solo son accesibles para el servicio CDC de Oracle, no para el propietario de la base de datos de la instancia CDC de Oracle de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 En la lista siguiente se describen los privilegios necesarios que se deben conceder al usuario de minería de registros:  
  
-   SELECT en \<any-captured-table>  
  
-   SELECT ANY TRANSACTION  
  
-   EXECUTE en DBMS_LOGMNR  
  
-   SELECT en V$LOGMNR_CONTENTS  
  
-   SELECT en V$ARCHIVED_LOG  
  
-   SELECT en V$LOG  
  
-   SELECT en V$LOGFILE  
  
-   SELECT en V$DATABASE  
  
-   SELECT en V$THREAD  
  
-   SELECT en ALL_INDEXES  
  
-   SELECT en ALL_OBJECTS  
  
-   SELECT en DBA_OBJECTS  
  
-   SELECT en ALL_TABLES  
  
 Si alguno de estos privilegios no se puede conceder a un V$xxx, se debe conceder al V $xxx.  
  
### <a name="schema-user"></a>Usuario de esquema  
 El usuario de esquema de Oracle es un usuario de Oracle con acceso de lectura para el esquema de las tablas de Oracle que se van a capturar. Este usuario es necesario cuando se trabaja con la Consola del diseñador CDC de Oracle recuperar la lista de esquemas de Oracle, tablas que se van a capturar y sus columnas, índices y claves.  
  
 Las credenciales para este usuario nunca se almacenan. La Consola del diseñador CDC las solicita cada vez que son necesarias y se mantienen para las demás sesiones de la interfaz de usuario.  
  
  
