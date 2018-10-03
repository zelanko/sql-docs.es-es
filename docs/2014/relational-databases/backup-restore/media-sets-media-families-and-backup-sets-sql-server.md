---
title: Conjuntos de medios, familias de medios y conjuntos de copias de seguridad (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- media sets [SQL Server], about media sets
- backup media [SQL Server], about backup media
- backups [SQL Server], media sets
- media sets [SQL Server]
- media headers [SQL Server]
- backup sets [SQL Server], about backup sets
- backup media [SQL Server], media sets
- backups [SQL Server], media families
- backup media [SQL Server], media families
- media families [SQL Server]
- backups [SQL Server], backup sets
- backup sets [SQL Server]
ms.assetid: 2b8f19a2-ee9d-4120-b194-fbcd2076a489
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 13466b4d9d5cc497830906f144e95f044442e318
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48197315"
---
# <a name="media-sets-media-families-and-backup-sets-sql-server"></a>Conjuntos de medios, familias de medios y conjuntos de copias de seguridad (SQL Server)
  En este tema se presenta la terminología básica de medios de copias de seguridad y restauración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y está pensada para lectores noveles de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Este tema describe el formato que usa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para los medios de copia de seguridad, la correspondencia entre los medios y los dispositivos de copia de seguridad, la organización de las copias de seguridad en los medios y varias consideraciones para los conjuntos y las familias de medios. El tema también describe los pasos inicializar o dar formato a los medios de copia de seguridad antes de usarlos por primera vez o reemplazar un conjunto de medios anterior por otro nuevo, cómo sobrescribir los conjuntos de copia de seguridad anteriores en un conjunto de medios y cómo agregar nuevos conjuntos de copia de seguridad a un conjunto de medios.  
  
> [!NOTE]  
>  Para obtener más información sobre la copia de seguridad de SQL Server en el servicio de almacenamiento Blob de Windows Azure, consulte, [SQL Server Backup and Restore with Windows Azure Blob Storage Service](sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md).  
  
  
##  <a name="TermsAndDefinitions"></a> Términos y definiciones  
 conjunto de medios  
 Colección ordenada de medios de copia de seguridad, cintas o archivos de disco en la que se han escrito una o varias operaciones de copia de seguridad mediante un tipo y número fijo de dispositivos de copia de seguridad.  
  
 familia de medios  
 Copias de seguridad creadas en un único dispositivo no reflejado o en un conjunto de dispositivos reflejados en un conjunto de medios.  
  
 conjunto de copia de seguridad  
 Contenido de la copia de seguridad que se agrega a un conjunto de medios mediante una operación de copia de seguridad correcta.  
  
  
##  <a name="OvMediaSetsFamiliesBackupSets"></a> Información general de conjuntos de medios, familias de medios y conjuntos de copia de seguridad  
 Las copias de seguridad de uno o varios medios de copia de seguridad constituyen un conjunto de medios. Un *conjunto de medios* es una colección ordenada de *medios de copia de seguridad*, cintas o archivos de disco, o blobs de Windows Azure en la que se han escrito una o más operaciones de copia de seguridad mediante un tipo y número fijo de dispositivos de copia de seguridad. Un conjunto de medios dado usa unidades de cinta, unidades de disco o blobs de Windows Azure, pero no una combinación de dos o más. Por ejemplo, los dispositivos de copia de seguridad asociados con un conjunto de medios pueden ser tres unidades de cinta denominadas `\\.\TAPE0`, `\\.\TAPE1`y `\\.\TAPE2`. Este conjunto de medios está formado solamente por cintas, empezando con un mínimo de tres (una por unidad). El tipo y número de los dispositivos de copia de seguridad se establece cuando se crea un conjunto de medios y ya no se pueden cambiar. Sin embargo, si es necesario, entre las operaciones de las copias de seguridad y restauración un dispositivo determinado puede sustituirse por un dispositivo del mismo tipo.  
  
 Un conjunto de medios se crea en el medio de copia de seguridad durante una operación de copia de seguridad al dar formato a un medio de copia de seguridad. Para obtener más información, vea [Crear un conjunto de medios](#CreatingMediaSet), más adelante en este tema. Después de dar formato, cada archivo o cinta contiene un encabezado de medios para el conjunto de medios y está listo para recibir el contenido de la copia de seguridad. Con el encabezado adecuado, la operación de copia de seguridad empieza a realizar la copia de seguridad de los datos especificados en los medios de copia de seguridad en todos los dispositivos de copia de seguridad especificados para la operación.  
  
> [!NOTE]  
>  Los conjuntos de medios pueden reflejarse como medida de protección ante posibles daños en el volumen de medios (una cinta o un archivo de disco). Para obtener más información, vea [Mirrored Backup Media Sets &#40;SQL Server&#41;](mirrored-backup-media-sets-sql-server.md).  
  
 [!INCLUDE[ssEnterpriseEd10](../../includes/sskatmai-md.md)] o versiones posteriores pueden leer copias de seguridad comprimidas. Para obtener más información, vea [Compresión de copia de seguridad &#40;SQL Server&#41;](backup-compression-sql-server.md).  
  
  
### <a name="media-families"></a>Familias de medios  
 Las copias de seguridad creadas en un único dispositivo no reflejado o en un conjunto de dispositivos reflejados en un conjunto de medios conforman una *familia de medios*. El número de dispositivos de copia de seguridad utilizados para el conjunto de medios determina el número de familias de medios del conjunto de medios. Por ejemplo, si un conjunto de medios utiliza dos dispositivos de copia de seguridad no reflejados, el conjunto de medios contiene dos familias de medios.  
  
> [!NOTE]  
>  En un conjunto de medios reflejados, cada familia de medios está reflejada. Por ejemplo, si se utilizan seis dispositivos de copia de seguridad para dar formato a un conjunto de medios en el que se usan dos reflejos, habrá tres familias de medios, cada una de ellas formada por dos copias equivalentes de los datos de la copia de seguridad. Para obtener más información sobre los conjuntos de medios reflejados, vea [Conjuntos de medios de copia de seguridad reflejados &#40;SQL Server&#41;](mirrored-backup-media-sets-sql-server.md).  
  
 Cada cinta o disco en una familia de medios tiene asignado un *número de secuencia de medios*. El número de secuencia del medio de un disco siempre es 1. En una familia de medios de cinta, el número de secuencia de la cinta inicial es 1, el número de secuencia de la segunda cinta es 2 y así sucesivamente. Para obtener más información, vea [Usar conjuntos y familias de medios](#ConsiderationsForMediaSetFamilies).  
  
#### <a name="the-media-header"></a>Encabezado de medios  
 Cada volumen de un medio de copia de seguridad (archivo de disco o cinta) contiene un encabezado de medios creado por la primera operación de copia de seguridad que usa la cinta (o disco). Este encabezado permanece intacto hasta que se vuelve a dar formato a los medios.  
  
 El encabezado de medios contiene toda la información necesaria para identificar los medios (archivo de disco o cinta) y reside en la familia de medios a la que pertenece. Esta información incluye:  
  
-   El nombre del medio.  
  
     El nombre del medio es opcional, aunque se recomienda utilizar de forma coherente nombres de medios que identifiquen con claridad los medios. El responsable de dar formato a los medios asigna el nombre a los medios.  
  
-   Número de identificación exclusivo del conjunto de medios.  
  
-   Número de familias de medios en el conjunto de medios.  
  
-   Número de secuencia de la familia de medios que contiene este medio.  
  
-   Número de identificación exclusivo de la familia de medios.  
  
-   Número de secuencia de este medio en la familia de medios. Para un archivo de disco, este valor es siempre 1.  
  
-   Si la descripción del medio contiene una etiqueta de medios MTF o una descripción del medio.  
  
    > [!NOTE]  
    >  Todos los medios que se usan para una operación de copia de seguridad o restauración utilizan un formato estándar de copia de seguridad denominado [!INCLUDE[msCoName](../../includes/ssnoversion-md.md)] conserva cualquier etiqueta de medios MTF escrita por otra aplicación pero no escribe etiquetas de medios MTF.  
  
-   Etiqueta de medios en formato de cinta de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] o descripción del medio (en texto sin formato).  
  
-   Nombre del software de copia de seguridad con que se escribió la etiqueta.  
  
-   Número exclusivo de identificación del proveedor del software que ha dado formato al medio.  
  
-   Fecha y hora en que se escribió la etiqueta.  
  
-   Número de reflejos en cada conjunto (1-4); 1 indica un dispositivo no reflejado.  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] puede procesar medios a los que se ha dado formato mediante versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
### <a name="backup-sets"></a>Conjuntos de copia de seguridad  
 Una operación de copia de seguridad correcta agrega un solo *conjunto de copia de seguridad* al conjunto de medios. El conjunto de copia de seguridad se describe como el conjunto de medios al que pertenece la copia de seguridad. Si el medio de copia de seguridad está compuesto solo por una familia de medios, esa familia contiene todo el conjunto de copia de seguridad. Si el medio de copia de seguridad está compuesto por varias familias de medios, el conjunto de copia de seguridad está distribuido entre ellas. En cada medio, el conjunto de copia de seguridad contiene un encabezado que describe el conjunto de copia de seguridad.  
  
 El ejemplo siguiente se muestra un [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucción que crea un conjunto de medios denominado `MyAdvWorks_MediaSet_1` para el [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] mediante tres unidades de cinta como dispositivos de copia de seguridad de base de datos:  
  
```  
BACKUP DATABASE AdventureWorks2012  
TO TAPE = '\\.\tape0', TAPE = '\\.\tape1', TAPE = '\\.\tape2'  
WITH   
   FORMAT,  
   MEDIANAME = 'MyAdvWorks_MediaSet_1'  
```  
  
 Si es correcta, esta operación de copia de seguridad genera un conjunto de medios nuevo que contiene un nuevo encabezado de medios y un conjunto de copia de seguridad distribuido en tres cintas. En la siguiente ilustración se muestran estos resultados:  
  
 ![Encabezado de medios y primera copia de seguridad establecidos en 3 cintas](../../database-engine/media/bnr-mediaset-new.gif "Encabezado de medios y primera copia de seguridad establecidos en 3 cintas")  
  
 Normalmente, después de la creación de un conjunto de medios, las operaciones de copia de seguridad posteriores adjuntan, una detrás de la otra, sus conjuntos de copia de seguridad al conjunto de medios. Todos los medios utilizados por un conjunto de copia de seguridad constituyen el conjunto de medios, independientemente del número de medios o dispositivos de copia de seguridad utilizados. Los conjuntos de copia de seguridad se enumeran secuencialmente según las posiciones que ocupan en el conjunto de medios, lo que le permite especificar la copia de seguridad que desea restaurar.  
  
 Cada operación de copia de seguridad realizada en un conjunto de medios debe escribirse en el mismo número y tipo de dispositivo de copia de seguridad. Si se utilizan varios dispositivos, como en el primer conjunto de copia de seguridad, el contenido de cada conjunto de copia de seguridad posterior se distribuye entre los medios de copia de seguridad en todos los dispositivos. Para continuar con el ejemplo anterior, una segunda operación de copia de seguridad (una copia de seguridad diferencial) anexa información al mismo conjunto de medios:  
  
```  
BACKUP DATABASE AdventureWorks2012  
TO TAPE = '\\.\tape0', TAPE = '\\.\tape1', TAPE = '\\.\tape2'  
WITH   
   NOINIT,  
   MEDIANAME = 'AdventureWorksMediaSet1',  
   DIFFERENTIAL  
```  
  
> [!NOTE]  
>  La opción NOINIT es el valor predeterminado, pero se incluye para evitar confusiones.  
  
 Si la segunda operación de copia de seguridad es correcta, se escribe un segundo conjunto de copia de seguridad en el conjunto de medios distribuyendo el contenido de la copia de seguridad de la siguiente manera:  
  
 ![El segundo conjunto de copia de seguridad se distribuye entre 3 cintas del conjunto de medios](../../database-engine/media/bnr-mediaset-appendedto.gif "El segundo conjunto de copia de seguridad se distribuye entre 3 cintas del conjunto de medios")  
  
 Al restaurar las copias de seguridad, puede usar la opción FILE para especificar las copias de seguridad que desea usar. En el siguiente ejemplo se muestra el uso de la cláusula FILE **=***número_de_archivo_de_conjunto_de_copias_de_seguridad* al restaurar una copia de seguridad completa de la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] seguida de una copia de seguridad diferencial de la base de datos en el mismo conjunto de medios. El conjunto de medios utiliza tres cintas de copia de seguridad, que se encuentran en las unidades de cinta `\\.\tape0`, `tape1`y `tape2`.  
  
```  
RESTORE DATABASE AdventureWorks2012 FROM TAPE = '\\.\tape0', TAPE = '\\.\tape1', TAPE = '\\.\tape2'  
   WITH   
   MEDIANAME = 'AdventureWorksMediaSet1',  
   FILE=1,   
   NORECOVERY;  
RESTORE DATABASE AdventureWorks2012 FROM TAPE = '\\.\tape0', TAPE = '\\.\tape1', TAPE = '\\.\tape2'   
   WITH   
   MEDIANAME = 'AdventureWorksMediaSet1',  
   FILE=2,   
   RECOVERY;  
GO  
```  
  
 Para obtener información sobre las tablas del historial en las que se almacena información sobre los conjuntos de medios y sus familias de medios y conjuntos de copia de seguridad, vea [Historial de copias de seguridad e información de encabezados &#40;SQL Server&#41;](backup-history-and-header-information-sql-server.md).  
  
 El número de medios de copia de seguridad en un conjunto de medios depende de varios factores:  
  
-   Número de dispositivos de copia de seguridad  
  
-   Tipo de dispositivos de copia de seguridad  
  
-   Número de conjuntos de copia de seguridad  
  
##  <a name="ConsiderationsForMediaSetFamilies"></a> Uso de medios conjuntos y familias  
 En esta sección se tratan varias consideraciones para usar los conjuntos y las familias de medios.  
  
  
  
###  <a name="CreatingMediaSet"></a> Crear un nuevo conjunto de medios  
 Para crear un conjunto de medios es necesario formatear el medio de copia de seguridad (una o varias cintas o archivos de disco). El proceso de formato cambia el medio de copia de seguridad de la siguiente manera:  
  
1.  Elimina el antiguo encabezado (si existe), eliminando adecuadamente el contenido anterior de los medios de copia de seguridad.  
  
     Al formatear un dispositivo de cinta se elimina todo el contenido anterior de la cinta actualmente montada. Formatear un disco afecta solo al archivo que especifique para la operación de copia de seguridad.  
  
2.  Escribe un nuevo encabezado de medios en el medio de copia de seguridad (cinta o archivo de disco) en cada uno de los dispositivos de copia de seguridad.  
  
  
###  <a name="UseExistingMediaSet"></a> Copia de seguridad en un conjunto de medios existente  
 Al hacer una copia de seguridad en un conjunto de medios existente, las opciones son las siguientes:  
  
-   Anexarlo al conjunto de copia de seguridad existente.  
  
     Para utilizar mejor el espacio disponible, se pueden agregar nuevos conjuntos de copia de seguridad al conjunto de medios existente. Agregar estos conjuntos a la copia de seguridad preserva las copias de seguridad anteriores. Para obtener más información, vea [Anexar a conjuntos de copia de seguridad existentes](#Appending), más adelante en esta sección.  
  
    > [!NOTE]  
    >  Agregarlo, que es el comportamiento predeterminado de la copia de seguridad (BACKUP), puede especificarse explícitamente mediante la opción NOINIT.  
  
-   Sobrescribir todos los conjuntos de copia de seguridad con la copia de seguridad actual, dejando el encabezado de medios actual en su sitio.  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tiene medidas de seguridad para evitar que se sobrescriban los medios accidentalmente. Sin embargo, la copia de seguridad puede sobrescribir automáticamente los conjuntos de copia de seguridad que hayan alcanzado una fecha de expiración predefinida.  
  
     Para los encabezados de cinta, dejar el encabezado en su sitio puede tener sentido. Para obtener más información, vea [Sobrescribir conjuntos de copia de seguridad](#Overwriting), más adelante en esta sección.  
  
    > [!NOTE]  
    >  Sobrescribir los conjuntos de copia de seguridad existentes se especifica mediante la opción INIT de la instrucción BACKUP.  
  
####  <a name="Appending"></a> Anexar a conjuntos de copia de seguridad existentes  
 En el mismo medio se pueden almacenar copias de seguridad de las mismas o diferentes bases de datos, realizadas en distintos momentos. Al anexar otro conjunto de copia de seguridad al medio existente, el contenido anterior del medio permanece intacto y la nueva copia de seguridad se escribe después del final de la última copia de seguridad del medio.  
  
 De manera predeterminada, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] siempre anexa nuevas copias de seguridad al medio. El anexo solo se puede agregar al final del medio. Por ejemplo, si el volumen de un medio contiene cinco conjuntos de copia de seguridad, no es posible omitir los primeros tres conjuntos para sobrescribir el cuarto con un nuevo conjunto de copia de seguridad.  
  
 Si utiliza BACKUP WITH NOREWIND para realizar una copia de seguridad en cinta, la cinta quedará abierta al final de la operación. Esto permite anexar más copias de seguridad a la cinta sin necesidad de rebobinarla y recorrerla después para encontrar el último conjunto de copia de seguridad. Puede encontrar la lista de unidades de cinta abiertas en la vista de administración dinámica **sys.dm_io_backup_tapes**; para obtener más información, vea [sys.dm_io_backup_tapes &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-io-backup-tapes-transact-sql).  
  
 Las copias de seguridad de Microsoft Windows y las copias de seguridad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pueden compartir el mismo medio, pero no son interoperables. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no puede realizar una copia de seguridad de datos de Windows.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssEnterpriseEd10](../../includes/sskatmai-md.md)] o versiones posteriores pueden leer copias de seguridad comprimidas. Para obtener más información, vea [Compresión de copia de seguridad &#40;SQL Server&#41;](backup-compression-sql-server.md).  
  
  
####  <a name="Overwriting"></a> Sobrescribir los conjuntos de copia de seguridad  
 La sobrescritura de los conjuntos de copia de seguridad existentes se especifica mediante la opción INIT de la instrucción BACKUP. Esta opción sobrescribe todos los conjuntos de copia de seguridad del medio y mantiene el encabezado de medios, si se mantiene algo. Si no existe ningún encabezado de medios, se crea uno.  
  
 Para los encabezados de cinta, dejar el encabezado en su sitio puede tener sentido. En medios de copia de seguridad en disco, solo se sobrescriben los archivos que utilizan los dispositivos de copia de seguridad especificados en la operación de copia de seguridad; los demás archivos del disco no se ven afectados. Cuando se sobrescriben copias de seguridad, se mantiene el encabezado de medios existente y la nueva copia de seguridad se crea como la primera en el dispositivo de copia de seguridad. Si no hay ningún encabezado de medios, se escribe automáticamente uno válido con el nombre y la descripción del medio correspondientes. Si el encabezado de medios existente no es válido, terminará la operación de copia de seguridad. Si el medio está vacío, se genera el nuevo encabezado de medios con los datos proporcionados por MEDIANAME, MEDIAPASSWORD y MEDIADESCRIPTION, si hubiera.  
  
> [!IMPORTANT]  
>  Empezando por [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], ya no está disponible la opción MEDIAPASSWORD para crear copias de seguridad. Sin embargo, todavía puede restaurar las copias de seguridad creadas con contraseñas.  
  
 No se sobrescribe el medio de copia de seguridad si existe alguna de las condiciones siguientes:  
  
-   Las copias de seguridad que hay en el medio no han expirado. (Si se especifica SKIP, no se comprueba la expiración.)  
  
     La fecha de expiración especifica la fecha en la que expira la copia de seguridad y se puede sobrescribir con otra copia de seguridad. Puede especificar la fecha de expiración al crear una copia de seguridad. De forma predeterminada, la fecha de expiración está determinada por la opción **Retención de medios** establecida con **sp_configure**. Para obtener más información, vea [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql).  
  
-   El nombre del medio, si se ha proporcionado, no coincide con el nombre del medio de copia de seguridad.  
  
     El nombre del medio es un nombre descriptivo que se proporciona para identificarlo fácilmente.  
  
 Si está seguro de que desea sobrescribir el medio existente (por ejemplo, si sabe que las copias de seguridad de la cinta ya no son necesarias), puede omitir explícitamente estas comprobaciones.  
  
 Si el medio de copia de seguridad está protegido con contraseña por Microsoft Windows, Microsoft SQL Server no escribe en el medio. Para sobrescribir un medio protegido por contraseña, debe reinicializarlo.  
  
  
###  <a name="SequenceNumbers"></a> Números de secuencia  
 El orden correcto es importante para varias familias de medios de un conjunto de medios o varios medios de copia de seguridad de una familia de medios. Por tanto, la copia de seguridad asigna números de secuencia de las maneras siguientes:  
  
-   Familias de medios secuenciales de un conjunto de medios  
  
     En un conjunto de medios, las familias de medios se numeran de forma secuencial según su posición en el conjunto. El número de familia de medios se registra en la columna **family_sequence_number** de la tabla **backupmediafamily** .  
  
-   Medios físicos de una familia de medios  
  
     Un número de secuencia de medios indica el orden de los medios físicos de una familia de medios. El número de secuencia 1 se utiliza para el medio inicial de copia de seguridad. Éste se etiqueta con 1, el segundo (la primera cinta de continuación) se etiqueta con 2, y así sucesivamente. Cuando restaure el conjunto de copia de seguridad, los números de secuencia de medios garantizan que el operador que restaura la copia de seguridad monta los medios correctos en el orden correcto.  
  
###  <a name="MultipleDevices"></a> Varios dispositivos  
 Cuando use varias unidades de cinta o archivos de disco, tenga en cuenta las consideraciones siguientes:  
  
-   Para las copias de seguridad:  
  
     En todas las operaciones de copia de seguridad siguientes se debe utilizar el conjunto de medios completo creado por una operación de copia de seguridad. Por ejemplo, si se creó un conjunto de medios con dos dispositivos de copia de seguridad en cinta, las siguientes operaciones de copia de seguridad que utilicen el mismo conjunto de medios deben utilizar dos dispositivos de copia de seguridad.  
  
-   Para las restauraciones:  
  
     Para cualquier restauración desde copias de seguridad en disco y para cualquier restauración en línea, deben montarse todas las familias de medios simultáneamente. Para una restauración sin conexión desde copias de seguridad en cinta, puede procesar las familias de medios desde menos dispositivos de copia de seguridad. Cada familia de medios debe procesarse completamente antes de iniciar el procesamiento de la siguiente familia. Las familias de medios siempre se procesan en paralelo, a menos que se realice una restauración con un solo dispositivo.  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
 **Para crear un medio nuevo conjunto**  
  
-   [Crear una copia de seguridad completa de base de datos &#40;SQL Server&#41;](create-a-full-database-backup-sql-server.md) (Opción **Hacer copia de seguridad en un nuevo conjunto de medios y borrar todos los conjuntos de copia de seguridad existentes**)  
  
-   [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql) (Opción FORMATO)  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Backup.FormatMedia%2A>  
  
 **Para anexar una nueva copia de seguridad a un medio existente**  
  
-   [Crear una copia de seguridad completa de la base de datos &#40;SQL Server&#41;](create-a-full-database-backup-sql-server.md) (Opción **Anexar al conjunto de copia de seguridad existente**)  
  
-   [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql) (Opción NOINIT)  
  
 **Para sobrescribir conjuntos de copia de seguridad existentes**  
  
-   [Crear una copia de seguridad completa de la base de datos &#40;SQL Server&#41;](create-a-full-database-backup-sql-server.md) (Opción **Sobrescribir todos los conjuntos de copia de seguridad existentes**)  
  
-   [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql) (Opción INIT)  
  
 **Para establecer la fecha de expiración**  
  
-   [Establecer la fecha de expiración de una copia de seguridad &#40;SQL Server&#41;](set-the-expiration-date-on-a-backup-sql-server.md)  
  
 **Para ver los números de secuencia de secuencia y la familia de medios**  
  
-   [Ver las propiedades y el contenido de un dispositivo lógico de copia de seguridad &#40;SQL Server&#41;](view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)  
  
-   [backupmediafamily &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/backupmediafamily-transact-sql) (Columna **family_sequence_number**)  
  
 **Para ver los conjuntos de copia de seguridad de un dispositivo de copia de seguridad determinado**  
  
-   [Ver los archivos de datos y de registro en un conjunto de copia de seguridad &#40;SQL Server&#41;](view-the-data-and-log-files-in-a-backup-set-sql-server.md)  
  
-   [Ver las propiedades y el contenido de un dispositivo lógico de copia de seguridad &#40;SQL Server&#41;](view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)  
  
-   [RESTORE HEADERONLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-headeronly-transact-sql)  
  
 **Para leer el encabezado de medios de los medios de un dispositivo de copia de seguridad**  
  
-   [RESTORE LABELONLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-labelonly-transact-sql)  
  
  
## <a name="see-also"></a>Vea también  
 [Realizar copias de seguridad y restaurar bases de datos de SQL Server](back-up-and-restore-of-sql-server-databases.md)   
 [Errores posibles de medios durante copia de seguridad y restauración &#40;SQL Server&#41;](possible-media-errors-during-backup-and-restore-sql-server.md)   
 [Historial de copias de seguridad e información de encabezados &#40;SQL Server&#41;](backup-history-and-header-information-sql-server.md)   
 [Conjuntos de medios de copia de seguridad reflejados &#40;SQL Server&#41;](mirrored-backup-media-sets-sql-server.md)   
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [RESTORE REWINDONLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-rewindonly-transact-sql)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
