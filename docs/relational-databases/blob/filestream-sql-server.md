---
title: FILESTREAM (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 01/11/2018
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: blob
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-blob
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- FILESTREAM [SQL Server]
- FILESTREAM [SQL Server], about
- FILESTREAM [SQL Server], overview
ms.assetid: 9a5a8166-bcbe-4680-916c-26276253eafa
caps.latest.revision: 13
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 54cc9bd8f9c209fa07fcbb920dcd22abd5c3dbb1
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="filestream-sql-server"></a>FILESTREAM (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

FILESTREAM permite a las aplicaciones basadas en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]almacenar datos no estructurados, como documentos e imágenes, en el sistema de archivos. Las aplicaciones pueden aprovechar las API de transmisión de datos enriquecidas y el rendimiento del sistema de archivos al mismo tiempo que mantienen la coherencia transaccional entre los datos no estructurados y los datos estructurados correspondientes.  
  
FILESTREAM integra [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] con sistemas de archivos NTFS o ReFS almacenando datos de objetos binarios grandes (BLOB) **varbinary(max)** como archivos en el sistema de archivos. [!INCLUDE[tsql](../../includes/tsql-md.md)] pueden insertar, actualizar, consultar, buscar y realizar copias de seguridad de los datos FILESTREAM. Las interfaces del sistema de archivos de Win32 proporcionan el acceso de la transmisión por secuencias a los datos.  
  
FILESTREAM usa la memoria caché del sistema NT para almacenar en memoria caché los datos de archivos. Esto ayuda a reducir cualquier efecto que los datos FILESTREAM podrían tener en el rendimiento de [!INCLUDE[ssDE](../../includes/ssde-md.md)] . No se usa el grupo de búferes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ; por consiguiente, esta memoria está disponible para el procesamiento de consultas.  
  
FILESTREAM no se habilita automáticamente al instalar o actualizar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Debe habilitar FILESTREAM utilizando el Administrador de configuración de SQL Server y [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para utilizar FILESTREAM, debe crear o modificar una base de datos que contenga un tipo especial de grupo de archivos. Luego, debe crear o modificar una tabla de modo que contenga una columna **varbinary(max)** con el atributo FILESTREAM. Después de completar estas tareas, puede usar [!INCLUDE[tsql](../../includes/tsql-md.md)] y Win32 para administrar los datos FILESTREAM.  

## <a name="when-to-use-filestream"></a>Cuándo se usa FILESTREAM

En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], los BLOB pueden ser datos de **varbinary(max)** estándar que almacena los datos en tablas u objetos FILESTREAM **varbinary(max)** que almacenan los datos en el sistema de archivos. El tamaño y el uso de los datos determinan si debería usar el almacenamiento de base de datos o el almacenamiento del sistema de archivos. Si las condiciones siguientes son verdaderas, debería pensar en usar FILESTREAM:  

- Los objetos que se están almacenando son, por término medio, mayores de 1 MB.  
- El acceso de lectura rápido es importante.
- Está desarrollando aplicaciones que usan un nivel intermedio para la lógica de la aplicación.  

Para objetos de menor tamaño, el almacenamiento de BLOB **varbinary(max)** en la base de datos a menudo proporciona un mejor rendimiento de la transmisión de datos.  

## <a name="filestream-storage"></a>Almacenamiento de FILESTREAM

El almacenamiento de FILESTREAM se implementa como una columna **varbinary(max)** en la que los datos están almacenados como BLOB en el sistema de archivos. Los tamaños de los BLOB están limitados solo por el tamaño del volumen del sistema de archivos. La limitación **varbinary(max)** estándar de tamaños de archivo de 2 GB no se aplica a BLOB que están almacenados en el sistema de archivos.  
  
Para especificar que una columna debería almacenar datos en el sistema de archivos, especifique el atributo FILESTREAM en una columna **varbinary(max)** . Esto hace que [!INCLUDE[ssDE](../../includes/ssde-md.md)] almacene todos los datos para esa columna en el sistema de archivos pero no en el archivo de base de datos.  
  
Los datos de FILESTREAM deben estar almacenados en los grupos de archivos FILESTREAM. Un grupo de archivos FILESTREAM es un grupo de archivos especial que contiene los directorios de sistema de archivos en lugar de los propios archivos. Estos directorios del sistema de archivos se denominan *contenedores de datos*. Los contenedores de datos son la interfaz entre el almacenamiento del [!INCLUDE[ssDE](../../includes/ssde-md.md)] y el almacenamiento del sistema de archivos. 

Cuando use el almacenamiento FILESTREAM, piense en lo siguiente:  

- Cuando una tabla contiene una columna FILESTREAM, cada fila debe tener un identificador de fila único distinto de NULL.  
- Se pueden agregar varios contenedores de datos a un grupo de archivos FILESTREAM.  
- Los contenedores de datos FILESTREAM no pueden estar anidados.  
- Cuando se usan clústeres de conmutación por error, los grupos de archivos FILESTREAM deben estar en recursos de disco compartido.  
- Los grupos de archivos FILESTREAM pueden estar en volúmenes comprimidos.

### <a name="integrated-management"></a>Administración integrada

Debido a que FILESTREAM se implementa como columna **varbinary(max)** y se integra directamente en el [!INCLUDE[ssDE](../../includes/ssde-md.md)], la mayoría de las funciones y de las herramientas de administración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] funcionan sin la modificación de los datos FILESTREAM. Por ejemplo, puede usar todos los modelos de recuperación y copia de seguridad con datos FILESTREAM y se realizan copias de seguridad de los datos FILESTREAM con los datos estructurados de la base de datos. Si no desea realizar una copia de seguridad de los datos FILESTREAM con datos relacionales, puede usar una copia de seguridad parcial para excluir los grupos de archivos FILESTREAM.  

