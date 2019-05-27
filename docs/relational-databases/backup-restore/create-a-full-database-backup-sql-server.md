---
title: Creación de una copia de seguridad completa de base de datos (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql
ms.prod_service: backup-restore
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
ms.openlocfilehash: 4529593459248b6cf0777019147ced855fc1c4fa
ms.sourcegitcommit: 8d288ca178e30549d793c40510c4e1988130afb0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/16/2019
ms.locfileid: "65801372"
---
# <a name="create-a-full-database-backup-sql-server"></a>Crear una copia de seguridad completa de base de datos (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
 > Para SQL Server 2014, vaya a [Crear una copia de seguridad completa de base de datos (SQL Server)](create-a-full-database-backup-sql-server.md).

  En este tema se explica cómo crear una copia de seguridad completa de la base de datos en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)]o PowerShell.  
  
>  Para obtener información sobre la copia de seguridad de SQL Server en el servicio de Windows Azure Blob storage, vea [SQL Server Backup and Restore with Microsoft Azure Blob Storage Service (Copia de seguridad y restauración de SQL Server con el servicio de Microsoft Azure Blob Storage)](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md) y [Copia de seguridad en URL de SQL Server](../../relational-databases/backup-restore/sql-server-backup-to-url.md).  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar 
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   La instrucción BACKUP no se permite en una transacción explícita o implícita.  
  
-   Las copias de seguridad que se crean en una versión más reciente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no se pueden restaurar en versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Para obtener información general, pero también especializada, sobre los conceptos y las tareas de las copias de seguridad, consulte [Información general de copia de seguridad &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md) antes de comenzar.  
  
###  <a name="Recommendations"></a> Recomendaciones  
  
-   A medida que la base de datos aumenta de tamaño, las copias de seguridad completas requieren una mayor cantidad de tiempo para finalizar y espacio de almacenamiento. En el caso de una base de datos grande, considere la posibilidad de complementar una copia de seguridad completa con una serie de [copias de seguridad diferenciales](../../relational-databases/backup-restore/differential-backups-sql-server.md). Para más información, consulte [SQL Server Backup to URL](../../relational-databases/backup-restore/sql-server-backup-to-url.md).  
  
-   Calcule el tamaño de una copia de seguridad completa de la base de datos mediante el procedimiento almacenado del sistema [sp_spaceused](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md) .  
  
-   De forma predeterminada, cada operación de copia de seguridad correcta agrega una entrada en el registro de errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y en el registro de eventos del sistema. Si realiza copias de seguridad con frecuencia, estos mensajes de aprobación se acumularán rápidamente, lo que dará lugar a enormes registros de errores. Esto puede dificultar la búsqueda de otros mensajes. En esos casos, puede suprimir estas entradas de registro de copia de seguridad con la marca de seguimiento 3226 si ninguno de los scripts depende de ellas. Para obtener más información, vea [Marcas de seguimiento &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md).  
  
###  <a name="Security"></a> Seguridad  
 TRUSTWORTHY se establece en OFF en una copia de seguridad de base de datos. Para obtener información sobre cómo establecer TRUSTWORTHY en ON, vea [Opciones de ALTER DATABASE SET &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md).  
  
 A partir de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] las opciones **PASSWORD** y **MEDIAPASSWORD** no se pueden utilizar para crear copias de seguridad. Todavía puede restaurar las copias de seguridad creadas con contraseñas.  
  
####  <a name="Permissions"></a> Permisos  
 De forma predeterminada, los permisos BACKUP DATABASE y BACKUP LOG corresponden a los miembros del rol fijo de servidor **sysadmin** y de los roles fijos de base de datos **db_owner** y **db_backupoperator** .  
  
 Los problemas de propiedad y permisos del archivo físico del dispositivo de copia de seguridad pueden interferir con una operación de copia de seguridad. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe poder leer y escribir en el dispositivo y la cuenta en la que se ejecuta el servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **debe** tener permisos de escritura. En cambio, [sp_addumpdevice](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md), que agrega una entrada para un dispositivo de copia de seguridad en las tablas del sistema, no comprueba los permisos de acceso a los archivos. Es posible que estos problemas con el archivo físico del dispositivo de copia de seguridad no aparezcan hasta que se tenga acceso al recurso físico, al intentar la copia de seguridad o la restauración.  
  
