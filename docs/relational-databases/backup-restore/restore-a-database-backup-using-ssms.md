---
title: Restaurar una copia de seguridad de base de datos con SSMS | Microsoft Docs
description: En este artículo se explica cómo restaurar una copia de seguridad completa de base de datos de SQL Server con SQL Server Management Studio.
ms.custom: ''
ms.date: 11/16/2016
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql13.swb.locatebackupfileazure.f1
- sql13.swb.specifybackup.f1
helpviewer_keywords:
- full backups [SQL Server]
- database restores [SQL Server], full backups
- backing up databases [SQL Server], full backups
- database backups [SQL Server], full backups
- restoring databases [SQL Server], full backups
ms.assetid: 24b3311d-5ce0-4581-9a05-5c7c726c7b21
author: cawrites
ms.author: chadam
ms.openlocfilehash: f93bb71a3f6dcbbd98e62cca67a877361c6766db
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/23/2020
ms.locfileid: "96125592"
---
# <a name="restore-a-database-backup-using-ssms"></a>Restauración de una copia de seguridad de base de datos con SSMS
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  En este tema se explica cómo restaurar una copia de seguridad completa de base de datos con SQL Server Management Studio.    
       
### <a name="important"></a>Importante:    
Para poder restaurar una base de datos en el modelo de recuperación completa u optimizado para cargas masivas de registros, es posible que deba realizar una copia de seguridad del registro de transacciones activo (conocido como [final del registro](tail-log-backups-sql-server.md)). Para obtener más información, vea [Realizar copia de seguridad de un registro de transacciones &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)).  

Cuando restaure una base de datos desde otra instancia, considere la información de [Administrar los metadatos cuando una base de datos pasa a estar disponible en otra instancia de servidor (SQL Server)](../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md).   
    
Para restaurar una base de datos cifrada, debe tener acceso al certificado o la clave simétrica usados para cifrar la base de datos. La base de datos no se puede restaurar sin el certificado o la clave asimétrica. Debe conservar el certificado usado para cifrar la clave de cifrado de base de datos durante el tiempo que necesite guardar la copia de seguridad. Para obtener más información, consulte [SQL Server Certificates and Asymmetric Keys](../../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md).    
    
Si restaura una base de datos de una versión anterior en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], la base de datos se actualizará automáticamente a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Esto evita que la base de datos se use con una versión anterior de [!INCLUDE[ssde_md](../../includes/ssde_md.md)]. Pero esto se relaciona con el estado de los metadatos y no afecta al [nivel de compatibilidad de la base de datos](../../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md). Si el nivel de compatibilidad de una base de datos de usuario es 100 o superior antes de la actualización, permanece igual después de la misma. Si el nivel de compatibilidad es 90 antes de la actualización, en la base de datos actualizada, el nivel de compatibilidad se establece en 100, que es el nivel de compatibilidad mínimo admitido en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Para obtener más información, vea [Nivel de compatibilidad de ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md).  
  
Normalmente, la base de datos está disponible inmediatamente. Pero si una base de datos de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] tiene índices de texto completo, el proceso de actualización los importa, los restablece o los vuelve a generar, según la configuración de la propiedad del servidor **Opción de actualización de texto completo** . Si la opción de actualización se establece en **Importar** o en **Volver a generar**, los índices de texto completo no estarán disponibles durante la actualización. Según la cantidad de datos que se indexen, la importación puede tardar varias horas y la opción de recompilación puede necesitar hasta diez veces más.     
    
Si la opción de actualización se establece en **Importar** y no hay disponible ningún catálogo de texto completo, se vuelven a generar los índices de texto completo asociados. Para obtener más información sobre cómo ver o cambiar la configuración de la propiedad **Opción de actualización de texto completo** , vea [Administrar y supervisar la búsqueda de texto completo para una instancia de servidor](../../relational-databases/search/manage-and-monitor-full-text-search-for-a-server-instance.md).    