### <a name="integrated-security"></a>Seguridad integrada

En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], los datos de FILESTREAM se protegen de la misma manera que los demás datos: concediendo permisos en el nivel de tabla o columna. Si un usuario tiene permiso para la columna FILESTREAM de una tabla, el usuario puede abrir los archivos asociados.  

> [!NOTE]
> El cifrado no se admite en los datos FILESTREAM.  

Solo la cuenta con la que la cuenta de servicio de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se ejecuta se permiten los permisos al contenedor FILESTREAM. Recomendamos que no se concedan permisos a ninguna otra cuenta en el contenedor de datos.

> [!NOTE]
> Los inicios de sesión de SQL no funcionarán con contenedores FILESTREAM. Solo la autenticación NTFS o ReFS funcionará con contenedores FILESTREAM.

## <a name="dual"></a> Acceso a datos BLOB con Transact-SQL y acceso de transmisión de datos del sistema de archivos

Después de almacenar los datos en una columna FILESTREAM, puede tener acceso a los archivos usando las transacciones de [!INCLUDE[tsql](../../includes/tsql-md.md)] o usando las API de Win32.  
  
### <a name="transact-sql-access"></a>Acceso a Transact-SQL

Usando [!INCLUDE[tsql](../../includes/tsql-md.md)], puede insertar, actualizar y eliminar los datos de FILESTREAM:  

- Puede usar una operación de inserción para rellenar previamente un campo FILESTREAM con un valor nulo, un valor vacío o un dato insertado relativamente corto. Sin embargo, se envía una gran cantidad de datos de manera más eficaz en un archivo que usa interfaces de Win32.  
- Al actualizar un campo FILESTREAM, modifica los datos de BLOB subyacentes en el sistema de archivos. Cuando un campo FILESTREAM está establecido en NULL, se eliminan los datos de BLOB asociados al campo. No puede usar ninguna actualización fragmentada de [!INCLUDE[tsql](../../includes/tsql-md.md)] , implementada como UPDATE **.** Write(), para realizar actualizaciones parciales en los datos. 
- Al eliminar una fila, o eliminar o truncar una tabla que contiene datos FILESTREAM, elimina los datos de BLOB subyacentes del sistema de archivos.

### <a name="file-system-streaming-access"></a>Acceso a la transmisión por secuencias del sistema de archivos

