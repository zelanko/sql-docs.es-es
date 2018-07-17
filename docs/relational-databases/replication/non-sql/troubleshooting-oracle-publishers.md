---
title: Solucionar problemas de los publicadores de Oracle | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Oracle publishing [SQL Server replication], troubleshooting
- troubleshooting [SQL Server replication], Oracle publishing
ms.assetid: be94f1c1-816b-4b1d-83f6-2fd6f5807ab7
caps.latest.revision: 62
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 80083eaf0630d75efcd96af801c7f1adf33f8374
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37352637"
---
# <a name="troubleshooting-oracle-publishers"></a>Solucionar problemas de los publicadores de Oracle
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  En este tema se describen varios problemas que pueden surgir al configurar y utilizar un publicador de Oracle.  
  
## <a name="an-error-is-raised-regarding-oracle-client-and-networking-software"></a>Aparece un error referente al cliente Oracle y al software de red  
 La cuenta con la que se ejecuta [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en el distribuidor debe tener permisos de lectura y escritura para el directorio (y todos los subdirectorios) en el que está instalado el software de red del cliente Oracle. Si no se conceden estos permisos o los componentes del cliente Oracle no están instalados correctamente, recibirá el siguiente mensaje de error:  
  
 "Error de conexión al servidor con [Proveedor Microsoft OLE DB para Oracle]. No se encontraron los componentes de cliente y de red de Oracle. Oracle Corporation proporciona estos componentes, que forman parte de la instalación del software de cliente de Oracle, versión 7.3.3 o posterior. El proveedor no funcionará hasta que se instalen estos componentes."  
  
 Si se ha instalado el cliente de Oracle correcto en el distribuidor, asegúrese de que [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] se haya detenido y reiniciado al terminar la instalación del cliente. Es necesario hacerlo para que [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] reconozca los componentes de cliente.  
  
 Si ha comprobado que tiene los permisos necesarios y que los componentes están instalados correctamente y el error persiste, compruebe que la configuración del Registro en HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDTC\MTxOCI sea correcta:  
  
-   Para Oracle 10g, la configuración correcta es  
  
    -   OracleOciLib = oci.dll  
  
    -   OracleSqlLib = orasql10.dll  
  
    -   OracleXaLib = oraclient10.dll  
  
-   Para Oracle 9i, la configuración correcta es  
  
    -   OracleOciLib = oci.dll  
  
    -   OracleSqlLib = orasql9.dll  
  
    -   OracleXaLib = oraclient9.dll  
  
## <a name="the-sql-server-distributor-cannot-connect-to-the-oracle-database-instance"></a>El distribuidor de SQL Server no puede conectarse a la instancia de base de datos de Oracle  
 Si el distribuidor de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no se puede conectar al publicador de Oracle, compruebe que:  
  
-   El software de Oracle necesario está instalado en el distribuidor.  
  
-   La base de datos de Oracle está en línea y puede conectarse a ella con una herramienta como SQL*Plus.  
  
-   El inicio de sesión que utiliza la replicación para conectarse al publicador de Oracle tiene permisos suficientes. Para obtener más información, vea [Configurar un publicador de Oracle](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md).  
  
-   Los nombres TNS definidos durante la configuración del publicador de Oracle aparecen en el archivo tnsnames.ora.  
  
-   Se utiliza el directorio de inicio de Oracle (Oracle Home) y la ruta de acceso correctos. Aunque solamente tenga un conjunto de archivos binarios de Oracle instalados en el distribuidor [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , asegúrese de que las variables de entorno relacionadas con el directorio de inicio de Oracle están configuradas correctamente. Si cambia los valores de las variables de entorno, deberá detener y reiniciar [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para que se aplique el cambio.  
  
 Para más información sobre la configuración y comprobación de la conectividad, vea la sección sobre instalación y configuración del software de red del cliente Oracle en el distribuidor de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], en [Configurar un publicador de Oracle](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md).  
  
## <a name="the-oracle-publisher-is-associated-with-another-distributor"></a>El publicador de Oracle está asociado con otro distribuidor  
 Un publicador de Oracle solamente se puede asociar con un distribuidor de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Si se asocia un distribuidor distinto con el publicador de Oracle, deberá quitarse para poder usar otro distribuidor. Si no se quita primero el distribuidor, aparecerá uno de los siguientes mensajes de error:  
  
-   "La instancia del servidor de Oracle "\<*NombrePublicadorOracle*>" se ha configurado previamente para usar "\<*NombreDistribuidorSQLServer*>" como distribuidor. Para empezar a usar "\<*NewSQLServerDistributorName*>" como distribuidor, debe quitar la configuración de replicación actual de la instancia del servidor de Oracle, lo que eliminará todas las publicaciones existentes en esa instancia del servidor".  
  
-   "Ya se ha definido el servidor Oracle "\<*NombreServidorOracle*>" como publicador "\<*NombrePublicadorOracle*>" en el distribuidor "\<*NombreDistribuidorSQLServer*>.*\<NombreBaseDatosDistribución>*". Quite el publicador o el sinónimo público "*\<NombreSinónimo>*" para volver a crearlo".  
  
 Al quitar un publicador de Oracle, los objetos de replicación de la base de datos de Oracle se limpian automáticamente. Sin embargo, en algunos casos es necesario limpiar manualmente los objetos de replicación de Oracle. Para limpiar manualmente los objetos de replicación de Oracle creados por la replicación:  
  
1.  Conéctese al publicador de Oracle con permisos de administrador de base de datos (DBA).  
  
2.  Emita el comando SQL `DROP PUBLIC SYNONYM MSSQLSERVERDISTRIBUTOR;`.  
  
3.  Emita el comando SQL `DROP USER <replication_administrative_user_schema>``CASCADE;`.  
  
## <a name="sql-server-error-21663-is-raised-regarding-the-lack-of-a-primary-key"></a>Aparece el error 21663 de SQL Server referente a la falta de una clave principal  
 Los artículos de las publicaciones transaccionales deben tener una clave principal válida. Si no tienen una clave principal válida, aparecerá el siguiente mensaje de error cuando intente agregar un artículo:  
  
 "No valid primary key found for source table [\<*TableOwner*>].[\<*TableName*>]" (No se encuentra ninguna clave principal válida para la tabla de origen [<PropietarioTabla>].[<NombreTabla>])  
  
 Para obtener información acerca de los requisitos para las claves principales, vea la sección sobre índices y restricciones únicos en el tema [Design Considerations and Limitations for Oracle Publishers](../../../relational-databases/replication/non-sql/design-considerations-and-limitations-for-oracle-publishers.md).  
  
## <a name="sql-server-error-21642-is-raised-regarding-a-duplicate-linked-server-login"></a>Aparece el error 21642 de SQL Server referente a un inicio de sesión duplicado en el servidor vinculado  
 Al configurar inicialmente el publicador de Oracle, se crea una entrada de servidor vinculado para la conexión entre el publicador y el distribuidor. El servidor vinculado tiene el mismo nombre que el servicio TNS de Oracle. Si intenta crear un servidor vinculado con el mismo nombre, aparecerá el siguiente mensaje de error:  
  
 "Los publicadores heterogéneos requieren un servidor vinculado. Ya existe un servidor vinculado con el nombre "*\<NombreServidorVinculado>*". Quítelo o elija otro nombre de publicador."  
  
 Este error puede aparecer si intenta crear el servidor vinculado directamente o si quitó anteriormente la relación entre el publicador de Oracle y el distribuidor de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , y está intentando volver a configurarla. Si recibe este error al intentar volver a configurar el publicador, quite el servidor vinculado con [sp_dropserver &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-dropserver-transact-sql.md).  
  
 Si necesita conectarse al publicador de Oracle a través de una conexión con el servidor vinculado, cree otro nombre de servicio TNS y después úselo para llamar a [sp_addlinkedserver &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md). Para obtener información acerca de cómo crear nombres de servicio TNS, vea la documentación de Oracle.  
  
## <a name="sql-server-error-21617-is-raised"></a>Aparece el error 21617 de SQL Server  
 En la publicación de Oracle se utiliza la aplicación SQL*PLUS de Oracle para descargar el paquete de código de compatibilidad con el publicador a la base de datos de Oracle. Antes de intentar configurar el publicador de Oracle, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] comprueba que se puede tener acceso a SQL\*PLUS a través de la ruta de acceso del sistema en el distribuidor. Si no se puede cargar SQL\*PLUS, se muestra el siguiente mensaje de error:  
  
 "No se pudo ejecutar SQL*PLUS. Compruebe que el código del cliente de Oracle instalado en el distribuidor corresponda a la versión actual."  
  
 Busque SQL\*PLUS en el distribuidor. Para una instalación de cliente Oracle 10g, el nombre de este ejecutable es sqlplus.exe. Normalmente está instalado en %ORACLE_HOME%/bin. Para comprobar que la ruta de acceso de SQL\*PLUS aparece en la ruta de acceso del sistema, observe el valor de la variable del sistema **Path**:  
  
1.  Haga clic con el botón secundario en **Mi PC**y, a continuación, haga clic en **Propiedades**.  
  
2.  Haga clic en la pestaña **Avanzadas** y, a continuación, haga clic en **Variables de entorno**.  
  
3.  En el cuadro de diálogo **Variables de entorno** , en la lista **Variables del sistema** , seleccione la variable **Path** y, a continuación, haga clic en **Modificar**.  
  
4.  En el cuadro de diálogo **Modificar la variable del sistema** : si la ruta de acceso a la carpeta en que se encuentra sqlplus.exe no aparece en el cuadro de texto **Valor de variable** , modifique la cadena para agregarla.  
  
5.  Haga clic en **Aceptar** en todos los cuadros de diálogo abiertos para salir y guardar los cambios.  
  
 Si no encuentra sqlplus.exe en el distribuidor, instale la versión actual del software de cliente de Oracle en el distribuidor. Para obtener más información, vea [Configurar un publicador de Oracle](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md).  
  
## <a name="sql-server-error-21620-is-raised"></a>Aparece el error 21620 de SQL Server  
 Si va a conectar a una base de datos Oracle anterior a la versión 8.1, la publicación de Oracle requiere que el software de cliente Oracle instalado en el distribuidor sea de la versión 9. Si se va a conectar a una base de datos Oracle que es de la versión 8.1 o posterior, se recomienda que el software del cliente Oracle sea de la versión 10 o posterior.  
  
 Antes de intentar configurar el publicador de Oracle, la publicación de Oracle comprueba que la versión de SQL*PLUS a la que se puede tener acceso través de la ruta de acceso del sistema en el distribuidor es la versión 9 o posterior. Si no lo es, se muestra el siguiente mensaje de error:  
  
 "La versión de SQL*PLUS a la que se tiene acceso a través de la variable Path del sistema no es lo suficientemente actual para admitir publicaciones de Oracle. Compruebe que el código del cliente de Oracle instalado en el distribuidor corresponda a la versión actual."  
  
 Si tiene varias versiones del software cliente de Oracle instaladas en el distribuidor, asegúrese de que la versión más reciente es la versión 9 como mínimo y que la variable del sistema Path hace referencia a esta versión en primer lugar (puede haber referencias a otras versiones, siempre que la referencia a la versión más reciente sea la primera). Para obtener más información sobre la modificación de la variable del sistema Path, vea la sección "Se provoca el error 21617 de SQL Server" de este tema.  
  
## <a name="sql-server-error-21624-or-error-21629-is-raised"></a>Aparece el error 21624 o 21629 de SQL Server  
 Para los distribuidores de 64 bits, la publicación de Oracle utiliza el proveedor Oracle OLEDB para Oracle (OraOLEDB.Oracle). Asegúrese de que el proveedor Oracle OLEDB está instalado y registrado en el distribuidor. Si el proveedor no está instalado y registrado, se muestra uno de los siguientes mensajes, o los dos:  
  
-   "No se puede encontrar el proveedor OLEDB de Oracle registrado, OraOLEDB.Oracle, en el distribuidor '%s'. Compruebe que la versión del proveedor OLEDB de Oracle instalada y registrada en el distribuidor sea la actual."  
  
-   "La clave del Registro CLSID que indica que el proveedor OLEDB de Oracle, OraOLEDB.Oracle, se ha registrado no está presente en el distribuidor. Compruebe que el proveedor OLEDB de Oracle se haya instalado y registrado en el distribuidor".  
  
 Si va a usar el software de cliente Oracle versión 10g, el proveedor es OraOLEDB10.dll; para la versión 9i, es OraOLEDB.dll. El proveedor está instalado en %ORACLE_HOME%\BIN (por ejemplo, C:\oracle\product\10.1.0\Client_1\bin). Si el proveedor Oracle OLEDB no está instalado en el distribuidor, instálelo desde el disco de instalación del software cliente de Oracle que proporciona Oracle. Para obtener más información, vea [Configurar un publicador de Oracle](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md).  
  
 Si el proveedor Oracle OLEDB está instalado, asegúrese de que está registrado. Para registrar el archivo DLL del proveedor, ejecute el siguiente comando desde el directorio en que esté instalado el archivo DLL y, a continuación, detenga y reinicie la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] :  
  
