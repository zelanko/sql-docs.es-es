---
title: Realizar copias de seguridad de archivos y grupos de archivos (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- backing up filegroups [SQL Server]
- file backups [SQL Server], how-to topics
- backing up files [SQL Server]
- backups [SQL Server], creating
- filegroups [SQL Server], backing up
ms.assetid: a0d3a567-7d8b-4cfe-a505-d197b9a51f70
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: c686e5eb9bb44517aa1636dc28c972f6782f8bfe
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "72782746"
---
# <a name="back-up-files-and-filegroups-sql-server"></a>Realizar copias de seguridad de archivos y grupos de archivos (SQL Server)
  En este tema se describe cómo realizar copias de seguridad de archivos y grupos de archivos en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)]o PowerShell. Cuando el tamaño y los requisitos de rendimiento de la base de datos hagan que no sea práctico realizar una copia de seguridad completa de la base de datos, puede crear una copia de seguridad de archivo en su lugar. Una *copia de seguridad de archivos* contiene todos los datos de uno o varios archivos (o grupos de archivos). Para obtener más información sobre las copias de seguridad de archivos, vea [Copias de seguridad de archivos completas &#40;SQL Server&#41;](full-file-backups-sql-server.md) y [Copias de seguridad diferenciales &#40;SQL Server&#41;](differential-backups-sql-server.md).  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Recomendaciones](#Recommendations)  
  
     [Seguridad](#Security)  
  
-   **Para realizar copias de seguridad de archivos y grupos de archivos, utilizando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   La instrucción BACKUP no se permite en una transacción explícita o implícita.  
  
-   En el modelo de recuperación simple, se debe hacer una copia de seguridad de todos los archivos de lectura/escritura juntos. Esto ayuda a garantizar que la base de datos se pueda restaurar a un punto temporal coherente. En lugar de especificar de forma individual cada grupo de archivos o cada archivo de lectura/escritura utilice la opción READ_WRITE_FILEGROUPS. Esta opción realiza una copia de seguridad de todos los grupos de archivos de lectura/escritura de la base de datos. Una copia de seguridad que se crea al especificar READ_WRITE_FILEGROUPS se conoce como *copia de seguridad parcial*. Para obtener más información, vea [Copias de seguridad parciales &#40;SQL Server&#41;](partial-backups-sql-server.md).  
  
-   Para obtener más información sobre las limitaciones y restricciones, vea [ Información general de copia de seguridad &#40;SQL Server&#41;](backup-overview-sql-server.md).  
  
###  <a name="Recommendations"></a> Recomendaciones  
  
-   De forma predeterminada, cada operación de copia de seguridad correcta agrega una entrada en el registro de errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y en el registro de eventos del sistema. Si se hace una copia de seguridad del registro de transacciones con frecuencia, estos mensajes que indican la corrección de la operación pueden acumularse rápidamente, con lo que se crean registros de errores muy grandes que pueden dificultar la búsqueda de otros mensajes. En esos casos, puede suprimir estas entradas de registro utilizando la marca de seguimiento 3226 si ninguno de los scripts depende de esas entradas. Para obtener más información, vea [Marcas de seguimiento &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql).  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 De forma predeterminada, los permisos BACKUP DATABASE y BACKUP LOG corresponden a los miembros del rol fijo de servidor **sysadmin** y de los roles fijos de base de datos **db_owner** y **db_backupoperator** .  
  
 Los problemas de propiedad y permisos del archivo físico del dispositivo de copia de seguridad pueden interferir con una operación de copia de seguridad. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe poder leer y escribir en el dispositivo y la cuenta en la que se ejecuta el servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe tener permisos de escritura. En cambio, [sp_addumpdevice](/sql/relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql), que agrega una entrada para un dispositivo de copia de seguridad en las tablas del sistema, no comprueba los permisos de acceso a los archivos. Es posible que estos problemas con el archivo físico del dispositivo de copia de seguridad no aparezcan hasta que se tenga acceso al recurso físico, al intentar la copia de seguridad o la restauración.  
  
##  <a name="SSMSProcedure"></a> Uso de SQL Server Management Studio  
  
#### <a name="to-back-up-database-files-and-filegroups"></a>Para realizar copias de seguridad de archivos y grupos de archivos de la base de datos  
  
1.  Después de conectarse a la instancia apropiada de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], en el Explorador de objetos, haga clic en el nombre del servidor para expandir el árbol de servidores.  
  
2.  Expanda **Bases de datos**y, en función de la base de datos, seleccione la base de datos de un usuario o expanda **Bases de datos del sistema** y seleccione una base de datos del sistema.  
  
3.  Haga clic con el botón derecho en la base de datos, seleccione **Tareas**y haga clic en **Copia de seguridad**. Aparece el cuadro de diálogo **Copia de seguridad de base de datos** .  
  
4.  En la lista **Base de datos**, compruebe el nombre de la base de datos. También puede seleccionar otra base de datos en la lista.  
  
5.  En la lista **Tipo de copia de seguridad**, seleccione **Completa** o **Diferencial**.  
  
6.  En la opción **Componente de copia de seguridad**, haga clic en **Archivo y grupos de archivos**.  
  
7.  En el cuadro de diálogo **Seleccionar archivos y grupos de archivos** , seleccione los archivos y los grupos de archivos cuya copia de seguridad desee realizar. Puede seleccionar uno o varios archivos, o bien activar la casilla de un grupo de archivos para seleccionar automáticamente todos los archivos de dicho grupo.  
  
8.  Acepte el nombre del conjunto de copia de seguridad predeterminado sugerido en el cuadro de texto **Nombre** o escriba un nombre diferente para el conjunto de copia de seguridad.  
  
9. Opcionalmente, en el cuadro de texto **Descripción**, escriba una descripción del conjunto de copia de seguridad.  
  
10. Especifique cuándo expirará el conjunto de copia de seguridad:  
  
    -   Para hacer que el conjunto de copia de seguridad expire después de un número concreto de días, haga clic en **Después de** (opción predeterminada). A continuación, escriba el número de días que deben transcurrir después de la creación del conjunto para que éste expire. Este valor puede estar entre 0 y 99999 días; el valor 0 significa que el conjunto de copia de seguridad no expirará nunca.  
  
         El valor predeterminado se establece en la opción **Tiempo predeterminado de retención de medios de copia de seguridad (días)** del cuadro de diálogo **Propiedades del servidor** (página**Configuración de base de datos** ). Para tener acceso a esta opción, haga clic con el botón derecho en el nombre del servidor en el Explorador de objetos y seleccione Propiedades y, luego, seleccione la página **Configuración de base de datos** .  
  
    -   Para que el conjunto de copia de seguridad expire en una determinada fecha, haga clic en **El**y escriba la fecha en la que expirará.  
  
11. Elija el tipo de destino de la copia de seguridad haciendo clic en **Disco** o **Cinta**. Para seleccionar las rutas de hasta 64 unidades de disco o de cinta que contengan un solo conjunto de medios, haga clic en **Agregar**. Las rutas seleccionadas se muestran en la lista **Copia de seguridad en**.  
  
    > [!NOTE]  
    >  Para eliminar un destino de copia de seguridad, selecciónelo y haga clic en **Quitar**. Para ver el contenido de un destino de copia de seguridad, selecciónelo y haga clic en **Contenido**.  
  
12. Para ver o seleccionar las opciones avanzadas, haga clic en **Opciones** en el panel **Seleccionar una página**.  
  
13. Seleccione una opción de **Sobrescribir medios** haciendo clic en una de las siguientes:  
  
    -   **Hacer copia de seguridad en el conjunto de medios existente**  
  
         Para esta opción, haga clic en **Anexar al conjunto de copia de seguridad existente** o **Sobrescribir todos los conjuntos de copia de seguridad existentes**. Para obtener más información sobre cómo hacer copias de seguridad de los conjuntos de medios existentes, vea [Conjuntos de medios, familias de medios y conjuntos de copias de seguridad &#40;SQL Server&#41;](media-sets-media-families-and-backup-sets-sql-server.md).  
  
         Opcionalmente, seleccione **Comprobar nombre de conjunto de medios y fecha de expiración del conjunto de copia de seguridad** para que la operación de copia de seguridad compruebe la fecha y la hora en que expiran el conjunto de medios y el conjunto de copia de seguridad.  
  
         También puede escribir un nombre en el cuadro de texto **Nombre del conjunto de medios** . Si no especifica ningún nombre, se creará un conjunto de medios con un nombre en blanco. Si especifica un nombre para el conjunto, se comprueban los medios (cinta o disco) para ver si el nombre real coincide con el nombre especificado aquí.  
  
         Si deja el nombre del conjunto de medios en blanco y selecciona la casilla para comprobarlo con los medios, el resultado correcto significará que el nombre del conjunto en los medios también está en blanco.  
  
    -   **Hacer una copia de seguridad en un nuevo conjunto de medios y borrar todos los conjuntos de copia de seguridad existentes**  
  
         Para esta opción, escriba un nombre en el cuadro de texto **Nuevo nombre del conjunto de medios** y, opcionalmente, describa el conjunto de medios en el cuadro de texto **Nueva descripción del conjunto de medios**. Para obtener más información sobre cómo crear un conjunto de medios, vea [Conjuntos de medios, familias de medios y conjuntos de copias de seguridad &#40;SQL Server&#41;](media-sets-media-families-and-backup-sets-sql-server.md).  
  
14. Opcionalmente, en la sección **Confiabilidad** , seleccione:  
  
    -   **Comprobar copia de seguridad al finalizar**.  
  
    -   **Realice una suma de comprobación antes de escribir en los medios**y, opcionalmente, **continúe con el error de suma de comprobación**. Para obtener más información sobre las sumas de comprobación, vea [Errores posibles de medios durante copia de seguridad y restauración &#40;SQL Server&#41;](possible-media-errors-during-backup-and-restore-sql-server.md).  
  
15. Si va a realizar copias de seguridad en una unidad de cinta (según se haya especificado en la sección **Destino** de la página **General**), la opción **Descargar la cinta después de realizar la copia de seguridad** está activa. Al hacer clic en esta opción, se habilita la opción **Rebobinar la cinta antes de descargar** .  
  
    > [!NOTE]  
    >  Las opciones de la sección **Registro de transacciones** se encuentran inactivas salvo que vaya a realizar una copia de seguridad de un registro de transacciones (según se haya especificado en la sección **Tipo de copia de seguridad** de la página **General**).  
  
16. [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)]y versiones posteriores admiten la [compresión de copia de seguridad](backup-compression-sql-server.md). De manera predeterminada, el hecho de que se comprima una copia de seguridad depende de la opción de configuración que tenga el servidor para el **valor predeterminado de la compresión de la copia de seguridad**. Sin embargo, independientemente del nivel predeterminado del servidor actual, puede comprimir una copia de seguridad activando **Comprimir copia de seguridad** y puede evitar la compresión activando **No comprimir copia de seguridad**.  
  
     **Para ver el valor predeterminado de la compresión de copia de seguridad actual**  
  
    -   [Ver o establecer la opción de configuración del servidor de compresión de copia de seguridad predeterminada](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md)  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-back-up-files-and-filegroups"></a>Para realizar copias de seguridad de archivos y grupos de archivos  
  
1.  Para crear una copia de seguridad de archivos o de un grupo de archivos, use una instrucción [BACKUP DATABASE <file_or_filegroup>](/sql/t-sql/statements/backup-transact-sql). Como mínimo, esta instrucción debe especificar:  
  
    -   Nombre de la base de datos.  
  
    -   Una cláusula FILE o FILEGROUP para cada archivo o grupo de archivos, respectivamente.  
  
    -   El dispositivo de copia de seguridad en el que se escribirá la copia de seguridad completa.  
  
     La sintaxis [!INCLUDE[tsql](../../includes/tsql-md.md)] básica para una copia de seguridad de archivos es:  
  
     BACKUP DATABASE *database*  
  
     {FILE **=** _logical_file_name_ | **=** _Logical_filegroup_name_ **de grupo de**archivos} [,... *f* ]  
  
     TO *backup_device* [ **,**...*n* ]  
  
     [ WITH *with_options* [ **,**...*o* ] ] ;  
  
    |Opción|Descripción|  
    |------------|-----------------|  
    |*base*|Es la base de datos para la que se realiza la copia de seguridad del registro de transacciones, de una parte de la base de datos o de la base de datos completa.|  
    |**=** _Logical_file_name_ de archivo|Especifica el nombre lógico de un archivo que se debe incluir en la copia de seguridad de archivos.|  
    |**=** _Logical_filegroup_name_ de grupo de archivos|Especifica el nombre lógico de un grupo de archivos que se debe incluir en la copia de seguridad de archivos. En el modelo de recuperación simple, se permite la copia de seguridad de un grupo de archivos solo si se trata de un grupo de archivos de solo lectura.|  
    |[ **,**...*f* ]|Se trata de un marcador de posición que indica que se pueden especificar varios archivos y grupos de archivos. El número de archivos o grupos de archivos es ilimitado.|  
    |*backup_device* [ **,**... *n* ]|Especifica una lista de 1 a 64 dispositivos de copia de seguridad que se pueden utilizar en la operación de copia de seguridad. Puede especificar un dispositivo físico de copia de seguridad o puede especificar un dispositivo de copia de seguridad lógico correspondiente, si ya se definió. Para especificar un dispositivo de copia de seguridad físico, use la opción DISK o TAPE:<br /><br /> {DISK &#124; TAPE} **=** _physical_backup_device_name_<br /><br /> Para obtener más información, vea [Dispositivos de copia de seguridad &#40;SQL Server&#41;](backup-devices-sql-server.md).|  
    |WITH *with_options* [ **,**...*o* ]|Opcionalmente, especifica una o más opciones, como DIFFERENTIAL.<br /><br /> Nota: Una copia de seguridad diferencial de archivos necesita una copia de seguridad completa de archivos como base. Para obtener más información, vea [Crear una copia de seguridad diferencial de base de datos &#40;SQL Server&#41;](create-a-differential-database-backup-sql-server.md).|  
  
2.  Con el modelo de recuperación completa, también debe realizar copias de seguridad del registro de transacciones. Para utilizar un conjunto completo de copias de seguridad de completas archivos para restaurar una base de datos, también debe tener suficientes copias de seguridad de registros que abarquen todas las copias de seguridad de archivos, desde el principio de la primera copia de seguridad de archivos. Para obtener más información, vea [Realizar copia de seguridad de un registro de transacciones &#40;SQL Server&#41;](back-up-a-transaction-log-sql-server.md)).  
  
###  <a name="TsqlExample"></a> Ejemplos (Transact-SQL)  
 Los siguientes ejemplos realizan copias de seguridad de uno o más archivos de los grupos de archivos secundarios de la base de datos `Sales` . Esta base de datos utiliza el modelo de recuperación completa y contiene los siguientes grupos de archivos secundarios:  
  
-   Un grupo de archivos denominado `SalesGroup1` , con los archivos `SGrp1Fi1` y `SGrp1Fi2`.  
  
-   Un grupo de archivos denominado `SalesGroup2` , con los archivos `SGrp2Fi1` y `SGrp2Fi2`.  
  
#### <a name="a-creating-a-file-backup-of-two-files"></a>A. Crear una copia de seguridad de archivos de dos archivos  
 En el siguiente ejemplo se crea una copia de seguridad diferencial de archivos solo del archivo `SGrp1Fi2` de `SalesGroup1` y del archivo `SGrp2Fi2` del grupo de archivos `SalesGroup2` .  
  
```sql  
--Backup the files in the SalesGroup1 secondary filegroup.  
BACKUP DATABASE Sales  
   FILE = 'SGrp1Fi2',   
   FILE = 'SGrp2Fi2'   
   TO DISK = 'G:\SQL Server Backups\Sales\SalesGroup1.bck';  
GO  
```  
  
#### <a name="b-creating-a-full-file-backup-of-the-secondary-filegroups"></a>B. Crear una copia de seguridad de archivos completa de los grupos de archivos secundarios  
 En el ejemplo siguiente se crea una copia de seguridad de archivos completa de cada archivo en los dos grupos de archivos secundarios.  
  
```sql  
--Back up the files in SalesGroup1.  
BACKUP DATABASE Sales  
   FILEGROUP = 'SalesGroup1',  
   FILEGROUP = 'SalesGroup2'  
   TO DISK = 'C:\MySQLServer\Backups\Sales\SalesFiles.bck';  
GO  
```  
  
#### <a name="c-creating-a-differential-file-backup-of-the-secondary-filegroups"></a>C. Crear una copia de seguridad de archivos diferencial de los grupos de archivos secundarios  
 En el ejemplo siguiente se crea una copia de seguridad de archivos diferencial de cada archivo en los dos grupos de archivos secundarios.  
  
```sql  
--Back up the files in SalesGroup1.  
BACKUP DATABASE Sales  
   FILEGROUP = 'SalesGroup1',  
   FILEGROUP = 'SalesGroup2'  
   TO DISK = 'C:\MySQLServer\Backups\Sales\SalesFiles.bck'  
   WITH   
      DIFFERENTIAL;  
GO  
```  
  
##  <a name="PowerShellProcedure"></a> Usar PowerShell  
  
Utilice el cmdlet `Backup-SqlDatabase` y especifique `Files` como el valor del parámetro `-BackupAction`. Especifique también uno de los parámetros siguientes:  
  
    -   Para realizar una copia de seguridad de un archivo `-DatabaseFile`específico, especifique el parámetro de *cadena* , donde *cadena* es uno o varios archivos de base de datos de los que se va a hacer una copia de seguridad.  
  
    -   Para realizar una copia de seguridad de todos los archivos de un grupo `-DatabaseFileGroup`de archivos determinado, especifique el parámetro *String* , donde *String* es uno o varios grupos de archivos de base de datos de los que se va a hacer una copia de seguridad.  
  
     En el ejemplo siguiente se crea una copia de seguridad de archivos completa de cada uno de los archivos de los dos grupos de archivos secundarios 'FileGroup1' y 'FileGroup2' de la base de datos `MyDB` . Las copias de seguridad se crean en la ubicación de copia de seguridad predeterminada de la instancia del servidor `Computer\Instance`.  
  
    ```powershell
    Backup-SqlDatabase -ServerInstance Computer\Instance -Database MyDB -BackupAction Files -DatabaseFileGroup "FileGroup1","FileGroup2"  
    ```  
  
Para configurar y usar el proveedor de SQL Server PowerShell, vea [proveedor de SQL Server PowerShell](../../powershell/sql-server-powershell-provider.md).
  
## <a name="see-also"></a>Consulte también  
 [Información general de copia de seguridad &#40;SQL Server&#41;](backup-overview-sql-server.md)   
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [Historial de copias de seguridad e información de encabezados &#40;SQL Server&#41;](backup-history-and-header-information-sql-server.md)   
 [Copia de seguridad de base de datos &#40;página general&#41;](../../integration-services/general-page-of-integration-services-designers-options.md)   
 [Copia de seguridad de base de datos &#40;página Opciones de copia de seguridad&#41;](back-up-database-backup-options-page.md)   
 [Copias de seguridad de archivos completas &#40;SQL Server&#41;](full-file-backups-sql-server.md)   
 [Copias de seguridad diferenciales &#40;SQL Server&#41;](differential-backups-sql-server.md)   
 [Restauraciones de archivos &#40;modelo de recuperación completa&#41;](file-restores-full-recovery-model.md)   
 [Restauraciones de archivos &#40;modelo de recuperación simple&#41;](file-restores-simple-recovery-model.md)  
  
  
