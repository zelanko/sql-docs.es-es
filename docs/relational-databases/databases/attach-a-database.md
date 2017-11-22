---
title: Adjuntar una base de datos | Microsoft Docs
ms.custom: 
ms.date: 10/24/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: databases
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.swb.attachdatabase.f1
helpviewer_keywords:
- database attaching [SQL Server]
- attaching databases [SQL Server]
ms.assetid: b4efb0ae-cfe6-4d81-a4b4-6e4916885caa
caps.latest.revision: "52"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 3abcab5e233c45e1fda0bf5fb53499ac9ca21732
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="attach-a-database"></a>Adjuntar una base de datos
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  En este tema se describe cómo adjuntar una base de datos en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Puede usar esta característica para copiar, mover o actualizar una base de datos de SQL Server.  
  
 
  
##  <a name="Prerequisites"></a> Requisitos previos  
  
-   La base de datos se debe separar primero. Si intenta adjuntar una base de datos que no se ha separado, se devolverá un error. Para obtener más información, vea [Separar una base de datos](../../relational-databases/databases/detach-a-database.md)  
  
-   Al adjuntar una base de datos, todos los archivos de datos deben estar disponibles (archivos MDF y LDF). Si algún archivo de datos tiene una ruta de acceso diferente a la que tenía cuando se creó la base de datos o cuando ésta se adjuntó por última vez, debe especificar la ruta actual.  
  
-   Cuando se adjunta una base de datos, si los archivos MDF y LDF se encuentran en directorios diferentes y una de las rutas de acceso incluye \\\\?\GlobalRoot, se producirá un error en la operación.  
  
###  <a name="Recommendations"></a> ¿Adjuntar es la mejor opción?  
 Se recomienda mover las bases de datos mediante el procedimiento de reubicación programada ALTER DATABASE, en lugar del método de separar y adjuntar, al mover archivos de bases de datos dentro de la misma instancia. Para más información, consulte [Move User Databases](../../relational-databases/databases/move-user-databases.md). 
 
No se recomienda usar separar y adjuntar para el proceso de copia de seguridad y recuperación. No hay copias de seguridad del registro de transacciones, y se pueden eliminar accidentalmente los archivos.
  
###  <a name="Security"></a> Seguridad  
 Los permisos de acceso a archivos se establecen durante una serie de operaciones de base de datos, incluidas las operaciones de desasociar o adjuntar una base de datos. Para obtener información sobre los permisos de archivo que se establecen siempre que se separa y se adjunta una base de datos, vea [Proteger archivos de datos y de registro](http://technet.microsoft.com/library/ms189128.aspx) en los Libros en pantalla de [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] (sigue siendo una lectura válida). 
  
 Se recomienda no adjuntar ni restaurar bases de datos de orígenes desconocidos o que no sean de confianza. Es posible que dichas bases de datos contengan código malintencionado que podría ejecutar código [!INCLUDE[tsql](../../includes/tsql-md.md)] no deseado o provocar errores al modificar el esquema o la estructura de la base de datos física. Para usar una base de datos desde un origen desconocido o que no sea de confianza, ejecute [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) en la base de datos de un servidor que no sea de producción y examine también el código, como procedimientos almacenados u otro código definido por el usuario, en la base de datos. Para obtener más información sobre cómo adjuntar bases de datos y sobre los cambios que se realizan en los metadatos al adjuntar una base de datos, vea [Adjuntar y separar bases de datos (SQL Server)](../../relational-databases/databases/database-detach-and-attach-sql-server.md).  
  
####  <a name="Permissions"></a> Permissions  
 Requiere el permiso CREATE DATABASE, CREATE ANY DATABASE o ALTER ANY DATABASE.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-attach-a-database"></a>Para adjuntar una base de datos  
  
1.  En el Explorador de objetos de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , conéctese a una instancia de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]y, después, haga clic para expandir esa vista de instancia en SSMS.  
  