1.  `regsvr32 OraOLEDB10.dll` o bien `regsvr32 OraOLEDB.dll`.  
  
## <a name="sql-server-error-21626-or-error-21627-is-raised"></a>Aparece el error 21626 o 21627 de SQL Server  
 Para comprobar que el entorno de la publicación de Oracle está configurado correctamente, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] trata de conectarse al publicador de Oracle con las credenciales de inicio de sesión especificadas durante la configuración. Si el distribuidor de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no se puede conectar al publicador de Oracle, se muestra el siguiente mensaje de error:  
  
-   "No se puede conectar con el servidor de base de datos Oracle '%s' mediante el proveedor OLEDB de Oracle, OraOLEDB.Oracle."  
  
 Si aparece este mensaje de error, compruebe la conexión con la base de datos de Oracle: ejecute SQL*PLUS directamente, con el mismo inicio de sesión y la misma contraseña especificados durante la configuración del publicador de Oracle. Para obtener más información, vea la sección "El distribuidor de SQL Server no puede conectarse a la instancia de base de datos de Oracle" de este tema.  
  
## <a name="sql-server-error-21628-is-raised"></a>Aparece el error 21628 de SQL Server  
 Para los distribuidores de 64 bits, la publicación de Oracle utiliza el proveedor Oracle OLEDB para Oracle (OraOLEDB.Oracle). [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] crea una entrada en el Registro para permitir que el proveedor de Oracle ejecutarse en proceso con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Si hay un problema de lectura o escritura con esta entrada del Registro, aparece el siguiente mensaje de error:  
  
 "No se puede actualizar el Registro del distribuidor '%s' para que el proveedor OLE DB de Oracle, OraOLEDB.Oracle, pueda ejecutarse con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Compruebe que el inicio de sesión actual esté autorizado a modificar las claves del Registro propiedad de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ."  
  
 La publicación de Oracle requiere que la entrada en el Registro exista y esté establecida en **1** para los distribuidores de 64 bits. Si la entrada no existe, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tratará de crearla. Si existe, pero está establecida en **0**, está opción no se modificará y se producirá un error en la configuración del publicador de Oracle.  
  
 Para ver y modificar la opción del Registro:  
  
