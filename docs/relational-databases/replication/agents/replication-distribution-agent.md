---
title: Agente de distribución de replicación | Microsoft Docs
ms.custom: ''
ms.date: 02/23/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Distribution Agent, executables
- agents [SQL Server replication], Distribution Agent
- Distribution Agent, parameter reference
- command prompt [SQL Server replication]
ms.assetid: 7b4fd480-9eaf-40dd-9a07-77301e44e2ac
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1864abc0cfa12e0b7ea60f5e080d372b9b50d989
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47790293"
---
# <a name="replication-distribution-agent"></a>Agente de distribución de replicación
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  El Agente de distribución de replicación es un ejecutable que mueve la instantánea (para la replicación de instantáneas y la replicación transaccional) y las transacciones de las tablas de base de datos de la distribución (para la replicación transaccional) a las tablas de destino en los suscriptores.  
  
> [!NOTE]  
>  Los parámetros se pueden especificar en cualquier orden. Cuando no se especifican parámetros opcionales, se utilizan valores de la configuración del Registro predefinida en el equipo local.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
distrib [-?]  
-Publisher server_name[\instance_name]  
-PublisherDB publisher_database  
-Subscriber server_name[\instance_name]  
-SubscriberDB subscriber_database   
[-AltSnapshotFolder alt_snapshot_folder_path]   
[-BcpBatchSize bcp_batch_size]  
[-CommitBatchSize commit_batch_size]  
[-CommitBatchThreshold commit_batch_threshold]  
[-Continuous]  
[-DefinitionFile def_path_and_file_name]  
[-Distributor distributor]  
[-DistributorLogin distributor_login]  
[-DistributorPassword distributor_password]  
[-DistributorSecurityMode [0|1]]  
[-EncryptionLevel [0|1|2]]  
[-ErrorFile error_path_and_file_name]  
[-ExtendedEventConfigFile configuration_path_and_file_name]  
[-FileTransferType [0|1]]  
[-FtpAddress ftp_address]  
[-FtpPassword ftp_password]   
[-FtpPort ftp_port]  
[-FtpUserName ftp_user_name]  
[-HistoryVerboseLevel [0|1|2|3]]  
[-Hostname host_name]  
[-KeepAliveMessageInterval keep_alive_message_interval_seconds]  
[-LoginTimeOut login_time_out_seconds]  
[-MaxBcpThreads]  
[-MaxDeliveredTransactions number_of_transactions]  
[-MessageInterval message_interval]  
[-OledbStreamThreshold oledb_stream_threshold]  
[-Output output_path_and_file_name]  
[-OutputVerboseLevel [0|1|2]]  
[-PacketSize packet_size]  
[-PollingInterval polling_interval]  
[-ProfileName profile_name]  
[-Publication publication]  
[-QueryTimeOut query_time_out_seconds]  
[-QuotedIdentifier quoted_identifier]  
[-SkipErrors native_error_id [:...n]]  
[-SubscriberDatabasePath subscriber_path]  
[-SubscriberLogin subscriber_login]  
[-SubscriberPassword subscriber_password]  
[-SubscriberSecurityMode [0|1]]  
[-SubscriberType [0|1|3]]  
[-SubscriptionStreams [1|2|...64]]  
[-SubscriptionTableName subscription_table]  
[-SubscriptionType [0|1|2]]  
[-TransactionsPerHistory [0|1|...10000]]  
[-UseDTS]  
[-UseInprocLoader]  
[-UseOledbStreaming]  
```  
  
## <a name="arguments"></a>Argumentos  
 **-?**  
 Imprime todos los parámetros disponibles.  
  
 **-Publisher** *nombre_de_servidor*[**\\***** nombre_de_instancia*]  
 Es el nombre del publicador. Especifique *server_name* para conectarse a la instancia predeterminada del [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en ese servidor. Especifique *server_name***\\***instance_name* para una instancia con nombre de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en ese servidor.  
  
 **-PublisherDB** *publisher_database*  
 Es el nombre de la base de datos del publicador.  
  
 **-Subscriber** *nombre_de_servidor*[**\\***nombre_de_instancia*]  
 Es el nombre del suscriptor. Especifique *server_name* para conectarse a la instancia predeterminada del [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en ese servidor. Especifique *server_name***\\***instance_name* para una instancia con nombre de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en ese servidor.  
  
 **-SubscriberDB** *subscriber_database*  
 Es el nombre de la base de datos del suscriptor.  
  
 **-AltSnapshotFolder** *alt_snapshot_folder_path*  
 Es la ruta de acceso a la carpeta que contiene la instantánea inicial para una suscripción.  
  
 **-BcpBatchSize** *bcp_batch_size*  
 Es el número de filas para enviar en una operación de copia masiva. Al realizar una operación **bcp in** , el tamaño del lote es el número de filas para enviar al servidor como una transacción y también el número de filas que se deben enviar antes de que el Agente de distribución registre un mensaje de progreso de **bcp** . Al realizar una operación **bcp out** , se usa un tamaño de lote fijo de **1000** .  
  
 **-CommitBatchSize** *commit_batch_size*  
 Es el número de transacciones que se va a emitir al Suscriptor antes de que se emita una instrucción COMMIT. El valor predeterminado es 100.  
  
 **-CommitBatchThreshold**  *commit_batch_threshold*  
 Es el número de comandos de replicación que se va a emitir al Suscriptor antes de que se emita una instrucción COMMIT. El valor predeterminado es 1000.  
  
 **-Continuous**  
 Especifica si el agente intenta sondear las transacciones replicadas continuamente. Si se especifica, el agente sondea las transacciones replicadas del origen en intervalos de sondeo, aunque no haya ninguna transacción pendiente.  
  
 **-DefinitionFile** *def_path_and_file_name*  
 Es la ruta de acceso del archivo de definición de agente. Un archivo de definición de agente contiene los argumentos de símbolo del sistema para el agente. El contenido del archivo se analiza como un archivo ejecutable. Utilice las comillas tipográficas (") para especificar valores de argumento que contienen caracteres arbitrarios.  
  
 **-Distributor** *distributor*  
 Es el nombre del distribuidor. Para la distribución (inserción) del Distribuidor, el nombre tiene como valor predeterminado el nombre del Distribuidor local.  
  
 **-DistributorLogin** *distributor_login*  
 Es el nombre de inicio de sesión del distribuidor.  
  
 **-DistributorPassword** *distributor_password*  
 Es la contraseña del distribuidor.  
  
 **-DistributorSecurityMode** [ **0**| **1**]  
 Especifica el modo de seguridad del distribuidor. Un valor de 0 hace referencia al modo de autenticación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y un valor de 1 hace referencia al modo de autenticación de Windows (valor predeterminado).  
  
 **-EncryptionLevel** [ **0** | **1** | **2** ]  
 Es el nivel de cifrado de Capa de sockets seguros (SSL) utilizado por el agente de distribución cuando realiza conexiones.  
  
|Valor de EncryptionLevel|Descripción|  
|---------------------------|-----------------|  
|**0**|Especifica que no se utiliza SSL.|  
|**1**|Especifica que se utiliza SSL, pero el agente no comprueba que un emisor confiable haya firmado el certificado del servidor SSL.|  
|**2**|Especifica que se usa SSL y que se ha comprobado el certificado.|  
  
 Para obtener más información, vea [Información general sobre seguridad &#40;replicación&#41;](../../../relational-databases/replication/security/security-overview-replication.md).  
  
 **-ErrorFile** *error_path_and_file_name*  
 Es la ruta y nombre del archivo de error generado por el Agente de distribución. Este archivo se genera en cualquier punto en el que se haya producido el error durante la aplicación de transacciones de replicación en el suscriptor; los errores que se producen en el publicador o el distribuidor no se registran en este archivo. Contiene las transacciones de replicación en las que se ha producido un error y los mensajes de error relacionados. Si no se especifica, el archivo de error se genera en el directorio actual del Agente de distribución. El nombre del archivo de error es el nombre del agente de distribución con la extensión .err. Si el nombre de archivo especificado existe, los mensajes de error se anexan al archivo. Este parámetro puede tener un máximo de 256 caracteres Unicode.  
  
 **-ExtendedEventConfigFile** *configuration_path_and_file_name*  
 Especifica el nombre y la ruta del archivo para el archivo de configuración XML de eventos extendidos. El archivo de configuración de eventos extendidos le permite configurar sesiones y habilitar eventos para su seguimiento.  
  
 **-FileTransferType** [ **0**| **1**]  
 Especifica el tipo de transferencia de archivo. Un valor de **0** indica UNC (convención de nomenclatura universal) y un valor de **1** indica FTP (protocolo de transferencia de archivos).  
  
 **-FtpAddress** *ftp_address*  
 Es la dirección de red del servicio FTP para el distribuidor. Cuando no se especifica, se utiliza **DistributorAddress** . Si no se especifica **DistributorAddress** , se utiliza **Distribuidor** .  
  
 **-FtpPassword** *ftp_password*  
 Es la contraseña del usuario que se utiliza para conectarse al servicio FTP.  
  
 **-FtpPort** *ftp_port*  
 Es el número de puerto del servicio FTP para el distribuidor. Cuando no se especifica, se utiliza el número de puerto predeterminado para el servicio FTP (21).  
  
 **-FtpUserName**  *nombre_de_usuario_de_ftp*  
 Es el nombre de usuario que se utiliza para conectar con el servicio FTP. Cuando no se especifica, se utiliza **anónimo** .  
  
 **-HistoryVerboseLevel** [ **0** | **1** | **2** | **3** ]  
 Especifica la cantidad de historial registrado durante una operación de la distribución. Puede minimizar el efecto sobre el rendimiento del registro del historial seleccionando **1**.  
  
|Valor HistoryVerboseLevel|Descripción|  
|-------------------------------|-----------------|  
|**0**|Los mensajes de progreso se escriben en la consola o bien en un archivo de resultados. Los registros del historial no se registran en la base de datos de distribución.|  
|**1**|Predeterminado: Siempre actualiza un mensaje del historial anterior del mismo estado (inicio, progreso, éxito, etc.). Si no existe ningún registro anterior con el mismo estado, inserta un nuevo registro.|  
|**2**|Inserta nuevos registros de historial a menos que el registro sea para mensajes de inactividad o mensajes de trabajos de ejecución prolongada, en cuyo caso actualiza los registros anteriores.|  
|**3**|Siempre inserta nuevos registros, a menos que sea para mensajes inactivos.|  
  
 **-Hostname** *host_name*  
 Es el nombre del host utilizado al conectarse al publicador. Este parámetro puede tener un máximo de 128 caracteres Unicode.  
  
 **-KeepAliveMessageInterval** *keep_alive_message_interval_seconds*  
 Es el número de segundos antes de que el subproceso del historial compruebe si cualquiera de las conexiones existentes está esperando una respuesta del servidor. Este valor se puede reducir para evitar que la comprobación del agente marque al agente de distribución como sospechoso al ejecutar un lote de ejecución prolongada. El valor predeterminado es **300** segundos.  
  
 **-LoginTimeOut** *login_time_out_seconds*  
 Es el número de segundos antes de que el inicio de sesión exceda el tiempo de espera. El valor predeterminado es de **15** segundos.  
  
 **-MaxBcpThreads** *number_of_threads*  
 Especifica el número de operaciones de copia masiva que se pueden realizar en paralelo. El número máximo de subprocesos y conexiones ODBC que existen simultáneamente es el menor entre **MaxBcpThreads** y el número de solicitudes de copia masiva que aparecen en la transacción de sincronización en la base de datos de distribución. **MaxBcpThreads** debe tener un valor mayor que **0** y no tiene ningún límite superior codificado de forma rígida. El valor predeterminado es **2** veces el número de procesadores, hasta un valor máximo de **8**. Al aplicar una instantánea que se generó en el publicador utilizando la opción de instantánea simultánea, se utiliza un subproceso, sin tener en cuenta el número especificado para **MaxBcpThreads**.  
  
 **-MaxDeliveredTransactions** *number_of_transactions*  
 Es el número máximo de transacciones de inserción o extracción aplicado a suscriptores en una sincronización. Un valor de **0** indica que el máximo es un número infinito de transacciones. Los suscriptores pueden utilizar otros valores para acortar la duración de una sincronización que se extrae de un publicador.  
  
> [!NOTE]  
>  Si se especifican tanto -MaxDeliveredTransactions como -Continuous, el Agente de distribución entrega el número especificado de transacciones y, a continuación, se detiene (aunque se especifique -Continuous). Debe reiniciar el Agente de distribución cuando el trabajo se complete.  
  
 **-MessageInterval**  *message_interval*  
 Es el intervalo de tiempo utilizado para el registro del historial. Un evento de historial se registra cuando se alcanza uno de estos parámetros:  
  
-   Se alcanza el valor **TransactionsPerHistory** una vez registrado el último evento de historial.  
  
-   Se alcanza el valor **MessageInterval** una vez registrado el último evento de historial.  
  
 Si no hay ninguna transacción replicada disponible en el origen, el agente envía un mensaje de no transacción al distribuidor. Esta opción especifica cuánto tiempo espera el agente para enviar otro mensaje que indica que no hay ninguna transacción. Los agentes siempre envían un mensaje que indica que no hay ninguna transacción cuando detectan que no hay ninguna transacción disponible en el origen después de procesar previamente las transacciones replicadas. El valor predeterminado es 60 segundos.  
  
 **-OledbStreamThreshold** *oledb_stream_threshold*  
 Especifica el tamaño mínimo, en bytes, para los datos del objeto binario grande por encima del cual los datos se vincularán como un flujo. Debe especificar **–UseOledbStreaming** para utilizar este parámetro. Los valores pueden ir de 400 a 1048576 bytes, con un valor predeterminado de 16384 bytes.  
  
 **-Output** *output_path_and_file_name*  
 Es la ruta de acceso del archivo de salida del agente. Si no se proporciona un nombre de archivo, el resultado se envía a la consola. Si el nombre de archivo especificado existe, el resultado se anexa al archivo.  
  
 **-OutputVerboseLevel** [ **0**| **1**| **2**]  
 Especifica si el resultado debería ser detallado. Si el nivel detallado es **0**, solo se imprimen los mensajes de error. Si el nivel detallado es **1**, se imprimen todos los mensajes del informe de progreso. Si el nivel detallado es **2** (valor predeterminado), se imprimen todos los mensajes de error y mensajes del informe de progreso, lo que es útil para la depuración.  
  
 **-PacketSize** *packet_size*  
 Es el tamaño del paquete, en bytes. El valor predeterminado es 4096 (bytes).  
  
 **-PollingInterval** *polling_interval*  
 Es la frecuencia, en segundos, con la que la base de datos de distribución recibe consultas de transacciones replicadas. El valor predeterminado es 5 segundos.  
  
 **-ProfileName** *profile_name*  
 Especifica un perfil de agente para utilizar para los parámetros del agente. Si **ProfileName** es NULL, el perfil de agente se deshabilita. Si no se especifica **ProfileName** , se utiliza el perfil predeterminado para el tipo de agente. Para obtener información, vea [Perfiles del Agente de replicación](../../../relational-databases/replication/agents/replication-agent-profiles.md).  
  
 **-Publication**  *publicación*  
 Es el nombre de la publicación. Este parámetro solamente es válido si la publicación se define para tener siempre una instantánea disponible para las suscripciones nuevas o reinicializadas.  
  
 **-QueryTimeOut** *query_time_out_seconds*  
 Es el número de segundos antes de que la consulta exceda el tiempo de espera. El valor predeterminado es 1800 segundos.  
  
 **-QuotedIdentifier** *quoted_identifier*  
 Especifica el carácter del identificador entrecomillado que se utilizará. El primer carácter del valor indica el valor que utiliza el agente de distribución. Si **QuotedIdentifier** se utiliza sin ningún valor, el agente de distribución utiliza un espacio. Si no se utiliza **QuotedIdentifier** , el agente de distribución utiliza cualquier identificador entrecomillado que admita el suscriptor.  
  
 **-SkipErrors** *identificador_de_error_nativo* [**:***...n*]  
 Es una lista separada por dos puntos que especifica los números de error que este agente omitirá.  
  
 **-SubscriberDatabasePath** *subscriber_database_path*  
 Es la ruta de acceso a la base de datos Jet (archivo .mdb) si **SubscriberType** es **2** (permite una conexión a una base de datos Jet sin un nombre del origen de datos ODBC (DSN)).  
  
 **-SubscriberLogin** *subscriber_login*  
 Es el nombre de inicio de sesión del suscriptor. Si **SubscriberSecurityMode** es **0** (para autenticación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ), se debe especificar este parámetro.  
  
 **-SubscriberPassword** *subscriber_password*  
 Es la contraseña del suscriptor. Si **SubscriberSecurityMode** es **0** (para autenticación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ), se debe especificar este parámetro.  
  
 **-SubscriberSecurityMode** [ **0**| **1**]  
 Especifica el modo de seguridad del suscriptor. Un valor de **0** hace referencia a la autenticación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y un valor de **1** hace referencia al modo de autenticación de Windows (valor predeterminado).  
  
 **-SubscriberType** [ **0**| **1**| **3**]  
 Especifica el tipo de conexión de suscriptor utilizada por el agente de distribución.  
  
|Valor SubscriberType|Descripción|  
|--------------------------|-----------------|  
|**0**|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]|  
|**1**|Origen de datos ODBC|  
|**3**|Origen de datos OLE DB|  
  
 **-SubscriptionStreams** [**0**|**1**|**2**|...**64**]  
 Es el número de conexiones permitidas por el agente de distribución para aplicar lotes de cambios en paralelo a un suscriptor, aunque manteniendo muchas de las características transaccionales presentes al utilizar un único subproceso. Para un publicador de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , se admite un intervalo de valores de 1 a 64. Este parámetro solo se admite cuando el publicador y el distribuidor se están ejecutando en [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] o en versiones posteriores. Este parámetro no se admite o debe ser 0 para suscriptores que no son de[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o suscripciones punto a punto.  
  
> [!NOTE]  
>  Si una de las conexiones no se puede ejecutar o confirmar, todas las conexiones anularán el lote actual y el agente utilizará un solo flujo para volver a intentar los lotes con errores. Antes de que finalice esta fase de reintento, pueden aparecer incoherencias transaccionales temporales en el suscriptor. Una vez que se han confirmado correctamente los lotes con errores, el suscriptor vuelve al estado de coherencia transaccional.  
  
> [!IMPORTANT]  
>  Al especificar un valor de 2 o mayor para **-SubscriptionStreams**, el orden en el que las transacciones se reciben en el suscriptor puede diferir del orden en el que se realizaron en el publicador. Si este comportamiento produce las infracciones de restricción durante la sincronización, debería utilizar la opción NOT FOR REPLICATION para deshabilitar el cumplimiento de restricciones durante la sincronización. Para obtener más información, vea [Controlar el comportamiento de desencadenadores y restricciones durante la sincronización &#40;programación de la replicación con Transact-SQL&#41;](../../../relational-databases/replication/control-behavior-of-triggers-and-constraints-in-synchronization.md).  
  
> [!NOTE]  
>  Los flujos de suscripción no funcionan en los artículos configurados para entregar [!INCLUDE[tsql](../../../includes/tsql-md.md)]. Para usar flujos de suscripción, configure en su lugar los artículos para que entreguen llamadas de procedimiento almacenado.  
  
 **-SubscriptionTableName** *subscription_table*  
 Es el nombre de la tabla de suscripción generada o usada en el Suscriptor determinado. Si no se especifica, se usa la tabla [MSreplication_subscriptions &#40;Transact-SQL&#41;](../../../relational-databases/system-tables/msreplication-subscriptions-transact-sql.md). Utilice esta opción para los sistemas de administración de bases de datos (DBMS) que no admiten los nombres largos del archivo.  
  
 **-SubscriptionType** [ **0**| **1**| **2**]  
 Especifica el tipo de suscripción para la distribución. Un valor de **0** indica una suscripción de inserción, un valor de **1** indica una suscripción de extracción y un valor de **2** indica una suscripción anónima.  
  
 **-TransactionsPerHistory** [ **0**| **1**|... **10000**]  
 Especifica el intervalo de la transacción para el registro del historial. Si el número de transacciones confirmadas después de la última instancia de registro del historial es mayor que esta opción, se registra un mensaje de historial. El valor predeterminado es 100. Un valor de **0** indica infinito **TransactionsPerHistory**. See the preceding **–MessageInterval**parameter.  
  
 **-UseDTS**  
 Se debe especificar como un parámetro para una publicación que permite la transformación de datos.  
  
 **-UseInprocLoader**  
 Mejora el rendimiento de la instantánea inicial haciendo que el agente de distribución utilice el comando BULK INSERT al aplicar los archivos de instantánea al Suscriptor. Este parámetro está obsoleto porque no es compatible con el tipo de datos XML. Si no replica datos XML, puede utilizar este parámetro. Este parámetro no se puede utilizar con instantáneas del modo de carácter o suscriptores que no son de[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Si utiliza este parámetro, la cuenta de servicio de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] del suscriptor debe tener permisos de lectura en el directorio donde se encuentran los archivos de datos .bcp de instantánea. Cuando no se utiliza este parámetro, el agente (para suscriptores que no son de[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ) o el controlador ODBC cargado por el agente (para suscriptores de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ) lee los archivos, por lo que no se utiliza el contexto de seguridad de la cuenta de servicio de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
 **-UseOledbStreaming**  
 Cuando se especifica, habilita el enlace de datos del objeto binario como un flujo. Utilice **-OledbStreamThreshold** para especificar el tamaño, en bytes, por encima del cual se utilizará un flujo. **UseOledbStreaming** se habilita de forma predeterminada. **UseOledbStreaming** escribe en la carpeta **C:\Archivos de programa\Microsoft SQL Server\\<versión\>\COM**.  
  
## <a name="remarks"></a>Notas  
  
> [!IMPORTANT]  
>  Si ha instalado el agente de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para que se ejecute en una cuenta de sistema local en lugar de debajo de una cuenta de usuario de dominio (el valor predeterminado), el servicio puede tener acceso solo al equipo local. Si el agente de distribución que se ejecuta en el agente de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] se configura para utilizar el modo de autenticación de Windows cuando inicia sesión en una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], el agente de distribución devuelve un error. La configuración predeterminada es la autenticación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Para obtener información acerca del cambio de cuentas de seguridad, vea [View and Modify Replication Security Settings](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md).  
  
 Para iniciar el agente de distribución, ejecute **distrib.exe** desde el símbolo del sistema. Para obtener información, vea [Conceptos de los ejecutables del Agente de replicación](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md).  
  
## <a name="change-history"></a>Historial de cambios  
  
|Contenido actualizado|  
|---------------------|  
|Se ha agregado el parámetro **-ExtendedEventConfigFile** .|  
  
## <a name="see-also"></a>Ver también  
 [Administración del Agente de replicación](../../../relational-databases/replication/agents/replication-agent-administration.md)  
  
  