2.  Haga clic con el botón derecho en **Bases de datos** y haga clic en **Adjuntar**.  
  
3.  En el cuadro de diálogo **Adjuntar bases de datos** , haga clic en **Agregar**para especificar la base de datos que se va a adjuntar y en el cuadro de diálogo **Buscar archivos de base de datos** , seleccione la unidad de disco en la que se halla la base de datos y expanda el árbol de directorios para buscar y seleccionar el archivo .mdf de la base de datos; por ejemplo:  
  
     `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\AdventureWorks2012_Data.mdf`  
  
    > [!IMPORTANT]  
    >  Si intenta seleccionar una base de datos que ya ha sido adjuntada se producirá un error.  
  
     **Bases de datos que se van a adjuntar**  
     Muestra información sobre las bases de datos seleccionadas.  
  
     \<no column header>  
     Muestra un icono que indica el estado de la operación de adjuntar. Los iconos posibles se indican en la descripción de **Estado** , que encontrará más adelante.  
  
     **Ubicación del archivo MDF**  
     Muestra la ruta de acceso y el nombre del archivo MDF seleccionado.  
  
     **Database Name**  
     Muestra el nombre de la base de datos.  
  
     **Adjuntar como**  
     Opcionalmente, especifica un nombre distinto con el que se debe adjuntar la base de datos.  
  
     **Propietario**  
     Ofrece una lista desplegable de los posibles propietarios de base de datos desde los que opcionalmente puede seleccionarse otro propietario.  
  
     **Estado**  
     Muestra el estado de la base de datos de acuerdo con la tabla siguiente.  
  
    |Icono|Texto de estado|Descripción|  
    |----------|-----------------|-----------------|  
    |(Sin icono)|(Sin texto)|La operación de adjuntar no se ha iniciado o puede estar pendiente para este objeto. Es la opción predeterminada al abrir el diálogo.|  
    |Triángulo verde hacia la derecha|En curso|La operación de adjuntar se ha iniciado, pero no ha finalizado.|  
    |Marca de verificación verde|Success|El objeto se ha adjuntado correctamente.|  
    |Círculo rojo con una cruz blanca|Error|La operación de adjuntar ha detectado un error y no ha finalizado correctamente.|  
    |Círculo con dos cuadrantes negros (a la izquierda y la derecha) y dos cuadrantes blancos (en la parte superior e inferior)|Detenido|La operación de adjuntar no ha finalizado correctamente porque el usuario la ha detenido.|  
    |Círculo con una flecha curvada que apunta hacia la izquierda|Revertido|La operación de adjuntar se ha ejecutado correctamente, pero se ha revertido debido a un error al adjuntar otro objeto.|  
  
     **de mensaje**  
     Muestra un mensaje en blanco o un hipervínculo que indica "Archivo no encontrado".  
  
     **Agregar**  
     Busca los archivos de base de datos principales necesarios. Si el usuario selecciona un archivo .mdf, la información pertinente se llena automáticamente en los respectivos campos de la cuadrícula **Bases de datos que se van a adjuntar** .  
  
     **Quitar**  
     Quita el archivo seleccionado de la cuadrícula **Bases de datos que se van a adjuntar** .  
  
     **"** *<database_name>* **" detalles de la base de datos**  
     Muestra los nombres de los archivos que se van a adjuntar. Para comprobar o cambiar el nombre de la ruta de acceso de un archivo, haga clic en el botón **Examinar** (**…**).  
  
    > [!NOTE]  
    >  Si un archivo no existe, la columna **Mensaje** muestra "No se encontró". Si un archivo de registro no se encuentra, indica que se halla en otro directorio o que se ha eliminado. En tal caso, debe actualizar la ruta de acceso del archivo en la cuadrícula **Detalles de la base de datos** para que señale la ubicación correcta o eliminar el archivo de registro de la cuadrícula. Si un archivo de datos .ndf no se encuentra, debe actualizar su ruta de acceso en la cuadrícula para que señale la ubicación correcta.  
  
     **Nombre del archivo original**  
     Muestra el nombre del archivo adjunto que pertenece a la base de datos.  
  
     **Tipo de archivo**  
     Indica el tipo de archivo, que puede ser de **datos** o de **registro**.  
  
     **Ruta de acceso del archivo actual**  
     Muestra la ruta de acceso del archivo de base de datos seleccionado. La ruta de acceso puede modificarse manualmente.  
  
     **de mensaje**  
     Muestra un mensaje en blanco o un hipervínculo que indica "**Archivo no encontrado**".  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-attach-a-database"></a>Para adjuntar una base de datos  
  
