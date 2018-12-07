---
title: Agente de mezcla de replicación | Microsoft Docs
ms.custom: ''
ms.date: 10/29/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Merge Agent, executables
- Merge Agent, parameter reference
- agents [SQL Server replication], Merge Agent
- command prompt [SQL Server replication]
ms.assetid: fe1e7f60-b0c8-45e9-a5e8-4fedfa73d7ea
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2d9760d692e30a7d33828f27202ba7818c1ac047
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/28/2018
ms.locfileid: "52523458"
---
# <a name="replication-merge-agent"></a>Replication Merge Agent
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  El Agente de mezcla de replicación es una utilidad ejecutable que aplica la instantánea inicial contenida en las tablas de base de datos a los Suscriptores. También mezcla los cambios incrementales de los datos que tienen lugar en el publicador después de la creación de la instantánea inicial y reconcilia los conflictos según las reglas configuradas por el usuario o mediante un solucionador personalizado creado por el usuario.  
  
> [!NOTE]  
>  Los parámetros se pueden especificar en cualquier orden. Cuando no se especifican parámetros opcionales, se utilizan valores de la configuración del Registro predefinida en el equipo local.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
replmerg [-?]   
-Publisher server_name[\instance_name]  
-PublisherDB publisher_database  
-Publication publication  
-Subscriber server_name[\instance_name]  
-SubscriberDB subscriber_database  
[-AltSnapshotFolder alt_snapshot_folder_path]  
[-Continuous]  
[-DefinitionFile def_path_and_file_name]  
[-DestThreads number_of_destination_threads]  
[-Distributor server_name[\instance_name]]  
[-DistributorLogin distributor_login]  
[-DistributorPassword distributor_password]  
[-DistributorSecurityMode [0|1]]  
[-DownloadGenerationsPerBatch download_generations_per_batch]  
[-DownloadReadChangesPerBatch download_read_changes_per_batch]  
[-DownloadWriteChangesPerBatch download_write_changes_per_batch]  
[-DynamicSnapshotLocation dynamic_snapshot_location]  
[-EncryptionLevel [0|1|2]]  
[-ExchangeType [1|2|3]]  
[-FastRowCount [0|1]]  
[-FileTransferType [0|1]]  
[-ForceConvergenceLevel [0|1|2 (Publisher|Subscriber|Both)]]  
[-FtpAddress ftp_address]  
[-FtpPassword ftp_password]  
[-FtpPort ftp_port]  
[-FtpUserNameftp_user_name]  
[-HistoryVerboseLevel [0|1|2|3]]  
[-Hostname host_name]  
[-InteractiveResolution [0|1]]  
[-InternetLogin internet_login]  
[-InternetPassword internet_password]  
[-InternetProxyLogin internet_proxy_login]  
[-InternetProxyPassword internet_proxy_password]  
[-InternetProxyServer internet_proxy_server]  
[-InternetSecurityMode [0|1]]  
[-InternetTimeout internet_timeout]  
[-InternetURL internet_url]  
[-KeepAliveMessageInterval keep_alive_message_interval_seconds]  
[-LoginTimeOut login_time_out_seconds]  
[-MakeGenerationInterval make_generation_interval_seconds]  
[-MaxBcpThreads number_of_threads]  
[-MaxDownloadChanges number_of_download_changes]  
[-MaxUploadChanges number_of_upload_changes]  
[-MetadataRetentionCleanup [0|1]]  
[-Output]  
[-OutputVerboseLevel [0|1|2]]  
[-ParallelUploadDownload [0|1]]  
[-PacketSize packet_size]   
[-PollingInterval polling_interval]  
[-ProfileName profile_name]  
[-PublisherFailoverPartner server_name[\instance_name] ]  
[-PublisherLogin publisher_login]  
[-PublisherPassword publisher_password]  
[-PublisherSecurityMode [0|1]]  
[-QueryTimeOut query_time_out_seconds]  
[-SrcThreads number_of_source_threads]  
[-StartQueueTimeout start_queue_timeout_seconds]  
[-SubscriberConflictClean [0|1]]  
[-SubscriberDatabasePath subscriber_path]  
[-SubscriberDBAddOption [0|1|2|3]]  
[-SubscriberLogin subscriber_login]  
[-SubscriberPassword subscriber_password   
[-SubscriberSecurityMode [0|1]]  
[-SubscriberType [0|1|2|3|4|5|6|7|8|9]]  
[-SubscriptionType [0|1|2]]  
[-SyncToAlternate [0|1]  
[-UploadGenerationsPerBatch upload_generations_per_batch]  
[-UploadReadChangesPerBatch upload_read_changes_per_batch]  
[-UploadWriteChangesPerBatch upload_write_changes_per_batch]  
[-UseInprocLoader]  
[-Validate [0|1|2|3]]  
[-ValidateInterval validate_interval]  
```  
  
## <a name="arguments"></a>Argumentos  
 **-?**  
 Imprime todos los parámetros disponibles.  
  
 **-Publisher** *nombre_de_servidor*[**\\***nombre_de_instancia*]  
 Es el nombre del publicador. Especifique *server_name* para conectarse a la instancia predeterminada del [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en ese servidor. Especifique *server_name***\\***instance_name* para una instancia con nombre de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en ese servidor.  
  
 **-PublisherDB** *publisher_database*  
 Es el nombre de la base de datos del publicador.  
  
 **-Publication** *publication*  
 Es el nombre de la publicación. Este parámetro solamente es válido si la publicación se define para tener siempre una instantánea disponible para las suscripciones nuevas o reinicializadas.  
  
 **-Subscriber** *nombre_de_servidor*[**\\***nombre_de_instancia*]  
 Es el nombre del suscriptor. Especifique *server_name* para conectarse a la instancia predeterminada del [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en ese servidor. Especifique *server_name***\\***instance_name* para una instancia con nombre de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en ese servidor.  
  
 **-SubscriberDB** *subscriber_database*  
 Es el nombre de la base de datos del suscriptor.  
  
 **-AltSnapshotFolder** *alt_snapshot_folder_path*  
 Es la ruta de acceso a la carpeta que contiene la instantánea inicial para una suscripción.  
  
 **-Continuous**  
 Especifica si el agente intenta sondear las transacciones replicadas continuamente. Si se especifica, el agente sondea las transacciones replicadas del origen en intervalos de sondeo, aunque no haya ninguna transacción pendiente.  
  
 **-DestThreads** *number_of_destination_threads*  
 Especifica el número de subprocesos de destino que el Agente de mezcla utiliza para aplicar los cambios en el destino. El destino es el Publicador durante la carga y el Suscriptor durante la descarga. El valor predeterminado es 4.  
  
 **-DefinitionFile** *def_path_and_file_name*  
 Es la ruta de acceso del archivo de definición de agente. Un archivo de definición de agente contiene los argumentos de símbolo del sistema para el agente. El contenido del archivo se analiza como un archivo ejecutable. Utilice las comillas tipográficas (") para especificar valores de argumento que contienen caracteres arbitrarios.  
  
 **-Distributor** *nombre_de_servidor*[**\\***nombre_de_instancia*]  
 Es el nombre del distribuidor. Especifique *server_name* para la instancia predeterminada de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en ese servidor. Especifique *server_name***\\***instance_name* para una instancia con nombre de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en ese servidor. Para la distribución del distribuidor (inserción), el nombre tiene como valor predeterminado el nombre de la instancia predeterminada de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en el equipo local.  
  
 **-DistributorLogin** *distributor_login*  
 Es el nombre de inicio de sesión del distribuidor.  
  
 **-DistributorPassword** *distributor_password*  
 Es la contraseña del distribuidor.  
  
 **-DistributorSecurityMode** [ **0**| **1**]  
 Especifica el modo de seguridad del distribuidor. Un valor de **0** hace referencia a la autenticación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (valor predeterminado) y un valor de **1** hace referencia al modo de autenticación de Windows.  
  
 **-DownloadGenerationsPerBatch** *download_generations_per_batch*  
 Es el número de generaciones que se va a procesar en un lote único mientras se descargan los cambios desde el Publicador al Suscriptor. Una generación se define como un grupo lógico de cambios por artículo. El valor predeterminado para un vínculo de comunicación confiable es 100. El valor predeterminado para un vínculo de comunicación no confiable es 10.  
  
 **-DownloadReadChangesPerBatch** *download_read_changes_per_batch*  
 Es el número de cambios que se va a leer en un lote único mientras se descargan los cambios desde el Publicador al Suscriptor. El valor predeterminado es 100.  
  
 **-DownloadWriteChangesPerBatch** *download_write_changes_per_batch*  
 Es el número de cambios que se va a aplicar en un lote único mientras se descargan los cambios desde el Publicador al Suscriptor. El valor predeterminado es 100.  
  
 **-DynamicSnapshotLocation** *dynamic_snapshot_location*  
 Es la ubicación de los archivos de instantánea de datos filtrados cuando la publicación utiliza los filtros de fila con parámetros.  
  
 **-EncryptionLevel** [ **0** | **1** | **2** ]  
 Es el nivel de cifrado de Capa de sockets seguros (SSL) utilizado por el agente de mezcla cuando realiza conexiones.  
  
|Valor de EncryptionLevel|Descripción|  
|---------------------------|-----------------|  
|**0**|Especifica que no se utiliza SSL.|  
|**1**|Especifica que se utiliza SSL, pero el agente no comprueba que un emisor confiable haya firmado el certificado del servidor SSL.|  
|**2**|Especifica que se usa SSL y que se ha comprobado el certificado.|  

 > [!NOTE]  
 >  Un certificado SSL válido se define con un nombre de dominio completo de SQL Server. Para que el agente se conecte correctamente al establecer -EncryptionLevel en 2, cree un alias en la instancia local de SQL Server. El parámetro "Alias Name" debe ser el nombre del servidor, mientras que el parámetro "Server" se debe establecer en el nombre completo de la instancia de SQL Server.

 Para obtener más información, vea [Información general sobre seguridad &#40;replicación&#41;](../../../relational-databases/replication/security/security-overview-replication.md).  
  
 **- ExchangeType** [ **1**| **2**| **3**]  
 > [!WARNING]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../../includes/ssnotedepfuturedontuse-md.md)] Para restringir la carga, use **@subscriber_upload_options** de **sp_addmergearticle** en su lugar.  
  
 Especifica el tipo de intercambio de datos durante la sincronización, que puede ser uno de los siguientes:  
  
|Valor ExchangeType|Descripción|  
|------------------------|-----------------|  
|**1**|El agente debe cargar los cambios de datos del Suscriptor al Publicador.|  
|**2**|El agente debe descargar los cambios de datos del Publicador al Suscriptor.|  
|**3** (valor predeterminado)|El Agente carga los cambios de datos del suscriptor al publicador y, a continuación, los descarga del publicador al suscriptor. Debe utilizar esta opción con sincronización web.|  
  
 Los artículos exclusivos para descarga le permiten controlar el comportamiento de sincronización de artículos individuales en una publicación y pueden proporcionar una mejora del rendimiento. Para más información, vea [Optimizar el rendimiento de la replicación de mezcla con artículos de solo descarga](../../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md).  
  
 Si usa **ExchangeType** para separar la fase de carga y descarga de la replicación de mezcla en sesiones diferentes, debe ejecutar el agente de mezcla con **ExchangeType** establecido en 1 primero y después ejecutar de nuevo el agente de mezcla con el valor 2. Si no se ejecuta el agente de mezcla con ambos parámetros, se eliminarán los metadatos y tendrá que reinicializar la suscripción (sin carga).  
  
 **-FastRowCount** [**0**|**1**]  
 Especifica qué tipo de método de cálculo de número de filas se utiliza para la validación de recuento de filas. Un valor de **1** (valor predeterminado) indica el método rápido. Un valor de **0** indica el método de recuento completo de filas.  
  
 **-FileTransferType** [**0**|**1**]  
 Especifica el tipo de transferencia de archivo. Un valor de **0** indica UNC (convención de nomenclatura universal) y un valor de **1** indica FTP (protocolo de transferencia de archivos).  
  
 **-ForceConvergenceLevel** [**0**|**1**|**2** ( **Publicador**| **Suscriptor**| **Ambos**)]  
 Especifica el nivel de convergencia que debe utilizar el Agente de mezcla. Puede ser uno de los siguientes:  
  
|Valor ForceConvergenceLevel|Descripción|  
|---------------------------------|-----------------|  
|**0** (valor predeterminado)|Predeterminado: Realiza una mezcla estándar sin convergencia adicional.|  
|**1**|Fuerza la convergencia para todas las generaciones.|  
|**2**|Fuerza la convergencia para todas las generaciones y corrige los linajes dañados. Al especificar este valor, especifique dónde se deben corregir los linajes: en el Publicador, en el Suscriptor o en el Publicador y el Suscriptor.|  
  
 **-FtpAddress** *ftp_address*  
 Es la dirección de red del servicio FTP para el distribuidor. Cuando no se especifica, se utiliza **Distribuidor** .  
  
 **-FtpPassword** *ftp_password*  
 Es la contraseña del usuario que se utiliza para conectarse al servicio FTP.  
  
 **-FtpPort** *ftp_port*  
 Es el número de puerto del servicio FTP para el distribuidor. Cuando no se especifica, se utiliza el número de puerto predeterminado para el servicio FTP (21).  
  
 **-FtpUserName** *ftp_user_name*  
 Es el nombre de usuario que se utiliza para conectar con el servicio FTP. Cuando no se especifica, se utiliza anónimo.  
  
 **-HistoryVerboseLevel** [**1**|**2**|**3**]  
 Especifica la cantidad de historial registrado durante una operación de mezcla. Puede minimizar el efecto sobre el rendimiento del registro del historial seleccionando **1**.  
  
|Valor HistoryVerboseLevel|Descripción|  
|-------------------------------|-----------------|  
|**0**|Registre el mensaje final de estado de agente, los detalles finales de la sesión y cualquier error.|  
|**1**|Registre la sesión incremental detalla en cada estado de la sesión, incluso el porcentaje completado, además del mensaje de estado final de agente, los detalles finales de la sesión y cualquier error.|  
|**2**|Predeterminado: Registre los detalles de sesión incremental en cada estado de la sesión y los detalles de sesión de nivel del artículo, incluso el porcentaje completado, además del mensaje de estado final de agente, los detalles finales de la sesión y cualquier error. Los mensajes de estado de agente también se registran.|  
|**3**|Igual que **-HistoryVerboseLevel** = **2**, salvo que se registran más mensajes de progreso de agente.|  
  
 **-Hostname** *host_name*  
 El nombre de e red del equipo local. La opción predeterminada es el nombre del equipo local.  
  
 **-InteractiveResolution** [**0**|**1**]  
 Especifica si se utiliza la resolución interactiva de conflictos cuando surge un conflicto durante la sincronización. El valor predeterminado es **0**, que indica que no se utiliza la resolución interactiva de conflictos.  
  
 **-InternetLogin** *internet_login*  
 Especifica el nombre de inicio de sesión utilizado al conectarse a una DLL ISAPI de escucha de replicación [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que requiere autenticación.  
  
 **-InternetPassword** *internet_password*  
 Especifica la contraseña utilizada al conectarse a una DLL ISAPI de escucha de replicación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que requiere autenticación.  
  
 **-InternetProxyLogin**  *internet_proxy_login*  
 Especifica el nombre de inicio de sesión utilizado para conectarse a un servidor proxy definido en *internet_proxy_server*que requiere autenticación.  
  
 **-InternetProxyPassword**  *internet_proxy_password*  
 Especifica la contraseña utilizada para conectarse a un servidor proxy definido en *internet_proxy_server*que requiere autenticación.  
  
 **-InternetProxyServer**  *internet_proxy_server*  
 Especifica qué servidor proxy se debe utilizar al obtener acceso al recurso HTTP especificado en *internet_url*.  
  
 **-InternetSecurityMode** [**0**|**1**]  
 Especifica el modo de seguridad de IIS utilizado al conectarse al servidor web durante la sincronización web. Un valor de **0** indica una autenticación básica, mientras que un valor de **1** indica la autenticación integrada de Windows (valor predeterminado).  
  
 **-InternetTimeout** *internet_timeout*  
 Es el número de segundos antes de que una conexión a la DLL ISAPI de escucha de replicación [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] expire.  
  
 **-InternetURL** *internet_url*  
 Especifica la dirección URL para conectarse a la DLL de ISAPI de escucha de replicación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Es necesario especificar esta propiedad.  
  
 **-KeepAliveMessageInterval** *keep_alive_message_interval_seconds*  
 Es el número de segundos antes de que el subproceso del historial compruebe si cualquiera de las conexiones existentes está esperando una respuesta del servidor. Este valor se puede reducir para evitar que la comprobación del agente marque al Agente de mezcla como sospechoso al ejecutar un lote de ejecución prolongada. El valor predeterminado es **300** segundos.  
  
 **-LoginTimeOut** *login_time_out_seconds*  
 Es el número de segundos antes de que el inicio de sesión exceda el tiempo de espera. El valor predeterminado es de **15** segundos.  
  
 **-MakeGenerationInterval** *make_generation_interval_seconds*  
 Es el número de segundos se espera entre la creación de generaciones, o lotes de cambios, para descargar al cliente. El valor predeterminado es **1** segundo.  
  
 Makegeneration es el proceso que prepara los cambios del editor para descargarse en los suscriptores y puede constituir un cuello de botella en el rendimiento durante las descargas. Si el proceso de makegeneration ya se ejecutó dentro del intervalo especificado por **- MakeGenerationInterval**, se omite en la sesión de sincronización actual. Esto puede beneficiar a la simultaneidad de la sincronización y ser especialmente útil si los suscriptores no esperan para descargar los cambios.  
  
 **-MaxBcpThreads** *number_of_threads*  
 Especifica el número de operaciones de copia masiva que se pueden realizar en paralelo. El número máximo de subprocesos y conexiones ODBC que existen simultáneamente es el menor de **MaxBcpThreads** o el número de solicitudes de copia masiva que aparecen en la tabla de sistema **sysmergeschemachange** en la base de datos de publicación. **MaxBcpThreads** debe tener un valor mayor que 0 y no tiene ningún límite superior codificado de forma rígida. El valor predeterminado es **1**.  
  
 **-MaxDownloadChanges** *number_of_download_changes*  
 Especifica el número máximo de filas cambiadas que se deberían descargar del Publicador al Suscriptor. El número de filas descargadas puede ser mayor que el máximo especificado porque: se procesan las generaciones completas y se pueden ejecutar los subprocesos de destino en paralelo, pudiendo cada uno de ellos a procesar por lo menos 100 cambios en su primer paso. De forma predeterminada se envían todos los cambios preparados para la descarga.  
  
 **-MaxUploadChanges** *number_of_upload_changes*  
 Especifica el número máximo de filas cambiadas que se deberían cargar del Suscriptor al Publicador. El número de filas cargadas puede ser mayor que el máximo especificado porque: se procesan las generaciones completas y se pueden ejecutar los subprocesos de destino en paralelo, pudiendo cada uno de ellos a procesar por lo menos 100 cambios en su primer paso. De forma predeterminada se envían todos los cambios preparados para la carga.  
  
 **-MetadataRetentionCleanup** [**0**|**1**]  
 Especifica si los metadatos se deben quitar de [MSmerge_genhistory](../../../relational-databases/system-tables/msmerge-genhistory-transact-sql.md), [MSmerge_contents](../../../relational-databases/system-tables/msmerge-contents-transact-sql.md), [MSmerge_tombstone](../../../relational-databases/system-tables/msmerge-tombstone-transact-sql.md), [MSmerge_past_partition_mappings](../../../relational-databases/system-tables/msmerge-past-partition-mappings-transact-sql.md)y [MSmerge_current_partition_mappings](../../../relational-databases/system-tables/msmerge-current-partition-mappings.md) basándose en el período de retención de publicaciones. El valor predeterminado es **1**, lo que indica que se debe realizar la limpieza. Un valor de **0** indica que la limpieza no debería realizarse automáticamente.  
  
 **-Output** *output_path_and_file_name*  
 Es la ruta de acceso del archivo de salida del agente. Si no se proporciona un nombre de archivo, el resultado se envía a la consola. Si el nombre de archivo especificado existe, el resultado se anexa al archivo.  
  
 **-OutputVerboseLevel** [**0**|**1**|**2**]  
 Especifica si el resultado debería ser detallado. Si el nivel detallado es **0**, solo se imprimen los mensajes de error. Si el nivel detallado es **1**, se imprimen todos los mensajes del informe de progreso. Si el nivel detallado es **2** (valor predeterminado), se imprimen todos los mensajes de error y mensajes del informe de progreso, lo que es útil para la depuración.  
  
 **-ParallelUploadDownload** [**0**|**1**]  
 Especifica si el Agente de mezcla debe procesar en paralelo los cambios cargados al Publicador y los descargados al Suscriptor. Esto es útil en entornos de grandes volúmenes con un ancho de banda de red elevado. Si **ParallelUploadDownload** es **1**, se habilita el procesamiento en paralelo.  
  
 **-PacketSize**  
 Es el tamaño del paquete, en bytes. El valor predeterminado es 4096 (bytes).  
  
 **-PollingInterval** *polling_interval*  
 Es la frecuencia, en segundos, con la que el Publicador o el Suscriptor recibe consultas de cambios de datos. El valor predeterminado es 60 segundos.  
  
 **-ProfileName** *profile_name*  
 Especifica un perfil de agente para utilizar para los parámetros del agente. Si **ProfileName** es NULL, el perfil de agente se deshabilita. Si no se especifica **ProfileName** , se utiliza el perfil predeterminado para el tipo de agente. Para obtener información, vea [Perfiles del Agente de replicación](../../../relational-databases/replication/agents/replication-agent-profiles.md).  
  
 **-PublisherFailoverPartner** *nombre_de_servidor*[**\\***nombre_de_instancia*]  
 Especifica la instancia del asociado de conmutación por error de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que participa en una sesión de creación de reflejo de la base de datos con la base de datos de publicación. Para obtener más información, vea [Replicación y creación de reflejo de la base de datos &#40;SQL Server&#41;](../../../database-engine/database-mirroring/database-mirroring-and-replication-sql-server.md).  
  
 **-PublisherLogin** *publisher_login*  
 Es el nombre de inicio de sesión del publicador. Si **PublisherSecurityMode** es **0** (para autenticación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ), se debe especificar este parámetro.  
  
 **-PublisherPassword** *publisher_password*  
 Es la contraseña del publicador. Si **PublisherSecurityMode** es **0** (para autenticación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ), se debe especificar este parámetro.  
  
 **-PublisherSecurityMode** [**0**|**1**]  
 Especifica el modo de seguridad del publicador. Un valor de **0** hace referencia a la autenticación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (predeterminado) y un valor de **1** hace referencia al modo de autenticación de Windows.  
  
 **-QueryTimeOut** *query_time_out_seconds*  
 Es el número de segundos antes de que la consulta exceda el tiempo de espera. El valor predeterminado es 300 segundos. El Agente de mezcla también utiliza el valor **QueryTimeout** para determinar cuánto tiempo es preciso esperar para la generación de una instantánea con particiones cuando este valor es mayor que 1800.  
  
 **-SrcThreads** *number_of_source_threads*  
 Especifica el número de subprocesos de origen que el Agente de mezcla utiliza para enumerar los cambios desde el origen. El origen es el Suscriptor durante la carga y el Publicador durante la descarga. El valor predeterminado es **3**.  
  
 **-StartQueueTimeout** *start_queue_timeout_seconds*  
 Es el número máximo de segundos que el Agente de mezcla espera cuando el número de procesos de mezcla simultáneos en ejecución ha alcanzado el límite establecido por la propiedad **@max_concurrent_merge** de **sp_addmergepublication**. Si se alcanza el número máximo de segundos y el Agente de mezcla todavía está esperando, se cerrará. Un valor de 0 significa que el agente espera indefinidamente, aunque puede cancelarse.  
  
 **-SubscriberDatabasePath** *subscriber_database_path*  
 Es la ruta de acceso a la base de datos Jet (archivo .mdb) si **SubscriberType** es **2** (permite una conexión a una base de datos Jet sin un nombre del origen de datos ODBC (DSN)).  
  
 **-SubscriberDBAddOption** [**0**| **1**| **2**| **3**]  
 Especifica si ya existe una base de datos de suscriptor.  
  
|Valor SubscriberDBAddOption|Descripción|  
|---------------------------------|-----------------|  
|**0**|Utiliza la base de datos existente (valor predeterminado).|  
|**1**|Crea una base de datos de suscriptor nueva y vacía.|  
|**2**|Crea una nueva base de datos y la adjunta al archivo especificado.|  
|**3**|Crea una nueva base de datos, la adjunta a la base de datos y habilita todas las suscripciones que puedan existir en el archivo.|  
  
> [!NOTE]  
>  Al utilizar los valores **2** y **3**, la ruta de acceso de la base de datos para el Suscriptor se debe especificar en la opción **SubscriberDatabasePath** .  
  
 **-SubscriberLogin** *subscriber_login*  
 Es el nombre de inicio de sesión del suscriptor. Si **SubscriberSecurityMode** es **0** (para autenticación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ), se debe especificar este parámetro.  
  
 **-SubscriberPassword** *subscriber_password*  
 Es la contraseña del suscriptor. Si **SubscriberSecurityMode** es **0** (para autenticación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ), se debe especificar este parámetro.  
  
 **-SubscriberSecurityMode** [ **0**| **1**]  
 Especifica el modo de seguridad del suscriptor. Un valor de **0** hace referencia a la autenticación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (predeterminado) y un valor de **1** hace referencia al modo de autenticación de Windows.  
  
 **-SubscriberConflictClean** [ **0**| **1**]  
 Especifica si las tablas de conflictos se limpian en el suscriptor durante el proceso de sincronización, donde un valor de **1** indica que las tablas de conflictos se limpian en el suscriptor. Este parámetro solamente se utiliza para las suscripciones a publicaciones con registro de conflicto descentralizado.  
  
 **-SubscriberType** [ **0**| **1**| **3**| **4**| **5**| **6**| **7**| **8**]  
 Especifica el tipo de conexión de suscriptor utilizada por el Agente de mezcla. Solo el valor predeterminado de **0** se admite para este parámetro.  
  
 **-SubscriptionType**[ **0**| **1**| **2**]  
 Especifica el tipo de suscripción para la distribución. Un valor de **0** indica una suscripción de inserción (predeterminado), un valor de **1** indica una suscripción de extracción y un valor de **2** indica una suscripción anónima.  
  
 **-SyncToAlternate** [ **0|1**]  
 Especifica si el Agente de mezcla está sincronizando entre un Suscriptor y un Publicador alternativo. Un valor de **1** indica que es un publicador alternativo. El valor predeterminado es **0**.  
  
 **-UploadGenerationsPerBatch** *upload_generations_per_batch*  
 Es el número de generaciones que se va a procesar en un lote único mientras se cargan los cambios desde el Suscriptor al Publicador. Una generación se define como un grupo lógico de cambios por artículo. El valor predeterminado para un vínculo de comunicación confiable es **100**. El valor predeterminado para un vínculo de comunicación no confiable es **1**.  
  
 **-UploadReadChangesPerBatch** *upload_read_changes_per_batch*  
 Es el número de cambios que se va a leer en un único lote mientras se cargan los cambios desde el Suscriptor al Publicador. El valor predeterminado es **100**.  
  
 **-UploadWriteChangesPerBatch** *upload_write_changes_per_batch*  
 Es el número de cambios que se va a aplicar en un único lote mientras se cargan los cambios del Suscriptor al Publicador. El valor predeterminado es **100**.  
  
 **-UseInprocLoader**  
 Mejora el rendimiento de la instantánea inicial haciendo que el Agente de mezcla utilice el comando BULK INSERT al aplicar los archivos de instantánea al Suscriptor. Este parámetro está obsoleto porque no es compatible con el tipo de datos XML. Si no replica datos XML, puede utilizar este parámetro. Este parámetro no se puede utilizar con instantáneas de modo de carácter. Si utiliza este parámetro, la cuenta de servicio de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] del suscriptor debe tener permisos de lectura en el directorio donde se encuentran los archivos de datos .bcp de instantánea. Cuando no se utiliza este parámetro, el controlador ODBC cargado por el agente lee los archivos, por lo que no se utiliza el contexto de seguridad de la cuenta de servicio de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
 **-Validate** [**0**|**1**|**2**|**3**]  
 Especifica si la validación se debería hacer al final de la sesión de mezcla, y, en ese caso, qué tipo de validación. **3** es el valor recomendado.  
  
|Valor de validación|Descripción|  
|--------------------|-----------------|  
|**0** (valor predeterminado)|Sin validación.|  
|**1**|Validación solo del recuento de filas|  
|**2**|Validación del recuento de filas y de la suma de comprobación.|  
|**3**|Validación del recuento de filas y de la suma de comprobación binaria.|  
  
> [!NOTE]  
>  La validación mediante suma de comprobación binaria o suma de comprobación puede informar incorrectamente sobre un error si los tipos de datos son diferentes en el suscriptor y en el publicador. Para obtener más información, vea la sección sobre consideraciones para la validación de datos del tema [Validate Replicated Data](../../../relational-databases/replication/validate-replicated-data.md) (Validar datos replicados).  
  
 **-ValidateInterval** *validate_interval*  
 Frecuencia, en minutos, con la que se valida la suscripción en modo continuo. El valor predeterminado es **60** minutos.  
  
## <a name="remarks"></a>Notas  
  
> [!IMPORTANT]  
>  Si ha instalado el agente de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para que se ejecute en una cuenta de sistema local en lugar de bajo una cuenta de usuario de dominio (valor predeterminado), el servicio puede acceder solamente al equipo local. Si el Agente de mezcla que se ejecuta en el agente de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] se configura para utilizar el modo de autenticación de Windows cuando inicia sesión en una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], el Agente de mezcla devuelve un error. La configuración predeterminada es la autenticación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
 Para iniciar el agente de mezcla, ejecute **replmerg.exe** desde el símbolo del sistema. Para obtener información, vea [Aplicaciones ejecutables del Agente de replicación](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md).  
  
 El historial del agente de mezcla de la sesión actual no se quita mientras se está ejecutando de forma continua. Una ejecución prolongada del agente puede tener como resultado un gran número de entradas en las tablas del historial de mezcla, lo que puede afectar al rendimiento. Para resolver este problema cambie al modo programado o siga usando el modo continuado, pero cree un trabajo dedicado para reiniciar periódicamente el agente de mezcla, o reduzca el nivel de detalle para reducir el número de filas y, en consecuencia, reducir el impacto en el rendimiento.  
  
## <a name="see-also"></a>Ver también  
 [Administración del Agente de replicación](../../../relational-databases/replication/agents/replication-agent-administration.md)  
  
  