1.  Haga clic en **Inicio**y, a continuación, haga clic en **Ejecutar**.  
  
2.  En el cuadro de diálogo **Ejecutar** , escriba **regedit**y, a continuación, haga clic en **Aceptar**.  
  
3.  Navegue hasta HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\\*\<nombreInstancia>* \Providers.  
  
     Se debe incluir en Proveedores una carpeta denominada OraOLEDB.Oracle. En esta carpeta debe encontrarse el nombre de valor DWORD **AllowInProcess**, con un valor de **1**.  
  
4.  Si determina que **AllowInProcess** tiene el valor **0**, actualice la entrada del Registro a **1**:  
  
    1.  Haga clic con el botón secundario en la entrada y, a continuación, haga clic en **Modificar**.  
  
    2.  En el cuadro de diálogo **Editar cadena** , escriba **1** en el campo **Datos del valor** .  
  
## <a name="sql-server-error-21684-is-raised"></a>Aparece el error 21684 de SQL Server  
 Si la cuenta de usuario administrativo no tiene privilegios suficientes, se muestra el siguiente mensaje de error:  
  
 "Los permisos asociados con el inicio de sesión de administrador del publicador de Oracle '%s' no son suficientes."  
  
 Para comprobar los permisos concedidos al usuario, ejecute la consulta siguiente: `SELECT * from session_privs`. La salida debe ser similar a la siguiente:  
  
 `PRIVILEGE`  
  
 `------------------`  
  
 `CREATE SESSION`  
  
 `CREATE TABLE`  
  
 `CREATE PUBLIC SYNONYM`  
  
 `DROP PUBLIC SYNONYM`  
  
 `CREATE VIEW`  
  
 `CREATE SEQUENCE`  
  
 `CREATE PROCEDURE`  
  
 `CREATE TRIGGER`  
  