Para obtener más información sobre la restauración de SQL Server en el servicio de almacenamiento de blobs de Microsoft Azure, vea [Copia de seguridad y restauración de SQL Server con el servicio de Almacenamiento de blobs de Microsoft Azure](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md).

## <a name="examples"></a>Ejemplos
    
### <a name="a-restore-a-full-database-backup"></a>A. Restaurar una copia de seguridad completa de la base de datos   
    
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] y expándala.  
    
2.  Haga clic con el botón derecho en **Bases de datos** y seleccione **Restaurar base de datos...**    
    
3.  En la página **General** , use la sección **Origen** para especificar el origen y la ubicación de los conjuntos de copias de seguridad que se deben restaurar. Seleccione una de las siguientes opciones:    
    
    -   **Base de datos**    
    
         Seleccione la base de datos que desea restaurar en la lista desplegable. La lista solo contiene las bases de datos de las que se han realizado copias de seguridad de acuerdo con el historial de copias de seguridad de **msdb** .    
    
        > [!NOTE]
        > Si la copia de seguridad se toma desde un servidor diferente, el servidor de destino no tendrá la información del historial de copia de seguridad de la base de datos especificada. En este caso, seleccione **Dispositivo** para especificar manualmente el archivo o dispositivo que se va a restaurar. 
    
    -   **Dispositivo**    
    
         Haga clic en el botón de exploración ( **...** ) para abrir el cuadro de diálogo **Seleccionar dispositivos de copia de seguridad** . 
         
        -   Cuadro de diálogo **Seleccionar dispositivos de copia de seguridad**  
        
            **Tipo de medio de copia de seguridad**  
         Seleccione un tipo de medio en la lista desplegable **Tipo de medio de copia de seguridad** .  Nota: La opción **Cinta** solo aparece si se ha montado una unidad de cinta en el sistema; la opción **Dispositivo de copia de seguridad** aparece únicamente si existe al menos un dispositivo de copia de seguridad.

            **Add (Agregar)**  
            En función del tipo de medio que seleccione en la lista desplegable **Tipo de medio de copia de seguridad** , al hacer clic en **Agregar** , se abrirá uno de los siguientes cuadros de diálogo. (Si la lista del cuadro de lista **Medio de copia de seguridad** está llena, el botón **Agregar** no está disponible).

            |Tipo de medio|Cuadro de diálogo|Descripción|    
            |----------------|----------------|-----------------|    
            |**Archivo**|**Buscar archivo de copia de seguridad**|En este cuadro de diálogo, puede seleccionar un archivo local en el árbol, o bien especificar un archivo remoto mediante su nombre UNC (convención de nomenclatura universal) completo. Para obtener más información, vea [Dispositivos de copia de seguridad &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md).|    
            |**Dispositivo**|**Seleccionar dispositivo de copia de seguridad**|En este cuadro de diálogo, puede seleccionar un dispositivo de una lista de dispositivos lógicos de copia de seguridad en la instancia del servidor.|    
            |**Cinta**|**Seleccionar cinta de copia de seguridad**|En este cuadro de diálogo, puede seleccionar una cinta de la lista de unidades de cinta que están conectadas físicamente al equipo en el que se ejecuta la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|    
            |**URL**|**Seleccionar ubicación de archivo de copia de seguridad**|En este cuadro de diálogo puede seleccionar un contenedor de almacenamiento de Azure o de credenciales de SQL Server existente, agregar un nuevo contenedor de almacenamiento de Azure con una firma de acceso compartido o generar una firma de acceso compartido y las credenciales de SQL Server para un contenedor de almacenamiento existente.  Vea también [Connect to a Microsoft Azure Subscription (Conectarse a una suscripción de Microsoft Azure)](../../relational-databases/backup-restore/connect-to-a-microsoft-azure-subscription.md).|  
         
             **Quitar**    
             Quita uno o varios archivos, cintas o dispositivos lógicos de copia de seguridad seleccionados.    
                 
             **Contenido**    
            Muestra el contenido de los medios de un archivo, una cinta o un dispositivo lógico de copia de seguridad seleccionado.  Este botón podría no funcionar si el tipo de medio es **Dirección URL**.  

             **Medio de copia de seguridad**   
             Muestra los medios seleccionados.
    
             Después de agregar los dispositivos que desee al cuadro de lista **Medio de copia de seguridad** , haga clic en **Aceptar** para volver a la página **General** .    
    
         En el cuadro de lista **Origen: Dispositivo: Base de datos**, seleccione el nombre de la base de datos que se debe restaurar.    
    
         > [!NOTE]
         > Esta lista solo está disponible cuando se selecciona la opción **Dispositivo** . Solo estarán disponibles las bases de datos que tienen copias de seguridad en el dispositivo seleccionado.    
     