##  <a name="SSMSProcedure"></a> Uso de SQL Server Management Studio  
  
>  Al especificar una tarea de copia de seguridad mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], puede generar el script [!INCLUDE[tsql](../../includes/tsql-md.md)] [BACKUP](../../t-sql/statements/backup-transact-sql.md) script by clicking the **Script** button and selecting a script destination.  
  
### <a name="back-up-a-database"></a>Realizar una copia de seguridad de una base de datos  
  
1.  Después de conectarse a la instancia apropiada de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], en el **Explorador de objetos**, haga clic en el nombre del servidor para expandir el árbol correspondiente.  
  
2.  Expanda **Bases de datos**y seleccione la base de datos de un usuario o expanda **Bases de datos del sistema** y seleccione una base de datos del sistema.  
  
3.  Haga clic con el botón derecho en la base de datos, seleccione **Tareas**y haga clic en **Copia de seguridad**. Aparece el cuadro de diálogo **Copia de seguridad de base de datos** .  

  #### <a name="general-page"></a>**Página General**
  
4.  En la lista desplegable **Base de datos** , compruebe el nombre de la base de datos. También puede seleccionar otra base de datos en la lista.  
  
5.  El cuadro de texto **Modelo de recuperación** es solo para referencia.  Puede realizar una copia de seguridad de la base de datos en cualquier modelo de recuperación (**FULL**, **BULK_LOGGED**o **SIMPLE**).  
  
6.  En la lista desplegable **Tipo de copia de seguridad** , seleccione **Completo**.  
  
     Tenga en cuenta que después de crear una copia de seguridad completa de la base de datos, puede crear una copia de seguridad diferencial; para obtener más información, vea [Crear una copia de seguridad diferencial de una base de datos &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-differential-database-backup-sql-server.md).  
  