## <a name="you-encounter-permissions-issues-for-the-replication-user-schema"></a>Tiene problemas de permisos para el esquema de usuario de la replicación  
 El esquema de usuario de la replicación debe tener los permisos que se describen en la sección sobre creación manual de esquemas de usuario en [Configurar un publicador de Oracle](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md).  
  
## <a name="oracle-error-ora-01000"></a>Error ORA-01000 de Oracle  
 Durante el proceso de agregar artículos a una publicación, la replicación utiliza cursores en el publicador de Oracle. Durante este proceso, es posible superar el número máximo de cursores disponibles en el publicador. Si esto ocurre, aparecerá el siguiente error:  
  
 "ORA-01000: maximum open cursors exceeded"  
  
 Para evitar este problema, asegúrese de que el parámetro **max_open_cursors** de las bases de datos de Oracle esté establecido en un número suficientemente alto (al menos 1000). Para obtener más información acerca de este parámetro, vea la documentación de Oracle.  
  
## <a name="oracle-error-ora-01555"></a>Error ORA-01555 de Oracle  
 El siguiente error de la base de datos de Oracle no está relacionado con la replicación de instantáneas, sino con la forma en que Oracle crea vistas de datos coherentes con la lectura:  
  
 "ORA-01555: Snapshot too old"  
  
 Oracle utiliza objetos conocidos como segmentos de reversión para crear vistas de datos coherentes con la lectura en el momento en que se emite una instrucción SQL. El error "snapshot too old" (instantánea demasiado antigua) se puede producir cuando otras sesiones simultáneas sobrescriben la información de reversión. Antes de Oracle 9i, el método recomendado para reducir la frecuencia de este error era aumentar el tamaño o el número de segmentos de reversión, y asignar transacciones grandes a un segmento de reversión específico.  
  
 En Oracle 9i, Oracle presentó el concepto de espacio de tabla UNDO, que sustituye al segmento de reversión. Para evitar el error "snapshot too old" en Oracle 9i, se recomienda:  
  