4.  En la sección **Destino** , el cuadro **Base de datos** se rellena automáticamente con el nombre de la base de datos que se va a restaurar. Para cambiar el nombre de la base de datos, especifique el nuevo nombre en el cuadro **Base de datos** .    
    
5.  En el cuadro **Restaurar en** , deje el valor predeterminado **A la última copia de seguridad tomada** o haga clic en **Escala de tiempo** para acceder al cuadro de diálogo **Escala de tiempo de copia de seguridad** para seleccionar manualmente un momento a fin de que se detenga la acción de recuperación. Para obtener más información acerca de cómo designar un momento específico, vea [Backup Timeline](../../relational-databases/backup-restore/backup-timeline.md).    
    
6.  En la cuadrícula **Conjuntos de copia de seguridad que se van a restaurar** , seleccione las copias de seguridad que desea restaurar. En esta cuadrícula se muestran las copias de seguridad disponibles en la ubicación especificada. De forma predeterminada, se sugiere un plan de recuperación. Para anular el plan de recuperación sugerido, puede cambiar las selecciones de la cuadrícula. Se anula automáticamente la selección de las copias de seguridad que dependen de la restauración de una copia de seguridad anterior cuando se anula la selección de una copia de seguridad anterior. Para obtener información sobre las columnas de la cuadrícula **Conjuntos de copia de seguridad que se van a restaurar** , vea [Restaurar la base de datos &#40;página General&#41;](../../relational-databases/backup-restore/restore-database-general-page.md)).    
    
7.  Si lo desea, haga clic en **Archivos** en el recuadro **Seleccionar una página** para obtener acceso al cuadro de diálogo **Archivos** . A partir de aquí, puede restaurar la base de datos a una nueva ubicación si especifica un nuevo destino de restauración para cada archivo de la cuadrícula **Restaurar los archivos de base de datos como** . Para obtener más información sobre esta cuadrícula, vea [Restaurar base de datos &#40;página Archivos&#41;](../../relational-databases/backup-restore/restore-database-files-page.md).    
    
8. Para ver o seleccionar las opciones avanzadas, en la página **Opciones** , en el panel **Opciones de restauración** , puede seleccionar cualquiera de las opciones siguientes si son apropiadas para su situación:    

   1. Opciones **WITH** (no necesarias):    
    
     - **Sobrescribir la base de datos existente (WITH REPLACE)**    
    
     - **Conservar la configuración de replicación (WITH KEEP_REPLICATION)**    
    
     - **Restringir el acceso a la base de datos restaurada (WITH RESTRICTED_USER)**    
    
   2. Seleccione una opción en el cuadro **Estado de recuperación** . Este cuadro determina el estado de la base de datos después de la operación de restauración.    
    
     - **RESTORE WITH RECOVERY** es el comportamiento predeterminado que deja la base de datos lista para usarse mediante la reversión de las transacciones no confirmadas. No pueden restaurarse registros de transacciones adicionales. Seleccione esta opción si va a restaurar ahora todas las copias de seguridad necesarias.    
    
     - **RESTORE WITH NORECOVERY** deja la base de datos no operativa y no revierte las transacciones no confirmadas. Pueden restaurarse registros de transacciones adicionales. La base de datos no puede se usar hasta que se recupera.    
    
     - **RESTORE WITH STANDBY** deja la base de datos en modo de solo lectura. Deshace las transacciones sin confirmar, pero guarda las acciones de deshacer en un archivo en espera para que los efectos de la recuperación puedan revertirse.    
    
   3. **Realice una copia del final del registro antes de la restauración.** No todos los escenarios de restauración requieren una copia del final del registro.  Para obtener más información, vea **Escenarios que requieren una copia del final del registro** en [Copias del final del registro (SQL Server)](../../relational-databases/backup-restore/tail-log-backups-sql-server.md).
  
   4. Puede haber errores en las operaciones de restauración si hay conexiones activas con la base de datos. Active la opción **Cerrar conexiones existentes** para asegurarse de que se cierren todas las conexiones activas entre [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] y la base de datos. Esta casilla establece la base de datos en modo de usuario único antes de realizar las operaciones de restauración, y establece la base de datos en modo multiusuario una vez completadas.    
  
   5. Seleccione **Preguntar antes de restaurar cada copia de seguridad** si desea que se le pregunte en cada operación de restauración. No suele ser necesario a menos que la base de datos sea grande y desee supervisar el estado de la operación de restauración.    
    
Para obtener más información sobre estas opciones de restauración, vea [Restaurar base de datos &#40;página Opciones&#41;](../../relational-databases/backup-restore/restore-database-options-page.md)).    
    
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)] 

### <a name="b-restore-an-earlier-disk-backup-over-an-existing-database"></a>B. Restaurar una copia de seguridad de disco anterior en una base de datos existente
En el ejemplo siguiente se restaura una copia de seguridad de disco anterior de `Sales` y se sobrescribe la base de datos `Sales` existente.

1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] y expándala.  
2.  Haga clic con el botón derecho en **Bases de datos** y seleccione **Restaurar base de datos...**  
3.  En la página **General** , seleccione **Dispositivo** en la sección **Origen** .
4.  Haga clic en el botón de exploración ( **...** ) para abrir el cuadro de diálogo **Seleccionar dispositivos de copia de seguridad** . Haga clic en **Agregar** y vaya a la copia de seguridad. Haga clic en **Aceptar** después de seleccionar los archivos de la copia de seguridad de disco.
5.  Haga clic en **Aceptar** para volver a la página **General** .
6.  Haga clic en **Opciones** en el panel **Seleccionar una página** .
7.  En la sección **Opciones de restauración** , active **Sobrescribir la base de datos existente (WITH REPLACE)** .

    > [!NOTE]
    > Si no activa esta opción, puede aparecer el mensaje de error siguiente: "System.Data.SqlClient.SqlError: El conjunto de copia de seguridad contiene una copia de una base de datos distinta de la existente "`Sales`". (Microsoft.SqlServer.SmoExtended)"

