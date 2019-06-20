---
title: Restaurar una copia de seguridad de base de datos (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql12.swb.locatebackupfileazure.f1
- sql12.swb.specifybackup.f1
helpviewer_keywords:
- full backups [SQL Server]
- database restores [SQL Server], full backups
- backing up databases [SQL Server], full backups
- database backups [SQL Server], full backups
- restoring databases [SQL Server], full backups
ms.assetid: 24b3311d-5ce0-4581-9a05-5c7c726c7b21
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 3d20276a90a64ca414b8bb6253b03df08908a1f1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62921239"
---
# <a name="restore-a-database-backup-sql-server-management-studio"></a>Restaurar una copia de seguridad de base de datos (SQL Server Management Studio)
  En este tema se explica cómo restaurar una copia de seguridad completa de la base de datos.  
  
> [!IMPORTANT]  
>  En el modelo de recuperación optimizado para cargas masivas de registros o completo, para poder restaurar una base de datos de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], se debe realizar una copia de seguridad del registro de transacciones activo (conocido como final del registro). Para obtener más información, vea [Realizar copia de seguridad de un registro de transacciones &#40;SQL Server&#41;](back-up-a-transaction-log-sql-server.md)). Para restaurar una base de datos cifrada, debe tener acceso al certificado o la clave asimétrica que se usó para cifrarla. La base de datos no se puede restaurar sin el certificado o la clave asimétrica. Como resultado, se debe conservar el certificado que se usa para cifrar la clave de cifrado de base de datos mientras se necesite la copia de seguridad. Para más información, consulte [SQL Server Certificates and Asymmetric Keys](../security/sql-server-certificates-and-asymmetric-keys.md).  
  
 Tenga en cuenta que si restaura una base de datos de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o una versión posterior a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], la base de datos se actualiza automáticamente. Normalmente, la base de datos está disponible inmediatamente. Pero, si una base de datos de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] tiene índices de texto completo, el proceso de actualización los importa, los restablece o los vuelve a generar, según la configuración de la propiedad del servidor **Opción de actualización de texto completo** . Si la opción de actualización se establece en **Importar** o en **Volver a generar**, los índices de texto completo no estarán disponibles durante la actualización. Dependiendo de la cantidad de datos que se indicen, la operación de importar puede requerir varias horas y la operación de volver a generar puede requerir hasta diez veces más. Tenga en cuenta también que si la opción de actualización se establece en **Importar**y no hay disponible ningún catálogo de texto completo, se vuelven a generar los índices de texto completo asociados. Para obtener más información sobre cómo ver o cambiar la configuración de la propiedad **Opción de actualización de texto completo** , vea [Administrar y supervisar la búsqueda de texto completo para una instancia de servidor](../search/manage-and-monitor-full-text-search-for-a-server-instance.md).  
  
### <a name="to-restore-a-full-database-backup"></a>Para restaurar una copia de seguridad completa de la base de datos  
  
1.  Después de conectarse a la instancia adecuada de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], en el Explorador de objetos, haga clic en el nombre del servidor para expandir el árbol de servidores.  
  
2.  Expanda **Bases de datos**. En función de la base de datos, seleccione una base de datos de usuario o expanda **Bases de datos del sistema**y, a continuación, seleccione una base de datos del sistema.  
  
3.  Haga clic en la base de datos, seleccione **tareas**, apunte a **restaurar**y, a continuación, haga clic en **base de datos**, lo que se abre el **Restaurar base de datos** cuadro de diálogo.  
  