La compatibilidad de transmisión por secuencias de Win32 funciona en el contexto de una transacción de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Dentro de una transacción, puede usar las funciones FILESTREAM para obtener una ruta de acceso al sistema de archivos de UNC lógica de un archivo. Tras ello, use la API OpenSqlFilestream para obtener un identificador de archivos. Después, este identificador lo pueden usar las interfaces de transmisión por secuencias de archivo de Win32, como ReadFile() y WriteFile(), para obtener acceso y actualizar el archivo a través del sistema de archivos.  

Dado que las operaciones de archivo son transaccionales, no puede eliminar ni cambiar el nombre de los archivos FILESTREAM a través del sistema de archivos.  

**Modelo de la instrucción**

El acceso del sistema de archivos de FILESTREAM modela una instrucción de [!INCLUDE[tsql](../../includes/tsql-md.md)] usando la apertura y el cierre de archivo. La instrucción se inicia cuando un identificador de archivos se abre y finaliza cuando se cierra el identificador. Por ejemplo, cuando se cierra un identificador de escritura, cualquier posible desencadenador de AFTER que esté registrado en la tabla se desencadena como si la instrucción UPDATE estuviera completada.

**Espacio de nombres de almacenamiento**

En FILESTREAM, el [!INCLUDE[ssDE](../../includes/ssde-md.md)] controla el espacio de nombres del sistema de archivos físico de BLOB. Una nueva función intrínseca, [PathName](../../relational-databases/system-functions/pathname-transact-sql.md), proporciona la ruta UNC lógica del BLOB que se corresponde con cada celda de FILESTREAM de la tabla. La aplicación usa esta ruta de acceso lógica para obtener el identificador de Win32 y funcionar en los datos de BLOB usando las interfaces del sistema de archivos de Win32 normales. La función devuelve NULL si el valor de la columna FILESTREAM es NULL.  

**Acceso al sistema de archivos transaccionales**

Una nueva función intrínseca, [GET_FILESTREAM_TRANSACTION_CONTEXT()](../../t-sql/functions/get-filestream-transaction-context-transact-sql.md), proporciona el token que representa la transacción actual a la que la sesión está asociada. Se debe haber iniciado la transacción y no haberse anulado ni confirmado todavía. Al obtener un token, la aplicación enlaza las operaciones de transmisión por secuencias del sistema de archivos FILESTREAM con una transacción iniciada. La función devuelve NULL en caso de no haber ninguna transacción explícitamente iniciada.  

Se deben cerrar todos los identificadores de archivo antes de que la transacción se confirme o se anule. Si un identificador se deja abierto más allá del ámbito de transacción, las lecturas adicionales frente al identificador producirán un error; las escrituras adicionales frente al identificador tendrán éxito pero los datos reales no se escribirán en el disco. De igual forma, si la base de datos o la instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)] se cierra, se invalidan todos los identificadores abiertos.  

**Durabilidad transaccional**

Con FILESTREAM, al confirmar la transacción, el [!INCLUDE[ssDE](../../includes/ssde-md.md)] asegura la durabilidad de la transacción para los datos de BLOB FILESTREAM que se modifican del acceso a la transmisión por secuencias del sistema de archivos.  

**Semántica de aislamiento**

La semántica de aislamiento se rige por los niveles de aislamiento de transacción del [!INCLUDE[ssDE](../../includes/ssde-md.md)] . Se admite el nivel de aislamiento de lectura confirmada para [!INCLUDE[tsql](../../includes/tsql-md.md)] y el acceso al sistema de archivos. Se admiten operaciones de lectura repetibles, así como serializables y aislamientos de instantáneas. No se admite la lectura de datos sucios.  

Las operaciones de apertura de acceso al sistema de archivos no esperan ningún bloqueo. En su lugar, se produce un error inmediato de las operaciones de apertura si no pueden obtener acceso a los datos debido al aislamiento de transacción. Se produce un error en las llamadas de API de transmisión por secuencias con ERROR_SHARING_VIOLATION si la operación de apertura no puede continuar debido a la infracción de aislamiento.  

