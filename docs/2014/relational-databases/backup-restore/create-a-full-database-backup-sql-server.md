---
title: Creación de una copia de seguridad completa de base de datos (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- backing up databases [SQL Server], full backups
- backing up databases [SQL Server], SQL Server Management Studio
- backups [SQL Server], creating
- database backups [SQL Server], SQL Server Management Studio
ms.assetid: 586561fc-dfbb-4842-84f8-204a9100a534
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: ec94f8387d7b833a80cd4df09f7d4208974d40a7
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2019
ms.locfileid: "70154820"
---
# <a name="create-a-full-database-backup-sql-server"></a>Crear una copia de seguridad completa de base de datos (SQL Server)
  En este tema se describe cómo crear una copia de seguridad completa de la base de datos en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)]o PowerShell.  
  
> [!NOTE]  
>  Para obtener información sobre SQL Server copia de seguridad en el servicio de almacenamiento de blobs de Azure, consulte [SQL Server Backup and restore with Azure BLOB Storage Service](sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md).  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Recomendaciones](#Recommendations)  
  
     [Seguridad](#Security)  
  
-   **Para crear una copia de seguridad completa de la base de datos, use:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
-   [Tareas relacionadas](#RelatedTasks)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   La instrucción BACKUP no se permite en una transacción explícita o implícita.  
  
-   Las copias de seguridad que se crean en una versión más reciente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no se pueden restaurar en versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Para obtener más información, vea [Información general de copia de seguridad &#40;SQL Server&#41;](backup-overview-sql-server.md).  
  
###  <a name="Recommendations"></a> Recomendaciones  
  
-   A medida que la base de datos aumenta de tamaño, las copias de seguridad completas requieren una mayor cantidad de tiempo para finalizar y espacio de almacenamiento. Por ello, para una base de datos grande, puede que desee complementar una copia de seguridad completa con una serie de *copias de seguridad diferenciales*. Para obtener más información, vea [Copias de seguridad diferenciales &#40;SQL Server&#41;](differential-backups-sql-server.md).  
  
-   Para calcular el tamaño de la copia de seguridad completa de la base de datos, use el procedimiento almacenado del sistema [sp_spaceused](/sql/relational-databases/system-stored-procedures/sp-spaceused-transact-sql) .  
  
-   De forma predeterminada, cada operación de copia de seguridad correcta agrega una entrada en el registro de errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y en el registro de eventos del sistema. Si hace una copia de seguridad del registro de transacciones con frecuencia, estos mensajes que indican la corrección de la operación pueden acumularse rápidamente, con lo que se crean registros de errores muy grandes que pueden dificultar la búsqueda de otros mensajes. En esos casos, puede suprimir estas entradas de registro utilizando la marca de seguimiento 3226 si ninguno de los scripts depende de esas entradas. Para obtener más información, vea [Marcas de seguimiento &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql).  
  
###  <a name="Security"></a> Seguridad  
 TRUSTWORTHY se establece en OFF en una copia de seguridad de base de datos. Para obtener información sobre cómo establecer TRUSTWORTHY en ON, vea [Opciones de ALTER DATABASE SET &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options).  
  
 A partir de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] las opciones `PASSWORD` y `MEDIAPASSWORD` se suspenden para crear copias de seguridad. Todavía puede restaurar las copias de seguridad creadas con contraseñas.  
  
####  <a name="Permissions"></a> Permisos  
 De forma predeterminada, los permisos BACKUP DATABASE y BACKUP LOG corresponden a los miembros del rol fijo de servidor **sysadmin** y de los roles fijos de base de datos **db_owner** y **db_backupoperator** .  
  
 Los problemas de propiedad y permisos del archivo físico del dispositivo de copia de seguridad pueden interferir con una operación de copia de seguridad. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe poder leer y escribir en el dispositivo y la cuenta en la que se ejecuta el servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe tener permisos de escritura. En cambio, [sp_addumpdevice](/sql/relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql), que agrega una entrada para un dispositivo de copia de seguridad en las tablas del sistema, no comprueba los permisos de acceso a los archivos. Es posible que estos problemas con el archivo físico del dispositivo de copia de seguridad no aparezcan hasta que se tenga acceso al recurso físico, al intentar la copia de seguridad o la restauración.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
> [!NOTE]  
>  Al especificar una tarea de copia de seguridad mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], puede generar el script [!INCLUDE[tsql](../../includes/tsql-md.md)] [BACKUP](/sql/t-sql/statements/backup-transact-sql) script by clicking the **Script** button and selecting a script destination.  
  
#### <a name="to-back-up-a-database"></a>Para realizar una copia de seguridad de una base de datos  
  
1.  Tras conectarse a la instancia apropiada de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], en el Explorador de objetos, haga clic en el nombre del servidor para expandir el árbol correspondiente.  
  
2.  Expanda **Bases de datos**y, dependiendo de la base de datos, seleccione una base de datos de usuario o expanda **Bases de datos del sistema** y seleccione una base de datos del sistema.  
  
3.  Haga clic con el botón derecho en la base de datos, seleccione **Tareas**y haga clic en **Copia de seguridad**. Aparece el cuadro de diálogo **Copia de seguridad de base de datos** .  
  
4.  En el `Database` cuadro de lista, compruebe el nombre de la base de datos. También puede seleccionar otra base de datos en la lista.  
  
5.  Puede realizar una copia de seguridad de la base de datos en cualquier modelo de recuperación (**FULL**, **BULK_LOGGED**o **SIMPLE**).  
  
6.  En el cuadro de lista **Tipo de copia de seguridad** , seleccione **Completa**.  
  
     Tenga en cuenta que después de crear una copia de seguridad completa de la base de datos, puede crear una copia de seguridad diferencial; para obtener más información, vea [Crear una copia de seguridad diferencial de una base de datos &#40;SQL Server&#41;](create-a-differential-database-backup-sql-server.md).  
  
7.  También puede seleccionar **Copia de seguridad de solo copia** para crear una copia de seguridad de solo copia. Una *copia de seguridad de solo copia* es una copia de seguridad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] independiente de la secuencia de copias de seguridad convencionales de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información, vea [Copias de seguridad de solo copia &#40;SQL Server&#41;](copy-only-backups-sql-server.md).  
  
    > [!NOTE]  
    >  Cuando la opción **Diferencial** está seleccionada, no puede crear una copia de seguridad de solo copia.  
  
8.  En **componente de copia**de `Database`seguridad, haga clic en.  
  
9. Acepte el nombre del conjunto de copia de seguridad predeterminado sugerido en el cuadro de texto **Nombre** o especifique otro nombre.  
  
10. Opcionalmente, en el cuadro de texto **Descripción** , escriba una descripción del conjunto de copia de seguridad.  
  
11. Elija el tipo de destino de la copia de seguridad haciendo clic en **Disco**, **Cinta** o **Dirección URL**. Para seleccionar las rutas de acceso de hasta 64 unidades de disco o cinta que contienen un solo conjunto de medios, haga clic en **Agregar**. Las rutas seleccionadas se muestran en el cuadro de lista **Copia de seguridad en** .  
  
     Para eliminar un destino de copia de seguridad, selecciónelo y haga clic en **Quitar**. Para ver el contenido de un destino de copia de seguridad, selecciónelo y haga clic en **Contenido**.  
  
12. Para ver o seleccionar las opciones multimedia, haga clic en **Opciones multimedia** en el panel **Seleccionar una página** .  
  
13. Seleccione una opción de **Sobrescribir medios** ; para ello, haga clic en una de las opciones siguientes:  
  
    -   **Hacer copia de seguridad en el conjunto de medios existente**  
  
         Para esta opción, haga clic en **Anexar al conjunto de copia de seguridad existente** o **Sobrescribir todos los conjuntos de copia de seguridad existentes**. Para obtener más información, vea [Conjuntos de medios, familias de medios y conjuntos de copias de seguridad &#40;SQL Server&#41;](media-sets-media-families-and-backup-sets-sql-server.md).  
  
         Opcionalmente, seleccione **Comprobar nombre de conjunto de medios y fecha de expiración del conjunto de copia de seguridad** para que la operación de copia de seguridad compruebe la fecha y la hora en que expiran el conjunto de medios y el conjunto de copia de seguridad.  
  
         También puede escribir un nombre en el cuadro de texto **Nombre del conjunto de medios** . Si no especifica ningún nombre, se creará un conjunto de medios con un nombre en blanco. Si especifica un nombre para el conjunto, los medios (cinta o disco) se comprueban para ver si el nombre real coincide con el nombre especificado aquí.  
  
        > [!IMPORTANT]  
        >  Esta opción está deshabilitada si seleccionó **Dirección URL** como destino de la copia de seguridad en la página **General** . Para obtener más información, vea [Copia de seguridad de la base de datos &#40;página Opciones multimedia&#41;](back-up-database-media-options-page.md).  
        >   
        >  Si piensa usar cifrado, no seleccione esta opción. Si selecciona esta opción, las opciones de cifrado de la página **Opciones de copia de seguridad** estarán deshabilitadas. No se admite el cifrado al anexar al conjunto de copia de seguridad existente.  
  
    -   **Hacer copia de seguridad en un nuevo conjunto de medios y borrar todos los conjuntos de copia de seguridad existentes**  
  
         Para esta opción, especifique un nombre en el cuadro de texto **Nuevo nombre del conjunto de medios** y, si lo desea, describa el conjunto de medios en el cuadro de texto **Nueva descripción del conjunto de medios** .  
  
        > [!IMPORTANT]  
        >  Esta opción está deshabilitada si seleccionó **Dirección URL** en la página **General** . Estas acciones no se admiten cuando se realiza una copia de seguridad en Azure Storage.  
  
14. Opcionalmente, en la sección **Confiabilidad** , seleccione:  
  
    -   **Comprobar copia de seguridad al finalizar**.  
  
    -   **Realizar suma de comprobación antes de escribir en los medios**y, si lo desea, **Continuar después de un error de suma de comprobación**. Para obtener más información sobre las sumas de comprobación, vea [Errores posibles de medios durante copia de seguridad y restauración &#40;SQL Server&#41;](possible-media-errors-during-backup-and-restore-sql-server.md).  
  
15. Si va a realizar copias de seguridad en una unidad de cinta (según se haya especificado en la sección **Destino** de la página **General**), la opción **Descargar la cinta después de realizar la copia de seguridad** está activa. Al hacer clic en esta opción se activa la opción **Rebobinar la cinta antes de descargar** .  
  
    > [!NOTE]  
    >  Las opciones de la sección **Registro de transacciones** se encuentran inactivas salvo que vaya a realizar una copia de seguridad de un registro de transacciones (según se haya especificado en la sección **Tipo de copia de seguridad** de la página **General** ).  
  
16. Para ver o seleccionar las opciones de copia de seguridad, haga clic en **Opciones de copia de seguridad** en el panel **Seleccionar una página** .  
  
17. Especifique cuándo expirará el conjunto de copia de seguridad y se podrá sobrescribir sin omitir explícitamente la comprobación de los datos de expiración:  
  
    -   Para que el conjunto de copia de seguridad expire al cabo de un número de días específico, haga clic en **Después de** (opción predeterminada) y escriba el número de días tras la creación del conjunto en que este expirará. Este valor puede estar entre 0 y 99999 días; el valor 0 significa que el conjunto de copia de seguridad no expirará nunca.  
  
         El valor predeterminado se establece en la opción **Tiempo predeterminado de retención de medios de copia de seguridad (días)** del cuadro de diálogo **Propiedades del servidor** (página Configuración de base de datos). Para acceder a esta opción, en el Explorador de objetos, haga clic con el botón derecho en el nombre del servidor y seleccione Propiedades; después, seleccione la página **Configuración de base de datos** .  
  
    -   Para que el conjunto de copia de seguridad expire en una determinada fecha, haga clic en **El**y escriba la fecha en la que expirará.  
  
         Para obtener más información sobre las fechas de expiración de la copia de seguridad, vea [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql).  
  
18. [!INCLUDE[ssEnterpriseEd10](../../../includes/ssenterpriseed10-md.md)] y las versiones posteriores admiten la [compresión de copia de seguridad](backup-compression-sql-server.md). De forma predeterminada, el hecho de que se comprima una copia de seguridad depende del valor de la opción de configuración del servidor **backup-compression default** . Pero, independientemente del valor predeterminado actual de nivel de servidor, puede comprimir una copia de seguridad si activa **Comprimir copia de seguridad**e impedir la compresión si activa **No comprimir copia de seguridad**.  
  
     **Para ver o cambiar el valor predeterminado de la compresión de copia de seguridad actual**  
  
    -   [Ver o establecer la opción de configuración del servidor de compresión de copia de seguridad predeterminada](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md)  
  
19. Especifique si desea utilizar cifrado para la copia de seguridad. Seleccione un algoritmo de cifrado para usar para el paso de cifrado y proporcione un certificado o clave asimétrica de una lista de los certificados existentes o de claves asimétricas. El cifrado se admite en SQL Server 2014 o posterior. Para obtener más detalles sobre las opciones de cifrado, vea [Copia de seguridad de la base de datos &#40;página Opciones de copia de seguridad&#41;](back-up-database-backup-options-page.md).  
  
> [!NOTE]  
>  Como alternativa para crear copias de seguridad de la base de datos, puede utilizar el Asistente para planes de mantenimiento.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-create-a-full-database-backup"></a>Para crear una copia de seguridad completa de la base de datos  
  
1.  Ejecute la instrucción BACKUP DATABASE para crear la copia de seguridad de base de datos completa, especificando:  
  
    -   El nombre de la base de datos de la que se va a realizar una copia de seguridad.  
  
    -   El dispositivo de copia de seguridad en el que se escribe la copia de seguridad de base de datos completa.  
  
     La sintaxis básica de [!INCLUDE[tsql](../../includes/tsql-md.md)] para crear una copia de seguridad de base de datos completa es:  
  
     BACKUP DATABASE *database*  
  
     TO *backup_device* [ **,** ...*n* ]  
  
     [ WITH *with_options* [ **,** ...*o* ] ] ;  
  
    |Opción|Descripción|  
    |------------|-----------------|  
    |*database*|Es la base de datos cuya copia de seguridad se desea hacer.|  
    |*backup_device* [ **,** ...*n* ]|Especifica una lista de 1 a 64 dispositivos de copia de seguridad que se pueden utilizar en la operación de copia de seguridad. Puede especificar un dispositivo físico de copia de seguridad o puede especificar un dispositivo de copia de seguridad lógico correspondiente, si ya se definió. Para especificar un dispositivo de copia de seguridad físico, use la opción DISK o TAPE:<br /><br /> { DISK &#124; TAPE } **=** _physical_backup_device_name_<br /><br /> Para obtener más información, vea [Dispositivos de copia de seguridad &#40;SQL Server&#41;](backup-devices-sql-server.md).|  
    |WITH *with_options* [ **,** ...*o* ]|De forma opcional, puede especificar una o varias opciones, *o*. Para obtener información sobre algunas de las opciones de WITH básicas, vea el paso 2.|  
  
2.  Opcionalmente, especifique una o varias opciones de WITH. A continuación se describen algunas de las opciones de WITH básicas. Para obtener información sobre todas las opciones de WITH, vea [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql).  
  
    -   Opciones de WITH básicas del conjunto de copia de seguridad:  
  
         { COMPRESSION | NO_COMPRESSION }  
         En [!INCLUDE[ssEnterpriseEd10](../../../includes/ssenterpriseed10-md.md)] y versiones posteriores únicamente, especifica si la [compresión de copia de seguridad](backup-compression-sql-server.md) se realiza en esta copia de seguridad, lo que invalida la configuración predeterminada del servidor.  
  
         ENCRYPTION (ALGORITHM, SERVER CERTIFICATE |ASYMMETRIC KEY)  
         En SQL Server 2014 o versiones posteriores únicamente, especifica el algoritmo de cifrado que se va a utilizar y el certificado o la clave asimétrica que se va a usar para proteger el cifrado.  
  
         Descripción **=** { ***'`text`* '**  |  text_variable **}@**  
         Especifica el texto sin formato que describe el conjunto de copia de seguridad. La cadena puede tener un máximo de 255 caracteres.  
  
         NAME **=** { *backup_set_name* |  **@** _backup_set_name_var_ }  
         Especifica el nombre del conjunto de copia de seguridad. Los nombres pueden tener un máximo de 128 caracteres. Si no se especifica NAME, está en blanco.  
  
    -   Opciones de WITH básicas del conjunto de copia de seguridad:  
  
         De forma predeterminada, BACKUP DATABASE anexa la copia de seguridad a un conjunto de medios existente, conservando los conjuntos de copia de seguridad existentes. Para especificar esto explícitamente, utilice la opción NOINIT. Para obtener información sobre la anexión a conjuntos de copia de seguridad existentes, vea [Conjuntos de medios, familias de medios y conjuntos de copias de seguridad &#40;SQL Server&#41;](media-sets-media-families-and-backup-sets-sql-server.md).  
  
         Opcionalmente, para dar formato a los medios de copia de seguridad, utilice la opción FORMAT:  
  
         FORMAT [ **,** MEDIANAME **=** { *media_name* |  **@** _media_name_variable_ } ] [ **,** MEDIADESCRIPTION **=** { *text* |  **@** _text_variable_ } ]  
         Utilice la cláusula FORMAT cuando emplee los medios por primera vez o cuando desee sobrescribir todos los datos existentes. De manera opcional, puede asignar a los nuevos medios un nombre y una descripción.  
  
        > [!IMPORTANT]  
        >  Tenga mucho cuidado cuando utilice la cláusula FORMAT de la instrucción BACKUP, ya que destruye cualquier copia de seguridad existente en el medio de copia de seguridad.  
  
###  <a name="TsqlExample"></a> Ejemplos (Transact-SQL)  
  
#### <a name="a-backing-up-to-a-disk-device"></a>A. Realizar la copia de seguridad en un dispositivo de disco  
 En el ejemplo siguiente se realiza una copia de seguridad completa de la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] en el disco y se usa `FORMAT` para crear un conjunto de medios nuevo.  
  
```sql  
USE AdventureWorks2012;  
GO  
BACKUP DATABASE AdventureWorks2012  
TO DISK = 'Z:\SQLServerBackups\AdventureWorks2012.Bak'  
   WITH FORMAT,  
      MEDIANAME = 'Z_SQLServerBackups',  
      NAME = 'Full Backup of AdventureWorks2012';  
GO  
```  
  
#### <a name="b-backing-up-to-a-tape-device"></a>b. Realizar la copia de seguridad en un dispositivo de cinta  
 En este ejemplo se realiza una copia de seguridad en cinta de la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]completa y se anexa a las copias de seguridad anteriores.  
  
```sql  
USE AdventureWorks2012;  
GO  
BACKUP DATABASE AdventureWorks2012  
   TO TAPE = '\\.\Tape0'  
   WITH NOINIT,  
      NAME = 'Full Backup of AdventureWorks2012';  
GO  
```  
  
#### <a name="c-backing-up-to-a-logical-tape-device"></a>C. Realizar la copia de seguridad en un dispositivo de cinta lógico  
 En este ejemplo, se crea un dispositivo de copia de seguridad lógico para una unidad de cinta. A continuación, se realiza una copia de seguridad completa de la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] en dicho dispositivo.  
  
```sql  
-- Create a logical backup device,   
-- AdventureWorks2012_Bak_Tape, for tape device \\.\tape0.  
USE master;  
GO  
EXEC sp_addumpdevice 'tape', 'AdventureWorks2012_Bak_Tape', '\\.\tape0'; USE AdventureWorks2012;  
GO  
BACKUP DATABASE AdventureWorks2012  
   TO AdventureWorks2012_Bak_Tape  
   WITH FORMAT,  
      MEDIANAME = 'AdventureWorks2012_Bak_Tape',  
      MEDIADESCRIPTION = '\\.\tape0',   
      NAME = 'Full Backup of AdventureWorks2012';  
GO  
```  
  
##  <a name="PowerShellProcedure"></a> Usar PowerShell  
  
1.  Utilice el cmdlet `Backup-SqlDatabase`. Para indicar explícitamente que se trata de una copia de seguridad completa de la base de datos, especifique el `Database`parámetro **-BackupAction** con su valor predeterminado,. Este parámetro es opcional para las copias de seguridad de base de datos completas.  
  
     En el ejemplo siguiente se crea una copia de seguridad completa de la base de datos `MyDB` en la ubicación de copia de seguridad predeterminada de la instancia de servidor `Computer\Instance`. Opcionalmente, en este ejemplo se especifica `-BackupAction Database`.  
  
    ```  
    --Enter this command at the PowerShell command prompt, C:\PS>  
    Backup-SqlDatabase -ServerInstance Computer\Instance -Database MyDB -BackupAction Database  
    ```  
  
 **Para configurar y usar el proveedor de SQL Server PowerShell**  
  
-   [Proveedor de SQL Server PowerShell Provider](../../powershell/sql-server-powershell-provider.md)  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
  
-   [Realizar una copia de seguridad de una base de datos (SQL Server)](create-a-full-database-backup-sql-server.md)  
  
-   [Crear una copia de seguridad diferencial de una base de datos &#40;SQL Server&#41;](create-a-differential-database-backup-sql-server.md)  
  
-   [Restaurar una copia de &#40;seguridad de base de datos SQL Server Management Studio&#41;](restore-a-database-backup-using-ssms.md)  
  
-   [Restaurar una copia de seguridad de base de datos en el modelo de recuperación simple &#40;Transact-SQL&#41;](restore-a-database-backup-under-the-simple-recovery-model-transact-sql.md)  
  
-   [Restaurar una base de datos según el punto de error en el modelo de recuperación completa &#40;Transact-SQL&#41;](restore-database-to-point-of-failure-full-recovery.md)  
  
-   [Restaurar una base de datos a una nueva ubicación &#40;SQL Server&#41;](restore-a-database-to-a-new-location-sql-server.md)  
  
-   [Usar el Asistente para planes de mantenimiento](../maintenance-plans/use-the-maintenance-plan-wizard.md)  
  
## <a name="see-also"></a>Vea también  
 [Información general de copia de seguridad &#40;SQL Server&#41;](backup-overview-sql-server.md)   
 [Copias de seguridad del registro de transacciones &#40;SQL Server&#41;](transaction-log-backups-sql-server.md)   
 [Conjuntos de medios, familias de medios y conjuntos de copias de seguridad &#40;SQL Server&#41;](media-sets-media-families-and-backup-sets-sql-server.md)   
 [sp_addumpdevice &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql)   
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [Copia de seguridad de base de datos &#40;página General&#41;](../../integration-services/general-page-of-integration-services-designers-options.md)   
 [Copia de seguridad de la base de datos &#40;página Opciones de copia de seguridad&#41;](back-up-database-backup-options-page.md)   
 [Copias de seguridad diferenciales &#40;SQL Server&#41;](differential-backups-sql-server.md)   
 [Copias de seguridad completas de bases de datos &#40;SQL Server&#41;](full-database-backups-sql-server.md)  
  
  