8.  En la sección **Copia del final del registro** , desactive **Realizar copia del final del registro de la cola antes de la restauración**.

    > [!NOTE]
    > No todos los escenarios de restauración requieren una copia del final del registro. No necesita una copia del final del registro si el punto de recuperación está incluido en una copia de seguridad de registros anterior. Además, no es necesaria una copia del final del registro si va a mover o reemplazar (sobrescribir) la base de datos y no necesita restaurarla a un momento posterior de la copia de seguridad más reciente. Para obtener más información, vea [Copias del final del registro (SQL Server)](../../relational-databases/backup-restore/tail-log-backups-sql-server.md).

    Esta opción no está disponible para las bases de datos en el modelo de recuperación SIMPLE.

9.  En la sección **Conexiones de servidor** , active **Cerrar las conexiones existentes con la base de datos de destino**.

    > [!NOTE]
    > Si no activa esta opción, puede aparecer el mensaje de error siguiente: "System.Data.SqlClient.SqlError: No se pudo obtener acceso exclusivo porque la base de datos está en uso. (Microsoft.SqlServer.SmoExtended)"
    
10. [!INCLUDE[clickOK](../../includes/clickok-md.md)] 

### <a name="c--restore-an-earlier-disk-backup-with-a-new-database-name-where-the-original-database-still-exists"></a>C.  Restaurar una copia de seguridad de disco anterior con un nuevo nombre de base de datos donde todavía existe la base de datos original
En el ejemplo siguiente se restaura una copia de seguridad de disco anterior de `Sales` y se crea una base de datos denominada `SalesTest`.  La base de datos original, `Sales`, sigue existiendo en el servidor.