4.  En la página **General** , use la sección **Origen** para especificar el origen y la ubicación de los conjuntos de copias de seguridad que se deben restaurar. Seleccione una de las siguientes opciones:  
  
    -   **Base de datos**  
  
         Seleccione la base de datos que desea restaurar en la lista desplegable. La lista solo contiene las bases de datos de las que se han realizado copias de seguridad de acuerdo con el historial de copias de seguridad de **msdb** .  
  
    > [!NOTE]  
    >  Si la copia de seguridad se toma desde un servidor diferente, el servidor de destino no tendrá la información del historial de copia de seguridad de la base de datos especificada. En este caso, seleccione **Dispositivo** para especificar manualmente el archivo o dispositivo que se va a restaurar.  
  
    -   **Dispositivo**  
  
         Haga clic en el botón de exploración (**...**) para abrir el cuadro de diálogo **Seleccionar dispositivos de copia de seguridad** . En el cuadro **Tipo de medio de copia de seguridad** , seleccione uno de los tipos de dispositivo. Para seleccionar uno o varios dispositivos del cuadro **Medio de copia de seguridad** , haga clic en **Agregar**.  
  
         Después de agregar los dispositivos que desee al cuadro de lista **Medio de copia de seguridad** , haga clic en **Aceptar** para volver a la página **General** .  
  
         En el cuadro de lista **Origen: Dispositivo: Base de datos**, seleccione el nombre de la base de datos que se debe restaurar.  
  
        > [!NOTE]  
        >  Esta lista solo está disponible cuando se selecciona la opción **Dispositivo** . Solo estarán disponibles las bases de datos que tienen copias de seguridad en el dispositivo seleccionado.  
  
         **Medios de copia de seguridad**  
         Seleccione el medio de la operación de restauración: **Archivo**, **cinta**, **URL**o **dispositivo de copia de seguridad**. La opción **Cinta** solo aparece si se ha montado una unidad de cinta en el sistema; la opción **Dispositivo de copia de seguridad** aparece únicamente si existe al menos un dispositivo de copia de seguridad.  
  
         **Ubicación de copia de seguridad**  
         Consulte, agregue o quite medios de la operación de restauración. La lista puede contener un máximo de 64 archivos, cintas o dispositivos de copia de seguridad.  
  
         **Agregar**  
         Agrega la ubicación de un dispositivo de copia de seguridad para el **ubicación de copia de seguridad** lista. En función del tipo de medio que seleccione en el campo **Medio para copia de seguridad** , al hacer clic en **Agregar** , se abrirá uno de los siguientes cuadros de diálogo.  
  
        |Tipo de medio|Cuadro de diálogo|Descripción|  
        |----------------|----------------|-----------------|  
        |**Archivo**|**Buscar archivo de copia de seguridad**|En este cuadro de diálogo, puede seleccionar un archivo local en el árbol, o bien especificar un archivo remoto mediante su nombre UNC (convención de nomenclatura universal) completo. Para obtener más información, vea [Dispositivos de copia de seguridad &#40;SQL Server&#41;](backup-devices-sql-server.md).|  
        |**Device**|**Seleccionar dispositivo de copia de seguridad**|En este cuadro de diálogo, puede seleccionar un dispositivo de una lista de dispositivos lógicos de copia de seguridad en la instancia del servidor.|  
        |**Cinta**|**Seleccionar cinta de copia de seguridad**|En este cuadro de diálogo, puede seleccionar una cinta de la lista de unidades de cinta que están conectadas físicamente al equipo en el que se ejecuta la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
        |**Dirección URL**|De esta forma se inician dos cuadros de diálogo en el siguiente orden:<br /><br /> 1) **conectarse a Windows Azure Storage**<br /><br /> 2) **Buscar archivo de copia de seguridad en Windows Azure**|En el cuadro de diálogo **Conectar con Almacenamiento de Windows Azure**  , seleccione una credencial existente de SQL que almacena la información del nombre de cuenta y de tecla de acceso de Almacenamiento de Windows Azure, o cree la nueva credencial de SQL especificando el nombre de cuenta de almacenamiento y la información de las teclas de acceso de almacenamiento. Para obtener más información, consulte [conectar a Windows Azure Storage &#40;restaurar&#41;](connect-to-microsoft-azure-storage-restore.md).<br /><br /> En el cuadro de diálogo **Buscar archivo de copia de seguridad** , puede seleccionar un archivo de la lista de contenedores mostrados en el marco de la izquierda.|  
  
         Si la lista está completa, el botón **Agregar** no está disponible.  
  
         **Quitar**  
         Quita uno o varios archivos, cintas o dispositivos lógicos de copia de seguridad seleccionados.  
  
         **Contenido**  
         Muestra el contenido de los medios de un archivo, una cinta o un dispositivo lógico de copia de seguridad seleccionado.  
  
5.  En la sección **Destino** , el cuadro **Base de datos** se rellena automáticamente con el nombre de la base de datos que se va a restaurar. Para cambiar el nombre de la base de datos, especifique el nuevo nombre en el cuadro **Base de datos** .  
  
6.  En el cuadro **Restaurar en** , deje el valor predeterminado **A la última copia de seguridad tomada** o haga clic en **Escala de tiempo** para acceder al cuadro de diálogo **Escala de tiempo de copia de seguridad** para seleccionar manualmente un momento a fin de que se detenga la acción de recuperación. Para obtener más información acerca de cómo designar un momento específico, vea [Backup Timeline](backup-timeline.md).  
  
7.  En la cuadrícula **Conjuntos de copia de seguridad que se van a restaurar** , seleccione las copias de seguridad que desea restaurar. En esta cuadrícula se muestran las copias de seguridad disponibles en la ubicación especificada. De forma predeterminada, se sugiere un plan de recuperación. Para anular el plan de recuperación sugerido, puede cambiar las selecciones de la cuadrícula. Se anula automáticamente la selección de las copias de seguridad que dependen de la restauración de una copia de seguridad anterior cuando se anula la selección de una copia de seguridad anterior. Para obtener información sobre las columnas de la cuadrícula **Conjuntos de copia de seguridad que se van a restaurar** , vea [Restaurar la base de datos &#40;página General&#41;](../../integration-services/general-page-of-integration-services-designers-options.md)).  
  
8.  Si lo desea, haga clic en **Archivos** en el recuadro **Seleccionar una página** para obtener acceso al cuadro de diálogo **Archivos** . A partir de aquí, puede restaurar la base de datos a una nueva ubicación si especifica un nuevo destino de restauración para cada archivo de la cuadrícula **Restaurar los archivos de base de datos como** . Para obtener más información sobre esta cuadrícula, vea [Restaurar base de datos &#40;página Archivos&#41;](restore-database-files-page.md).  
  
9. Para ver o seleccionar las opciones avanzadas, en la página **Opciones** , en el panel **Opciones de restauración** , puede seleccionar cualquiera de las opciones siguientes si son apropiadas para su situación:  
  
    1.  Opciones `WITH` (no necesarias):  
  
        -   **Sobrescribir la base de datos existente (WITH REPLACE)**  
  
        -   **Conservar la configuración de replicación (WITH KEEP_REPLICATION)**  
  
        -   **Restringir el acceso a la base de datos restaurada (WITH RESTRICTED_USER)**  
  
    2.  Seleccione una opción en el cuadro **Estado de recuperación** . Este cuadro determina el estado de la base de datos después de la operación de restauración.  
  
        -   **RESTORE WITH RECOVERY** es el comportamiento predeterminado que deja la base de datos lista para usarse mediante la reversión de las transacciones no confirmadas. No pueden restaurarse registros de transacciones adicionales. Seleccione esta opción si va a restaurar ahora todas las copias de seguridad necesarias.  
  
        -   **RESTORE WITH NORECOVERY** deja la base de datos no operativa y no revierte las transacciones no confirmadas. Pueden restaurarse registros de transacciones adicionales. La base de datos no puede se usar hasta que se recupera.  
  
        -   **RESTORE WITH STANDBY** deja la base de datos en modo de solo lectura. Deshace las transacciones sin confirmar, pero guarda las acciones de deshacer en un archivo en espera para que los efectos de la recuperación puedan revertirse.  
  
    3.  **Realizar copia del final del registro de la cola antes de la restauración** se seleccionará si es necesario en el momento dado que ha seleccionado. No es necesario modificar este valor, pero puede optar por realizar la copia del final del registro incluso si no es necesario. ¿Un nombre de archivo aquí? Si el primer conjunto de copia de seguridad de la página **General** está en Windows Azure, el registro de cola también se copia en el mismo contenedor de almacenamiento.  
  
    4.  Puede haber errores en las operaciones de restauración si hay conexiones activas con la base de datos. Active la opción **Cerrar conexiones existentes** para asegurarse de que se cierren todas las conexiones activas entre [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] y la base de datos. Esta casilla establece la base de datos en modo de usuario único antes de realizar las operaciones de restauración, y establece la base de datos en modo multiusuario una vez completadas.  
  
    5.  Seleccione **Preguntar antes de restaurar cada copia de seguridad** si desea que se le pregunte en cada operación de restauración. No suele ser necesario a menos que la base de datos sea grande y desee supervisar el estado de la operación de restauración.  
  
     Para obtener más información sobre estas opciones de restauración, vea [Restaurar base de datos &#40;página Opciones&#41;](restore-database-options-page.md)).  
  
10. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Vea también  
 [Realizar copia de seguridad de un registro de transacciones &#40;SQL Server&#41;](back-up-a-transaction-log-sql-server.md)   
 [Crear una copia de seguridad completa de base de datos &#40;SQL Server&#41;](create-a-full-database-backup-sql-server.md)   
 [Restaurar una base de datos a una nueva ubicación &#40;SQL Server&#41;](restore-a-database-to-a-new-location-sql-server.md)   
 [Restaurar una copia de seguridad del registro de transacciones &#40;SQL Server&#41;](restore-a-transaction-log-backup-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [Restaurar base de datos &#40;página Opciones&#41;](restore-database-options-page.md)   
 [Restaurar la base de datos &#40;página General&#41;](../../integration-services/general-page-of-integration-services-designers-options.md)  
  
  