-   Crear un espacio de tabla UNDO con una cantidad apropiada de espacio disponible.  
  
-   Establecer la garantía de retención en el espacio de tabla (Oracle 10G y superior).  
  
-   Configurar los parámetros de inicialización de Oracle UNDO_MANAGEMENT y UNDO_RETENTION.  
  
 Para obtener más información acerca de cómo evitar el error "snapshot too old", vea la documentación de Oracle.  
  
## <a name="oracle-error-ora-22285"></a>Error ORA-22285 de Oracle  
 Si una tabla incluye una columna BFILE, los datos de la columna se guardan en el sistema de archivos. La cuenta de usuario administrativo de la replicación debe tener acceso al directorio en el que se almacenan los datos, con la siguiente sintaxis:  
  
 `GRANT READ ON DIRECTORY <directory_name> TO <replication_administrative_user_schema>`  
  
 Si no se concede el acceso, el Agente de registro del LOG muestra el siguiente error:  
  
 "ORA-22285: non-existent directory or file for FILEOPEN operation"  
  
## <a name="changes-are-made-that-require-reconfiguration-of-the-publisher"></a>Se han realizado cambios que requieren volver a configurar el publicador  
 Los cambios en los procedimientos o en las tablas de metadatos de la replicación obligan a quitar y configurar de nuevo el publicador. Para volver a configurar el publicador, debe quitarlo y configurarlo de nuevo con [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], Transact-SQL o RMO. Para más información sobre la configuración del publicador, vea [Configurar un publicador de Oracle](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md).  
  
 **Para eliminar un publicador de Oracle (** SQL Server Management Studio **)**  
  
1.  Conéctese al distribuidor del publicador de Oracle en [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] y expanda el nodo de servidor.  
  
2.  Haga clic con el botón secundario en **Replicación**y, a continuación, haga clic en **Propiedades del distribuidor**.  
  
3.  En la página **Publicadores** del cuadro de diálogo **Propiedades del distribuidor** , desactive la casilla del publicador de Oracle.  
  
4.  Haga clic en **Aceptar**.  
  
 **Para quitar un publicador de Oracle (Transact-SQL)**  
  
-   Ejecute **sp_dropdistpublisher**. Para más información, vea [sp_dropdistpublisher &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql.md).  
  
## <a name="see-also"></a>Ver también  
 [Configurar un publicador de Oracle](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)   
 [Información general de la publicación de Oracle](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md)  
  
  