1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] y expándala.  
2.  Haga clic con el botón derecho en **Bases de datos** y seleccione **Restaurar base de datos...**  
3.  En la página **General** , seleccione **Dispositivo** en la sección **Origen** .
4.  Haga clic en el botón de exploración ( **...** ) para abrir el cuadro de diálogo **Seleccionar dispositivos de copia de seguridad** . Haga clic en **Agregar** y vaya a la copia de seguridad. Haga clic en **Aceptar** después de seleccionar los archivos de la copia de seguridad de disco.
5.  Haga clic en **Aceptar** para volver a la página **General** .
6.  En la sección **Destino** , el cuadro **Base de datos** se rellena automáticamente con el nombre de la base de datos que se va a restaurar. Para cambiar el nombre de la base de datos, especifique el nuevo nombre en el cuadro **Base de datos** .
7.  Haga clic en **Opciones** en el panel **Seleccionar una página** .
8.  En la sección **Copia del final del registro** , desactive "**Realizar copia del final del registro de la cola antes de la restauración**".

    > [!IMPORTANT]
    > Si no desactiva esta opción, la base de datos existente ( `Sales`) cambiará al estado de restauración.

9. [!INCLUDE[clickOK](../../includes/clickok-md.md)] 

    > [!NOTE]
    > Si recibe el mensaje de error siguiente:      
    > "System.Data.SqlClient.SqlError: No se hizo copia de seguridad del final del registro de la base de datos "`Sales`". Use `BACKUP LOG WITH NORECOVERY` para realizar una copia de seguridad del registro si contiene trabajo que no quiere perder. Use la cláusula `WITH REPLACE` o `WITH STOPAT` de la instrucción `RESTORE` para sobrescribir el contenido del registro. (Microsoft.SqlServer.SmoExtended)".      
    > Lo más probable es que no haya escrito el nuevo nombre de la base de datos del paso 6. La opción Restore suele impedir que se sobrescriba accidentalmente una base de datos con otra base de datos. Si la base de datos especificada en una instrucción `RESTORE` ya existe en el servidor actual y el GUID de la familia de base de datos especificado difiere del de la familia de base de datos registrada en el conjunto de copia de seguridad, la base de datos no se restaura. Ésta es una importante medida preventiva.

### <a name="d--restore-earlier-disk-backups-to-a-point-in-time"></a>D.  Restaurar copias de seguridad de disco anteriores a un momento dado
En el ejemplo siguiente se restaura una base de datos al estado en que se encontraba a las `1:23:17 PM` del `May 30, 2016` y se muestra una operación de restauración que implica varias copias de seguridad de registros. La base de datos no existe actualmente en el servidor.

1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] y expándala.  
2.  Haga clic con el botón derecho en **Bases de datos** y seleccione **Restaurar base de datos...**  
3.  En la página **General** , seleccione **Dispositivo** en la sección **Origen** .
4.  Haga clic en el botón de exploración ( **...** ) para abrir el cuadro de diálogo **Seleccionar dispositivos de copia de seguridad** . Haga clic en **Agregar** y vaya a la copia de seguridad completa y a todas las copias de seguridad del registro de transacciones pertinentes.  Haga clic en **Aceptar** después de seleccionar los archivos de la copia de seguridad de disco.
5.  Haga clic en **Aceptar** para volver a la página **General** .
6.  En la sección **Destino** , haga clic en **Escala de tiempo** para tener acceso al cuadro de diálogo **Escala de tiempo de la copia de seguridad** para seleccionar manualmente un momento a fin de que se detenga la acción de recuperación.
7.  Seleccione **Fecha y hora específicas**.  
8.  Cambie el **Intervalo de escala de tiempo** a **Hora** en el cuadro desplegable (opcional).  
9.  Mueva el control deslizante hasta la hora que quiera.
10. Haga clic en **Aceptar** para volver a la página General.
11. [!INCLUDE[clickOK](../../includes/clickok-md.md)] 