Para permitir que se realicen actualizaciones parciales, la aplicación puede emitir un control FS de dispositivo (FSCTL_SQL_FILESTREAM_FETCH_OLD_CONTENT) para capturar el contenido anterior en el archivo al que hace referencia el identificador abierto. Esto desencadenará una copia de contenido antiguo de servidor. Para un mejor rendimiento de la aplicación, y para evitar encontrarse con posibles tiempos de espera mientras trabaja con archivos muy grandes, recomendamos que use E/S asincrónica.  

Si se emite FSCTL una vez que se haya escrito en el identificador, se conservará la última operación de escritura y se perderán las escrituras anteriores realizadas en el identificador.

**API del sistema de archivos y niveles de aislamiento admitidos**

Cuando una API del sistema de archivos no puede abrir un archivo a causa de una infracción de aislamiento, se devuelve una excepción ERROR_SHARING_VIOLATION. Esta infracción de aislamiento se produce cuando dos transacciones intentan acceder al mismo archivo. El resultado de la operación de acceso depende del modo en el que se abrió el archivo y de la versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la que se ejecute la transacción. En la tabla siguiente se explican resumidamente los posibles resultados de dos transacciones que están accediendo al mismo archivo.

|Transacción 1|Transacción 2|Resultado en SQL Server 2008|Resultado en SQL Server 2008 R2 y versiones posteriores|  
|-------------------|-------------------|--------------------------------|------------------------------------------------------|  
|Abrir para lectura.|Abrir para lectura.|Ambas son correctas.|Ambas son correctas.|  
|Abrir para lectura.|Abrir para escritura.|Ambas son correctas. Las operaciones de escritura de la transacción 2 no influyen en las operaciones de lectura realizadas en la transacción 1.|Ambas son correctas. Las operaciones de escritura de la transacción 2 no influyen en las operaciones de lectura realizadas en la transacción 1.|  
|Abrir para escritura.|Abrir para lectura.|Se produce un error en la operación de apertura de la transacción 2 con una excepción ERROR_SHARING_VIOLATION.|Ambas son correctas.|  
|Abrir para escritura.|Abrir para escritura.|Se produce un error en la operación de apertura de la transacción 2 con una excepción ERROR_SHARING_VIOLATION.|Se produce un error en la operación de apertura de la transacción 2 con una excepción ERROR_SHARING_VIOLATION.|  
|Abrir para lectura.|Abrir para SELECT.|Ambas son correctas.|Ambas son correctas.|  
|Abrir para lectura.|Abrir para UPDATE o DELETE.|Ambas son correctas. Las operaciones de escritura de la transacción 2 no influyen en las operaciones de lectura realizadas en la transacción 1.|Ambas son correctas. Las operaciones de escritura de la transacción 2 no influyen en las operaciones de lectura realizadas en la transacción 1.|  
|Abrir para escritura.|Abrir para SELECT.|La transacción 2 se bloquea hasta que la transacción 1 se confirme o finalice la transacción. O bien, se agota el tiempo de espera de bloqueo de la transacción.|Ambas son correctas.|  
|Abrir para escritura.|Abrir para UPDATE o DELETE.|La transacción 2 se bloquea hasta que la transacción 1 se confirme o finalice la transacción. O bien, se agota el tiempo de espera de bloqueo de la transacción.|La transacción 2 se bloquea hasta que la transacción 1 se confirme o finalice la transacción. O bien, se agota el tiempo de espera de bloqueo de la transacción.|  
|Abrir para SELECT.|Abrir para lectura.|Ambas son correctas.|Ambas son correctas.|  
|Abrir para SELECT.|Abrir para escritura.|Ambas son correctas. Las operaciones de escritura de la transacción 2 no influyen en la transacción 1.|Ambas son correctas. Las operaciones de escritura de la transacción 2 no influyen en la transacción 1.|  
|Abrir para UPDATE o DELETE.|Abrir para lectura.|Se produce un error en la operación de apertura de la transacción 2 con una excepción ERROR_SHARING_VIOLATION.|Ambas son correctas.|  
|Abrir para UPDATE o DELETE.|Abrir para escritura.|Se produce un error en la operación de apertura de la transacción 2 con una excepción ERROR_SHARING_VIOLATION.|Se produce un error en la operación de apertura de la transacción 2 con una excepción ERROR_SHARING_VIOLATION.|  
|Abrir para SELECT con REPEATABLE READ.|Abrir para lectura.|Ambas son correctas.|Ambas son correctas.|  
|Abrir para SELECT con REPEATABLE READ.|Abrir para escritura.|Se produce un error en la operación de apertura de la transacción 2 con una excepción ERROR_SHARING_VIOLATION.|Se produce un error en la operación de apertura de la transacción 2 con una excepción ERROR_SHARING_VIOLATION.|