7.  También puede activar la casilla **Copia de seguridad de solo copia** para crear una copia de seguridad de solo copia. Una *copia de seguridad de solo copia* es una copia de seguridad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] independiente de la secuencia de copias de seguridad convencionales de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información, vea [Copias de seguridad de solo copia &#40;SQL Server&#41;](../../relational-databases/backup-restore/copy-only-backups-sql-server.md).  Una copia de seguridad de solo copia no está disponible para el tipo de copia de seguridad **Diferencial**.  

8.  En **Componente de copia de seguridad**, seleccione el botón de radio **Base de datos** .  
  
9. En la sección **Destino** , use la lista desplegable **Copia de seguridad en** para seleccionar el destino de la copia de seguridad. Haga clic en **Agregar** para agregar objetos o destinos de copia de seguridad adicionales.
  
     Para eliminar un destino de copia de seguridad, selecciónelo y haga clic en **Quitar**. Para ver el contenido de un destino de copia de seguridad existente, selecciónelo y haga clic en **Contenido**.  

  #### <a name="media-options-page"></a>**Página Opciones de medios**  
10. Para ver o seleccionar las opciones multimedia, haga clic en **Opciones multimedia** en el panel **Seleccionar una página** .   
    
11. Seleccione una opción de **Sobrescribir medios** ; para ello, haga clic en una de las opciones siguientes: 

    > [!IMPORTANT]  
    >  La opción **Sobrescribir medios** está deshabilitada si seleccionó **Dirección URL** como destino de la copia de seguridad en la página **General**. Para obtener más información, vea [Copia de seguridad de la base de datos &#40;página Opciones multimedia&#41;](../../relational-databases/backup-restore/back-up-database-media-options-page.md).  


  -   **Hacer copia de seguridad en el conjunto de medios existente**  
  
      > [!IMPORTANT]  
      >  Si piensa usar cifrado, no seleccione esta opción. Si selecciona esta opción, las opciones de cifrado de la página **Opciones de copia de seguridad** estarán deshabilitadas. No se admite el cifrado al anexar al conjunto de copia de seguridad existente.  
  
         Para esta opción, haga clic en **Anexar al conjunto de copia de seguridad existente** o **Sobrescribir todos los conjuntos de copia de seguridad existentes**. Para obtener más información, vea [Conjuntos de medios, familias de medios y conjuntos de copias de seguridad &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md).  
  
         Opcionalmente, seleccione **Comprobar nombre de conjunto de medios y fecha de expiración del conjunto de copia de seguridad** para que la operación de copia de seguridad compruebe la fecha y la hora en que expiran el conjunto de medios y el conjunto de copia de seguridad.  
  
         También puede escribir un nombre en el cuadro de texto **Nombre del conjunto de medios** . Si no especifica ningún nombre, se creará un conjunto de medios con un nombre en blanco. Si especifica un nombre para el conjunto, los medios (cinta o disco) se comprueban para ver si el nombre real coincide con el nombre especificado aquí.  
  
-   **Hacer copia de seguridad en un nuevo conjunto de medios y borrar todos los conjuntos de copia de seguridad existentes**  
  
    Para esta opción, especifique un nombre en el cuadro de texto **Nuevo nombre del conjunto de medios** y, si lo desea, describa el conjunto de medios en el cuadro de texto **Nueva descripción del conjunto de medios** .  
  
14. Opcionalmente, en la sección **Confiabilidad** , seleccione:  
  
    -   **Comprobar copia de seguridad al finalizar**.  
  
    -   **Realizar suma de comprobación antes de escribir en los medios**.  Para obtener más información sobre las sumas de comprobación, vea [Errores posibles de medios durante copia de seguridad y restauración &#40;SQL Server&#41;](../../relational-databases/backup-restore/possible-media-errors-during-backup-and-restore-sql-server.md).  
    
    -   **Continuar después de un error**. 

15. La sección **Registro de transacciones** se encuentra inactiva salvo que vaya a realizar una copia de seguridad de un registro de transacciones (según se haya especificado en la sección **Tipo de copia de seguridad** de la página **General** ).  
      
16. En la sección **Unidad de cinta** , la opción **Descargar la cinta después de realizar la copia de seguridad** está activa si va a realizar una copia de seguridad en una unidad de cinta (según se haya especificado en la sección **Destino** de la página **General** ). Al hacer clic en esta opción se activa la opción **Rebobinar la cinta antes de descargar** .   

  #### <a name="backup-options-page"></a>**Página Opciones de copia de seguridad**  

17. Para ver o seleccionar las opciones de copia de seguridad, haga clic en **Opciones de copia de seguridad** en el panel **Seleccionar una página** .  
  
18. En el cuadro de texto **Nombre** , acepte el nombre del conjunto de copia de seguridad predeterminado o escriba otro nombre para el conjunto de copia de seguridad.  
  
19. En el cuadro de texto **Descripción** , también puede escribir una descripción del conjunto de copia de seguridad.  
  
20. Especifique cuándo expirará el conjunto de copia de seguridad y se podrá sobrescribir sin omitir explícitamente la comprobación de los datos de expiración:  
  
    -   Para que el conjunto de copia de seguridad expire al cabo de un número de días específico, haga clic en **Después de** (opción predeterminada) y escriba el número de días tras la creación del conjunto en que este expirará. Este valor puede estar entre 0 y 99999 días; el valor 0 significa que el conjunto de copia de seguridad no expirará nunca.  
  
         El valor predeterminado se establece en la opción **Tiempo predeterminado de retención de medios de copia de seguridad (días)** del cuadro de diálogo **Propiedades del servidor** (página Configuración de base de datos). Para acceder a esta opción, en el Explorador de objetos, haga clic con el botón derecho en el nombre del servidor y seleccione Propiedades; después, seleccione la página **Configuración de base de datos** .  
  
    -   Para que el conjunto de copia de seguridad expire en una determinada fecha, haga clic en **El**y escriba la fecha en la que expirará.  
  
         Para obtener más información sobre las fechas de expiración de la copia de seguridad, vea [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md).  
  
21. En la sección **Compresión** , use la lista desplegable **Establecer la compresión de copia de seguridad** para seleccionar el nivel de compresión que desea.  [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] y las versiones posteriores admiten la [compresión de copia de seguridad](../../relational-databases/backup-restore/backup-compression-sql-server.md). De forma predeterminada, el hecho de que se comprima una copia de seguridad depende del valor de la opción de configuración del servidor **backup-compression default** . Pero, independientemente del valor predeterminado actual de nivel de servidor, puede comprimir una copia de seguridad si activa **Comprimir copia de seguridad**e impedir la compresión si activa **No comprimir copia de seguridad**.  
  
     Para más información sobre la configuración de la compresión de copia de seguridad, consulte [Ver o establecer la opción de configuración del servidor de compresión de copia de seguridad predeterminada](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md).  
  
22. En la sección **Cifrado** , use la casilla **Cifrar copia de seguridad** para decidir si usar el cifrado en la copia de seguridad. Use la lista desplegable **Algoritmo** para seleccionar un algoritmo de cifrado.  Use la lista desplegable **Certificado o clave asimétrica** para seleccionar un certificado o una clase asimétrica existente. El cifrado se admite en SQL Server 2014 o posterior. Para obtener más detalles sobre las opciones de cifrado, vea [Copia de seguridad de la base de datos &#40;página Opciones de copia de seguridad&#41;](../../relational-databases/backup-restore/back-up-database-backup-options-page.md).  
  
  
Puede usar el [Asistente para planes de mantenimiento](../maintenance-plans/use-the-maintenance-plan-wizard.md) para crear copias de seguridad de base de datos. 

### <a name="examples"></a>Ejemplos  
#### <a name="a--full-back-up-to-disk-to-default-location"></a>**A.  Crear copia de seguridad completa en disco en una ubicación predeterminada**
En este ejemplo, se creará una copia de seguridad de la base de datos `Sales` en disco en la ubicación de copia de seguridad predeterminada.  Nunca se ha creado una copia de seguridad de `Sales` .
1.  En el **Explorador de objetos**, conéctese a una instancia del Motor de base de datos de SQL Server y expándala.

2.  Expanda **Bases de datos**, haga clic con el botón derecho en `Sales`, seleccione **Tareas**y, luego, haga clic en **Copia de seguridad...**

3.  Haga clic en **Aceptar**.

#### <a name="b--full-back-up-to-disk-to-non-default-location"></a>**B.  Crear copia de seguridad completa en disco en una ubicación no predeterminada**
En este ejemplo, se creará una copia de seguridad de la base de datos `Sales` en disco en `E:\MSSQL\BAK`.  Se han creado copias de seguridad de `Sales` anteriores.
1.  En el **Explorador de objetos**, conéctese a una instancia del Motor de base de datos de SQL Server y expándala.

2.  Expanda **Bases de datos**, haga clic con el botón derecho en `Sales`, seleccione **Tareas**y, luego, haga clic en **Copia de seguridad...**

3.  En la página **General** , en la sección **Destino** , seleccione **Disco** en la lista desplegable **Copia de seguridad en:** .

4.  Haga clic en **Quitar** hasta que se quiten todos los archivos de copia de seguridad existentes.

5.  Haga clic en **Agregar** y se abrirá el cuadro de diálogo **Seleccionar destino de la copia de seguridad** .

6.  Escriba `E:\MSSQL\BAK\Sales_20160801.bak` en el cuadro de texto **nombre de archivo** .

7.  Haga clic en **Aceptar**.

8.  Haga clic en **Aceptar**.

#### <a name="c--create-an-encrypted-backup"></a>**C.  Crear una copia de seguridad cifrada**
En este ejemplo, se creará una copia de seguridad de la base de datos `Sales` con cifrado en la ubicación de copia de seguridad predeterminada.  Ya se creó una  [**clave maestra de base de datos**](../../relational-databases/security/encryption/create-a-database-master-key.md) .  Ya se creó un  [**certificado**](../../t-sql/statements/create-certificate-transact-sql.md) con el nombre `MyCertificate`. Puede ver un ejemplo T-SQL de cómo crear una **clave maestra de base de datos** y un **certificado** en [Crear una copia de seguridad cifrada](../../relational-databases/backup-restore/create-an-encrypted-backup.md).  
1.  En el **Explorador de objetos**, conéctese a una instancia del Motor de base de datos de SQL Server y expándala.

2.  Expanda **Bases de datos**, haga clic con el botón derecho en `Sales`, seleccione **Tareas**y, luego, haga clic en **Copia de seguridad...**

3.  En la página **Opciones de medios** , en la sección **Sobrescribir medios** , seleccione **Hacer copia de seguridad en un nuevo conjunto de medios y borrar todos los conjuntos de copia de seguridad existentes**.

4.  En la página **Opciones de copia de seguridad** , en la sección **Cifrado** , active la casilla **Cifrar copia de seguridad** .

5.  En la lista desplegable **Algoritmo** , seleccione **AES 256**.

6.  En la lista desplegable **Certificado o clave asimétrica** , seleccione `MyCertificate`.

7.  Haga clic en **Aceptar**.

#### <a name="d--back-up-to-the-azure-blob-storage-service"></a>**D.  Copia de seguridad en el servicio de Azure Blob Storage**
#### <a name="common-steps"></a>**Pasos comunes**  
Los tres ejemplos siguientes realizan una copia de seguridad completa de la base de datos `Sales` en el servicio de almacenamiento de blobs de Microsoft Azure.  El nombre de la cuenta de almacenamiento es `mystorageaccount`.  El contenedor se denomina `myfirstcontainer`.  Por motivos de brevedad, los cuatro primeros pasos se enumeran aquí una vez y todos los ejemplos se iniciarán en el **paso 5**.
1.  En el **Explorador de objetos**, conéctese a una instancia del Motor de base de datos de SQL Server y expándala.

2.  Expanda **Bases de datos**, haga clic con el botón derecho en `Sales`, seleccione **Tareas**y, luego, haga clic en **Copia de seguridad...**

3.  En la página **General** de la sección **Destino** , seleccione **URL** en la lista desplegable **Copia de seguridad en:** .

4.  Haga clic en **Agregar** y se abrirá el cuadro de diálogo **Seleccionar destino de la copia de seguridad** .

    **D1.  Ya existen una copia de seguridad distribuida en URL y una credencial de SQL Server**  
Se ha creado una directiva de acceso almacenada con derechos de lectura, escritura y lista.  La credencial de SQL Server, `https://mystorageaccount.blob.core.windows.net/myfirstcontainer`, se creó con una firma de acceso compartido asociada a la directiva de acceso almacenada.  
*
    5.  Seleccione `https://mystorageaccount.blob.core.windows.net/myfirstcontainer` en el cuadro de texto **Contenedor de almacenamiento de Azure** .

   6.  En el cuadro de texto **Archivo de copia de seguridad** , escriba `Sales_stripe1of2_20160601.bak`.

   7.  Haga clic en **Aceptar**.

   8.  Repita los pasos **4** y **5**.

   9.  En el cuadro de texto **Archivo de copia de seguridad** , escriba `Sales_stripe2of2_20160601.bak`.

   10.  Haga clic en **Aceptar**.

   11.   Haga clic en **Aceptar**.

   **D2.  Existe una firma de acceso compartido pero no una credencial de SQL Server**
  5.    Escriba `https://mystorageaccount.blob.core.windows.net/myfirstcontainer` en el cuadro de texto **Contenedor de almacenamiento de Azure** .
  
  6.    Escriba la firma de acceso compartido en el cuadro de texto **Directiva de acceso compartido** .
  
  7.    Haga clic en **Aceptar**.
  
  8.    Haga clic en **Aceptar**.

   **D3.  No existe ninguna firma de acceso compartido**
  5.    Haga clic en el botón **Nuevo contenedor** y se abrirá el cuadro de diálogo **Conectarse a una suscripción de Microsoft** .  
  
  6.    Complete el cuadro de diálogo **Conectarse a una suscripción de Microsoft** y haga clic en **Aceptar** para volver al cuadro de diálogo **Seleccionar destino de la copia de seguridad** .  Vea [Connect to a Microsoft Azure Subscription (Conectarse a una suscripción de Microsoft Azure)](../../relational-databases/backup-restore/connect-to-a-microsoft-azure-subscription.md) para obtener más información.
  
  7.    Haga clic en **Aceptar** en el cuadro de diálogo **Seleccionar destino de la copia de seguridad** .
  
  8.    Haga clic en **Aceptar**.

  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
### <a name="create-a-full-database-backup"></a>Crear una copia de seguridad completa de base de datos  
  
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
    |*backup_device* [ **,** ...*n* ]|Especifica una lista de 1 a 64 dispositivos de copia de seguridad que se pueden utilizar en la operación de copia de seguridad. Puede especificar un dispositivo físico de copia de seguridad o puede especificar un dispositivo de copia de seguridad lógico correspondiente, si ya se definió. Para especificar un dispositivo de copia de seguridad físico, use la opción DISK o TAPE:<br /><br /> { DISK &#124; TAPE } **=**_nombre\_dispositivo\_copia de seguridad\_física_<br /><br /> Para obtener más información, vea [Dispositivos de copia de seguridad &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md).|  
    |WITH *with_options* [ **,** ...*o* ]|De forma opcional, puede especificar una o varias opciones, *o*. Para obtener información sobre algunas de las opciones de WITH básicas, vea el paso 2.|  
  
2.  Opcionalmente, especifique una o varias opciones de WITH. A continuación se describen algunas de las opciones de WITH básicas. Para obtener información sobre todas las opciones de WITH, vea [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md).  
  
    -   Opciones de WITH básicas del conjunto de copia de seguridad:  
  
         { COMPRESSION | NO_COMPRESSION }  
         En [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] y versiones posteriores únicamente, especifica si la [compresión de copia de seguridad](../../relational-databases/backup-restore/backup-compression-sql-server.md) se realiza en esta copia de seguridad, lo que invalida la configuración predeterminada del servidor.  
  
         ENCRYPTION (ALGORITHM, SERVER CERTIFICATE |ASYMMETRIC KEY)  
         En SQL Server 2014 o versiones posteriores únicamente, especifica el algoritmo de cifrado que se va a utilizar y el certificado o la clave asimétrica que se va a usar para proteger el cifrado.  
  
         DESCRIPTION **=** { **'** _text_ **'**  |  **@** _text\_variable_ }  
         Especifica el texto sin formato que describe el conjunto de copia de seguridad. La cadena puede tener un máximo de 255 caracteres.  
  
         NAME **=** { *nombre conjunto_copia_seguridad* |  **@** _variable\_nombre\_conjunto\_copia de seguridad_ }  
         Especifica el nombre del conjunto de copia de seguridad. Los nombres pueden tener un máximo de 128 caracteres. Si no se especifica NAME, está en blanco.  
  
    -   Opciones de WITH básicas del conjunto de copia de seguridad:  
  
         De forma predeterminada, BACKUP DATABASE anexa la copia de seguridad a un conjunto de medios existente, conservando los conjuntos de copia de seguridad existentes. Para especificar esto explícitamente, utilice la opción NOINIT. Para obtener información sobre la anexión a conjuntos de copia de seguridad existentes, vea [Conjuntos de medios, familias de medios y conjuntos de copias de seguridad &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md).  
  
         Opcionalmente, para dar formato a los medios de copia de seguridad, utilice la opción FORMAT:  
  
         FORMAT [ **,** MEDIANAME**=** { *media_name* |  **@** _media\_name\_variable_ } ] [ **,** MEDIADESCRIPTION **=** { *text* |  **@** _text\_variable_ } ]  
         Utilice la cláusula FORMAT cuando emplee los medios por primera vez o cuando desee sobrescribir todos los datos existentes. De manera opcional, puede asignar a los nuevos medios un nombre y una descripción.  
  
        > [!IMPORTANT]  
        >  Tenga mucho cuidado cuando utilice la cláusula FORMAT de la instrucción BACKUP, ya que destruye cualquier copia de seguridad existente en el medio de copia de seguridad.  
  
###  <a name="TsqlExample"></a> Ejemplos (Transact-SQL)  
  
#### <a name="a-back-up-to-a-disk-device"></a>**A. Realizar la copia de seguridad en un dispositivo de disco**  
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
  
#### <a name="b-back-up-to-a-tape-device"></a>**B. Realizar la copia de seguridad en un dispositivo de cinta**  
 En este ejemplo se realiza una copia de seguridad en cinta de la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] completa y se anexa a las copias de seguridad anteriores.  
  
```sql  
USE AdventureWorks2012;  
GO  
BACKUP DATABASE AdventureWorks2012  
   TO TAPE = '\\.\Tape0'  
   WITH NOINIT,  
      NAME = 'Full Backup of AdventureWorks2012';  
GO  
```  
  
#### <a name="c-back-up-to-a-logical-tape-device"></a>**C. Realizar la copia de seguridad en un dispositivo de cinta lógico**  
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
Use el cmdlet **Backup-SqlDatabase** . Para indicar explícitamente que esta es una copia de seguridad completa de la base de datos, especifique el parámetro **-BackupAction**  con su valor predeterminado, **Database**. Este parámetro es opcional para las copias de seguridad de base de datos completas.  

### <a name="examples"></a>Ejemplos
#### <a name="a--full-local-backup"></a>**A.  Copia de seguridad local completa**  
En el ejemplo siguiente se crea una copia de seguridad completa de la base de datos `MyDB` en la ubicación de copia de seguridad predeterminada de la instancia de servidor `Computer\Instance`. Opcionalmente, en este ejemplo se especifica **-BackupAction Database**.  
```powershell 
Backup-SqlDatabase -ServerInstance Computer\Instance -Database MyDB -BackupAction Database  
```
 
#### <a name="b--full-backup-to-microsoft-azure"></a>**B.  Copia de seguridad completa en Microsoft Azure**  
En el ejemplo siguiente se crea una copia de seguridad completa de la base de datos `Sales` de la instancia de `MyServer` en el servicio de almacenamiento de blobs de Microsoft Azure.  Se ha creado una directiva de acceso almacenada con derechos de lectura, escritura y lista.  La credencial de SQL Server, `https://mystorageaccount.blob.core.windows.net/myfirstcontainer`, se creó con una firma de acceso compartido asociada a la directiva de acceso almacenada.  El comando de PowerShell usa el parámetro **BackupFile** para especificar la ubicación (dirección URL) y el nombre del archivo de copia de seguridad.

```powershell  
import-module sqlps;
$container = 'https://mystorageaccount.blob.core.windows.net/myfirstcontainer';
$FileName = 'Sales.bak';
$database = 'Sales';
$BackupFile = $container + '/' + $FileName ;
  
Backup-SqlDatabase -ServerInstance "MyServer" -Database $database -BackupFile $BackupFile;
```
 
 **Para configurar y usar el proveedor de SQL Server PowerShell**  
  
-   [Proveedor de SQL Server PowerShell Provider](../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
  
-   [Realizar una copia de seguridad de una base de datos (SQL Server)](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)  
  
-   [Crear una copia de seguridad diferencial de una base de datos &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-differential-database-backup-sql-server.md)  
  
-   [Restore a Database Backup Using SSMS](../../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)  
  
-   [Restaurar una copia de seguridad de base de datos en el modelo de recuperación simple &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/restore-a-database-backup-under-the-simple-recovery-model-transact-sql.md)  
  
-   [Restaurar una base de datos según el punto de error en el modelo de recuperación completa &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/restore-database-to-point-of-failure-full-recovery.md)  
  
-   [Restaurar una base de datos a una nueva ubicación &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-database-to-a-new-location-sql-server.md)  
  
-   [Usar el Asistente para planes de mantenimiento](../../relational-databases/maintenance-plans/use-the-maintenance-plan-wizard.md)  
  
## <a name="see-also"></a>Vea también  
**[Solución de problemas de SQL Server de backup y restore de las operaciones](https://support.microsoft.com/kb/224071)**          
[Información general de copia de seguridad &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)   
 [Copias de seguridad del registro de transacciones &#40;SQL Server&#41;](../../relational-databases/backup-restore/transaction-log-backups-sql-server.md)   
 [Conjuntos de medios, familias de medios y conjuntos de copias de seguridad &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)   
 [sp_addumpdevice &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md)   
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [Copia de seguridad de base de datos &#40;página General&#41;](../../relational-databases/backup-restore/back-up-database-general-page.md)   
 [Copia de seguridad de la base de datos &#40;página Opciones de copia de seguridad&#41;](../../relational-databases/backup-restore/back-up-database-backup-options-page.md)   
 [Copias de seguridad diferenciales &#40;SQL Server&#41;](../../relational-databases/backup-restore/differential-backups-sql-server.md)   
 [Copias de seguridad completas de bases de datos &#40;SQL Server&#41;](../../relational-databases/backup-restore/full-database-backups-sql-server.md)  
  
  
