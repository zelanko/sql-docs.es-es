---
title: Adjuntar una base de datos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql12.swb.attachdatabase.f1
helpviewer_keywords:
- database attaching [SQL Server]
- attaching databases [SQL Server]
ms.assetid: b4efb0ae-cfe6-4d81-a4b4-6e4916885caa
author: stevestein
ms.author: sstein
ms.openlocfilehash: cb11b5c257007872e92d3f0a7eadb3e46b4969cd
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84952255"
---
# <a name="attach-a-database"></a>Adjuntar una base de datos
  En este tema se describe cómo adjuntar una base de datos en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Puede usar esta característica para copiar, mover o actualizar una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Requisitos previos](#Prerequisites)  
  
     [Recomendaciones](#Recommendations)  
  
     [Seguridad](#Security)  
  
-   **Para adjuntar una base de datos, use:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Seguimiento:**  [Después de actualizar una base de datos](#FollowUp)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> Requisitos previos  
  
-   La base de datos se debe separar primero. Si intenta adjuntar una base de datos que no se ha separado, se devolverá un error. Para obtener más información, vea [Separar una base de datos](detach-a-database.md)  
  
-   Al adjuntar una base de datos, todos los archivos de datos deben estar disponibles (archivos MDF y LDF). Si algún archivo de datos tiene una ruta de acceso diferente a la que tenía cuando se creó la base de datos o cuando ésta se adjuntó por última vez, debe especificar la ruta actual.  
  
-   Cuando se adjunta una base de datos, si los archivos MDF y LDF se encuentran en directorios diferentes y una de las rutas de acceso incluye \\\\?\GlobalRoot, se producirá un error en la operación.  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> Recomendaciones  
Se recomienda que mueva las bases de datos mediante el `ALTER DATABASE` procedimiento de reubicación planeada, en lugar de usar separar y adjuntar. Para más información, consulte [Move User Databases](move-user-databases.md).  
  
###  <a name="security"></a><a name="Security"></a> Seguridad  
Los permisos de acceso a archivos se establecen durante una serie de operaciones de base de datos, incluidas las operaciones de desasociar o adjuntar una base de datos. Para obtener información sobre los permisos de archivo que se establecen siempre que se separa y se adjunta una base de datos, vea [Proteger archivos de datos y de registro](https://technet.microsoft.com/library/ms189128.aspx) en los Libros en pantalla de [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] .  
  
Se recomienda no adjuntar ni restaurar bases de datos de orígenes desconocidos o que no sean de confianza. Es posible que dichas bases de datos contengan código malintencionado que podría ejecutar código [!INCLUDE[tsql](../../includes/tsql-md.md)] no deseado o provocar errores al modificar el esquema o la estructura de la base de datos física. Para usar una base de datos desde un origen desconocido o que no sea de confianza, ejecute [DBCC CHECKDB](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql) en la base de datos de un servidor que no sea de producción y examine también el código, como procedimientos almacenados u otro código definido por el usuario, en la base de datos. Para obtener más información sobre cómo adjuntar bases de datos y sobre los cambios que se realizan en los metadatos al adjuntar una base de datos, vea [Adjuntar y separar bases de datos &#40;SQL Server&#41;](database-detach-and-attach-sql-server.md).  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permisos  
Requiere el permiso `CREATE DATABASE`, `CREATE ANY DATABASE` o `ALTER ANY DATABASE`.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Uso de SQL Server Management Studio  
  
### <a name="to-attach-a-database"></a>Para adjuntar una base de datos  
  
1.  En el Explorador de objetos de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , conéctese a una instancia del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]y, después, expándala.  
  
2.  Haga clic con el botón derecho en **Bases de datos** y haga clic en **Adjuntar**.  
  
3.  En el cuadro de diálogo **Adjuntar bases de datos** , haga clic en **Agregar**para especificar la base de datos que se va a adjuntar y en el cuadro de diálogo **Buscar archivos de base de datos** , seleccione la unidad de disco en la que se halla la base de datos y expanda el árbol de directorios para buscar y seleccionar el archivo .mdf de la base de datos; por ejemplo:  
  
     `C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA\AdventureWorks2012_Data.mdf`  
  
    > [!IMPORTANT]  
    > Si intenta seleccionar una base de datos que ya ha sido adjuntada se producirá un error.  
  
     **Bases de datos que se van a adjuntar**  
     Muestra información sobre las bases de datos seleccionadas.  
  
     \<no column header>  
     Muestra un icono que indica el estado de la operación de adjuntar. Los iconos posibles se indican en la descripción de **Estado** , que encontrará más adelante.  
  
     **Ubicación del archivo MDF**  
     Muestra la ruta de acceso y el nombre del archivo MDF seleccionado.  
  
     **Nombre de la base de datos**  
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
    |Marca de verificación verde|Correcto|El objeto se ha adjuntado correctamente.|  
    |Círculo rojo con una cruz blanca|Error|La operación de adjuntar ha detectado un error y no ha finalizado correctamente.|  
    |Círculo con dos cuadrantes negros (a la izquierda y la derecha) y dos cuadrantes blancos (en la parte superior e inferior)|Detenido|La operación de adjuntar no ha finalizado correctamente porque el usuario la ha detenido.|  
    |Círculo con una flecha curvada que apunta hacia la izquierda|Revertido|La operación de adjuntar se ha ejecutado correctamente, pero se ha revertido debido a un error al adjuntar otro objeto.|  
  
     **Mensaje**  
     Muestra un mensaje en blanco o un hipervínculo que indica "Archivo no encontrado".  
  
     **Add (Agregar)**  
     Busca los archivos de base de datos principales necesarios. Si el usuario selecciona un archivo .mdf, la información pertinente se llena automáticamente en los respectivos campos de la cuadrícula **Bases de datos que se van a adjuntar** .  
  
     **Remove**  
     Quita el archivo seleccionado de la cuadrícula **Bases de datos que se van a adjuntar** .  
  
     **"** *<database_name>* **" detalles de la base de datos**  
     Muestra los nombres de los archivos que se van a adjuntar. Para comprobar o cambiar el nombre de la ruta de acceso de un archivo, haga clic en el botón **Examinar** ( **...** ).  
  
    > [!NOTE]  
    > Si un archivo no existe, la columna **Mensaje** muestra "No se encontró". Si un archivo de registro no se encuentra, indica que se halla en otro directorio o que se ha eliminado. En tal caso, debe actualizar la ruta de acceso del archivo en la cuadrícula **Detalles de la base de datos** para que señale la ubicación correcta o eliminar el archivo de registro de la cuadrícula. Si un archivo de datos .ndf no se encuentra, debe actualizar su ruta de acceso en la cuadrícula para que señale la ubicación correcta.  
  
     **Nombre del archivo original**  
     Muestra el nombre del archivo adjunto que pertenece a la base de datos.  
  
     **Tipo de archivo**  
     Indica el tipo de archivo, que puede ser de **datos** o de **registro**.  
  
     **Ruta de acceso del archivo actual**  
     Muestra la ruta de acceso del archivo de base de datos seleccionado. La ruta de acceso puede modificarse manualmente.  
  
     **Mensaje**  
     Muestra un mensaje en blanco o un hipervínculo que indica "**Archivo no encontrado**".  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usar Transact-SQL  
  
### <a name="to-attach-a-database"></a>Para adjuntar una base de datos  
  
1.  Conéctese con el [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra Estándar, haga clic en **Nueva consulta**.  
  
3.  Use la instrucción [Create Database](/sql/t-sql/statements/create-database-sql-server-transact-sql) con el `FOR ATTACH` cierre.  
  
     Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**. En este ejemplo se adjuntan los archivos de la base de datos [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] y se cambia el nombre de la base de datos a `MyAdventureWorks`.  
  
    ```sql  
    CREATE DATABASE MyAdventureWorks   
        ON (FILENAME = 'C:\MySQLServer\AdventureWorks_Data.mdf'),   
        (FILENAME = 'C:\MySQLServer\AdventureWorks_Log.ldf')   
        FOR ATTACH;  
    ```  
  
    > [!NOTE]  
    > También puede usar los procedimientos almacenados [sp_attach_db](/sql/relational-databases/system-stored-procedures/sp-attach-db-transact-sql) o [sp_attach_single_file_db](/sql/relational-databases/system-stored-procedures/sp-attach-single-file-db-transact-sql) . Sin embargo, estos procedimientos almacenados se quitarán en una versión futura de Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Se recomienda usar CREATE DATABASE... PARA ATTACH en su lugar.  
  
##  <a name="follow-up-after-upgrading-a-sql-server-database"></a><a name="FollowUp"></a> Seguimiento: Después de actualizar una base de datos de SQL Server  
 spués actualiza una base de datos mediante el método attach, la base de datos está disponible inmediatamente y se actualiza automáticamente. Si la base de datos tiene índices de texto completo, el proceso de actualización los importa, los restablece o los vuelve a generar, en función del valor de la propiedad del servidor **Opción de actualización de texto completo** . Si la opción de actualización se establece en **Importar** o en **Volver a generar**, los índices de texto completo no estarán disponibles durante la actualización. Dependiendo de la cantidad de datos que se indicen, la importación puede requerir varias horas y volver a generar puede requerir hasta diez veces más. Tenga en cuenta también que si la opción de actualización se establece en **Importar**y no hay disponible ningún catálogo de texto completo, se vuelven a generar los índices de texto completo asociados.  
  
Si el nivel de compatibilidad de una base de datos de usuario es 100 o superior antes de la actualización, permanece igual después de la misma. Si el nivel de compatibilidad es 90 antes de la actualización, en la base de datos actualizada, el nivel de compatibilidad se establece en 100, que es el nivel de compatibilidad mínimo admitido en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Para obtener más información, vea [Nivel de compatibilidad de ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level).  
  
## <a name="see-also"></a>Consulte también  
 [CREATE DATABASE &#40;Transact-SQL de SQL Server&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql)   
 [Separar una base de datos](detach-a-database.md)  
  
  