### <a name="e--restore-a-backup-from-the-microsoft-azure-storage-service"></a>E.  Restaurar una copia de seguridad desde el servicio de almacenamiento de Microsoft Azure

#### <a name="common-steps"></a>Pasos comunes
En los dos ejemplos siguientes se realiza una restauración de `Sales` desde una copia de seguridad que se encuentra en el servicio de almacenamiento de Microsoft Azure.  El nombre de la cuenta de almacenamiento es `mystorageaccount`.  El contenedor se denomina `myfirstcontainer`.  Por motivos de brevedad, los seis primeros pasos se enumeran aquí una vez y todos los ejemplos iniciarán en el **paso 7**.
1.  En el **Explorador de objetos**, conéctese a una instancia del Motor de base de datos de SQL Server y expándala.
2.  Haga clic con el botón derecho en **Bases de datos** y seleccione **Restaurar base de datos...**
3.  En la página **General** , seleccione **Dispositivo** en la sección **Origen** .
4.  Haga clic en el botón Examinar (...) para abrir el cuadro de diálogo **Seleccionar dispositivos de copia de seguridad** .    
5.  Seleccione **Dirección URL** en la lista desplegable **Tipo de medio de copia de seguridad:** .
6.  Haga clic en **Agregar** y se abrirá el cuadro de diálogo **Seleccionar ubicación de archivo de copia de seguridad** .

#### <a name="e1---restore-a-striped-backup-over-an-existing-database-and-a-shared-access-signature-exists"></a>E1.   Restaurar una copia de seguridad seccionada en una base de datos existente cuando existe una firma de acceso compartido
Se ha creado una directiva de acceso almacenada con derechos de lectura, escritura, eliminación y lista.  Además, se ha creado para el contenedor `https://mystorageaccount.blob.core.windows.net/myfirstcontainer`una firma de acceso compartido asociada a la directiva de acceso almacenada.  Los pasos son básicamente los mismos si ya existe una credencial de SQL Server.  La base de datos `Sales` ya existe actualmente en el servidor.  Los archivos de copia de seguridad son `Sales_stripe1of2_20160601.bak` y `Sales_stripe2of2_20160601.bak`.  

1.  Seleccione `https://mystorageaccount.blob.core.windows.net/myfirstcontainer` en la lista desplegable **Contenedor de almacenamiento de Azure:** si ya existe una credencial de SQL Server. En caso de que no exista, escriba manualmente el nombre del contenedor, `https://mystorageaccount.blob.core.windows.net/myfirstcontainer`. 
1. Escriba la firma de acceso compartido en el cuadro de texto enriquecido **Firma de acceso compartido:** .
1. Haga clic en **Aceptar** y se abrirá el cuadro de diálogo **Buscar archivo de copia de seguridad en Microsoft Azure** .
1. Expanda **Contenedores** y vaya a `https://mystorageaccount.blob.core.windows.net/myfirstcontainer`.
1. Mantenga pulsada la tecla CTRL y seleccione los archivos `Sales_stripe1of2_20160601.bak` y `Sales_stripe2of2_20160601.bak`.
1. Haga clic en **OK**.
1. Haga clic en **Aceptar** para volver a la página **General** .
1. Haga clic en **Opciones** en el panel **Seleccionar una página** .
1. En la sección **Opciones de restauración** , active **Sobrescribir la base de datos existente (WITH REPLACE)** .
1. En la sección **Copia del final del registro** , desactive **Realizar copia del final del registro de la cola antes de la restauración**.
1. En la sección **Conexiones de servidor** , active **Cerrar las conexiones existentes con la base de datos de destino**.
1. Haga clic en **OK**.