**Escritura continua desde clientes remotos**

El acceso del sistema de archivos remoto a los datos FILESTREAM está habilitado por el protocolo Bloque de mensajes de servidor (SMB). Si el cliente es remoto, no se almacena en caché ninguna operación de escritura del lado cliente. Las operaciones de escritura siempre se enviarán al servidor. Los datos pueden se pueden almacenar en memoria caché en el servidor. Recomendamos que las aplicaciones que se están ejecutando en clientes remotos consoliden pequeñas operaciones de escritura para realizar menos operaciones de escritura mediante un tamaño de datos mayor.  

No se admite la creación de vistas asignadas de memoria (E/S asignada de memoria) usando un identificador FILESTREAM. Si la asignación de memoria se usa para los datos FILESTREAM, el [!INCLUDE[ssDE](../../includes/ssde-md.md)] no puede garantizar la coherencia y la durabilidad de los datos o la integridad de la base de datos.  

## <a name="related-tasks"></a>Related Tasks

[Habilitar y configurar FILESTREAM](../../relational-databases/blob/enable-and-configure-filestream.md)  
[crear una base de datos habilitada para FILESTREAM](../../relational-databases/blob/create-a-filestream-enabled-database.md)  
[Crear una tabla para almacenar datos FILESTREAM](../../relational-databases/blob/create-a-table-for-storing-filestream-data.md)  
[Obtener acceso a datos FILESTREAM con Transact-SQL](../../relational-databases/blob/access-filestream-data-with-transact-sql.md) [Crear aplicaciones cliente para datos FILESTREAM](../../relational-databases/blob/create-client-applications-for-filestream-data.md)  
[Obtener acceso a los datos FILESTREAM con OpenSqlFilestream](../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md)  
[Realizar actualizaciones parciales de los datos FILESTREAM](../../relational-databases/blob/make-partial-updates-to-filestream-data.md)  
[Evitar conflictos con operaciones de base de datos en aplicaciones FILESTREAM](../../relational-databases/blob/avoid-conflicts-with-database-operations-in-filestream-applications.md)  
[Mover una base de datos habilitada para FILESTREAM](../../relational-databases/blob/move-a-filestream-enabled-database.md)  
[Configurar FILESTREAM en un clúster de conmutación por error](../../relational-databases/blob/set-up-filestream-on-a-failover-cluster.md)  
[Configurar un Firewall para el acceso de FILESTREAM](../../relational-databases/blob/configure-a-firewall-for-filestream-access.md)

## <a name="related-content"></a>Contenido relacionado

[Compatibilidad de FILESTREAM con otras características de SQL Server](../../relational-databases/blob/filestream-compatibility-with-other-sql-server-features.md)
<br>[Vistas de administración dinámica de secuencia de archivo y FileTable (Transact-SQL)](../system-dynamic-management-views/filestream-and-filetable-dynamic-management-views-transact-sql.md)
<br>[Vistas de catálogo de secuencia de archivo y FileTable (Transact-SQL)](../system-catalog-views/filestream-and-filetable-catalog-views-transact-sql.md)
<br>[Procedimientos almacenados del sistema de Filestream y FileTable (Transact-SQL)](../system-stored-procedures/filestream-and-filetable-system-stored-procedures.md)

