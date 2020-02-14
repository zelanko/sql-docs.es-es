---
title: Nueva generación de bases de datos del sistema | Microsoft Docs
ms.custom: ''
ms.date: 06/06/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- master database [SQL Server], rebuilding
- REBUILDDATABASE parameter
- rebuilding databases, master
- system databases [SQL Server], rebuilding
ms.assetid: af457ecd-523e-4809-9652-bdf2e81bd876
author: stevestein
ms.author: sstein
ms.openlocfilehash: e31a24a949968e3d17b50c32b42e92cdd0997483
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "76516556"
---
# <a name="rebuild-system-databases"></a>Volver a generar bases de datos del sistema
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Las bases de datos del sistema deben volver a generarse para corregir problemas por daños en las bases de datos [maestra](../../relational-databases/databases/master-database.md), [modelo](../../relational-databases/databases/model-database.md), [msdb](../../relational-databases/databases/msdb-database.md)o de [recursos](../../relational-databases/databases/resource-database.md) , o para modificar la intercalación de nivel de servidor predeterminada. En este tema se ofrecen instrucciones paso a paso para volver a generar las bases de datos del sistema en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Requisitos previos](#Prerequisites)  
  
-   **Procedimientos:**  
  
     [Volver a generar bases de datos del sistema](#RebuildProcedure)  
  
     [Volver a generar la base de datos de recursos](#Resource)  
  
     [Crear una base de datos msdb](#CreateMSDB)  
  
-   **Seguimiento:**  
  
     [Solucionar errores de recompilación](#Troubleshoot)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
 Cuando se vuelven a generar las bases de datos maestra, modelo, msdb y tempdb del sistema, las bases de datos se quitan y se vuelven a crear en su ubicación original. Si se especifica una nueva intercalación en la instrucción para volver a generar las bases de datos del sistema, estas se crearán con esa configuración de intercalación. Se perderán las modificaciones que los usuarios hayan realizado en esas bases de datos. Por ejemplo, es posible que haya objetos definidos por los usuarios en la base de datos maestra, trabajos programados en msdb o cambios en la configuración predeterminada de la base de datos modelo.  
  
###  <a name="Prerequisites"></a> Requisitos previos  
 Realice las tareas siguientes antes de volver a generar las bases de datos del sistema para asegurarse de que puede restaurar la configuración actual de las mismas.  
  
1.  Registre todos los valores de configuración del servidor.  
  
    ```  
    SELECT * FROM sys.configurations;  
    ```  
  
2.  Registre todas las correcciones aplicadas a la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y la intercalación actual. Debe aplicar estas correcciones de nuevo después de recompilar las bases de datos del sistema.  
  
    ```  
    SELECT  
    SERVERPROPERTY('ProductVersion ') AS ProductVersion,  
    SERVERPROPERTY('ProductLevel') AS ProductLevel,  
    SERVERPROPERTY('ResourceVersion') AS ResourceVersion,  
    SERVERPROPERTY('ResourceLastUpdateDateTime') AS ResourceLastUpdateDateTime,  
    SERVERPROPERTY('Collation') AS Collation;  
    ```  
  
3.  Registre la ubicación actual de todos los archivos de registro y datos de las bases de datos del sistema. Al volver a generar las bases de datos del sistema, todas ellas se instalan en su ubicación original. Si ha movido los archivos de registro o datos de las bases de datos del sistema a otra ubicación, deberá volver a moverlos.  
  
    ```  
    SELECT name, physical_name AS current_file_location  
    FROM sys.master_files  
    WHERE database_id IN (DB_ID('master'), DB_ID('model'), DB_ID('msdb'), DB_ID('tempdb'));  
    ```  
  
4.  Busque la copia de seguridad actual de las bases de datos maestra, modelo y msdb.  
  
5.  Si la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se configura como Distribuidor de replicación, busque la copia de seguridad actual de la base de datos de distribución.  
  
6.  Asegúrese de que tiene los permisos adecuados para volver a generar las bases de datos del sistema. Para realizar esta operación, debe ser miembro del rol fijo de servidor **sysadmin** . Para obtener más información, vea [Roles de nivel de servidor](../../relational-databases/security/authentication-access/server-level-roles.md).  
  
7.  Compruebe que haya copias de los archivos de plantilla de registro y datos de las bases de datos maestra, modelo y msdb en el servidor local. La ubicación predeterminada de los archivos de plantilla es C:\Archivos de programa\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn\Templates. Estos archivos se usan durante el proceso de volver a generar las bases de datos y deben estar presentes para que la instalación se realice correctamente. Si no lo están, ejecute la característica de reparación del programa de instalación o copie los archivos manualmente desde el disco de instalación. Para encontrar los archivos en el soporte físico de instalación, navegue hasta el directorio de la plataforma correcta (x86 o x64) y, a continuación, navegue hasta setup\sql_engine_core_inst_msi\Pfiles\SqlServr\MSSQL.X\MSSQL\Binn\Templates.  
  
##  <a name="RebuildProcedure"></a> Volver a generar bases de datos del sistema  
 Con el procedimiento siguiente se vuelven a generar las bases de datos maestra, modelo, msdb y tempdb del sistema. No se pueden especificar las bases de datos del sistema que se van a volver a generar. En el caso de las instancias en clúster, este procedimiento se debe realizar en el nodo activo y desconectar el recurso de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] del grupo de aplicaciones en clúster antes de realizar el procedimiento.  
  
 Este procedimiento no vuelve a generar la base de datos de recursos. Vea la sección "Procedimiento para volver a generar la base de datos de recursos" más adelante en este mismo tema.  
  
#### <a name="to-rebuild-system-databases-for-an-instance-of-sql-server"></a>Para volver a generar las bases de datos del sistema para una instancia de SQL Server:  
  
1.  Inserte el disco de instalación de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] en la unidad de disco o, en el símbolo del sistema, cambie el directorio a la ubicación del servidor local donde se encuentra el archivo setup.exe. La ubicación predeterminada en el servidor es \Archivos de programa\Microsoft SQL Server\130\Setup Bootstrap\SQLServer2016.  
  
2.  En una ventana del símbolo del sistema, escriba el siguiente comando. Los parámetros entre corchetes son opcionales. No escriba los corchetes. Cuando se usa un sistema operativo Windows que tiene el Control de cuentas de usuario (UAC) habilitado, para ejecutar el programa de instalación se requieren privilegios elevados. El símbolo del sistema se debe ejecutar como Administrador.  
  
     **Setup /QUIET /ACTION=REBUILDDATABASE /INSTANCENAME=nombreDeInstancia /SQLSYSADMINACCOUNTS=cuentas [ /SAPWD=contraseñaSegura ] [ /SQLCOLLATION=nombreDeIntercalación]**  
  
    |Nombre de parámetro|Descripción|  
    |--------------------|-----------------|  
    |/QUIET o /Q|Especifica que el programa de instalación se ejecute sin ninguna interfaz de usuario.|  
    |/ACTION=REBUILDDATABASE|Especifica que el programa de instalación vuelva a crear las bases de datos del sistema.|  
    |/INSTANCENAME=*InstanceName*|Es el nombre de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para la instancia predeterminada, escriba MSSQLSERVER.|  
    |/SQLSYSADMINACCOUNTS=*accounts*|Especifica las cuentas individuales o de grupos de Windows que se agregarán al rol fijo de servidor **sysadmin** . Si especifica varias cuentas, sepárelas con un espacio en blanco. Escriba, por ejemplo, **BUILTIN\Administrators MyDomain\MyUser**. Cuando está especificando una cuenta que contiene un espacio en blanco dentro del nombre, agregue la cuenta entre comillas tipográficas. Escriba, por ejemplo, **NT AUTHORITY\SYSTEM**.|  
    |[ /SAPWD=*StrongPassword* ]|Especifica la contraseña de la cuenta **sa** de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Este parámetro es obligatorio si la instancia usa el modo Autenticación mixta (autenticación de[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y de Windows).<br /><br /> **&#42;&#42; Nota de seguridad &#42;&#42;** La cuenta **sa** es una cuenta conocida de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y suele ser el objetivo de usuarios malintencionados. Es muy importante que use una contraseña segura en el inicio de sesión de **sa** .<br /><br /> No especifique este parámetro para el modo Autenticación de Windows.|  
    |[ /SQLCOLLATION=*CollationName* ]|Especifica una nueva intercalación de nivel de servidor. Este parámetro es opcional. Cuando no se especifica, se usa la intercalación actual del servidor.<br /><br /> **\*\* Importante \*\*** Al cambiar la intercalación de nivel de servidor, no se cambia la de las bases de datos de usuario existentes. Todas las bases de datos de usuario nuevas usarán la nueva intercalación de manera predeterminada.<br /><br /> Para obtener más información, vea [Configurar o cambiar la intercalación del servidor](../../relational-databases/collations/set-or-change-the-server-collation.md).|  
    |[ /SQLTEMPDBFILECOUNT=númeroDeArchivos ]|Especifica el número de archivos de datos de tempdb. Este valor se puede aumentar hasta 8 o hasta el número de núcleos, lo que sea mayor.<br /><br /> Valor predeterminado: 8 o el número de núcleos, lo que sea menor.|  
    |[ /SQLTEMPDBFILESIZE=tamañoDeArchivoEnMB ]|Especifica el tamaño inicial en MB de cada archivo de datos de tempdb. El programa de instalación permite que el tamaño alcance los 1024 MB.<br /><br /> Valor predeterminado: 8|  
    |[ /SQLTEMPDBFILEGROWTH=tamañoDeArchivoEnMB ]|Especifica el incremento de crecimiento de archivo en MB de cada archivo de datos de tempdb. El valor 0 indica que el crecimiento automático está desactivado y no se permite más espacio. El programa de instalación permite que el tamaño alcance los 1024 MB.<br /><br /> Valor predeterminado: 64|  
    |[ /SQLTEMPDBLOGFILESIZE=tamañoDeArchivoEnMB ]|Especifica el tamaño inicial en MB del archivo de registro de tempdb. El programa de instalación permite que el tamaño alcance los 1024 MB.<br /><br /> Valor predeterminado: 8.<br /><br /> Intervalo permitido: Mín. = 8, máx. = 1024.|  
    |[ /SQLTEMPDBLOGFILEGROWTH=tamañoDeArchivoEnMB ]|Especifica el incremento de crecimiento de archivo en MB del archivo de registro de tempdb. El valor 0 indica que el crecimiento automático está desactivado y no se permite más espacio. El programa de instalación permite que el tamaño alcance los 1024 MB.<br /><br /> Valor predeterminado: 64<br /><br /> Intervalo permitido: Mín. = 8, máx. = 1024.|  
    |[ /SQLTEMPDBDIR=Directorios ]|Especifica el directorio de los archivos de datos de tempdb. Si especifica varios directorios, sepárelos con un espacio en blanco. Si se especifican varios directorios, los archivos de datos de tempdb se distribuirán por turnos entre los directorios.<br /><br /> Valor predeterminado: directorio de datos del sistema|  
    |[ /SQLTEMPDBLOGDIR=Directorio ]|Especifica el directorio de los archivos de registro de tempdb.<br /><br /> Valor predeterminado: directorio de datos del sistema|  
  
3.  Una vez completada la regeneración de las bases de datos del sistema, el programa de instalación regresa al símbolo del sistema sin mostrar ningún mensaje. Examine el archivo de registro Summary.txt para comprobar que el proceso se completó correctamente. Este archivo se encuentra en C:\Archivos de programa\Microsoft SQL Server\130\Setup Bootstrap\Logs.  
  
4.  El escenario RebuildDatabase elimina las bases de datos del sistema y las instala de nuevo en un estado limpio. Dado que el valor del recuento de archivos de tempdb no se conserva, el valor del número de archivos de tempdb no se conoce durante la instalación. Por lo tanto, el escenario RebuildDatabase no conoce el recuento de archivos de tempdb que se van a volver a agregar. Puede volver a proporcionar el valor del número de archivos de tempdb con el parámetro SQLTEMPDBFILECOUNT. Si no se proporciona el parámetro, RebuildDatabase agregará un número predeterminado de archivos de tempdb, que será de tantos archivos de tempdb como el recuento de CPU o de 8, lo que sea menor.  
  
## <a name="post-rebuild-tasks"></a>Tareas posteriores al proceso de volver a generar bases de datos  
 Después de volver a generar la base de datos, quizás deba realizar las tareas adicionales siguientes:  
  
-   Restaurar las copias de seguridad completas más recientes de las bases de datos maestra, modelo y msdb. Para obtener más información, vea [Realizar copias de seguridad y restaurar bases de datos del sistema &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md).  
  
    > [!IMPORTANT]  
    >  Si ha cambiado la intercalación del servidor, no restaure las bases de datos del sistema. Si lo hace, reemplazará la nueva intercalación por la antigua.  
  
     Si no dispone de una copia de seguridad o si la copia de seguridad restaurada no es actual, vuelva a crear las entradas que no se encuentren. Por ejemplo, vuelva a crear todas las entradas que no se encuentren de las bases de datos de usuario, los dispositivos de copia de seguridad, los inicios de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , los puntos de conexión, etc. La mejor forma de volver a crear las entradas es ejecutar los scripts originales que se usaron para crearlas.  
  
> [!IMPORTANT]  
>  Se recomienda proteger los scripts para evitar que los modifiquen personas no autorizadas.  
  
-   Si la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se configura como Distribuidor de replicación, debe restaurar la base de datos de distribución. Para obtener más información, vea [Realizar copias de seguridad y restaurar bases de datos de SQL Server](../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md).  
  
-   Mover las bases de datos del sistema a las ubicaciones registradas anteriormente. Para obtener más información, vea [Mover bases de datos del sistema](../../relational-databases/databases/move-system-databases.md).  
  
-   Comprobar que los valores de configuración de todo el servidor coinciden con los valores registrados anteriormente.  
  
##  <a name="Resource"></a> Volver a generar la base de datos de recursos  
 Con el procedimiento siguiente se vuelve a generar la base de datos de recursos. Al recompilar la base de datos de recursos, se pierden todas las correcciones y, por lo tanto, se deben volver a aplicar.  
  
#### <a name="to-rebuild-the-resource-system-database"></a>Para volver a generar la base de datos de recursos:  
  
1.  Inicie el programa de instalación de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] (setup.exe) desde los discos de distribución.  
  
2.  En el área de navegación izquierda, haga clic en **Mantenimiento**y, a continuación, en **Reparar**.  
  
3.  Las rutinas de archivo y de reglas auxiliares del programa de instalación se ejecutan para asegurarse de que el sistema tiene instalados los requisitos previos y que el equipo supera las reglas de validación del programa de instalación. Haga clic en **Aceptar** o en **Instalar** para continuar.  
  
4.  En la página Seleccionar instancia, seleccione la instancia que desea reparar y, a continuación, haga clic en **Siguiente**.  
  
5.  Las reglas de reparación se ejecutarán para validar la operación. Para continuar, haga clic en **Siguiente**.  
  
6.  En la página **Listo para reparar** , haga clic en **Reparar**. La página Operación completada indica que la operación ha finalizado.  
  
##  <a name="CreateMSDB"></a> Crear una base de datos msdb  
 Si la base de datos **msdb** se daña y no tiene una copia de seguridad de la base de datos **msdb** , puede crear una nueva **msdb** con el script **instmsdb** .  
  
> [!WARNING]  
>  Al recompilar la base de datos **msdb** con el script **instmsdb** , eliminará toda la información almacenada en **msdb** como los trabajos, las alertas, los operadores, los planes de mantenimiento, el historial de copia de seguridad, la configuración de la administración basada en directivas, Correo electrónico de base de datos, Almacenamiento de datos de rendimiento, etc.  
  
1.  Detenga todos los servicios que se conectan al [!INCLUDE[ssDE](../../includes/ssde-md.md)], incluido el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , [!INCLUDE[ssRS](../../includes/ssrs.md)], [!INCLUDE[ssIS](../../includes/ssis-md.md)]y todas las aplicaciones que usan [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como almacén de datos.  
  
2.  Inicie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] desde la línea de comandos usando el comando: `NET START MSSQLSERVER /T3608`  
  
     Para más información, consulte [Iniciar, detener, pausar, reanudar y reiniciar el motor de base de datos, Agente SQL Server o el Servicio SQL Server Browser](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md).  
  
3.  En otra ventana de la línea de comandos, separe la base de datos **msdb** ejecutando el siguiente comando y reemplazando *\<servername>* por la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: `SQLCMD -E -S<servername> -dmaster -Q"EXEC sp_detach_db msdb"`  
  
4.  Con el Explorador de Windows, cambie el nombre de los archivos de la base de datos **msdb** . De forma predeterminada, están en la subcarpeta DATA de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
5.  Con el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , detenga y reinicie el servicio [!INCLUDE[ssDE](../../includes/ssde-md.md)] de la forma normal.  
  
6.  En una ventana de línea de comandos, conéctese a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y ejecute el comando: `SQLCMD -E -S<servername> -i"C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Install\instmsdb.sql" -o"C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Install\instmsdb.out"`  
  
     Reemplace *\<servername>* por la instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Use la ruta de acceso al sistema de archivos de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
7.  Con el Bloc de notas de Windows, abra el archivo **instmsdb.out** y compruebe si hay errores en la salida.  
  
8.  Vuelva a aplicar las correcciones instaladas en la instancia.  
  
9. Vuelva a crear el contenido de usuario almacenado en la base de datos **msdb** , como los trabajos, la alerta, etc.  
  
10. Haga una copia de seguridad de la base de datos **msdb** .  
  
##  <a name="Troubleshoot"></a> Solucionar errores de recompilación  
 Los errores de sintaxis y otros errores en tiempo de ejecución se muestran en la ventana del símbolo del sistema. Examine la instrucción de instalación en busca de los siguientes errores de sintaxis:  
  
-   La barra diagonal (/) no aparece delante de los nombres de los parámetros.  
  
-   Se ha omitido el signo de igualdad (=) entre el nombre del parámetro y su valor.  
  
-   Hay espacios en blanco entre el nombre del parámetro y el signo igual.  
  
-   Presencia de comas (,) u otros caracteres que no se especifican en la sintaxis.  
  
 Cuando se haya completado el proceso de volver a generar la base de datos, examine los registros de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en busca de errores. De manera predeterminada, están en C:\Archivos de programa\Microsoft SQL Server\130\Setup Bootstrap\Logs. Para encontrar el archivo de registro que contiene los resultados del proceso de volver a generar bases de datos, cambie el directorio a la carpeta Logs en un símbolo del sistema y, a continuación, ejecute `findstr /s RebuildDatabase summary*.*`. Esta búsqueda indicará los archivos de registro que contengan los resultados del proceso de volver a generar las bases de datos del sistema. Abra los archivos de registro y examine si contienen mensajes de error relevantes.  
  
## <a name="see-also"></a>Consulte también  
 [Bases de datos del sistema](../../relational-databases/databases/system-databases.md)  
  
  