#### <a name="e2---a-shared-access-signature-does-not-exist"></a>E2.   No existe ninguna firma de acceso compartido
En este ejemplo, la base de datos `Sales` no existe actualmente en el servidor.
1. Haga clic en **Agregar** y se abrirá el cuadro de diálogo **Conectarse a una suscripción de Microsoft** .  
1. Complete el cuadro de diálogo **Conectarse a una suscripción de Microsoft** y haga clic en **Aceptar** para volver al cuadro de diálogo **Seleccionar ubicación de archivo de copia de seguridad** .  Consulte [Connect to a Microsoft Azure Subscription (Conectarse a una suscripción de Microsoft Azure)](../../relational-databases/backup-restore/connect-to-a-microsoft-azure-subscription.md) para obtener más información.
1. Haga clic en **Aceptar** en el cuadro de diálogo **Seleccionar ubicación de archivo de copia de seguridad** y se abrirá el cuadro de diálogo **Buscar archivo de copia de seguridad en Microsoft Azure** .
1. Expanda **Contenedores** y vaya a `https://mystorageaccount.blob.core.windows.net/myfirstcontainer`.
1. Seleccione el archivo de copia de seguridad y haga clic en **Aceptar**.
1. Haga clic en **Aceptar** para volver a la página **General** .
1. Haga clic en **OK**.

#### <a name="f-restore-local-backup-to-microsoft-azure-storage-url"></a>F. Restaurar copia de seguridad local en el almacenamiento de Microsoft Azure (dirección URL)
La base de datos `Sales` se restaurará en el contenedor de almacenamiento de Microsoft Azure `https://mystorageaccount.blob.core.windows.net/myfirstcontainer` desde una copia de seguridad que se encuentra en `E:\MSSQL\BAK`.  Ya se ha creado la credencial de SQL Server para el contenedor de Azure.  Debe existir una credencial de SQL Server para el contenedor de destino, ya que no se puede crear mediante la tarea **Restaurar** .  La base de datos `Sales` no existe actualmente en el servidor.
1.  En el **Explorador de objetos**, conéctese a una instancia del Motor de base de datos de SQL Server y expándala.
2.  Haga clic con el botón derecho en **Bases de datos** y seleccione **Restaurar base de datos...**
3.  En la página **General** , seleccione **Dispositivo** en la sección **Origen** .
4.  Haga clic en el botón Examinar (...) para abrir el cuadro de diálogo **Seleccionar dispositivos de copia de seguridad** .  
5.  Seleccione **Archivo** en la lista desplegable **Tipo de medio de copia de seguridad:** .
6.  Haga clic en **Agregar** y se abrirá el cuadro de diálogo **Buscar archivo de copia de seguridad** .
7.  Vaya a `E:\MSSQL\BAK`, seleccione el archivo de copia de seguridad y haga clic en **Aceptar**.
8.  Haga clic en **Aceptar** para volver a la página **General** .
9.  Haga clic en **Archivos** en el panel **Seleccionar una página** .
10. Active la casilla **Reubicar todos los archivos en la carpeta**.
11. Especifique el contenedor, `https://mystorageaccount.blob.core.windows.net/myfirstcontainer`, en los cuadros de texto para **Carpeta de archivos de datos:** y **Carpeta de archivos de registro:** .
12. Haga clic en **OK**.

## <a name="see-also"></a>Consulte también    
 [Realizar copia de seguridad de un registro de transacciones &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)     
 [Crear una copia de seguridad completa de base de datos &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)     
 [Restaurar una base de datos a una nueva ubicación &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-database-to-a-new-location-sql-server.md)     
 [Restaurar una copia de seguridad del registro de transacciones &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md)     
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)     
 [Restaurar base de datos &#40;página Opciones&#41;](../../relational-databases/backup-restore/restore-database-options-page.md)     
 [Restaurar la base de datos &#40;página General&#41;](../../relational-databases/backup-restore/restore-database-general-page.md)    
    
  
