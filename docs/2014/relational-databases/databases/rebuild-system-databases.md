---
title: Nueva generación de bases de datos del sistema | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: b58378e8ba2193a186fb58e3e784bf9bc3cb4d4c
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52749407"
---
# <a name="rebuild-system-databases"></a>Volver a generar bases de datos del sistema
  Las bases de datos del sistema deben volver a generarse para corregir problemas por daños en las bases de datos [maestra](master-database.md), [modelo](model-database.md), [msdb](msdb-database.md)o de [recursos](resource-database.md) , o para modificar la intercalación de nivel de servidor predeterminada. En este tema se ofrecen instrucciones paso a paso para volver a generar las bases de datos del sistema en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
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
  
2.  Registre todos los Service Pack y todas las revisiones que se hayan aplicado a la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y la intercalación actual. Deberá aplicar estas actualizaciones de nuevo después de volver a generar las bases de datos del sistema.  
  
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
  
6.  Asegúrese de que tiene los permisos adecuados para volver a generar las bases de datos del sistema. Para realizar esta operación, debe ser miembro del rol fijo de servidor `sysadmin`. Para obtener más información, vea [Roles de nivel de servidor](../security/authentication-access/server-level-roles.md).  
  
7.  Compruebe que haya copias de los archivos de plantilla de registro y datos de las bases de datos maestra, modelo y msdb en el servidor local. La ubicación predeterminada de los archivos de plantilla es C:\Archivos de programa\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Binn\Templates. Estos archivos se usan durante el proceso de volver a generar las bases de datos y deben estar presentes para que la instalación se realice correctamente. Si no lo están, ejecute la característica de reparación del programa de instalación o copie los archivos manualmente desde el disco de instalación. Para encontrar los archivos en el soporte físico de instalación, navegue hasta el directorio de la plataforma correcta (x86 o x64) y, a continuación, navegue hasta setup\sql_engine_core_inst_msi\Pfiles\SqlServr\MSSQL.X\MSSQL\Binn\Templates.  
  
##  <a name="RebuildProcedure"></a> Volver a generar bases de datos del sistema  
 Con el procedimiento siguiente se vuelven a generar las bases de datos maestra, modelo, msdb y tempdb del sistema. No se pueden especificar las bases de datos del sistema que se van a volver a generar. En el caso de las instancias en clúster, este procedimiento se debe realizar en el nodo activo y desconectar el recurso de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] del grupo de aplicaciones en clúster antes de realizar el procedimiento.  
  
 Este procedimiento no vuelve a generar la base de datos de recursos. Vea la sección "Procedimiento para volver a generar la base de datos de recursos" más adelante en este mismo tema.  
  
#### <a name="to-rebuild-system-databases-for-an-instance-of-sql-server"></a>Para volver a generar las bases de datos del sistema para una instancia de SQL Server:  
  
1.  Inserte el disco de instalación de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] en la unidad de disco o, en el símbolo del sistema, cambie el directorio a la ubicación del servidor local donde se encuentra el archivo setup.exe. La ubicación predeterminada en el servidor es C:\Archivos de programa\Microsoft SQL Server\120\Setup Bootstrap\Release.  
  