1.  Conéctese al [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Desde la barra Estándar, haga clic en **Nueva consulta**.  
  
3.  Use la instrucción [CREATE DATABASE](../../t-sql/statements/create-database-sql-server-transact-sql.md) con la cláusula FOR ATTACH.  
  
     Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**. En este ejemplo se adjuntan los archivos de la base de datos [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] y se cambia el nombre de la base de datos a `MyAdventureWorks`.  
  
    ```  
    CREATE DATABASE MyAdventureWorks   
        ON (FILENAME = 'C:\MySQLServer\AdventureWorks_Data.mdf'),   
        (FILENAME = 'C:\MySQLServer\AdventureWorks_Log.ldf')   
        FOR ATTACH;  
  
    ```  
  
    > [!NOTE]  
    >  También puede usar los procedimientos almacenados [sp_attach_db](../../relational-databases/system-stored-procedures/sp-attach-db-transact-sql.md) o [sp_attach_single_file_db](../../relational-databases/system-stored-procedures/sp-attach-single-file-db-transact-sql.md) . Sin embargo, estos procedimientos almacenados se quitarán en una versión futura de Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, se recomienda usar CREATE DATABASE … FOR ATTACH en lugar.  
  
##  <a name="FollowUp"></a> Seguimiento: Después de actualizar una base de datos de SQL Server  
 Después de actualizar una base de datos mediante el método de adjuntarla, la base de datos queda disponible inmediatamente y se actualiza automáticamente. Si la base de datos tiene índices de texto completo, el proceso de actualización los importa, los restablece o los vuelve a generar, en función del valor de la propiedad del servidor **Opción de actualización de texto completo** . Si la opción de actualización se establece en **Importar** o en **Volver a generar**, los índices de texto completo no estarán disponibles durante la actualización. Dependiendo de la cantidad de datos que se indicen, la importación puede requerir varias horas y volver a generar puede requerir hasta diez veces más. Tenga en cuenta también que si la opción de actualización se establece en **Importar**y no hay disponible ningún catálogo de texto completo, se vuelven a generar los índices de texto completo asociados.  
  
 Si el nivel de compatibilidad de una base de datos de usuario es 100 o superior antes de la actualización, permanece igual después de la misma. Si el nivel de compatibilidad es 90 antes de la actualización, en la base de datos actualizada, el nivel de compatibilidad se establece en 100, que es el nivel de compatibilidad mínimo admitido en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Para obtener más información, vea [Nivel de compatibilidad de ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md).  
  
  > [!NOTE]
  > Si va a adjuntar una base de datos de una instancia que ejecuta SQL Server 2014 o versiones anteriores que tenían una captura de datos de cambios (CDC) habilitada, también necesitará ejecutar el comando siguiente para actualizar los metadatos de captura de datos de cambios (CDC).
  ```
  USE <database name>
  EXEC sys.sp_cdc_vupgrade  
  ``` 
  
## <a name="see-also"></a>Vea también  
 [CREATE DATABASE &#40;Transact-SQL de SQL Server&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [Separar una base de datos](../../relational-databases/databases/detach-a-database.md)  
  
  