2.  En una ventana del símbolo del sistema, escriba el siguiente comando. Los parámetros entre corchetes son opcionales. No escriba los corchetes. Cuando se usa un sistema operativo Windows que tiene el Control de cuentas de usuario (UAC) habilitado, para ejecutar el programa de instalación se requieren privilegios elevados. El símbolo del sistema se debe ejecutar como Administrador.  
  
     `Setup /QUIET /ACTION=REBUILDDATABASE /INSTANCENAME=InstanceName /SQLSYSADMINACCOUNTS=accounts [ /SAPWD= StrongPassword ] [ /SQLCOLLATION=CollationName]`  
  
    |Nombre del parámetro|Descripción|  
    |--------------------|-----------------|  
    |/QUIET o /Q|Especifica que el programa de instalación se ejecute sin ninguna interfaz de usuario.|  
    |/ACTION=REBUILDDATABASE|Especifica que el programa de instalación vuelva a crear las bases de datos del sistema.|  
    |/INSTANCENAME=*InstanceName*|Es el nombre de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para la instancia predeterminada, escriba MSSQLSERVER.|  
    |/SQLSYSADMINACCOUNTS=*accounts*|Especifica las cuentas individuales o de grupos de Windows que se agregarán al rol fijo de servidor `sysadmin`. Si especifica varias cuentas, sepárelas con un espacio en blanco. Escriba, por ejemplo, **BUILTIN\Administrators MyDomain\MyUser**. Cuando está especificando una cuenta que contiene un espacio en blanco dentro del nombre, agregue la cuenta entre comillas tipográficas. Por ejemplo, escriba `NT AUTHORITY\SYSTEM`:|  
    |[ /SAPWD=*StrongPassword* ]|Especifica la contraseña de la cuenta `sa` de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Este parámetro es obligatorio si la instancia usa el modo Autenticación mixta (autenticación de[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y de Windows).<br /><br /> **\*\* Nota de seguridad \* \***  el `sa` cuenta es una cuenta conocida [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cuenta y a menudo el objetivo de usuarios malintencionados. Es muy importante que use una contraseña segura en el inicio de sesión de `sa`.<br /><br /> No especifique este parámetro para el modo Autenticación de Windows.|  
    |[ /SQLCOLLATION=*CollationName* ]|Especifica una nueva intercalación de nivel de servidor. Este parámetro es opcional. Cuando no se especifica, se usa la intercalación actual del servidor.<br /><br /> **\*\* Importante \* \***  cambiar la intercalación de nivel de servidor no cambia la intercalación de bases de datos de usuario existentes. Todas las bases de datos de usuario nuevas usarán la nueva intercalación de manera predeterminada.<br /><br /> Para obtener más información, vea [Configurar o cambiar la intercalación del servidor](../collations/set-or-change-the-server-collation.md).|  
  
3.  Una vez completada la regeneración de las bases de datos del sistema, el programa de instalación regresa al símbolo del sistema sin mostrar ningún mensaje. Examine el archivo de registro Summary.txt para comprobar que el proceso se completó correctamente. Este archivo se encuentra en C:\Archivos de programa\Microsoft SQL Server\120\Setup Bootstrap\Logs.  
  
## <a name="post-rebuild-tasks"></a>Tareas posteriores al proceso de volver a generar bases de datos  
 Después de volver a generar la base de datos, quizás deba realizar las tareas adicionales siguientes:  
  
-   Restaurar las copias de seguridad completas más recientes de las bases de datos maestra, modelo y msdb. Para obtener más información, vea [Realizar copias de seguridad y restaurar bases de datos del sistema &#40;SQL Server&#41;](../backup-restore/back-up-and-restore-of-system-databases-sql-server.md).  
  
    > [!IMPORTANT]  
    >  Si ha cambiado la intercalación del servidor, no restaure las bases de datos del sistema. Si lo hace, reemplazará la nueva intercalación por la antigua.  
  
     Si no dispone de una copia de seguridad o si la copia de seguridad restaurada no es actual, vuelva a crear las entradas que no se encuentren. Por ejemplo, vuelva a crear todas las entradas que no se encuentren de las bases de datos de usuario, los dispositivos de copia de seguridad, los inicios de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , los puntos de conexión, etc. La mejor forma de volver a crear las entradas es ejecutar los scripts originales que se usaron para crearlas.  
  
> [!IMPORTANT]  
>  Se recomienda proteger los scripts para evitar que los modifiquen personas no autorizadas.  
  
-   Si la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se configura como Distribuidor de replicación, debe restaurar la base de datos de distribución. Para obtener más información, vea [Realizar copias de seguridad y restaurar bases de datos de SQL Server](../replication/administration/back-up-and-restore-replicated-databases.md).  
  
-   Mover las bases de datos del sistema a las ubicaciones registradas anteriormente. Para obtener más información, vea [Mover bases de datos del sistema](system-databases.md).  
  
-   Comprobar que los valores de configuración de todo el servidor coinciden con los valores registrados anteriormente.  
  
##  <a name="Resource"></a> Volver a generar la base de datos de recursos  
 Con el procedimiento siguiente se vuelve a generar la base de datos de recursos. Al volver a generar la base de datos de recursos, se pierden todos los Service Pack y las revisiones y, por lo tanto, se deben volver a aplicar.  
  
#### <a name="to-rebuild-the-resource-system-database"></a>Para volver a generar la base de datos de recursos:  
  
1.  Inicie el programa de instalación de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] (setup.exe) desde los discos de distribución.  
  
2.  En el área de navegación izquierda, haga clic en **Mantenimiento**y, a continuación, en **Reparar**.  
  
3.  Las rutinas de archivo y de reglas auxiliares del programa de instalación se ejecutan para asegurarse de que el sistema tiene instalados los requisitos previos y que el equipo supera las reglas de validación del programa de instalación. Haga clic en **Aceptar** o en **Instalar** para continuar.  
  
4.  En la página Seleccionar instancia, seleccione la instancia que desea reparar y, a continuación, haga clic en **Siguiente**.  
  
5.  Las reglas de reparación se ejecutarán para validar la operación. Para continuar, haga clic en **Siguiente**.  
  
6.  En la página **Listo para reparar** , haga clic en **Reparar**. La página Operación completada indica que la operación ha finalizado.  
  
##  <a name="CreateMSDB"></a> Crear una base de datos msdb  
 Si el `msdb` base de datos está dañada y no tiene una copia de seguridad de la `msdb` base de datos, puede crear un nuevo `msdb` utilizando el **instmsdb** secuencia de comandos.  
  
> [!WARNING]  
>  Volver a generar el `msdb` base de datos mediante el **instmsdb** script eliminará toda la información almacenada en `msdb` como trabajos, alerta, operadores, los planes de mantenimiento, historial de copia de seguridad, la configuración de administración basada en directivas , Correo, etcetera, el almacenamiento de datos de rendimiento de la base de datos.  
  
1.  Detenga todos los servicios que se conectan al [!INCLUDE[ssDE](../../includes/ssde-md.md)], incluido el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , [!INCLUDE[ssRS](../../includes/ssrs.md)], [!INCLUDE[ssIS](../../includes/ssis-md.md)]y todas las aplicaciones que usan [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como almacén de datos.  
  
2.  Inicie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] desde la línea de comandos usando el comando: `NET START MSSQLSERVER /T3608`  
  
     Para más información, consulte [Iniciar, detener, pausar, reanudar y reiniciar el motor de base de datos, Agente SQL Server o el Servicio SQL Server Browser](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md).  
  
3.  En otra ventana de línea de comandos, separe el `msdb` base de datos ejecutando el comando siguiente, reemplazando  *\<servername >* con la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: `SQLCMD -E -S<servername> -dmaster -Q"EXEC sp_detach_db msdb"`  
  
4.  Con el Explorador de Windows, cambie el nombre del `msdb` los archivos de base de datos. De forma predeterminada, están en la subcarpeta DATA de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
5.  Con el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , detenga y reinicie el servicio [!INCLUDE[ssDE](../../includes/ssde-md.md)] de la forma normal.  
  
6.  En una ventana de línea de comandos, conéctese a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y ejecute el comando: `SQLCMD -E -S<servername> -i"C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Install\instmsdb.sql" -o" C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Install\instmsdb.out"`  
  
     Reemplace *\<servername>* por la instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Use la ruta de acceso al sistema de archivos de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
7.  Con el Bloc de notas de Windows, abra el archivo **instmsdb.out** y compruebe si hay errores en la salida.  
  
8.  Vuelva a aplicar todos los Service Pack y todas las revisiones instaladas en la instancia.  
  
9. Volver a crear el contenido de usuario almacenado en el `msdb` base de datos, como los trabajos, alertas, etcetera.  
  
10. Copia de seguridad el `msdb` base de datos.  
  
##  <a name="Troubleshoot"></a> Solucionar errores de recompilación  
 Los errores de sintaxis y otros errores en tiempo de ejecución se muestran en la ventana del símbolo del sistema. Examine la instrucción de instalación en busca de los siguientes errores de sintaxis:  
  
-   La barra diagonal (/) no aparece delante de los nombres de los parámetros.  
  
-   Se ha omitido el signo de igualdad (=) entre el nombre del parámetro y su valor.  
  
-   Hay espacios en blanco entre el nombre del parámetro y el signo igual.  
  
-   Presencia de comas (,) u otros caracteres que no se especifican en la sintaxis.  
  
 Cuando se haya completado el proceso de volver a generar la base de datos, examine los registros de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en busca de errores. De manera predeterminada, están en C:\Archivos de programa\Microsoft SQL Server\120\Setup Bootstrap\Logs. Para encontrar el archivo de registro que contiene los resultados del proceso de volver a generar bases de datos, cambie el directorio a la carpeta Logs en un símbolo del sistema y, a continuación, ejecute `findstr /s RebuildDatabase summary*.*`. Esta búsqueda indicará los archivos de registro que contengan los resultados del proceso de volver a generar las bases de datos del sistema. Abra los archivos de registro y examine si contienen mensajes de error relevantes.  
  
## <a name="see-also"></a>Vea también  
 [Bases de datos del sistema](system-databases.md)  
  
  
