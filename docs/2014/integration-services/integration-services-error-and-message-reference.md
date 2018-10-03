---
title: Referencia de errores y mensajes de Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- error numbers [Integration Services]
- hresults [Integration Services]
- errors [Integration Services], listed
ms.assetid: 2c825c07-5074-42ad-90ea-0dc5a588dcf7
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a3ae4c2b4742365bc2022e602d15f00a3b37b96c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48106735"
---
# <a name="integration-services-error-and-message-reference"></a>Referencia de errores y mensajes de Integration Services
  En las tablas siguientes se muestra una lista de los errores [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] predefinidos, advertencias y mensajes informativos, en orden numérico ascendente dentro de cada categoría, junto con sus códigos numéricos y nombres simbólicos. Cada uno de estos errores se define como un campo en la clase <xref:Microsoft.SqlServer.Dts.Runtime.Hresults> en el espacio de nombres <xref:Microsoft.SqlServer.Dts.Runtime> .  
  
 Esta lista puede resultarle útil si encuentra un código de error sin su descripción. En este momento, la lista no incluye información sobre cómo solucionar problemas.  
  
> [!IMPORTANT]  
>  Muchos de los mensajes de error que puede llegar a ver mientras trabaja con [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] provienen de otros componentes. En este tema, encontrará todos los errores generados por componentes [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . Si su error no aparece en la lista, el error lo generó un componente externo a [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. Éstos pueden incluir proveedores de OLE DB, otros componentes de bases de datos como [!INCLUDE[ssDE](../includes/ssde-md.md)] y [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] u otros servicios o componentes como el sistema de archivos, el servidor SMTP o Message Queue Server (llamado también MSMQ), etc. Para encontrar información acerca de estos mensajes de error externos, vea la documentación específica del componente.  
  
 Esta lista contiene los grupos de mensajes siguientes:  
  
-   [Mensajes de error (DTS_E_ *)](#msgError)  
  
-   [Mensajes de advertencia (DTS_W_ *)](#msgWarning)  
  
-   [Mensajes informativos (DTS_I_*)](#msgInfo)  
  
-   [Mensajes generales y de eventos (DTS_MSG_*)](#msgGeneral)  
  
-   [Mensajes de aprobación (DTS_S_*)](#msgSuccess)  
  
-   [Mensajes de error de componentes de flujo de datos (DTSBC_E_*)](#msgPipeline)  
  
##  <a name="msgError"></a> mensajes de error  
 Los nombres simbólicos de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] mensajes de error que comienzan por `DTS_E_`.  
  
|Código hexadecimal|Código decimal|Nombre simbólico|Descripción|  
|----------------------|------------------|-------------------|-----------------|  
|0x8002F347|-2147290297|DTS_E_STOREDPROCSTASK_OVERWRITINGSPATDESTINATION|Sobrescribiendo el procedimiento almacenado "%1" en el destino.|  
|0x8020837E|-2145352834|DTS_E_ADOSRCUNKNOWNTYPEMAPPEDTONTEXT|El tipo de datos "%1" de la columna "%2" no es compatible con %3 Esta columna se convertirá a DT_NTEXT.|  
|0x8020838C|-2145352820|DTS_E_XMLSRCSCHEMACOLUMNNOTINEXTERNALMETADATA|La columna %1 de la tabla %2 en el esquema XML no tiene una asignación en las columnas de metadatos externas.|  
|0xC0000032|-1073741774|DTS_E_NOTINITIALIZED|No se inicializó un objeto interno o una variable. Código de error interno,  que se devuelve cuando una variable no tiene un valor válido que debería tener.|  
|0xC0000033|-1073741773|DTS_E_EXPIRED|Ha expirado el período de evaluación de Integration Services.|  
|0xC0000034|-1073741772|DTS_E_NEGATIVEVALUESNOTALLOWED|Esta propiedad no puede tener asignado un valor negativo. Este error se produce cuando se asigna un valor negativo a una propiedad que solo puede contener valores positivos, como la propiedad COUNT.|  
|0xC0000035|-1073741771|DTS_E_NEGATIVEINDEXNOTALLOWED|Los índices no pueden ser negativos. Este error se produce si se utiliza un valor negativo como índice de una colección.|  
|0xC00060AB|-1073717077|DTS_E_INVALIDSSISSERVERNAME|Nombre de servidor no válido %1". El servicio SSIS no admite el uso de múltiples instancias; utilice únicamente el nombre de servidor en lugar de "nombre\instancia del servidor".|  
|0xC0008445|-1073707963|DTS_E_SCRIPTMIGRATIONFAILED64BIT|No es posible realizar la migración de scripts VSA en plataformas de 64 bits debido a la falta de compatibilidad con el diseñador de Visual Tools for Applications. Ejecute la migración bajo WOW64 en plataformas de 64 bits.|  
|0xC000931A|-1073704166|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_ERRORSINCOMMAND|La ejecución del comando generó errores.|  
|0xC000F427|-1073679321|DTS_E_SSISSTANDALONENOTINSTALLED|Para ejecutar un paquete SSIS fuera de [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] , debe instalar %1 de Integration Services o posterior.|  
|0xC0010001|-1073676287|DTS_E_VARIABLENOTFOUND|No se encuentra la variable. Esto sucede si, durante la ejecución de un paquete, se intenta recuperar una variable de la colección Variables de un contenedor y no se encuentra. Puede ser que el nombre de la variable haya cambiado o que ésta no se esté creando.|  
|0xC0010003|-1073676285|DTS_E_VARIABLEREADONLY|Error al intentar escribir en una variable de solo lectura, "%1".|  
|0xC0010004|-1073676284|DTS_E_MANAGEDCOMPONENTSTORENOTFOUND|No se encuentran los directorios que contienen los componentes de tareas y de la tarea Flujo de datos. Compruebe la integridad de la instalación.|  
|0xC0010006|-1073676282|DTS_E_PACKAGENAMETOOLONG|El nombre del paquete es demasiado largo. El límite es de 128 caracteres. Acorte el nombre del paquete.|  
|0xC0010007|-1073676281|DTS_E_PACKAGEDESCRIPTIONTOOLONG|La descripción del paquete es demasiado larga. El límite es de 1024 caracteres. Acorte la descripción del paquete.|  
|0xC0010008|-1073676280|DTS_E_VERCOMMENTSTOOLONG|La propiedad VersionComments es demasiado larga. El límite es de 1024 caracteres. Intente acortar VersionComments.|  
|0xC0010009|-1073676279|DTS_E_ELEMENTNOTFOUND|No se encuentra el elemento en una colección. Este error se produce si, durante la ejecución del paquete, se intenta recuperar un elemento de una colección de un contenedor y no se encuentra.|  
|0xC001000A|-1073676278|DTS_E_PACKAGENOTFOUND|No se pudo cargar el paquete especificado de la base de datos de SQL Server. |  
|0xC001000C|-1073676276|DTS_E_INVALIDVARIABLEVALUE|El valor asignado a la variable no es válido. Este error se produce si el cliente o una tarea asignan un objeto en tiempo de ejecución a un valor de la variable.|  
|0xC001000D|-1073676275|DTS_E_RESERVEDNAMESPACE|Error al asignar un espacio de nombres a la variable. El espacio de nombres "System" está reservado para uso del sistema. Este error se produce si un componente o tarea intenta crear una variable con un espacio de nombres "System".|  
|0xC001000E|-1073676274|DTS_E_CONNECTIONNOTFOUND|No se encuentra la conexión "%1". La colección Connections envía este error cuando no se encuentra el elemento de conexión específico.|  
|0xC001000F|-1073676273|DTS_E_64BITVARIABLERECAST|La variable "%1" es una variable entera de 64 bits no admitida en este sistema operativo. La variable se ha reasignado a una de tipo entero de 32 bits.|  
|0xC0010010|-1073676272|DTS_E_CANTCHANGEREADONLYATRUNTIME|Se intentó cambiar un atributo de solo lectura en la variable "%1". Este error se produce si se cambia en tiempo de ejecución un atributo de solo lectura de una variable. Los atributos de solo lectura solamente se pueden cambiar en tiempo de diseño.|  
|0xC0010011|-1073676271|DTS_E_VARIABLEINVALIDCONTAINERREF|Intento no válido de establecer una variable en una referencia de contenedor.  Las variables no pueden hacer referencia a los contenedores.|  
|0xC0010013|-1073676269|DTS_E_INVALIDVARVALUE|Asignación de un valor u objeto no válido a la variable "%1". Este error se genera cuando un valor no es adecuado para las variables.|  
|0xC0010014|-1073676268|DTS_E_GENERICERROR|Se produjeron uno o varios errores. Debería haber errores más específicos, anteriores a éste, donde se expliquen los detalles. Este mensaje se utiliza como un valor devuelto de funciones que encuentran errores.|  
|0xC0010016|-1073676266|DTS_E_INVALIDARRAYVALUE|Error al obtener o establecer un valor de matriz. El tipo "%1" no está permitido. Esto sucede cuando se carga una matriz en una variable.|  
|0xC0010017|-1073676265|DTS_E_UNSUPPORTEDARRAYTYPE|Tipo no compatible en una matriz. Esto ocurre cuando se guarda una matriz de tipos no compatibles en una variable.|  
|0xC0010018|-1073676264|DTS_E_PERSISTENCEERROR|Error al cargar el valor "%1" desde el nodo "%2".|  
|0xC0010019|-1073676263|DTS_E_INVALIDNODE|El nodo "%1" no es válido. Esto sucede si hay un error al guardar.|  
|0xC0010020|-1073676256|DTS_E_ERRORLOADINGTASK|No se pudo cargar la tarea "%1", tipo "%2". La información de contacto de esta tarea es "%3".|  
|0xC0010021|-1073676255|DTS_E_ERRORELEMENTNOTINCOLL|El elemento "%1" no existe en la colección "%2".|  
|0xC0010022|-1073676254|DTS_E_MISSINGOBJECTDATA|El elemento ObjectData falta en el bloque de XML de un objeto hospedado. Esto sucede si el analizador XML intenta localizar el elemento de datos de un objeto y no lo encuentra.|  
|0xC0010023|-1073676253|DTS_E_VARIABLENOTFOUNDINCOLL|No se encuentra la variable "%1". Este error se produce si, durante la ejecución de un paquete, se intenta recuperar una variable de una colección de variables de un contenedor y no se encuentra.  Puede ser que el nombre de la variable haya cambiado o que ésta no se esté creando.|  
|0xC0010025|-1073676251|DTS_E_HASEMPTYTASKHOSTS|El paquete no se puede ejecutar porque contiene tareas que no se cargaron.|  
|0xC0010026|-1073676250|DTS_E_TASKISEMPTY|La tarea no se ha cargado. La información de contacto de esta tarea es "%1".|  
|0xC0010027|-1073676249|DTS_E_ERRORLOADINGTASKNOCONTACT|Error al cargar la tarea "%1".|  
|0xC0010028|-1073676248|DTS_E_ERRORATLOADTASK|Error al cargar la tarea. Esto sucede si no se puede cargar una tarea de XML.|  
|0xC0010200|-1073675776|DTS_E_MULTIPLECACHEWRITES|"%1" no puede escribir en la caché porque %2 ya ha escrito en ella.|  
|0xC0010201|-1073675775|DTS_E_SETCACHEFORINSERTFAILED|Error al preparar la caché para los nuevos datos.|  
|0xC0010202|-1073675774|DTS_E_SETCACHEFORFILLFAILED|Error al marcar la caché como cumplimentada con datos.|  
|0xC0010203|-1073675773|DTS_E_READUNINITIALIZEDCACHE|La caché no se ha inicializado y "%1" no puede leer sus datos.|  
|0xC0010204|-1073675772|DTS_E_SETCACHEFORREADFAILED|Error al preparar la caché para proporcionar datos.|  
|0xC0010205|-1073675771|DTS_E_READNOTFILLEDCACHE|%1 está escribiendo en la caché y %2 no puede leer sus datos.|  
|0xC0010206|-1073675770|DTS_E_WRITEWHILECACHEINUSE|%1 está leyendo datos de la caché y %2 no puede escribir en ella.|  
|0xC0011001|-1073672191|DTS_E_CANTLOADFROMNODE|No se puede cargar el objeto de tiempo de ejecución del nodo XML especificado.  Esto sucede al intentar cargar un paquete u otro objeto de un nodo XML que no es del tipo correcto como, por ejemplo, un nodo XML que no sea de SSIS.|  
|0xC0011002|-1073672190|DTS_E_OPENPACKAGEFILE|No se pudo abrir el archivo de paquete "%1" debido al error 0x%2!8.8X! "%3".  Esto sucede si se carga un paquete y no es posible abrir o cargar correctamente el archivo en el documento XML. Puede ser que se haya proporcionado un nombre de archivo incorrecto al llamar a LoadPackage o que el archivo XML especificado tenga un formato incorrecto.|  
|0xC0011003|-1073672189|DTS_E_LOADPACKAGEXML|No se pudo cargar el archivo XML debido al error 0x%1!8.8X! "%2". Esto ocurre cuando se carga un paquete y el archivo no se puede abrir o cargar correctamente en el documento XML.  Esto puede ser debido a que se proporcionó un nombre de archivo incorrecto al método LoadPackage o a que el archivo XML especificado tenía un formato incorrecto.|  
|0xC0011004|-1073672188|DTS_E_LOADPACKAGEXMLFILE|No se pudo cargar el archivo XML del archivo de paquete "%1" debido al error 0x%2!8.8X!. "%3".  Esto ocurre cuando se carga un paquete y el archivo no se puede abrir o cargar correctamente en un documento XML. Esto puede ser debido a que se proporcionó un nombre de archivo incorrecto al método LoadPackage o a que el archivo XML especificado tenía un formato incorrecto.|  
|0xC0011005|-1073672187|DTS_E_OPENFILE|Error al abrir el archivo de paquete. Esto ocurre cuando se carga un paquete y el archivo no se puede abrir o cargar correctamente en un documento XML. Esto puede ser debido a que se proporcionó un nombre de archivo incorrecto al método LoadPackage o a que el archivo XML especificado tenía un formato incorrecto.|  
|0xC0011006|-1073672186|DTS_E_UNABLETODECODEBINARYFORMAT|No puede descodificar un formato binario en el paquete.|  
|0xC0011007|-1073672185|DTS_E_FUNDAMENTALLOADINGERROR|No se puede cargar el paquete como XML porque no tiene un formato XML válido. Se expondrá un error del analizador XML concreto.|  
|0xC0011008|-1073672184|DTS_E_LOADFROMXML|Error al cargar desde XML. No se puede proporcionar información más detallada del error porque no se pasó ningún objeto Events donde pueda almacenarse información detallada del error.|  
|0xC0011009|-1073672183|DTS_E_XMLDOMERROR|No puede crear una instancia del Modelo de objetos de documento de XML. Puede que no esté registrado MSXML.|  
|0xC001100D|-1073672179|DTS_E_CANNOTLOADOLDPACKAGES|No se puede cargar el paquete. Esto sucede si se intenta cargar un paquete de una versión anterior o si el archivo de paquete hace referencia a un objeto estructurado no válido.|  
|0xC001100E|-1073672178|DTS_E_SAVEFILE|Error al guardar el archivo de paquete.|  
|0xC001100F|-1073672177|DTS_E_SAVEPACKAGEFILE|No se pudo guardar el archivo de paquete "%1" con el error 0x%2!8.8X! "%3".|  
|0xC001200D|-1073668083|DTS_E_IDTSNAMENOTSUPPORTED|El objeto debe heredar de IDTSName100 y no es así.|  
|0xC0012018|-1073668072|DTS_E_CONFIGFORMATINVALID_PACKAGEDELIMITER|La entrada de configuración "%1" tiene un formato incorrecto porque no comienza por un delimitador de paquete. No contenía un delimitador "\package".|  
|0xC0012019|-1073668071|DTS_E_CONFIGFORMATINVALID|El formato de la entrada de configuración "%1" no es correcto. Es posible que falte un delimitador o que haya errores de formato, por ejemplo, un delimitador de matriz no válido.|  
|0xC001201B|-1073668069|DTS_E_CONFIGFILEFAILEDEXPORT|Error al exportar el archivo de configuración.|  
|0xC0012021|-1073668063|DTS_E_PROPERTIESCOLLECTIONREADONLY|No se puede modificar la colección Properties.|  
|0xC0012022|-1073668062|DTS_E_DTRXMLSAVEFAILURE|No se puede guardar el archivo de configuración. El archivo puede ser de solo lectura.|  
|0xC0012023|-1073668061|DTS_E_FAILPACKAGEONFAILURENA|La propiedad FailPackageOnFailure no es aplicable al contenedor de paquetes. |  
|0xC0012024|-1073668060|DTS_E_TASKPRODUCTLEVEL|No se puede ejecutar la tarea "%1" en la instalación %2 de Integration Services. Requiere %3 o una edición de nivel superior.|  
|0xC0012029|-1073668055|DTS_E_UNABLETOSAVETOFILE|No se puede guardar el archivo xml en "%1". El archivo puede ser de solo lectura.|  
|0xC0012037|-1073668041|DTS_E_CONFIGTYPECONVERSIONFAILED|Error al convertir un tipo en la configuración "%1" de la ruta de acceso del paquete "%2".  Esto sucede si no se puede convertir un valor de configuración de una cadena en el tipo de destino adecuado. Compruebe el valor de configuración para asegurarse de que puede convertirse al tipo de la propiedad o variable de destino.|  
|0xC0012049|-1073668023|DTS_E_CONFIGFAILED|Error de configuración. Se trata de una advertencia genérica para todos los tipos de configuración. Otras advertencias deben preceder a ésta con más información.|  
|0xC0012050|-1073668016|DTS_E_REMOTEPACKAGEVALIDATION|Error al validar el paquete de la tarea ExecutePackage. No se puede ejecutar el paquete.|  
|0xC0013001|-1073663999|DTS_E_FAILTOCREATEMUTEX|No se pudo crear la exclusión mutua "%1" a causa del error 0x%2!8.8X!.|  
|0xC0013002|-1073663998|DTS_E_MUTEXOWNBYDIFFUSER|La exclusión mutua "%1" ya existe y pertenece a otro usuario.|  
|0xC0013003|-1073663997|DTS_E_WAITFORMUTEXFAILED|No se pudo adquirir la exclusión mutua "%1" a causa del error 0x%2!8.8X!.|  
|0xC0013004|-1073663996|DTS_E_FAILTORELEASEMUTEX|No se pudo liberar la exclusión mutua "%1" a causa del error 0x%2!8.8X!.|  
|0xC0014003|-1073659901|DTS_E_INVALIDTASKPOINTER|El puntero de la tarea de contenedor no es válido. El contenedor tiene un puntero no válido a una tarea.|  
|0xC0014004|-1073659900|DTS_E_ALREADYADDED|Se ha agregado el ejecutable a la colección Executables de otro contenedor. Esto sucede si un cliente intenta agregar un ejecutable a más de una colección Executables. Es necesario quitar el ejecutable de la colección Executables actual antes de intentar agregarlo.|  
|0xC0014005|-1073659899|DTS_E_UNKNOWNCONNECTIONMANAGERTYPE|El tipo de conexión "%1" especificada para el administrador de conexiones "%2" no se reconoce como un tipo de administrador de conexiones válido. Este error se devuelve cuando se intenta crear un administrador de conexiones para un tipo de conexión desconocido. Compruebe si el nombre del tipo de conexión está escrito correctamente.|  
|0xC0014006|-1073659898|DTS_E_COLLECTIONCOULDNTADD|Se creó un objeto pero no se pudo agregar a una colección. Puede deberse a que no hay memoria suficiente.|  
|0xC0014007|-1073659897|DTS_E_ODBCERRORENV|Error al crear un entorno de Conectividad abierta de bases de datos (ODBC).|  
|0xC0014008|-1073659896|DTS_E_ODBCERRORDBC|Error al crear una conexión de base de datos de Conectividad abierta de bases de datos (ODBC).|  
|0xC0014009|-1073659895|DTS_E_ODBCERRORCONNECT|Error al intentar establecer una conexión de Conectividad abierta de bases de datos (ODBC) con el servidor de bases de datos.|  
|0xC001400A|-1073659894|DTS_E_CONNECTIONMANAGERQUALIFIERALREADYSET|Ya se ha establecido el calificador de esta instancia del administrador de conexiones. El calificador puede establecerse una sola vez por instancia.|  
|0xC001400B|-1073659893|DTS_E_CONNECTIONMANAGERQUALIFIERNOTSET|El calificador no se ha establecido en esta instancia del administrador de conexiones. Se requiere establecer el calificador para completar la inicialización.|  
|0xC001400C|-1073659892|DTS_E_CONNECTIONMANAGERQUALIFIERNOTSUPPORTED|Este administrador de conexiones no admite la especificación de calificadores.|  
|0xC001400D|-1073659891|DTS_E_CANNOTCLONECONNECTIONMANAGER|El administrador de conexiones "0x%1" no puede clonarse para ejecutarse fuera de proceso.|  
|0xC001400E|-1073659890|DTS_E_NOSQLPROFILERDLL|El proveedor de registro de SQL Server Profiler no pudo cargar el archivo pfclnt.dll. Compruebe que SQL Server Profiler está instalado.|  
|0xC001400F|-1073659889|DTS_E_LOGFAILED|Error en la infraestructura de registro de SSIS. Código de error: 0x%1!8.8X!. Este error indica que el error de registro no es atribuible a un proveedor de registro concreto.|  
|0xC0014010|-1073659888|DTS_E_LOGPROVIDERFAILED|Error del proveedor de registro de SSIS. Código de error: 0x%2!8.8X! (%3).  Este código indica que el error de registro se atribuye al proveedor de registro especificado.|  
|0xC0014011|-1073659887|DTS_E_SAVETOSQLSERVER_OLEDB|El método SaveToSQLServer encontró el código de error de OLE DB 0x%1!8.8X! (%2).  Error en la instrucción SQL emitida. |  
|0xC0014012|-1073659886|DTS_E_LOADFROMSQLSERVER_OLEDB|El método LoadFromSQLServer encontró el código de error de OLE DB 0x%1!8.8X! (%2).  Error en la instrucción SQL emitida. |  
|0xC0014013|-1073659885|DTS_E_REMOVEFROMSQLSERVER_OLEDB|El método RemoveFromSQLServer encontró el código de error de OLE DB 0x%1!8.8X! (%2) Error en la instrucción SQL emitida.|  
|0xC0014014|-1073659884|DTS_E_EXISTSONSQLSERVER_OLEDB|El método ExistsOnSQLServer encontró el código de error de OLE DB 0x%1!8.8X! (%2). Error en la instrucción SQL emitida.|  
|0xC0014015|-1073659883|DTS_E_CONNECTIONSTRING|OLE DB no pudo establecer una conexión de base de datos con la cadena de conexión proporcionada.|  
|0xC0014016|-1073659882|DTS_E_FROMEXECISNOTCHILD|Al agregar una restricción de precedencia, se especificó un ejecutable From que no es un elemento secundario de este contenedor.|  
|0xC0014017|-1073659881|DTS_E_TOEXECISNOTCHILD|El ejecutable To especificado al agregar una restricción de precedencia no es un elemento secundario de este contenedor.|  
|0xC0014018|-1073659880|DTS_E_ODBCTRANSACTIONENLIST|Error al intentar dar de alta una conexión ODBC en una transacción. SQLSetConnectAttr no puedo establecer el atributo SQL_ATTR_ENLIST_IN_DTC.|  
|0xC0014019|-1073659879|DTS_E_CONNECTIONOFFLINE|El administrador de conexiones "%1" no adquirirá una conexión porque la propiedad OfflineMode del paquete tiene el valor TRUE. Cuando OfflineMode es TRUE, no se pueden adquirir conexiones.|  
|0xC001401A|-1073659878|DTS_E_BEGINTRANSACTION|El objeto de tiempo de ejecución de SSIS no pudo iniciar la transacción distribuida debido al error 0x%1!8.8X! "%2". No se pudo iniciar la transacción de DTC. Esto puede deberse a que el servicio MSDTC no se está ejecutando.|  
|0xC001401B|-1073659877|DTS_E_SETQUALIFIERDESIGNTIMEONLY|No se puede llamar al método SetQualifier en un administrador de conexiones durante la ejecución de paquetes. Este método solamente se usa en tiempo de diseño.|  
|0xC001401C|-1073659876|DTS_E_SQLPERSISTENCEVERSION|El almacenamiento y la modificación de paquetes en SQL Server requieren que la base de datos y el tiempo de ejecución de SSIS sean de la misma versión. No se admite el almacenamiento de paquetes en versiones anteriores.|  
|0xC001401D|-1073659875|DTS_E_CONNECTIONVALIDATIONFAILED|Error al validar la conexión "%1".|  
|0xC001401E|-1073659874|DTS_E_INVALIDFILENAMEINCONNECTION|El nombre de archivo "%1" especificado en la conexión no era válido.|  
|0xC001401F|-1073659873|DTS_E_MULTIPLEFILESONRETAINEDCONNECTION|No se pueden especificar varios nombres de archivo en una conexión cuando la propiedad Retain es TRUE. Se encontraron barras verticales en la cadena de conexión, lo que significa que se especificaron varios nombres de archivo y, además, la propiedad Retain es TRUE.|  
|0xC0014020|-1073659872|DTS_E_ODBCERROR|Error de ODBC %1!d! .|  
|0xC0014021|-1073659871|DTS_E_PRECEDENCECONSTRAINT|Error en la restricción de precedencia entre "%1" y "%2".|  
|0xC0014022|-1073659870|DTS_E_FAILEDPOPNATIVEFEE|Error al llenar la colección ForEachEnumeratorInfos con ForEachEnumerators nativos. Código de error: %1.|  
|0xC0014023|-1073659869|DTS_E_GETENUMERATOR|Error del método GetEnumerator del enumerador Foreach: 0x%1!8.8X! "%2". Esto puede ocurrir si el enumerador ForEach no puede enumerar.|  
|0xC0014024|-1073659868|DTS_E_CANTGETCERTDATA|No es posible obtener datos de certificados sin formato del objeto de certificado proporcionado (error: %1). Esto sucede si CPackage::put_CertificateObject no puede crear una instancia del objeto ManagedHelper, se produce un error en el objeto ManagedHelper o el objeto ManagedHelper devuelve una matriz incorrecta.|  
|0xC0014025|-1073659867|DTS_E_CANTCREATECERTCONTEXT|Error al crear el contexto de certificado (error: %1). Esto sucede en CPackage::put_CertificateObject o CPackage::LoadFromXML cuando la función CryptoAPI correspondiente produce un error.|  
|0xC0014026|-1073659866|DTS_E_CANTOPENCERTSTORE|Error al abrir el almacén de certificados MY: "%1". Esto sucede en CPackage::LoadUserCertificateByName y en CPackage::LoadUserCertificateByHash.|  
|0xC0014027|-1073659865|DTS_E_CANTFINDCERTBYNAME|No se encuentra el certificado especificado por el nombre en el almacén MY (error: %1). Esto sucede en CPackage::LoadUserCertificateByName.|  
|0xC0014028|-1073659864|DTS_E_CANTFINDCERTBYHASH|No se encuentra el certificado especificado mediante hash en el almacén "MY" (error: %1). Esto sucede en CPackage:: LoadUserCertificateByHash.|  
|0xC0014029|-1073659863|DTS_E_INVALIDCERTHASHFORMAT|El valor hash no es una matriz de bytes unidimensional (error: %1). Esto sucede en CPackage:: LoadUserCertificateByHash.|  
|0xC001402A|-1073659862|DTS_E_CANTACCESSARRAYDATA|No se puede tener acceso a los datos de la matriz (error: %1). Este error puede producirse dondequiera que se llame a GetDataFromSafeArray.|  
|0xC001402B|-1073659861|DTS_E_CREATEMANAGEDHELPERFAILED|No se pudo crear el objeto de asistente administrado por SSIS. Error: 0x%1!8.8X! "%2". Esto sucede si hay un error en CoCreateInstance CLSID_DTSManagedHelper.|  
|0xC001402C|-1073659860|DTS_E_OLEDBTRANSACTIONENLIST|El objeto de tiempo de ejecución de SSIS no pudo dar de alta la conexión OLE DB en una transacción distribuida. Error: 0x%1!8.8X! "%2".|  
|0xC001402D|-1073659859|DTS_E_SIGNPACKAGEFAILED|Error de firma del paquete: 0x%1!8.8X! "%2". Esto sucede si hay un error en el método ManagedHelper.SignDocument. |  
|0xC001402E|-1073659858|DTS_E_CHECKENVELOPEFAILED|Error al comprobar la envolvente de la firma XML en el paquete. Error: 0x%1!8.8X! "%2". Esto sucede en CPackage::LoadFromXML.|  
|0xC001402F|-1073659857|DTS_E_GETXMLSOURCEFAILED|No se pudo obtener el origen XML del objeto DOM XML. Error: 0x%1!8.8X! "%2". Esto ocurre cuando se produce un error en IXMLDOMDocument::get_xml.|  
|0xC0014030|-1073659856|DTS_E_PACKAGEVERIFICATIONFAILED|No se pudo comprobar la firma criptográfica del paquete. Error: 0x%1!8.8X! "%2". Esto sucede si hay un error en la operación de comprobación de firma.|  
|0xC0014031|-1073659855|DTS_E_GETKEYFROMCERTFAILED|No se pudo obtener el par de claves de cifrado asociado al certificado especificado. Error: 0x%1!8.8X! "%2". Compruebe que tiene el par de claves para el cual se emitió el certificado. Este error suele producirse al intentar firmar un documento con un certificado para el cual no se tiene una clave privada.|  
|0xC0014032|-1073659854|DTS_E_INVALIDSIGNATURE|La firma digital no es válida. Se ha modificado el contenido del paquete.|  
|0xC0014033|-1073659853|DTS_E_UNTRUSTEDSIGNATURE|La firma digital es válida; sin embargo, el firmante no es de confianza y, por lo tanto, no se puede garantizar la autenticidad.|  
|0xC0014034|-1073659852|DTS_E_TRANSACTIONENLISTNOTSUPPORTED|La conexión no permite el alta en transacciones distribuidas.|  
|0xC0014035|-1073659851|DTS_E_PACKAGEPROTECT|No se pudo aplicar la protección del paquete. Error: 0x%1!8.8X! "%2". Este error se produce al guardar en XML.|  
|0xC0014036|-1073659850|DTS_E_PACKAGEUNPROTECT|No se pudo quitar la protección del paquete. Error: 0x%1!8.8X! "%2". Esto sucede en el método CPackage::LoadFromXML|  
|0xC0014037|-1073659849|DTS_E_PACKAGEPASSWORD|El paquete está cifrado con una contraseña. No se especificó la contraseña o no es correcta.|  
|0xC0014038|-1073659848|DTS_E_DUPLICATECONSTRAINT|Ya existe una restricción de precedencia entre los ejecutables especificados. No se permite más de una restricción de precedencia.|  
|0xC0014039|-1073659847|DTS_E_PACKAGELOADFAILED|No se pudo cargar el paquete. Error: 0x%1!8.8X! "%2". Esto sucede si hay un error en CPackage::LoadFromXML.|  
|0xC001403A|-1073659846|DTS_E_PACKAGEOBJECTNOTENVELOPED|No se pudo encontrar el objeto del paquete en la envolvente de la firma XML. Error: 0x%1!8.8X! "%2". Esto sucede si el XML firmado no contiene un paquete SSIS, tal y como se espera.|  
|0xC001403B|-1073659845|DTS_E_JAGGEDEVENTINFO|Los nombres de parámetros, tipos y matrices de descripciones no tienen la misma longitud. Deben tener la misma longitud. Esto sucede si la longitud de las matrices no coincide. Debería haber una entrada por cada parámetro de cada matriz.|  
|0xC001403C|-1073659844|DTS_E_GETPACKAGEINFOS|Error de OLE DB 0x%1!8.8X! (%2) durante la enumeración de los paquetes Se emitió una instrucción SQL y produjo un error.|  
|0xC001403D|-1073659843|DTS_E_UNKNOWNLOGPROVIDERTYPE|El tipo de proveedor de registro "%1" especificado para el proveedor de registro "%2" no se reconoce como un tipo de proveedor de registro válido. Este error se produce cuando se intenta crear un proveedor de registro de un tipo desconocido. Compruebe si el nombre del tipo de proveedor de registro está escrito correctamente.|  
|0xC001403E|-1073659842|DTS_E_UNKNOWNLOGPROVIDERTYPENOSUBS|El tipo de proveedor de registro no se reconoce como un tipo de proveedor de registro válido. Este error se produce cuando se intenta crear un proveedor de registro de un tipo desconocido. Compruebe si el nombre del tipo de proveedor de registro está escrito correctamente.|  
|0xC001403F|-1073659841|DTS_E_UNKNOWNCONNECTIONMANAGERTYPENOSUBS|El tipo de conexión especificado para el administrador de conexiones no es un tipo de administrador de conexiones válido. Este error se produce cuando se intenta crear un administrador de conexiones para un tipo de conexión desconocida. Compruebe si el nombre de tipo de conexión está escrito correctamente.|  
|0xC0014040|-1073659840|DTS_E_PACKAGEREMOVEFAILED|Error al intentar quitar el paquete "%1" de SQL Server.|  
|0xC0014042|-1073659838|DTS_E_FOLDERADDFAILED|Error al intentar crear en la carpeta "%2" de SQL Server una carpeta denominada "%1".|  
|0xC0014043|-1073659837|DTS_E_CREATEFOLDERONSQLSERVER_OLEDB|El método CreateFolderOnSQLServer encontró el código de error de OLE DB 0x%1!8.8X! (%2) Error en la instrucción SQL emitida.|  
|0xC0014044|-1073659836|DTS_E_FOLDERRENAMEFAILED|Error al cambiar el nombre de la carpeta "%1\\\\%2" a "%1\\\\%3" en SQL Server.|  
|0xC0014045|-1073659835|DTS_E_RENAMEFOLDERONSQLSERVER_OLEDB|El método RenameFolderOnSQLServer encontró el código de error de OLE DB 0x%1!8.8X! (%2). Error en la instrucción SQL emitida.|  
|0xC0014046|-1073659834|DTS_E_FOLDERDELETEFAILED|Error al eliminar la carpeta "%1" de SQL Server.|  
|0xC0014047|-1073659833|DTS_E_REMOVEFOLDERFROMSQLSERVER_OLEDB|El método RemoveFolderOnSQLServer encontró el código de error de OLE DB 0x%1!8.8X! (%2). Error en la instrucción SQL emitida.|  
|0xC0014048|-1073659832|DTS_E_INVALIDPATHTOPACKAGE|La ruta de acceso del paquete especificada no contiene un nombre de paquete. Esto sucede si la ruta no contiene al menos una barra diagonal inversa o una barra diagonal.|  
|0xC0014049|-1073659831|DTS_E_FOLDERNOTFOUND|No se encuentra la carpeta "%1".|  
|0xC001404A|-1073659830|DTS_E_FINDFOLDERONSQLSERVER_OLEDB|Error de OLE DB al intentar buscar una carpeta en SQL. Código de error: 0x%1!8.8X! (%2).|  
|0xC001404B|-1073659829|DTS_E_OPENLOGFAILED|El proveedor de registro de SSIS no pudo abrir el registro.  Código de error: 0x%1!8.8X!.|  
|0xC001404C|-1073659828|DTS_E_GETCONNECTIONINFOS|Error al obtener la colección ConnectionInfos: 0x%1!8.8X! "%2". Este error se produce cuando no se puede llamar a IDTSApplication100::get_ConnectionInfos.|  
|0xC001404D|-1073659827|DTS_E_VARIABLEDEADLOCK|Se detectó un interbloqueo al intentar bloquear las variables. Los bloqueos no pueden adquirirse después de 16 intentos. Se agotó el tiempo de espera de los bloqueos.|  
|0xC001404E|-1073659826|DTS_E_NOTDISPENSED|No se ha devuelto la colección Variables de VariableDispenser. Se intentó realizar una operación que solo se permite en colecciones dispensadas.|  
|0xC001404F|-1073659825|DTS_E_VARIABLESALREADYUNLOCKED|Esta colección Variables ya se ha desbloqueado. Solo se llama una vez al método Unlock en una colección Variables dispensada.|  
|0xC001404F|-1073659824|DTS_E_VARIABLEUNLOCKFAILED|Error al desbloquear una o varias variables.|  
|0xC0014051|-1073659823|DTS_E_DISPENSEDREADONLY|Se devolvió la colección Variables de VariableDispenser y no puede modificarse. No es posible agregar elementos ni quitarlos de las colecciones dispensadas.|  
|0xC0014052|-1073659822|DTS_E_VARIABLEALREADYONREADLIST|La variable "%1" ya está en la lista de lectura. Una variable solo puede agregarse una vez a la lista de bloqueo de lectura o a la lista de bloqueo de escritura.|  
|0xC0014053|-1073659821|DTS_E_VARIABLEALREADYONWRITELIST|La variable "%1" ya está en la lista de escritura. Una variable solo puede agregarse una vez a la lista de bloqueo de lectura o a la lista de bloqueo de escritura.|  
|0xC0014054|-1073659820|DTS_E_LOCKVARIABLEFORREAD|Error al bloquear el acceso de lectura de la variable "%1": 0x%2!8.8X! "%3".|  
|0xC0014055|-1073659819|DTS_E_LOCKVARIABLEFORWRITE|Error al bloquear el acceso de lectura/escritura de la variable "%1": 0x%2!8.8X! "%3".|  
|0xC0014056|-1073659818|DTS_E_CUSTOMEVENTCONFLICT|Ya se ha declarado el evento personalizado "%1" con una lista de parámetros distinta. Una tarea está intentando declarar un evento personalizado que ya ha sido declarado por otra tarea con una lista de parámetros distinta.|  
|0xC0014057|-1073659817|DTS_E_EVENTHANDLERNOTALLOWED|La tarea que proporciona el evento personalizado "%1" no permite controlar este evento en el paquete. El evento personalizado se declaró con AllowEventHandlers = FALSE.|  
|0xC0014059|-1073659815|DTS_E_UNSAFEVARIABLESALREADYSET|VariableDispenser recibió una colección Variables no segura. No se puede repetir esta operación.|  
|0xC001405A|-1073659814|DTS_E_INVALIDPARENTPACKAGEPATH|Se llamó a GetPackagePath en ForEachEnumerator pero no se especificó ninguna ruta de acceso del paquete ForEachLoop.|  
|0xC001405B|-1073659813|DTS_E_VARIABLEDEADLOCK_READ|Se detectó un interbloqueo al intentar bloquear el acceso de lectura de la variable "%1". No se pudo adquirir el bloqueo después de 16 intentos porque se agotó el tiempo de espera.|  
|0xC001405C|-1073659812|DTS_E_VARIABLEDEADLOCK_READWRITE|Se detectó un interbloqueo al intentar bloquear el acceso de lectura/escritura de las variables "%1". Un bloqueo no puede adquirirse después de 16 intentos. Se agotó el tiempo de espera de los bloqueos.|  
|0xC001405D|-1073659811|DTS_E_VARIABLEDEADLOCK_BOTH|Se detectó un interbloqueo al intentar bloquear el acceso de lectura de las variables "%1" y el acceso de lectura/escritura de las variables "%2". Un bloqueo no puede adquirirse después de 16 intentos. Se agotó el tiempo de espera de los bloqueos.|  
|0xC001405E|-1073659810|DTS_E_PACKAGEPASSWORDEMPTY|El nivel de protección del paquete requiere una contraseña, pero la propiedad PackagePassword está vacía.|  
|0xC001405F|-1073659809|DTS_E_DECRYPTXML_PASSWORD|Error al descifrar y cifrar el nodo XML porque no se especificó la contraseña o porque no era correcta. Se intentará continuar con la carga del paquete sin la información cifrada.|  
|0xC0014060|-1073659808|DTS_E_DECRYPTPACKAGE_USERKEY|Error al descifrar un paquete cifrado con una clave de usuario. Puede ser que no sea el usuario que cifró este paquete o que no esté utilizando el mismo equipo que se utilizó para guardar el paquete.|  
|0xC0014061|-1073659807|DTS_E_SERVERSTORAGEDISALLOWED|No se puede utilizar el nivel de protección ServerStorage al guardar en este destino. El sistema no pudo comprobar si el destino admite el almacenamiento seguro.|  
|0xC0014062|-1073659806|DTS_E_LOADFROMSQLSERVER|Error del método LoadFromSQLServer.|  
|0xC0014063|-1073659805|DTS_E_SIGNATUREPOLICYVIOLATION|No se puede cargar el paquete porque el estado de la firma digital infringe la directiva de firmas. Error 0x%1!8.8X! "%2"|  
|0xC0014064|-1073659804|DTS_E_SIGNATURENOTPRESENT|El paquete no está firmado.|  
|0xC0014065|-1073659803|DTS_E_SQLPROFILERDLL_ONLY_X86|El proveedor de registro de SQL Server Profiler no pudo cargar pfclnt.dll porque solamente se admite en sistemas de 32 bits.|  
|0xC0014100|-1073659648|DTS_E_NAMEALREADYADDED|No puede agregarse el objeto porque ya existe en la colección un objeto con el mismo nombre. Utilice otro nombre para solucionar este error.|  
|0xC0014101|-1073659647|DTS_E_NAMEALREADYEXISTS|No es posible cambiar el nombre de objeto "%1" por "%2" porque ya hay en la colección un objeto con ese nombre. Utilice otro nombre para solucionar este error.|  
|0xC0014103|-1073659645|DTS_E_FAILEDDEPENDENCIES|Error al enumerar las dependencias de paquetes. Consulte otros mensajes para obtener más información.|  
|0xC0014104|-1073659644|DTS_E_INVALIDCHECKPOINT_TRANSACTION|La configuración actual del paquete no es compatible.  Cambie la propiedad SaveCheckpoints o la propiedad TransactionOption.|  
|0xC001410E|-1073659634|DTS_E_CONNECTIONMANAGERJOINTRANSACTION|Error del administrador de conexiones al darse de baja en la transacción.|  
|0xC0015001|-1073655807|DTS_E_BPDUPLICATE|El Id. de punto de interrupción especificado ya existe. Este error se produce cuando una tarea llama a CreateBreakpoint varias veces con el mismo Id. Es posible crear varias veces un punto de interrupción con el mismo Id. si la tarea llama a RemoveBreakpoint en la primera creación, antes de crear el segundo.|  
|0xC0015002|-1073655806|DTS_E_BPUNKNOWNID|El Id. de punto de interrupción especificado no existe. Este error se produce cuando una tarea hace referencia a un punto de interrupción que no existe.|  
|0xC0015004|-1073655804|DTS_E_CANTWRITETOFILE|No se pudo abrir el archivo ""%1"" para escribir en él. Puede ser que el archivo sea de solo lectura o que no tenga los permisos correctos.|  
|0xC0015005|-1073655803|DTS_E_NOROWSETRETURNED|No hay ningún conjunto de filas de resultados asociado a la ejecución de esta consulta. El resultado no se ha especificado correctamente.|  
|0xC0015105|-1073655547|DTS_E_DUMP_FAILED|No se generaron correctamente los archivos de volcado de depuración. El código de hresult es 0x%1!8.8X!.|  
|0xC0016001|-1073651711|DTS_E_INVALIDURL|La dirección URL especificada no es válida. Esto puede suceder si la dirección URL del servidor o el proxy es null, o si el formato no es correcto. El formato de URL válido es http://ServerName:Port/ResourcePath o bien https://ServerName:Port/ResourcePath.|  
|0xC0016002|-1073651710|DTS_E_INVALIDSCHEME|La dirección URL %1 no es válida. Esto puede suceder si se especifica un esquema que no sea http o https, o si el formato de la dirección URL no es correcto. El formato de URL válido es http://ServerName:Port/ResourcePath o bien https://ServerName:Port/ResourcePath.|  
|0xC0016003|-1073651709|DTS_E_WINHTTPCANNOTCONNECT|No se puede establecer una conexión con el servidor %1. Este error puede producirse si el servidor no existe o si la configuración de proxy no es correcta.|  
|0xC0016004|-1073651708|DTS_E_CONNECTIONTERMINATED|Se ha restablecido la conexión con el servidor o ha finalizado. Vuelva a intentarlo más tarde.|  
|0xC0016005|-1073651707|DTS_E_LOGINFAILURE|Error en el intento de inicio de sesión de "%1". Este error se produce si las credenciales de inicio de sesión proporcionadas no son correctas. Compruebe las credenciales de inicio de sesión.|  
|0xC0016006|-1073651706|DTS_E_INVALIDSERVERNAME|No se puede resolver el nombre de servidor especificado en la dirección URL %1.|  
|0xC0016007|-1073651705|DTS_E_PROXYAUTH|Error de autenticación proxy. Este error se produce si no se proporcionan credenciales de inicio de sesión o si no son correctas.|  
|0xC0016008|-1073651704|DTS_E_SECUREFAILURE|La respuesta de certificado SSL obtenida del servidor no es válida. No se puede procesar la solicitud.|  
|0xC0016009|-1073651703|DTS_E_TIMEOUT|La solicitud ha agotado el tiempo de espera. Este error puede producirse si el tiempo de espera especificado es demasiado corto o si no puede establecerse una conexión con el servidor o proxy. Asegúrese de que la dirección URL del servidor y del proxy son correctas.|  
|0xC001600A|-1073651702|DTS_E_CLIENTAUTH|Falta el certificado de cliente. Este error se produce si el servidor está esperando un certificado de cliente SSL y el usuario ha proporcionado un certificado no válido o no ha proporcionado ningún certificado. Debe configurarse un certificado de cliente para esta conexión.|  
|0xC001600B|-1073651701|DTS_E_REDIRECTFAILURE|La dirección URL del servidor especificada, %1, tiene un redireccionamiento y se ha producido un error en la solicitud de redireccionamiento.|  
|0xC001600C|-1073651700|DTS_E_SERVERAUTH|Error de autenticación del servidor. Este error se produce si no se proporcionan credenciales de inicio de sesión o si no son correctas.|  
|0xC001600D|-1073651699|DTS_E_WINHTTPUNKNOWNERROR|No se puede procesar la solicitud. Vuelva a intentarlo más tarde.|  
|0xC001600E|-1073651698|DTS_E_UNKNOWNSTATUSCODE|El servidor devolvió el código de estado %1!u! : %2. Este error se produce si hay problemas en el servidor.|  
|0xC001600F|-1073651697|DTS_E_WINHTTPNOTSUPPORTED|Los servicios WinHttp no admiten esta plataforma.|  
|0xC0016010|-1073651696|DTS_E_INVALIDTIMEOUT|Valor de tiempo de espera no válido. El tiempo de espera debería estar en el intervalo entre %1!d! a %2!d!. (segundos).|  
|0xC0016011|-1073651695|DTS_E_INVALIDCHUNKSIZE|El tamaño del fragmento no es válido. La propiedad ChunkSize debería estar en el intervalo entre %1!d! a %2!d!. (en KB).|  
|0xC0016012|-1073651694|DTS_E_CERTERROR|Error al procesar el certificado de cliente. Este error puede producirse si el certificado de cliente proporcionado no se encuentra en el almacén de certificados personales. Compruebe si el certificado de cliente es válido.|  
|0xC0016013|-1073651693|DTS_E_FORBIDDEN|El servidor devolvió el código de error "403 - Prohibido". Este error puede producirse si el recurso especificado necesita acceso "https" pero ha expirado el período de validez del certificado, si el certificado no es válido para el usuario solicitado o si se ha revocado el certificado o no puede comprobarse la revocación.|  
|0xC0016014|-1073651692|DTS_E_WINHTTPOPEN|Error al inicializar la sesión HTTP con el proxy "%1". Este error puede producirse si se especifica un proxy no válido. El administrador de conexiones HTTP solamente admite servidores proxy de tipo CERN.|  
|0xC0016015|-1073651691|DTS_E_OPENCERTSTORE|Error al abrir almacén de certificados.|  
|0xC0016016|-1073651690|DTS_E_UNPROTECTXMLFAILED|Error al descifrar el nodo XML "%1" protegido: 0x%2!8.8X! "%3". Es posible que no esté autorizado para obtener acceso a esta información. Este error se produce si hay un error de cifrado. Compruebe si la clave es correcta.|  
|0xC0016017|-1073651689|DTS_E_UNPROTECTCONNECTIONSTRINGFAILED|Error al descifrar una cadena de conexión protegida del servidor "%1": 0x%2!8.8X! "%3". Es posible que no esté autorizado para obtener acceso a esta información. Este error se produce si hay un error de cifrado. Compruebe si la clave es correcta.|  
|0xC0016018|-1073651688|DTS_E_NEGATIVEVERSION|El número de versión no puede ser negativo. Este error se produce si el valor de la propiedad VersionMajor, VersionMinor o VersionBuild del paquete es negativo.|  
|0xC0016019|-1073651687|DTS_E_PACKAGEMIGRATED|Se ha migrado el paquete a una versión posterior durante la carga. Debe volver a cargarse para completar el proceso. Código de error interno.|  
|0xC0016020|-1073651680|DTS_E_PACKAGEMIGRATIONFAILED|Error al migrar el paquete de la versión %1!d! a la versión %2!d!: 0x%3!8.8X! "%4".|  
|0xC0016021|-1073651679|DTS_E_PACKAGEMIGRATIONMODULELOAD|Error al cargar el módulo de migración de paquetes.|  
|0xC0016022|-1073651678|DTS_E_PACKAGEMIGRATIONMODULE|Error en el módulo de migración de paquetes.|  
|0xC0016023|-1073651677|DTS_E_CANTDETERMINEWHICHPROPTOPERSIST|No se puede almacenar el objeto con la persistencia predeterminada. Este error se produce si la persistencia predeterminada no puede determinar los objetos que contiene el objeto hospedado.|  
|0xC0016024|-1073651676|DTS_E_CANTADDREMOVEWHENEXECUTING|No se puede agregar o quitar un elemento de un paquete en modo de tiempo de ejecución. Este error se produce si se intenta agregar o quitar un objeto de una colección mientras se está ejecutando el paquete.|  
|0xC0016025|-1073651675|DTS_E_NODENOTFOUND|No se encuentra el nodo "%1" en la persistencia personalizada predeterminada. Este error se produce si el XML de un objeto extensible guardado de forma predeterminada se ha cambiado y ya no se encuentra un objeto guardado, o si se cambia el propio objeto extensible.|  
|0xC0016026|-1073651674|DTS_E_COLLECTIONLOCKED|No se puede modificar esta colección durante la validación o ejecución del paquete.|  
|0xC0016027|-1073651673|DTS_E_COLLOCKED|La colección "%1" no se puede modificar durante la validación de paquetes ni la ejecución. No se puede agregar "%2" a la colección.|  
|0xC0016029|-1073651671|DTS_E_FTPNOTCONNECTED|No se ha establecido la conexión con el servidor FTP.|  
|0xC001602A|-1073651670|DTS_E_FTPERROR|Error en la operación de FTP solicitada. Descripción detallada del error: %1.|  
|0xC001602B|-1073651669|DTS_E_FTPINVALIDRETRIES|Número de reintentos no válido. El número de reintentos debe estar entre %1!d! y %2!d!.|  
|0xC001602C|-1073651668|DTS_E_LOADWININET|El administrador de conexiones FTP necesita la siguiente DLL para poder funcionar: %1.|  
|0xC001602D|-1073651667|DTS_E_FTPINVALIDCONNECTIONSTRING|El puerto especificado en la cadena de conexión no es válido. El formato de ConnectionString es ServerName:Port. El puerto debe ser un valor entero entre %1!d! y %2!d!.|  
|0xC001602E|-1073651666|DTS_E_FTPCREATEFOLDER|Creando la carpeta "%1"... %2.|  
|0xC001602F|-1073651665|DTS_E_FTPDELETEFOLDER|Eliminando la carpeta "%1" ... %2.|  
|0xC0016030|-1073651664|DTS_E_FTPCHANGEFOLDER|Cambiando el directorio actual por "%1". %2.|  
|0xC0016031|-1073651663|DTS_E_FTPFILESEMPTY|No hay ningún archivo para transferir. Este error puede producirse si se ejecuta una operación de envío o recepción y no se especifica ningún archivo para transferir.|  
|0xC0016032|-1073651662|DTS_E_FTPINVALIDLOCALPATH|La ruta de acceso local especificada no es válida. Especifique una ruta de acceso local válida. Esto puede producirse si la ruta de acceso local especificada tiene un valor null.|  
|0xC0016033|-1073651661|DTS_E_FTPNOFILESTODELETE|No se especificó ningún archivo para eliminar.|  
|0xC0016034|-1073651660|DTS_E_WINHTTPCERTDECODE|El error interno al cargar el certificado. Este error puede producirse si los datos del certificado no son válidos.|  
|0xC0016035|-1073651659|DTS_E_WINHTTPCERTENCODE|Error interno al guardar los datos del certificado.|  
|0xC0016049|-1073651639|DTS_E_CHECKPOINTMISMATCH|El archivo de punto de comprobación "%1" no coincide con este paquete. El Id. del paquete no coincide con el Id. del archivo de punto de comprobación.|  
|0xC001604A|-1073651638|DTS_E_CHECKPOINTFILEALREADYEXISTS|Parece ser que el contenido de un archivo de punto de comprobación existente no corresponde a este paquete, de forma que no se puede sobrescribir el archivo para empezar a guardar nuevos puntos de comprobación. Quite el archivo de punto de comprobación existente y vuelva a intentarlo. Este error se produce cuando hay un archivo de punto de comprobación y se establece que el paquete no debe utilizar un archivo de punto de comprobación sino guardar puntos de comprobación. No se sobrescribirá el archivo de punto de comprobación existente.|  
|0xC001604B|-1073651637|DTS_E_CHECKPOINTFILELOCKED|Otro proceso ha bloqueado el archivo de punto de comprobación "%1". Esto puede producirse si se está ejecutando otra instancia de este paquete.|  
|0xC001604C|-1073651636|DTS_E_OPENCHECKPOINTFILE|Error al abrir el archivo de punto de comprobación "%1". Error: 0x%2!8.8X! "%3".|  
|0xC001604D|-1073651635|DTS_E_CREATECHECKPOINTFILE|Error al crear el archivo de punto de comprobación "%1". Error: 0x%2!8.8X! "%3".|  
|0xC0016050|-1073651632|DTS_E_FTPINVALIDPORT|El puerto FTP contiene un valor no válido. El valor del puerto FTP debe ser un entero entre %1!d! y %2!d!.|  
|0xC00160AA|-1073651542|DTS_E_CONNECTTOSERVERFAILED|Error al conectar con el servicio SSIS en el equipo "%1":<br /><br /> %2.|  
|0xC0017002|-1073647614|DTS_E_PROPERTYEXPRESSIONSDISABLEDONVARIABLES|La propiedad Expression no se admite en objetos Variable. Use la propiedad EvaluateAsExpression en su lugar.|  
|0xC0017003|-1073647613|DTS_E_PROPERTYEXPRESSIONEVAL|No se puede evaluar la expresión "%1" en la propiedad "%2". Modifique la expresión para que sea válida.|  
|0xC0017004|-1073647612|DTS_E_PROPERTYEXPRESSIONSET|El resultado de la expresión "%1" en la propiedad "%2" no se puede escribir en la propiedad. Se evaluó la expresión pero no puede establecerse en la propiedad.|  
|0xC0017005|-1073647611|DTS_E_FORLOOPEVALEXPRESSIONINVALID|La expresión de evaluación del bucle no es válida. Es necesario modificar la expresión. Debería haber otros mensajes de error.|  
|0xC0017006|-1073647610|DTS_E_EXPRESSIONNOTBOOLEAN|El resultado de la evaluación de la expresión "%1" debe ser True o False. Cambie la expresión para que se evalúe como un valor booleano.|  
|0xC0017007|-1073647609|DTS_E_FORLOOPHASNOEXPRESSION|No hay ninguna expresión para evaluar en el bucle. Este error se produce si la expresión en el bucle For está vacía. Agregue una expresión.|  
|0xC0017008|-1073647608|DTS_E_FORLOOPASSIGNEXPRESSIONINVALID|La expresión de asignación del bucle no es válida y necesita modificarse. Debería haber otros mensajes de error.|  
|0xC0017009|-1073647607|DTS_E_FORLOOPINITEXPRESSIONINVALID|La expresión de inicialización del bucle no es válida y necesita modificarse. Debería haber otros mensajes de error.|  
|0xC001700A|-1073647606|DTS_E_INVALIDVERSIONNUMBER|El número de versión del paquete no es válido. El número de versión no puede ser mayor que el número de versión actual.|  
|0xC001700C|-1073647604|DTS_E_INVALIDVERNUMCANTBENEGATIVE|El número de versión del paquete no es válido. El número de versión es negativo.|  
|0xC001700D|-1073647603|DTS_E_PACKAGEUPDATEDISABLED|El paquete tiene una versión de formato antigua, pero la actualización automática de formato de paquetes está deshabilitada.|  
|0xC001700E|-1073647602|DTS_E_EXPREVALTRUNCATIONASERROR|Se produjo un truncamiento al evaluar la expresión.|  
|0xC0019001|-1073639423|DTS_E_FAILEDSETEXECVALVARIABLE|El contenedor no pudo establecer el valor de la variable especificada en la propiedad ExecutionValueVariable.|  
|0xC0019004|-1073639420|DTS_E_VARIABLEEXPRESSIONERROR|No se pudo evaluar la expresión de la variable "%1". Error en la expresión.|  
|0xC0019305|-1073638651|DTS_E_UNSUPPORTEDSQLVERSION|La operación que ha intentado realizar no es compatible con esta versión de la base de datos.|  
|0xC001A003|-1073635325|DTS_E_TXNSPECINVALID|No se puede especificar una transacción si se utiliza una conexión retenida. Este error se produce si se establece el valor TRUE en Retain en el administrador de conexiones, pero se llama a AcquireConnection con un parámetro de transacción que no sea null.|  
|0xC001A004|-1073635324|DTS_E_INCOMPATIBLETRANSACTIONCONTEXT|Se especificó un contexto de transacción no compatible en una conexión retenida. Esta conexión se ha establecido en un contexto de transacción distinto. Se pueden utilizar conexiones retenidas exactamente en un contexto de transacción.|  
|0xC001B001|-1073631231|DTS_E_NOTSUSPENDED|Error en la llamada a Resume porque el paquete no está suspendido. Esto sucede si el cliente llama a Resume pero el paquete no está suspendido.|  
|0xC001B002|-1073631230|DTS_E_ALREADYEXECUTING|Error en la llamada a Execute porque ya se está ejecutando el ejecutable. Este error se produce si el cliente llama a Execute en un contenedor que todavía se está ejecutando desde la última llamada a Execute.|  
|0xC001B003|-1073631229|DTS_E_NOTEXECUTING|Error en la llamada a Suspend o Resume porque no se está ejecutando el ejecutable o porque no es un ejecutable de nivel superior. Este error se produce si el cliente llama a Suspend o Resume en un ejecutable que actualmente no está procesando una llamada a Execute.|  
|0xC001C002|-1073627134|DTS_E_INVALIDFILE|El archivo especificado en el enumerador For Each File no es válido. Compruebe que el archivo especificado en el enumerador Foreach File existe.|  
|0xC001C010|-1073627120|DTS_E_VALUEINDEXNOTINTEGER|El índice de valor no es un entero. Asignando un número %1!d! de variable de Foreach a la variable “%2".|  
|0xC001C011|-1073627119|DTS_E_VALUEINDEXNEGATIVE|El índice de valor es negativo. Asignando un número %1!d! de variable de ForEach a la variable "%2".|  
|0xC001C012|-1073627118|DTS_E_FOREACHVARIABLEMAPPING|No se puede aplicar el número de variable de ForEach %1!d! a la variable "%2".|  
|0xC001C013|-1073627117|DTS_E_OBJECTNOTINFOREACHLOOP|Error al agregar un objeto a ForEachPropertyMapping que no es un elemento secundario directo del contenedor ForEachLoop.|  
|0xC001F001|-1073614847|DTS_E_FAILEDSYSTEMVARIABLEREMOVE|Error al quitar una variable del sistema. Este error se produce si se quita una variable necesaria.  Las variables necesarias son las que se crean en tiempo de ejecución para establecer la comunicación entre las tareas y el tiempo de ejecución.|  
|0xC001F002|-1073614846|DTS_E_CHANGESYSTEMVARIABLEREADONLYFAILED|Error al cambiar la propiedad de una variable porque es una variable del sistema. Las variables del sistema son de solo lectura.|  
|0xC001F003|-1073614845|DTS_E_CHANGESYSTEMVARIABLENAMEFAILED|Error al cambiar el nombre de una variable porque es una variable del sistema. Las variables del sistema son de solo lectura.|  
|0xC001F004|-1073614844|DTS_E_CHANGESYSTEMVARIABLENAMESPACEFAILED|Error al cambiar el espacio de nombres de una variable porque es una variable del sistema. Las variables del sistema son de solo lectura.|  
|0xC001F006|-1073614842|DTS_E_EVENTHANDLERNAMEREADONLY|Error al cambiar el nombre del controlador de eventos. Los nombres de controlador de eventos son de solo lectura.|  
|0xC001F008|-1073614840|DTS_E_PATHUNKNOWN|No se puede recuperar la ruta de acceso la objeto. Error de sistema.|  
|0xC001F009|-1073614839|DTS_E_RUNTIMEVARIABLETYPECHANGE|El tipo del valor asignado a la variable "%1" difiere del tipo de variable actual. Las variables no pueden cambiar de tipo durante su ejecución. Los tipos de variable son estrictos, excepto en las variables de tipo Object.|  
|0xC001F010|-1073614832|DTS_E_INVALIDSTRING|Caracteres no válidos en la cadena "%1". Esto sucede si una cadena proporcionada para un valor de propiedad contiene caracteres que no pueden imprimirse.|  
|0xC001F011|-1073614831|DTS_E_INVALIDOBJECTNAME|El nombre de objeto SSIS no válido. Se habrán mostrado errores más específicos donde se explique el problema exacto de asignación de nombre.|  
|0xC001F021|-1073614815|DTS_E_PROPERTYREADONLY|La propiedad "%1" es de solo lectura. Esto sucede si se intenta cambiar una propiedad de solo lectura.|  
|0xC001F022|-1073614814|DTS_E_FAILEDGETTYPEINFO|El objeto no admite la información de tipo. Esto sucede si el objeto de tiempo de ejecución intenta obtener la información de tipo de un objeto para llenar la colección Properties.  El objeto debe admitir la información de tipo.|  
|0xC001F023|-1073614813|DTS_E_FAILEDPROPERTYGET|Error al recuperar el valor de la propiedad "%1". Código de error: 0x%2!8.8X!.|  
|0xC001F024|-1073614812|DTS_E_FAILEDPROPERTYGET_ERRORINFO|Error al recuperar el valor de la propiedad "%1". Código de error: 0x%2!8.8X! "%3".|  
|0xC001F025|-1073614811|DTS_E_FAILEDPROPERTYSET|Error al establecer el valor de la propiedad "%1". El error devuelto es 0x%2!8.8X!.|  
|0xC001F026|-1073614810|DTS_E_FAILEDPROPERTYSET_ERRORINFO|Error al establecer el valor de la propiedad "%1". El error devuelto es 0x%2!8.8X! "%3".|  
|0xC001F027|-1073614809|DTS_E_PROPERTYWRITEONLY|La propiedad "%1" es de solo escritura. Este error se produce si se intenta recuperar el valor de una propiedad a través de un objeto de propiedad, pero la propiedad es de solo escritura.|  
|0xC001F028|-1073614808|DTS_E_NODISPATCH|El objeto no implementa IDispatch. Este error se produce si un objeto de propiedad o una colección de propiedades intenta obtener acceso a una interfaz IDispatch en un objeto.|  
|0xC001F029|-1073614807|DTS_E_NOCONTAININGTYPELIB|No se puede recuperar la biblioteca de tipos del objeto. Este error se produce si la colección Properties intenta recuperar la biblioteca de tipos de un objeto a través de su interfaz IDispatch.|  
|0xC001F02A|-1073614806|DTS_E_INVALIDTASKMONIKER|No se puede crear una tarea a partir de XML para la tarea "%1!s!", tipo "%2!s!". debido al error 0x%3!8.8X! "%4!s!".|  
|0xC001F02C|-1073614804|DTS_E_FAILEDCREATEXMLDOCUMENT|Error al crear un documento XML "%1".|  
|0xC001F02D|-1073614803|DTS_E_PMVARPROPTYPESDIFFERENT|Se produjo un error porque se asignó una propiedad de una variable a una propiedad con un tipo distinto. El tipo de propiedad debe coincidir con el tipo de variable.|  
|0xC001F02E|-1073614802|DTS_E_PMINVALIDPROPMAPTARGET|Se intentó establecer la asignación de propiedad a un tipo de objeto de destino no compatible. Este error se produce si se pasa un tipo de objeto no compatible a una asignación de propiedad.|  
|0xC001F02F|-1073614801|DTS_E_COULDNOTRESOLVEPACKAGEPATH|No se puede resolver la ruta de acceso de un paquete a un objeto del paquete "%1".  Compruebe si la ruta de acceso del paquete es válida.|  
|0xC001F030|-1073614800|DTS_E_PMNODESTPROPERTY|La propiedad de destino de la asignación de propiedad está vacía. Establezca el nombre de la propiedad de destino.|  
|0xC001F031|-1073614799|DTS_E_INVALIDPROPERTYMAPPINGSFOUND|El paquete no pudo restaurar la asignación de al menos una propiedad.|  
|0xC001F032|-1073614798|DTS_E_AMBIGUOUSVARIABLENAME|El nombre de la variable es ambiguo porque hay varias variables con este nombre en distintos espacios de nombres. Especifique el nombre calificado de espacio de nombres para evitar la ambigüedad.|  
|0xC001F033|-1073614797|DTS_E_DESTINATIONOBJECTPARENTLESS|El objeto de destino de una asignación de propiedad no tiene elemento primario. El objeto de destino no es un elemento secundario de ningún contenedor de secuencias. Es posible que se haya quitado del paquete.|  
|0xC001F036|-1073614794|DTS_E_INVALIDPROPERTYMAPPING|La asignación de propiedad no es válida. Se omitirá la asignación.|  
|0xC001F038|-1073614792|DTS_E_PMFAILALERTREMOVE|Error al avisar a las asignaciones de propiedad de que se ha quitado un destino.|  
|0xC001F03A|-1073614790|DTS_E_INVALIDFOREACHPROPERTYMAPPING|Asignación de propiedad no válida en el bucle For Each. Esto sucede si no puede restaurarse la asignación de propiedad ForEach.|  
|0xC001F040|-1073614784|DTS_E_PMPROPERTYINVALID|Se especificó una propiedad de destino en una asignación de propiedad no válida. Esto sucede si se especifica una propiedad en un objeto de destino que no se encuentra en dicho objeto.|  
|0xC001F041|-1073614783|DTS_E_INVALIDTASKMONIKERNOPARAM|No se puede crear una tarea desde XML. Esto sucede si el objeto de tiempo de ejecución no puede resolver el nombre para crear una tarea. Compruebe si el nombre es correcto.|  
|0xC001F080|-1073614720|DTS_E_COULDNOTREPLACECHECKPOINTFILE|No se puede sustituir el archivo de punto de comprobación actual por el archivo de punto de comprobación actualizado. El punto de comprobación se creó correctamente en un archivo temporal pero no se pudo sobrescribir el archivo existente con el nuevo archivo.|  
|0xC001F081|-1073614719|DTS_E_CHECKPOINTFILENOTSPECIFIED|El paquete está configurado para reiniciarse siempre desde un punto de comprobación, pero no se ha especificado ningún archivo de punto de comprobación.|  
|0xC001F082|-1073614718|DTS_E_CHECKPOINTLOADXML|Error al intentar cargar el archivo de punto de comprobación XML "%1". Error: 0x%2!8.8X! "%3". Compruebe si el nombre de archivo especificado es correcto y si el archivo existe.|  
|0xC001F083|-1073614717|DTS_E_LOADCHECKPOINT|No pudo ejecutarse el paquete porque no puede cargarse el archivo de punto de comprobación. La ejecución del paquete requiere un archivo de punto de comprobación. Este error suele producirse si en la propiedad CheckpointUsage se establece el valor ALWAYS, que especifica que el paquete se reinicia siempre.|  
|0xC001F185|-1073614459|DTS_E_NOEVALEXPRESSION|La expresión de condición de evaluación en el bucle For "%1" está vacía. Debe haber una expresión de evaluación booleana en el bucle For.|  
|0xC001F186|-1073614458|DTS_E_EXPREVALASSIGNMENTTYPEMISMATCH|El resultado de la expresión de asignación "%1" no puede convertirse a un tipo compatible con la variable a la que se asignó.|  
|0xC001F187|-1073614457|DTS_E_EXPREVALASSIGNMENTTOREADONLYVARIABLE|Error al usar una variable de solo lectura "%1" en una expresión de asignación. El resultado de la expresión no puede asignarse a la variable porque ésta es de solo lectura. Elija una variable en la que se pueda escribir o quite la expresión de esta variable.|  
|0xC001F188|-1073614456|DTS_E_EXPREVALASSIGNMENTVARIABLELOCKFORWRITEFAILED|No se puede evaluar la expresión "%1" porque la variable "%2" no existe o no tiene acceso de escritura. El resultado de la expresión no se puede asignar a la variable porque no se encontró la variable o no pudo bloquearse en ella el acceso de escritura.|  
|0xC001F189|-1073614455|DTS_E_EXPREVALRESULTTYPENOTSUPPORTED|La expresión "%1" tiene un tipo de resultado, "%2", que no puede convertirse a un tipo compatible.|  
|0xC001F18A|-1073614454|DTS_E_EXPREVALRESULTTYPECONVERSIONFAILED|Error al convertir el resultado de la expresión "%1" del tipo "%2" a un tipo compatible. Código de error: 0x%3!8.8X!. Ocurrió un error inesperado al intentar convertir el resultado de la expresión a un tipo compatible con el motor de tiempo de ejecución, aunque se admita la conversión de tipo.|  
|0xC001F200|-1073614336|DTS_E_DTSNAME_NOTNULL|El nombre de objeto no es válido. El nombre no puede tener el valor NULL.|  
|0xC001F201|-1073614335|DTS_E_DTSNAME_NOTEMPTY|El nombre de objeto no es válido. El nombre no puede estar en blanco.|  
|0xC001F202|-1073614334|DTS_E_DTSNAME_LEGAL|El nombre de objeto "%1" no es válido. El nombre no puede contener los caracteres siguientes: =|  
|0xC001F203|-1073614333|DTS_E_DTSNAME_PRINTABLE|El nombre de objeto "%1" no es válido. El nombre no puede contener caracteres de control que impidan que pueda imprimirse.|  
|0xC001F204|-1073614332|DTS_E_DTSNAME_NOLEADWHITESP|El nombre de objeto "%1" no es válido. El nombre no puede comenzar con un espacio en blanco.|  
|0xC001F205|-1073614331|DTS_E_DTSNAME_NOTRAILWHITESP|El nombre de objeto "%1" no es válido. El nombre no puede terminar en un espacio en blanco.|  
|0xC001F206|-1073614330|DTS_E_DTSNAME_BEGINSWITHALPHA|El nombre de objeto "%1" no es válido. El nombre debe comenzar con un carácter alfabético.|  
|0xC001F207|-1073614329|DTS_E_DTSNAME_BEGINSWITHALPHAUNDERBAR|El nombre de objeto "%1" no es válido. El nombre debe comenzar por un carácter alfabético o un signo de subrayado "_".|  
|0xC001F208|-1073614328|DTS_E_DTSNAME_ALPHADIGITUNDERBAR|El nombre de objeto "%1" no es válido. El nombre solamente puede contener caracteres alfanuméricos o de subrayado "_".|  
|0xC001F209|-1073614327|DTS_E_DTSNAME_VALIDFILENAME|El nombre de objeto "%1" no es válido. El nombre no puede contener los caracteres siguientes: / \ : ? " \< >&#124;|  
|0xC001F420|-1073613792|DTS_E_FAILLOADINGPROPERTY|No se pudo cargar la propiedad de valor "%1" usando la persistencia predeterminada.|  
|0xC001F422|-1073613790|DTS_E_NODELISTENUM_INVALIDCONNMGRTYPE|El administrador de conexiones "%1" no es del tipo "%2"|  
|0xC001F423|-1073613789|DTS_E_NODELISTENUM_XPATHISEMPTY|"%1" está vacío|  
|0xC001F424|-1073613788|DTS_E_NODELISTENUM_INVALIDDATANODE|Nodo de datos no válido en la sección del enumerador de lista de nodos|  
|0xC001F425|-1073613787|DTS_E_NODELISTENUM_NOENUMERATORCREATED|No se puede crear ningún enumerador|  
|0xC001F427|-1073613785|DTS_E_OPERATIONFAILCACHEINUSE|Error de la operación porque la caché está en uso.|  
|0xC001F428|-1073613784|DTS_E_PROPERTYCANNOTBEMODIFIED|No se puede modificar la propiedad.|  
|0xC001F429|-1073613783|DTS_E_PACKAGEUPGRADEFAILED|Error al actualizar el paquete.|  
|0xC00220DE|-1073602338|DTS_E_TKEXECPACKAGE_UNABLETOLOADFILE|Error 0x%1!8.8X! al cargar el archivo de paquete "%3". %2.|  
|0xC00220DF|-1073602337|DTS_E_TKEXECPACKAGE_UNSPECIFIEDPACKAGE|No se ha especificado el paquete.|  
|0xC00220E0|-1073602336|DTS_E_TKEXECPACKAGE_UNSPECIFIEDCONNECTION|No se ha especificado la conexión.|  
|0xC00220E2|-1073602334|DTS_E_TKEXECPACKAGE_INCORRECTCONNECTIONMANAGERTYPE|El administrador de conexiones "%1" tiene un tipo "%2" no compatible. Solo se admiten los administradores de conexión "FILE" y "OLEDB".|  
|0xC00220E3|-1073602333|DTS_E_TKEXECPACKAGE_UNABLETOLOADXML|Error 0x%1!8.8X! al cargar el archivo de paquete "%3" en un documento XML. %2.|  
|0xC00220E4|-1073602332|DTS_E_TKEXECPACKAGE_UNABLETOLOAD|Error 0x%1!8.8X! al preparar la carga del paquete. %2.|  
|0xC0024102|-1073594110|DTS_E_TASKVALIDATIONFAILED|Error del método Validate en la tarea. Se devolvió el código de error 0x%1!8.8X! (%2). El método Validate debe ejecutarse correctamente e indicar el resultado con un parámetro "out".|  
|0xC0024104|-1073594108|DTS_E_TASKEXECUTEFAILED|El método Execute en la tarea devolvió el código de error 0x%1!8.8X! (%2). El método Execute debe ejecutarse correctamente e indicar el resultado con un parámetro "out".|  
|0xC0024105|-1073594107|DTS_E_RETRIEVINGDEPENDENCIES|Error en la tarea “%1": 0x%2!8.8X! mientras se recuperaban las dependencias. El error se produjo cuando se recuperaban las dependencias de la colección de dependencias de la tarea. Puede ser que la tarea haya implementado incorrectamente una de las interfaces de dependencia.|  
|0xC0024107|-1073594105|DTS_E_TASKVALIDATIONERROR|Se produjeron errores al validar la tarea.|  
|0xC0024108|-1073594104|DTS_E_CONNECTIONSTRINGFORMAT|El formato de la cadena de conexión no es válido. Debe estar formado por uno o más componentes X=Y, separados por puntos y comas. Este error se produce si se establece una cadena de conexión con cero componentes en el administrador de conexiones de base de datos.|  
|0xC0024109|-1073594103|DTS_E_UNQUOTEDSEMICOLON|Los componentes de la cadena de conexión no pueden contener puntos y comas sin comillas. Si el valor debe contener un punto y coma, ponga todo el valor entre comillas. Este error se produce si los valores de la cadena de conexión contienen puntos y comas sin comillas, como la propiedad InitialCatalog.|  
|0xC002410A|-1073594102|DTS_E_LOGPROVIDERVALIDATIONFAILED|Error al validar uno o varios proveedores de registro. El paquete no se puede ejecutar. El paquete no se ejecuta cuando hay un error de validación en un proveedor de registro.|  
|0xC002410B|-1073594101|DTS_E_INVALIDVALUEINARRAY|Valor no válido en la matriz.|  
|0xC002410C|-1073594100|DTS_E_ENUMERATIONELEMENTNOTENUMERABLE|Un elemento del enumerador devuelto por el enumerador ForEach no implementa IEnumerator, en contra de lo que indica la propiedad CollectionEnumerator del enumerador ForEach.|  
|0xC002410D|-1073594099|DTS_E_INVALIDENUMERATORINDEX|El enumerador no pudo recuperar el elemento en el índice "%1!d!".|  
|0xC0029100|-1073573632|DTS_E_AXTASK_MISSING_ENTRY_METHOD_NAME|No se encuentra la función.|  
|0xC0029101|-1073573631|DTS_E_AXTASK_EMPTY_SCRIPT|No se encuentra la función.|  
|0xC0029102|-1073573630|DTS_E_AXTASK_INITIALIZATION_WITH_WRONG_XML_ELEMENT|Se inició la tarea Script de ActiveX con un elemento XML incorrecto.|  
|0xC0029105|-1073573627|DTS_E_AXTASK_HANDLER_NOT_FOUND|No se encuentra el controlador.|  
|0xC0029106|-1073573626|DTS_E_AXTASKUTIL_ENUMERATE_LANGUAGES_FAILED|Error al intentar recuperar los lenguajes de scripting instalados en el sistema.|  
|0xC0029107|-1073573625|DTS_E_AXTASKUTIL_SCRIPTHOST_CREATE_FAILED|Error al crear el host de script de ActiveX. Compruebe si se ha instalado correctamente el host de script.|  
|0xC0029108|-1073573624|DTS_E_AXTASKUTIL_SCRIPTHOSTINIT_FAILED|Error al intentar crear una instancia del host de script del lenguaje elegido. Compruebe si el lenguaje de script elegido está instalado en el sistema.|  
|0xC0029109|-1073573623|DTS_E_AXTASKUTIL_ADDVARIABLES_FAILED|Error al agregar las variables SSIS al espacio de nombres del host de script. Esto podría impedir que la tarea utilizara variables SSIS en el script.|  
|0xC002910A|-1073573622|DTS_E_AXTASKUTIL_SCRIPT_PARSING_FAILED|Error irrecuperable al intentar analizar el texto del script. Compruebe si el motor de script del lenguaje elegido está instalado correctamente.|  
|0xC002910B|-1073573621|DTS_E_AXTASKUTIL_MSG_BAD_FUNCTION|El nombre de función especificado no es válido. Compruebe que se ha especificado un nombre de función válido.|  
|0xC002910C|-1073573620|DTS_E_AXTASKUTIL_EXECUTION_FAILED|Error al ejecutar el script. Compruebe que el motor de script del lenguaje seleccionado está instalado correctamente.|  
|0xC002910D|-1073573619|DTS_E_AXTASKUTIL_ADDTYPELIB_FAILED|Error al agregar la biblioteca de tipos administrada al host de script. Compruebe que está instalado el objeto de tiempo de ejecución de DTS 2000.|  
|0xC002910E|-1073573618|DTS_E_BITASK_INITIALIZATION_WITH_WRONG_XML_ELEMENT|Se inició la tarea Inserción masiva con un elemento XML incorrecto.|  
|0xC002910F|-1073573617|DTS_E_BITASK_DATA_FILE_NOT_SPECIFIED|No se especificó el nombre del archivo de datos.|  
|0xC0029110|-1073573616|DTS_E_BITASK_HANDLER_NOT_FOUND|No se encuentra el controlador.|  
|0xC0029111|-1073573615|DTS_E_BITASK_CANNOT_ACQUIRE_CONNECTION|Error al adquirir la conexión especificada: "%1".|  
|0xC0029112|-1073573614|DTS_E_BITASK_NO_CONNECTION_MANAGER_SPECIFIED|Error al intentar obtener el Administrador de conexiones.|  
|0xC0029113|-1073573613|DTS_E_BITASK_INVALID_CONNECTION|La conexión no es válida.|  
|0xC0029114|-1073573612|DTS_E_BITASK_NULL_CONNECTION|La conexión es nula.|  
|0xC0029115|-1073573611|DTS_E_BITASK_EXECUTE_FAILED|Error de ejecución.|  
|0xC0029116|-1073573610|DTS_E_BITASK_CANNOT_RETRIEVE_TABLES|Error al recuperar las tablas de la base de datos.|  
|0xC0029117|-1073573609|DTS_E_BITASK_CANNOT_RETRIEVE_COLUMN_INFO|Error al recuperar las columnas de la tabla.|  
|0xC0029118|-1073573608|DTS_E_BITASK_ERROR_IN_DB_OPERATION|Error en la operación de base de datos.|  
|0xC0029119|-1073573607|DTS_E_BITASK_INVALIDSOURCECONNECTIONNAME|La conexión especificada "%1" no es válida o apunta a un objeto no válido. Para continuar, especifique una conexión válida.|  
|0xC002911A|-1073573606|DTS_E_BITASK_INVALIDDESTCONNECTIONNAME|La conexión de destino especificada no es válida. Proporcione una conexión válida para poder continuar.|  
|0xC002911B|-1073573605|DTS_E_BITASK_DESTINATION_TABLE_NOT_SPECIFIED|Debe especificar un nombre de tabla para poder continuar.|  
|0xC002911C|-1073573604|DTS_E_BITASK_ERROR_IN_LOAD_FROM_XML|Error de LoadFromXML en la etiqueta "%1".|  
|0xC002911D|-1073573603|DTS_E_BITASK_ERROR_IN_SAVE_TO_XML|Error de SaveToXML en la etiqueta "%1".|  
|0xC002911E|-1073573602|DTS_E_BITASKUNMANCONNECTION_INVALID_CONNECTION|La conexión no es válida.|  
|0xC002911F|-1073573601|DTS_E_BITASKUNMANCONNECTION_EXECUTE_FAILED|Error de ejecución.|  
|0xC0029120|-1073573600|DTS_E_BITASKUNMANCONNECTION_CANNOT_RETRIEVE_TABLES|Error al recuperar las tablas de la base de datos.|  
|0xC0029121|-1073573599|DTS_E_BITASKUNMANCONNECTION_CANNOT_RETRIEVE_COLUMN_INFO|Error al recuperar las columnas de la tabla.|  
|0xC0029122|-1073573598|DTS_E_BITASKUNMANCONNECTION_CANNOT_OPEN_FILE|Error al intentar abrir el archivo de datos.|  
|0xC0029123|-1073573597|DTS_E_BITASKUNMANCONNECTION_OEM_CONVERSION_FAILED|No se puede convertir el archivo OEM de entrada al formato especificado.|  
|0xC0029124|-1073573596|DTS_E_BITASKUNMANCONNECTION_ERROR_IN_DB_OPERATION|Error de funcionamiento de la base de datos.|  
|0xC0029125|-1073573595|DTS_E_DTSPROCTASK_NOCONNECTIONSPECIFIED|Administrador de conexiones no especificado.|  
|0xC0029126|-1073573594|DTS_E_DTSPROCTASK_CONNECTIONMANAGERNOTOLAP|La conexión "%1" no es una conexión de Analysis Services.|  
|0xC0029127|-1073573593|DTS_E_DTSPROCTASK_UNABLETOLOCATECONNECTIONMANAGER|No se puede encontrar la conexión "%1".|  
|0xC0029128|-1073573592|DTS_E_DTSPROCTASK_INVALIDTASKDATANODEEXE|La tarea Ejecutar DDL de Analysis Services recibió un nodo de datos de tarea no válido.|  
|0xC0029129|-1073573591|DTS_E_DTSPROCTASK_INVALIDTASKDATANODEPROC|La tarea Procesamiento de Analysis Services recibió un nodo de datos de tarea no válido.|  
|0xC002912A|-1073573590|DTS_E_DTSPROCTASK_INVALIDDDL|El DDL no es válido.|  
|0xC002912B|-1073573589|DTS_E_DTSPROCTASK_INVALIDDDLPROCESSINGCOMMANDS|Se encontró un DDL no válido en ProcessingCommands.|  
|0xC002912C|-1073573588|DTS_E_DTSPROCTASK_CANNOTWRITEINAREADONLYVARIABLE|El resultado de la ejecución no se puede guardar en una variable de solo lectura.|  
|0xC002912D|-1073573587|DTS_E_DTSPROCTASK_INVALIDVARIABLE|No se ha definido la variable "%1".|  
|0xC002912E|-1073573586|DTS_E_DTSPROCTASK_CONNECTIONNOTFOUND|No se ha definido el administrador de conexiones "%1".|  
|0xC002912F|-1073573585|DTS_E_DTSPROCTASK_INVALIDCONNECTION|El administrador de conexiones "%1" no es un administrador de conexiones de archivos.|  
|0xC0029130|-1073573584|DTS_E_DTSPROCTASK_NONEXISTENTATTRIBUTE|No se encontró "%1" durante la deserialización.|  
|0xC0029131|-1073573583|DTS_E_DTSPROCTASK_TRACEHASBEENSTOPPED|Se detuvo el seguimiento a causa de una excepción.|  
|0xC0029132|-1073573582|DTS_E_DTSPROCTASK_DDLEXECUTIONFAILED|Error de ejecución de DDL.|  
|0xC0029133|-1073573581|DTS_E_DTSPROCTASK_FILEDOESNOTEXIST|No hay ningún archivo asociado a la conexión "%1".|  
|0xC0029134|-1073573580|DTS_E_DTSPROCTASK_VARIABLENOTDEFINED|La variable "%1" no está definida.|  
|0xC0029135|-1073573579|DTS_E_DTSPROCTASK_FILECONNECTIONNOTDEFINED|No se ha definido la conexión de archivos "%1".|  
|0xC0029136|-1073573578|DTS_E_EXEC2000PKGTASK_INITIALIZATION_WITH_WRONG_XML_ELEMENT|La tarea Ejecutar paquete DTS 2000 se ha iniciado con un elemento XML incorrecto.|  
|0xC0029137|-1073573577|DTS_E_EXEC2000PKGTASK_HANDLER_NOT_FOUND|No se encuentra el controlador.|  
|0xC0029138|-1073573576|DTS_E_EXEC2000PKGTASK_PACKAGE_NAME_NOT_SPECIFIED|Nombre de paquete no especificado.|  
|0xC0029139|-1073573575|DTS_E_EXEC2000PKGTASK_PACKAGE_ID_NOT_SPECIFIED|Id. de paquete no especificado.|  
|0xC002913A|-1073573574|DTS_E_EXEC2000PKGTASK_PACKAGE_VERSIONGUID_NOT_SPECIFIED|GUID de la versión del paquete no especificado.|  
|0xC002913B|-1073573573|DTS_E_EXEC2000PKGTASK_SQLSERVER_NOT_SPECIFIED|SQL Server no especificado.|  
|0xC002913C|-1073573572|DTS_E_EXEC2000PKGTASK_SQL_USERNAME_NOT_SPECIFIED|Nombre de usuario de SQL Server no especificado.|  
|0xC002913D|-1073573571|DTS_E_EXEC2000PKGTASK_FILE_NAME_NOT_SPECIFIED|Nombre de archivo de almacenamiento no especificado.|  
|0xC002913E|-1073573570|DTS_E_EXEC2000PKGTASK_DTS2000CANTBEEMPTY|La propiedad del paquete DTS 2000 está vacía.|  
|0xC002913F|-1073573569|DTS_E_EXEC2000PKGTASK_ERROR_IN_PACKAGE_EXECUTE|Error al ejecutar el paquete DTS 2000.|  
|0xC0029140|-1073573568|DTS_E_EXEC2000PKGTASK_SQLSERVER_NOT_AVAILABLE_NETWORK|No se pueden cargar los servidores SQL Server de la red. Compruebe la conexión de red.|  
|0xC0029141|-1073573567|DTS_E_EXEC2000PKGTASK_DATATYPE_NULL|El tipo de datos no puede ser nulo. Especifique el tipo de datos correcto que debe utilizarse para validar el valor.|  
|0xC0029142|-1073573566|DTS_E_EXEC2000PKGTASK_NULL_VALUE|No se puede validar un valor nulo con ningún tipo de datos.|  
|0xC0029143|-1073573565|DTS_E_EXEC2000PKGTASK_NULL_VALUE_ARGUMENT|Un argumento requerido tiene el valor nulo.|  
|0xC0029144|-1073573564|DTS_E_EXEC2000PKGTASK_CLS_NOT_REGISTRED_EXCEPTION|Para ejecutar la tarea Ejecutar paquete DTS 2000, inicie el programa de instalación de SQL Server y utilice el botón Avanzadas de la página Componentes para instalar para seleccionar Componentes heredados.|  
|0xC0029145|-1073573563|DTS_E_EXEC2000PKGTASK_NOT_PRIMITIVE_TYPE|"%1" no es un tipo de valor.|  
|0xC0029146|-1073573562|DTS_E_EXEC2000PKGTASK_CONVERT_FAILED|No se pudo convertir "%1" en "%2".|  
|0xC0029147|-1073573561|DTS_E_EXEC2000PKGTASK_ERROR_IN_VALIDATE|No se pudo validar "%1" con "%2".|  
|0xC0029148|-1073573560|DTS_E_EXEC2000PKGTASK_ERROR_IN_LOAD_FROM_XML|Error de LoadFromXML en la etiqueta "%1".|  
|0xC0029149|-1073573559|DTS_E_EXEC2000PKGTASK_ERROR_IN_SAVE_TO_XML|Error de SaveToXML en la etiqueta "%1".|  
|0xC002914A|-1073573558|DTS_E_EXECPROCTASK_INVALIDTIMEOUT|El valor de tiempo de espera proporcionado no es válido. Especifique el número de segundos que la tarea permite ejecutar el proceso. El tiempo de espera mínimo es 0, lo que indica que no se utiliza ningún valor de tiempo de espera y que el proceso se ejecuta hasta que se completa o hasta que se produce un error. El tiempo de espera máximo es 2147483 (((2^31) - 1)/1000).|  
|0xC002914B|-1073573557|DTS_E_EXECPROCTASK_CANTREDIRECTIO|No se pueden redirigir flujos si el proceso puede seguirse ejecutando más allá de la duración de la tarea.|  
|0xC002914C|-1073573556|DTS_E_EXECPROCTASK_PROCESSHASTIMEDOUT|El proceso agotó el tiempo de espera.|  
|0xC002914D|-1073573555|DTS_E_EXECPROCTASK_EXECUTABLENOTSPECIFIED|Archivo ejecutable no especificado.|  
|0xC002914E|-1073573554|DTS_E_EXECPROCTASK_STDOUTVARREADONLY|La variable de salida estándar es de solo lectura.|  
|0xC002914F|-1073573553|DTS_E_EXECPROCTASK_STDERRVARREADONLY|La variable de error estándar es de solo lectura.|  
|0xC0029150|-1073573552|DTS_E_EXECPROCTASK_RECEIVEDINVALIDTASKDATANODE|La tarea Ejecutar proceso recibió un nodo de datos de tarea no válido.|  
|0xC0029151|-1073573551|DTS_E_EXECPROCTASK_PROCESSEXITCODEEXCEEDS|Al ejecutar "%2" "%3" en "%1", el código de salida del proceso obtenido fue "%4" y se esperaba "%5".|  
|0xC0029152|-1073573550|DTS_E_EXECPROCTASK_WORKINGDIRDOESNOTEXIST|El directorio "%1" no existe.|  
|0xC0029153|-1073573549|DTS_E_EXECPROCTASK_FILEDOESNOTEXIST|El archivo o proceso "%1" no existe en el directorio "%2".|  
|0xC0029154|-1073573548|DTS_E_EXECPROCTASK_FILENOTINPATH|El archivo o proceso "%1" no se encuentra en la ruta de acceso.|  
|0xC0029156|-1073573546|DTS_E_EXECPROCTASK_WORKINGDIRECTORYDOESNOTEXIST|El directorio de trabajo "%1" no existe.|  
|0xC0029157|-1073573545|DTS_E_EXECPROCTASK_ERROREXECUTIONVALUE|El proceso terminó con el código de retorno "%1". Sin embargo, se esperaba "%2".|  
|0xC0029158|-1073573544|DTS_E_FSTASK_SYNCFAILED|Error del objeto de sincronización.|  
|0xC0029159|-1073573543|DTS_E_FSTASK_INVALIDDATA|La tarea Sistema de archivos recibió un nodo de datos de tarea no válido.|  
|0xC002915A|-1073573542|DTS_E_FSTASK_DIRECTORYEXISTS|Ya existe el directorio.|  
|0xC002915B|-1073573541|DTS_E_FSTASK_PATHNOTVALID|"%1" no es un valor válido en el tipo de operación "%2".|  
|0xC002915C|-1073573540|DTS_E_FSTASK_DESTINATIONNOTSET|No se ha establecido la propiedad de destino de la operación "%1".|  
|0xC002915D|-1073573539|DTS_E_FSTASK_SOURCENOTSET|No se ha establecido la propiedad de origen de la operación "%1".|  
|0xC002915E|-1073573538|DTS_E_FSTASK_CONNECTIONTYPENOTFILE|El tipo de conexión "%1" no es un archivo.|  
|0xC002915F|-1073573537|DTS_E_FSTASK_VARIABLEDOESNTEXIST|La variable "%1" no existe.|  
|0xC0029160|-1073573536|DTS_E_FSTASK_VARIABLENOTASTRING|La variable "%1" no es una cadena.|  
|0xC0029163|-1073573533|DTS_E_FSTASK_FILEDOESNOTEXIST|No existe el archivo o el directorio "%1" representado por la conexión "%2".|  
|0xC0029165|-1073573531|DTS_E_FSTASK_DESTCONNUSAGETYPEINVALID|El administrador de conexiones de archivos de destino "%1" tiene un tipo de uso "%2" no válido.|  
|0xC0029166|-1073573530|DTS_E_FSTASK_SRCCONNUSAGETYPEINVALID|El administrador de conexiones de archivos de origen "%1" tiene un tipo de uso "%2" no válido.|  
|0xC0029167|-1073573529|DTS_E_FSTASK_LOGENTRYGETTINGFILEOPERATION|FileSystemOperation|  
|0xC0029168|-1073573528|DTS_E_FSTASK_LOGENTRYGETTINGFILEOPERATIONDESC|Proporciona información relacionada con las operaciones del sistema de archivos.|  
|0xC0029169|-1073573527|DTS_E_FSTASK_TASKDISPLAYNAME|Tarea Sistema de archivos|  
|0xC002916A|-1073573526|DTS_E_FSTASK_TASKDESCRIPTION|Realiza operaciones de sistema de archivos como copiar y eliminar archivos.|  
|0xC002916B|-1073573525|DTS_E_FTPTASK_SYNCOBJFAILED|Error del objeto de sincronización.|  
|0xC002916C|-1073573524|DTS_E_FTPTASK_UNABLETOOBTAINFILELIST|No se puede obtener la lista de archivos.|  
|0xC002916D|-1073573523|DTS_E_FTPTASK_LOCALPATHEMPTY|La ruta de acceso local está vacía.|  
|0xC002916E|-1073573522|DTS_E_FTPTASK_REMOTEPATHEMPTY|La ruta de acceso remota está vacía.|  
|0xC002916F|-1073573521|DTS_E_FTPTASK_LOCALVARIBALEEMPTY|La variable local está vacía.|  
|0xC0029170|-1073573520|DTS_E_FTPTASK_REMOTEVARIBALEEMPTY|La variable remota está vacía.|  
|0xC0029171|-1073573519|DTS_E_FTPTASK_FTPRCVDINVLDDATANODE|La tarea FTP recibió un nodo de datos de tarea no válido.|  
|0xC0029172|-1073573518|DTS_E_FTPTASK_CONNECTION_NAME_NULL|La conexión está vacía. Compruebe que se ha especificado una conexión FTP válida.|  
|0xC0029173|-1073573517|DTS_E_FTPTASK_CONNECTION_NOT_FTP|La conexión especificada no es una conexión FTP. Compruebe que se ha especificado una conexión FTP válida.|  
|0xC0029175|-1073573515|DTS_E_FTPTASK__INITIALIZATION_WITH_NULL_XML_ELEMENT|No se puede inicializar la tarea con un elemento XML de tipo nulo.|  
|0xC0029176|-1073573514|DTS_E_FTPTASK_SAVE_TO_NULL_XML_ELEMENT|No se puede guardar la tarea en un documento XML de tipo nulo.|  
|0xC0029177|-1073573513|DTS_E_FTPTASK_ERROR_IN_LOAD_FROM_XML|Error de LoadFromXML en la etiqueta "%1".|  
|0xC0029178|-1073573512|DTS_E_FTPTASK_NOFILESATLOCATION|No hay archivos en "%1".|  
|0xC0029179|-1073573511|DTS_E_FTPTASK_LOCALVARIABLEISEMPTY|La variable "%1" está vacía.|  
|0xC002917A|-1073573510|DTS_E_FTPTASK_REMOTEVARIABLEISEMPTY|La variable "%1" está vacía.|  
|0xC002917B|-1073573509|DTS_E_FTPTASK_NOFILESINCONNMGR|El archivo "%1" no contiene rutas de acceso de archivos.|  
|0xC002917C|-1073573508|DTS_E_FTPTASK_NOFILEPATHSINLOCALVAR|La variable "%1" no contiene rutas de acceso de archivos.|  
|0xC002917D|-1073573507|DTS_E_FTPTASK_VARIABLENOTASTRING|La variable "%1" no es una cadena.|  
|0xC002917E|-1073573506|DTS_E_FTPTASK_VARIABLENOTFOUND|La variable "%1" no existe.|  
|0xC002917F|-1073573505|DTS_E_FTPTASK_INVALIDPATHONOPERATION|Ruta de acceso no válida en la operación "%1".|  
|0xC0029180|-1073573504|DTS_E_FTPTASK_DIRECTORYEXISTS|"%1" ya existe.|  
|0xC0029182|-1073573502|DTS_E_FTPTASK_CONNECTIONTYPENOTFILE|El tipo de conexión "%1" no es un archivo.|  
|0xC0029183|-1073573501|DTS_E_FTPTASK_FILEDOESNOTEXIST|El archivo representado por "%1" no existe.|  
|0xC0029184|-1073573500|DTS_E_FTPTASK_INVALIDDIRECTORY|Directorio no especificado en la variable "%1".|  
|0xC0029185|-1073573499|DTS_E_FTPTASK_NOFILESFOUND|No se encontraron archivos en "%1".|  
|0xC0029186|-1073573498|DTS_E_FTPTASK_NODIRECTORYPATHINCONMGR|Directorio no especificado en el administrador de conexiones de archivos "%1".|  
|0xC0029187|-1073573497|DTS_E_FTPTASK_UNABLETODELETELOCALEFILE|No se puede eliminar el archivo local "%1".|  
|0xC0029188|-1073573496|DTS_E_FTPTASK_UNABLETOREMOVELOCALDIRECTORY|No se puede quitar el directorio local "%1".|  
|0xC0029189|-1073573495|DTS_E_FTPTASK_UNABLETOCREATELOCALDIRECTORY|No se puede crear el directorio local "%1".|  
|0xC002918A|-1073573494|DTS_E_FTPTASK_UNABLETORECEIVEFILES|No se pueden recibir archivos con "%1".|  
|0xC002918B|-1073573493|DTS_E_FTPTASK_UNABLETOSENDFILES|No se pueden enviar archivos con "%1".|  
|0xC002918C|-1073573492|DTS_E_FTPTASK_UNABLETOMAKEDIRREMOTE|No se puede crear el directorio remoto con "%1".|  
|0xC002918D|-1073573491|DTS_E_FTPTASK_UNABLETOREMOVEDIRREMOTE|No se puede quitar el directorio remoto con "%1".|  
|0xC002918E|-1073573490|DTS_E_FTPTASK_UNABLETODELETEREMOTEFILES|No se pueden eliminar archivos remotos con "%1".|  
|0xC002918F|-1073573489|DTS_E_FTPTASK_UNABLETOCONNECTTOSERVER|No se puede conectar al servidor FTP con "%1".|  
|0xC0029190|-1073573488|DTS_E_FTPTASK_INVALIDVARIABLEVALUE|La variable "%1" no empieza por "/".|  
|0xC0029191|-1073573487|DTS_E_FTPTASK_INVALIDREMOTEPATH|La ruta de acceso remoto "%1" no empieza por "/".|  
|0xC0029192|-1073573486|DTS_E_DTS_E_FTPTASK_CANNOT_ACQUIRE_CONNECTION|Error al establecer la conexión FTP. Compruebe si ha especificado un tipo de conexión válido "%1".|  
|0xC0029193|-1073573485|DTS_E_MSGQTASKUTIL_CERT_OPEN_STORE_FAILED|Error al abrir el almacén de certificados.|  
|0xC0029194|-1073573484|DTS_E_MSGQTASKUTIL_CERT_FAILED_GETTING_DISPLAY_NAME|Error al recuperar el nombre para mostrar del certificado.|  
|0xC0029195|-1073573483|DTS_E_MSGQTASKUTIL_CERT_FAILED_GETTING_ISSUER_NAME|Error al recuperar el nombre del emisor del certificado.|  
|0xC0029196|-1073573482|DTS_E_MSGQTASKUTIL_CERT_FAILED_GETTING_FRIENDLY_NAME|Error al recuperar el nombre descriptivo del certificado.|  
|0xC0029197|-1073573481|DTS_E_MSMQTASK_NO_CONNECTION|No se ha establecido el nombre de la conexión MSMQ.|  
|0xC0029198|-1073573480|DTS_E_MSMQTASK_INITIALIZATION_WITH_WRONG_XML_ELEMENT|Se inicializó la tarea con el elemento XML incorrecto.|  
|0xC0029199|-1073573479|DTS_E_MSMQTASK_DATA_FILE_NAME_EMPTY|El nombre del archivo de datos está vacío.|  
|0xC002919A|-1073573478|DTS_E_MSMQTASK_DATA_FILE_SAVE_NAME_EMPTY|El nombre especificado para el archivo de datos para guardar está vacío.|  
|0xC002919B|-1073573477|DTS_E_MSMQTASK_DATA_FILE_SIZE_ERROR|El tamaño de archivo debe ser inferior a 4 MB.|  
|0xC002919C|-1073573476|DTS_E_MSMQTASK_DATA_FILE_SAVE_FAILED|Error al guardar el archivo de datos.|  
|0xC002919D|-1073573475|DTS_E_MSMQTASK_STRING_COMPARE_VALUE_MISSING|El valor del filtro de cadena está vacío.|  
|0xC002919E|-1073573474|DTS_E_MSMQTASK_INVALID_QUEUE_PATH|Ruta de acceso de cola no válida.|  
|0xC002919F|-1073573473|DTS_E_MSMQTASK_NOT_TRANSACTIONAL|La tarea de la cola de mensajes no admite la inscripción en las transacciones distribuidas.|  
|0xC00291A0|-1073573472|DTS_E_MSMQTASK_INVALID_MESSAGE_TYPE|Tipo de mensaje no válido.|  
|0xC00291A1|-1073573471|DTS_E_MSMQTASK_TASK_TIMEOUT|Se agotó el tiempo de espera de la cola de mensajes. No se han recibido mensajes.|  
|0xC00291A2|-1073573470|DTS_E_MSMQTASK_INVALID_PROPERTY_VALUE|La propiedad especificada no es válida. Compruebe que el tipo de argumento es correcto.|  
|0xC00291A3|-1073573469|DTS_E_MSMQTASK_MESSAGE_NON_AUTHENTICATED|Mensaje no autenticado.|  
|0xC00291A4|-1073573468|DTS_E_MSMQTASK_INVALID_ENCRYPTION_ALGO_WRAPPER|Está intentando establecer el valor del algoritmo de cifrado con un objeto no válido.|  
|0xC00291A5|-1073573467|DTS_E_MSMQTASK_VARIABLE_TO_RECEIVE_STRING_MSG_EMPTY|La variable para recibir el mensaje de la cadena está vacía.|  
|0xC00291A6|-1073573466|DTS_E_MSMQTASK_RECEIVE_VARIABLE_EMPTY|La variable para recibir el mensaje de la variable está vacía.|  
|0xC00291A7|-1073573465|DTS_E_MSMQTASK_CONNECTIONTYPENOTMSMQ|La conexión "%1" no es del tipo MSMQ.|  
|0xC00291A8|-1073573464|DTS_E_MSMQTASK_DATAFILE_ALREADY_EXISTS|El archivo de datos "%1" ya existe en la ubicación especificada. No se puede sobrescribir el archivo porque la opción de sobrescritura está establecida en False.|  
|0xC00291A9|-1073573463|DTS_E_MSMQTASK_STRING_MSG_TO_VARIABLE_NOT_FOUND|La variable especificada "%1" para recibir el mensaje de cadena no se encuentra en la colección de variables del paquete.|  
|0xC00291AA|-1073573462|DTS_E_MSMQTASK_CONNMNGRNULL|El administrador de conexiones "%1" está vacío.|  
|0xC00291AB|-1073573461|DTS_E_MSMQTASK_CONNMNGRDOESNOTEXIST|No existe el administrador de conexiones "%1".|  
|0xC00291AC|-1073573460|DTS_E_SCRIPTTASK_COMPILEERRORMSG|Error "%1": "%2 "\r\nLínea "%3" Columna "%4" hasta "%5".|  
|0xC00291AD|-1073573459|DTS_E_SCRIPTTASK_COMPILEERRORMSG2|Error al compilar el script: "%1".|  
|0xC00291AE|-1073573458|DTS_E_SCRIPTTASK_COMPILEERRORMSG3|Error "%1": "%2"\r\nLínea "%3" Columnas "%4"-"%5"\r\nTexto de línea: "%6".|  
|0xC00291AF|-1073573457|DTS_E_SCRIPTTASK_SCRIPTREPORTEDFAILURE|El script de usuario devolvió un resultado incorrecto.|  
|0xC00291B0|-1073573456|DTS_E_SCRIPTTASK_SCRIPTFILESFAILEDTOLOAD|Error al cargar los archivos de script.|  
|0xC00291B1|-1073573455|DTS_E_SCRIPTTASK_SCRIPTTHREWEXCEPTION|El script de usuario inició una excepción: "%1".|  
|0xC00291B2|-1073573454|DTS_E_SCRIPTTASK_COULDNOTCREATEENTRYPOINTCLASS|No se pudo crear una instancia de la clase de punto de entrada "%1".|  
|0xC00291B3|-1073573453|DTS_E_SCRIPTTASK_LOADFROMXMLEXCEPTION|Excepción al cargar la tarea Script desde XML: "%1".|  
|0xC00291B4|-1073573452|DTS_E_SCRIPTTASK_SOURCEITEMNOTFOUNDEXCEPTION|No se encontró el elemento de origen "%1" en el paquete.|  
|0xC00291B5|-1073573451|DTS_E_SCRIPTTASK_BINARYITEMNOTFOUNDEXCEPTION|No se encontró el elemento binario "%1" en el paquete.|  
|0xC00291B6|-1073573450|DTS_E_SCRIPTTASK_UNRECOGNIZEDSCRIPTLANGUAGEEXCEPTION|No se ha reconocido "%1" como un lenguaje de script válido.|  
|0xC00291B7|-1073573449|DTS_E_SCRIPTTASK_ILLEGALSCRIPTNAME|El nombre del script no es válido. No puede contener espacios, barras diagonales, caracteres especiales ni empezar por un número.|  
|0xC00291B8|-1073573448|DTS_E_SCRIPTTASK_INVALIDSCRIPTLANGUAGE|El lenguaje de script especificado no es válido.|  
|0xC00291B9|-1073573447|DTS_E_SCRIPTTASK_CANTINITNULLTASK|No se puede inicializar en una tarea de tipo nulo.|  
|0xC00291BA|-1073573446|DTS_E_SCRIPTTASK_MUSTINITWITHRIGHTTASK|La interfaz de usuario de la tarea Script debe inicializarse en una tarea Script.|  
|0xC00291BB|-1073573445|DTS_E_SCRIPTTASK_WASNOTINITED|No se ha inicializado la interfaz de usuario de la tarea Script.|  
|0xC00291BC|-1073573444|DTS_E_SCRIPTTASK_HOST_NAME_CANT_EMPTY|El nombre no puede estar vacío.|  
|0xC00291BD|-1073573443|DTS_E_SCRIPTTASK_INVALID_SCRIPT_NAME|El nombre de proyecto no es válido. No puede contener espacios, barras diagonales, caracteres especiales ni empezar por un número.|  
|0xC00291BE|-1073573442|DTS_E_SCRIPTTASK_INVALID_SCRIPT_LANGUAGE|El lenguaje de script especificado no es válido.|  
|0xC00291BF|-1073573441|DTS_E_SCRIPTTASK_INVALID_ENTRY_POINT|Punto de entrada no encontrado.|  
|0xC00291C0|-1073573440|DTS_E_SCRIPTTASK_LANGUAGE_EMPTY|No se ha especificado el lenguaje de script. Compruebe que se especifica un lenguaje de script válido.|  
|0xC00291C1|-1073573439|DTS_E_SCRIPTTASK_INITIALIZATION_WITH_NULL_TASK|Inicialización de la interfaz de usuario: la tarea es NULL.|  
|0xC00291C2|-1073573438|DTS_E_SCRIPTTASK_UI_INITIALIZATION_WITH_WRONG_TASK|La interfaz de usuario de la tarea Script se inicializó con una tarea incorrecta.|  
|0xC00291C3|-1073573437|DTS_E_SENDMAILTASK_RECIPIENT_EMPTY|No se especificó un destinatario.|  
|0xC00291C4|-1073573436|DTS_E_SENDMAILTASK_SMTP_SERVER_NOT_SPECIFIED|Servidor de protocolo simple de transferencia de correo (SMTP) no especificado. Proporcione una dirección IP o un nombre válido del servidor SMTP.|  
|0xC00291C5|-1073573435|DTS_E_SENDMAILTASK_TASK_INITIALIZATION_WITH_WRONG_XML_ELEMENT|La tarea Enviar correo se ha inicializado con un elemento XML incorrecto.|  
|0xC00291CB|-1073573429|DTS_E_SENDMAILTASK_INVALIDATTACHMENT|No existe el archivo "%1" o no tiene permisos de acceso al archivo.|  
|0xC00291CD|-1073573427|DTS_E_SENDMAILTASK_CHECK_VALID_SMTP_SERVER|Compruebe si el servidor de protocolo simple de transferencia de correo (SMTP) especificado es válido.|  
|0xC00291CE|-1073573426|DTS_E_SENDMAILTASK_CONNECTIONTYPENOTFILE|La conexión "%1" no es del tipo Archivo.|  
|0xC00291CF|-1073573425|DTS_E_SENDMAILTASK_FILEDOESNOTEXIST|El archivo "%1" no existe en la operación "%2".|  
|0xC00291D0|-1073573424|DTS_E_SENDMAILTASK_VARIABLETYPEISNOTSTRING|La variable "%1" no es de tipo de cadena.|  
|0xC00291D1|-1073573423|DTS_E_SENDMAILTASK_CONNECTIONTYPENOTSMTP|La conexión "%1" no es de tipo SMTP.|  
|0xC00291D2|-1073573422|DTS_E_SENDMAILTASK_CONNMNGRNULL|La conexión "%1" está vacía.|  
|0xC00291D3|-1073573421|DTS_E_SENDMAILTASK_NOCONNMNGR|No existe la conexión especificada "%1".|  
|0xC00291D4|-1073573420|DTS_E_SQLTASK_NOSTATEMENTSPECIFIED|No se especificó ninguna instrucción Transact-SQL.|  
|0xC00291D5|-1073573419|DTS_E_SQLTASK_NOXMLSUPPORT|La conexión no admite conjuntos de resultados XML.|  
|0xC00291D6|-1073573418|DTS_E_SQLTASK_NOHANDLERFORCONNECTION|No se encuentra un controlador para el tipo de conexión especificado.|  
|0xC00291D7|-1073573417|DTS_E_SQLTASK_NOCONNECTIONMANAGER|No se ha especificado ningún administrador de conexiones.|  
|0xC00291D8|-1073573416|DTS_E_SQLTASK_CANNOTACQUIRECONNMANAGER|No se puede adquirir una conexión del administrador de conexiones.|  
|0xC00291D9|-1073573415|DTS_E_SQLTASK_NULLPARAMETERNAME|No puede haber un nombre de parámetro con valor nulo.|  
|0xC00291DA|-1073573414|DTS_E_SQLTASK_INVALIDPARAMETERNAME|El nombre de parámetro no es válido.|  
|0xC00291DB|-1073573413|DTS_E_SQLTASK_VALIDPARAMETERTYPES|Los nombres de parámetros válidos son de tipo entero o cadena.|  
|0xC00291DC|-1073573412|DTS_E_SQLTASK_READONLYVARIABLE|No se puede usar la variable "%1" en un enlace de resultados porque es de solo lectura.|  
|0xC00291DD|-1073573411|DTS_E_SQLTASK_INDESNOTINCOLLECTION|El índice no está asignado en esta colección.|  
|0xC00291DE|-1073573410|DTS_E_SQLTASK_ROVARINOUTPARAMETER|No se puede usar la variable "%1" como un parámetro de "salida" o valor devuelto en un enlace de parámetros porque es de solo lectura.|  
|0xC00291DF|-1073573409|DTS_E_SQLTASK_OBJECTNOTINCOLLECTION|El objeto no existe en esta colección.|  
|0xC00291E0|-1073573408|DTS_E_SQLTASK_UNABLETOACQUIREMANAGEDCONN|No se puede adquirir una conexión administrada.|  
|0xC00291E1|-1073573407|DTS_E_UNABLETOPOPRESULT|No se pueden llenar las columnas de resultados para el tipo de resultados de fila única. La consulta devolvió un conjunto de resultados vacío.|  
|0xC00291E2|-1073573406|DTS_E_SQLTASK_INVALIDNUMOFRESULTBINDINGS|Se devolvió un número no válido de enlaces de resultados para ResultSetType: "%1".|  
|0xC00291E3|-1073573405|DTS_E_SQLTASK_RESULTBINDTYPEFORROWSETXML|El nombre del enlace de resultados debe establecerse en cero para el conjunto de resultados completo y los resultados XML.|  
|0xC00291E4|-1073573404|DTS_E_SQLTASK_INVALIDEPARAMDIRECTIONFALG|La marca de direcciones de parámetros no es válida.|  
|0xC00291E5|-1073573403|DTS_E_SQLTASK_NOSQLTASKDATAINXMLFRAGMENT|El fragmento XML no contiene datos de la tarea Ejecutar SQL.|  
|0xC00291E6|-1073573402|DTS_E_SQLTASK_MULTIPLERETURNVALUEPARAM|Un parámetro con tipo de valor devuelto no es el primer parámetro, o bien hay más de un parámetro de tipo de valor devuelto.|  
|0xC00291E7|-1073573401|DTS_E_SQLTASK_CONNECTIONTYPENOTFILE|La conexión "%1" no es un administrador de conexiones de archivos.|  
|0xC00291E8|-1073573400|DTS_E_SQLTASK_FILEDOESNOTEXIST|El archivo representado por "%1" no existe.|  
|0xC00291E9|-1073573399|DTS_E_SQLTASK_VARIABLETYPEISNOTSTRING|El tipo de variable "%1" no es una cadena.|  
|0xC00291EA|-1073573398|DTS_E_SQLTASK_VARIABLENOTFOUND|La variable "%1" no existe o no se pudo bloquear.|  
|0xC00291EB|-1073573397|DTS_E_SQLTASK_CANNOTLOCATECONNMANAGER|No existe el administrador de conexiones "%1".|  
|0xC00291EC|-1073573396|DTS_E_SQLTASK_FAILEDTOACQUIRECONNECTION|No se pudo adquirir la conexión "%1". Puede ser que la conexión no esté configurada correctamente o que no tenga los permisos adecuados en esta conexión.|  
|0xC00291ED|-1073573395|DTS_E_SQLTASK_RESULTBYNAMENOTSUPPORTED|Este tipo de conexión no admite el enlace de resultados llamado "%1".|  
|0xC00291EE|-1073573394|DTS_E_SQLTASKCONN_ERR_NO_ROWS|Se ha especificado un tipo de conjunto de resultados de fila única, pero no se devolvieron filas.|  
|0xC00291EF|-1073573393|DTS_E_SQLTASKCONN_ERR_NO_DISCONNECTED_RS|No hay ningún conjunto de registros desconectado disponible para la instrucción Transact-SQL.|  
|0xC00291F0|-1073573392|DTS_E_SQLTASKCONN_ERR_UNSUPPORTED_TYPE|Tipo no compatible.|  
|0xC00291F1|-1073573391|DTS_E_SQLTASKCONN_ERR_UNKNOWN_TYPE|Tipo desconocido.|  
|0xC00291F2|-1073573390|DTS_E_SQLTASKCONN_ERR_PARAM_DATA_TYPE|Tipo de datos no compatible en el enlace de parámetros \\"%s\\".|  
|0xC00291F3|-1073573389|DTS_E_SQLTASKCONN_ERR_PARAM_NAME_MIX|Los nombres de parámetros no pueden ser una combinación de tipos con nombre y ordinales.|  
|0xC00291F4|-1073573388|DTS_E_SQLTASKCONN_ERR_PARAM_DIR|La dirección del parámetro en el enlace de parámetros \\"%s\\" no es válida.|  
|0xC00291F5|-1073573387|DTS_E_SQLTASKCONN_ERR_RESULT_DATA_TYPE|No se admite el tipo de datos del enlace de conjuntos de resultados \\"%s\\".|  
|0xC00291F6|-1073573386|DTS_E_SQLTASKCONN_ERR_RESULT_COL_INDEX|El índice de columna de resultados %d no es válido.|  
|0xC00291F7|-1073573385|DTS_E_SQLTASKCONN_ERR_UNKNOWN_RESULT_COL|No se encuentra la columna \\"%s\\" en el conjunto de resultados.|  
|0xC00291F9|-1073573383|DTS_E_SQLTASKCONN_ERR_NOROWSET|No hay ningún conjunto de filas de resultados asociado a la ejecución de esta consulta.|  
|0xC00291FA|-1073573382|DTS_E_SQLTASKCONN_ERR_ODBC_DISCONNECTED|Los conjuntos de registros desconectados no están disponibles en las conexiones ODBC.|  
|0xC00291FB|-1073573381|DTS_E_SQLTASKCONN_ERR_RESULT_SET_DATA_TYPE|El tipo de datos de la columna %hd del conjunto de resultados no es compatible.|  
|0xC00291FC|-1073573380|DTS_E_SQLTASKCONN_ERR_CANT_LOAD_XML|No se puede cargar XML con el resultado de la consulta.|  
|0xC00291FD|-1073573379|DTS_E_TTGENTASK_NOCONNORVARIABLE|Debe especificarse un nombre de conexión o de variable para el paquete.|  
|0xC00291FE|-1073573378|DTS_E_TTGENTASK_FAILEDCREATE|No se pudo crear el paquete.|  
|0xC00291FF|-1073573377|DTS_E_TTGENTASK_BADTABLEMETADATA|TableMetaDataNode no es un valor XMLNode.|  
|0xC0029200|-1073573376|DTS_E_TTGENTASK_FAILEDCREATEPIPELINE|No se pudo crear la canalización.|  
|0xC0029201|-1073573375|DTS_E_TTGENTASK_BADVARIABLETYPE|La variable no es del tipo correcto.|  
|0xC0029202|-1073573374|DTS_E_TTGENTASK_NOTFILECONNECTION|El administrador de conexiones especificado no es un administrador de conexiones de archivos.|  
|0xC0029203|-1073573373|DTS_E_TTGENTASK_BADFILENAME|Nombre de archivo no válido especificado en el administrador de conexiones "%1".|  
|0xC0029204|-1073573372|DTS_E_WEBSERVICETASK_CONNECTION_NAME_NULL|La conexión está vacía. Compruebe si se ha especificado una conexión HTTP válida.|  
|0xC0029205|-1073573371|DTS_E_WEBSERVICETASK_CONNECTION_NOT_FOUND|La conexión no existe. Compruebe si se ha especificado una conexión HTTP válida.|  
|0xC0029206|-1073573370|DTS_E_WEBSERVICETASK_CONNECTION_NOT_HTTP|La conexión especificada no es una conexión HTTP. Compruebe si se ha especificado una conexión HTTP válida.|  
|0xC0029207|-1073573369|DTS_E_WEBSERVICETASK_SERVICE_NULL|El nombre del servicio web está vacío. Compruebe que se ha especificado un nombre de servicio web válido.|  
|0xC0029208|-1073573368|DTS_E_WEBSERVICETASK_METHODNAME_NULL|El nombre del método web está vacío. Compruebe que se ha especificado un método web válido.|  
|0xC0029209|-1073573367|DTS_E_WEBSERVICETASK_WEBMETHODINFO_NULL|El método web está vacío o es posible que no exista. Compruebe si hay un método web existente para especificar.|  
|0xC002920A|-1073573366|DTS_E_WEBSERVICETASK_OUTPUTLOC_NULL|La ubicación de salida está vacía. Compruebe si se ha especificado una variable o una conexión de archivos existente.|  
|0xC002920B|-1073573365|DTS_E_WEBSERVICETASK_VARIABLE_NOT_FOUND|No se encuentra la variable. Compruebe si la variable existe en el paquete.|  
|0xC002920C|-1073573364|DTS_E_WEBSERVICETASK_VARIABLE_READONLY|No se puede guardar el resultado. Compruebe si la variable no es de solo lectura.|  
|0xC002920D|-1073573363|DTS_E_WEBSERVICETASK_ERROR_IN_LOAD_FROM_XML|Error de LoadFromXML en la etiqueta "%1".|  
|0xC002920E|-1073573362|DTS_E_WEBSERVICETASK_ERROR_IN_SAVE_TO_XML|Error de SaveToXML en la etiqueta "%1".|  
|0xC002920F|-1073573361|DTS_E_WEBSERVICETASK_TASK_SAVE_TO_NULL_XML_ELEMENT|No se puede guardar la tarea en un documento XML de tipo nulo.|  
|0xC0029210|-1073573360|DTS_E_WEBSERVICETASK_TASK_INITIALIZATION_WITH_NULL_XML_ELEMENT|No se puede inicializar la tarea con un elemento XML de tipo nulo.|  
|0xC0029211|-1073573359|DTS_E_WEBSERVICETASK_TASK_INITIALIZATION_WITH_WRONG_XML_ELEMENT|La tarea Servicio web se inicializa con un elemento XML incorrecto.|  
|0xC0029212|-1073573358|DTS_E_WEBSERVICETASK_UNEXPECTED_XML_ELEMENT|Se encontró un elemento XML inesperado.|  
|0xC0029213|-1073573357|DTS_E_WEBSERVICETASK_CANNOT_ACQUIRE_CONNECTION|Error al adquirir la conexión HTTP. Compruebe si se ha especificado un tipo de conexión válido.|  
|0xC0029214|-1073573356|DTS_E_WEBSERVICETASK_FILE_CONN_NOT_FOUND|No se puede guardar el resultado. Compruebe si existe una conexión de archivos.|  
|0xC0029215|-1073573355|DTS_E_WEBSERVICETASK_FILE_NOT_FOUND|No se puede guardar el resultado. Compruebe si el archivo existe.|  
|0xC0029216|-1073573354|DTS_E_WEBSERVICETASK_FILE_NULL|No se puede guardar el resultado. El nombre de archivo está vacío o bien hay otro proceso que está usando el archivo.|  
|0xC0029217|-1073573353|DTS_E_WEBSERVICETASK_CANNOT_ACQUIRE_FILE_CONNECTION|Error al establecer la conexión de archivos. Compruebe si se ha especificado una conexión de archivos válida.|  
|0xC0029218|-1073573352|DTS_E_WEBSERVICETASK_DATATYPE_NOT_SUPPORTED|Solo se admiten tipos complejos con valores primitivos, matrices primitivas y enumeraciones.|  
|0xC0029219|-1073573351|DTS_E_WEBSERVICETASK_PARAMTYPE_NOT_SUPPORTED|Solo se admiten los tipos primitivos, enumeración, complejos, PrimitiveArray y ComplexArray.|  
|0xC002921A|-1073573350|DTS_E_WEBSERVICETASK_WSDL_VERSION_NOT_SUPPORTED|Esta versión de WSDL no es compatible.|  
|0xC002921B|-1073573349|DTS_E_WEBSERVICETASK_WRONG_XML_ELEMENT|Se ha inicializado con un elemento XML incorrecto.|  
|0xC002921C|-1073573348|DTS_E_WEBSERVICETASK_XML_ATTRIBUTE_NOT_FOUND|No se ha encontrado un atributo obligatorio.|  
|0xC002921D|-1073573347|DTS_E_WEBSERVICETASK_ENUM_NO_VALUES|La enumeración "%1" no tiene valores. El archivo WSDL está dañado.|  
|0xC002921E|-1073573346|DTS_E_WEBSERVICETASK_CONNECTIONNOTFOUND|No se encuentra la conexión.|  
|0xC002921F|-1073573345|DTS_E_WEBSERVICETASK_CONNECTION_ALREADY_EXISTS|Ya existe una conexión con este nombre.|  
|0xC0029220|-1073573344|DTS_E_WEBSERVICETASK_NULL_CONNECTION|La conexión no puede ser nula ni estar vacía.|  
|0xC0029221|-1073573343|DTS_E_WEBSERVICETASK_NOT_HTTP_CONNECTION|La conexión especificada no es una conexión HTTP. Compruebe si se ha especificado una conexión HTTP válida.|  
|0xC0029222|-1073573342|DTS_E_WEBSERVICETASK_WSDL_NOT_FOUND|El identificador uniforme de recursos (URI) especificado no contiene un archivo WSDL válido.|  
|0xC0029223|-1073573341|DTS_E_WEBSERVICETASK_ERROR_IN_DOWNLOAD|No se pudo leer el archivo WSDL. El archivo WSDL de entrada no es válido. El lector generó un error: "%1".|  
|0xC0029224|-1073573340|DTS_E_WEBSERVICETASK_SERVICE_DESC_NULL|La descripción del servicio no puede ser nula.|  
|0xC0029225|-1073573339|DTS_E_WEBSERVICETASK_SERVICENULL|El nombre de servicio no puede ser nulo.|  
|0xC0029226|-1073573338|DTS_E_WEBSERVICETASK_WSDL_NULL|La dirección URL no puede ser nula.|  
|0xC0029227|-1073573337|DTS_E_WEBSERVICETASK_SERVICE_NOT_FOUND|El servicio no está disponible actualmente.|  
|0xC0029228|-1073573336|DTS_E_WEBSERVICETASK_SOAPPORT_NOT_FOUND|El servicio no está disponible en el puerto SOAP.|  
|0xC0029229|-1073573335|DTS_E_WEBSERVICETASK_SOAPBINDING_NOT_FOUND|Error al analizar el archivo WSDL (Lenguaje de descripción de servicios web). No se puede encontrar el enlace correspondiente al puerto SOAP.|  
|0xC002922A|-1073573334|DTS_E_WEBSERVICETASK_SOAPPORTTYPE_NOT_FOUND|Error al analizar el archivo WSDL (Lenguaje de descripción de servicios web). No se puede encontrar un valor PortType correspondiente al puerto SOAP.|  
|0xC002922B|-1073573333|DTS_E_WEBSERVICETASK_MSG_NOT_FOUND|No se puede encontrar el mensaje correspondiente al método especificado.|  
|0xC002922C|-1073573332|DTS_E_WEBSERVICETASK_CANNOT_GEN_PROXY|No se pudo generar el proxy para el servicio web especificado. Se encontraron los siguientes errores al generar el proxy: "%1".|  
|0xC002922D|-1073573331|DTS_E_WEBSERVICETASK_CANNOT_LOAD_PROXY|No se pudo cargar el proxy para el servicio web especificado. El error exacto es: "%1".|  
|0xC002922E|-1073573330|DTS_E_WEBSERVICETASK_INVALID_SERVICE|No se pudo encontrar el servicio especificado. El error exacto es: "%1".|  
|0xC002922F|-1073573329|DTS_E_WEBSERVICETASK_WEBMETHOD_INVOKE_FAILED|El servicio web generó el siguiente error durante la ejecución del método: "%1".|  
|0xC0029230|-1073573328|DTS_E_WEBSERVICETASK_INVOKE_ERR|No se pudo ejecutar el método web. El error exacto es: "%1".|  
|0xC0029231|-1073573327|DTS_E_WEBSERVICETASK_METHODINFO_NULL|MethodInfo no puede ser nulo.|  
|0xC0029232|-1073573326|DTS_E_WEBSERVICETASK_VALUE_NOT_PRIMITIVE|La propiedad WebMethodInfo especificada es incorrecta. El parámetro ParamValue suministrado no coincide con ParamType. El valor DTSParamValue encontrado no es de tipo PrimitiveValue.|  
|0xC0029233|-1073573325|DTS_E_WEBSERVICETASK_VALUE_NOT_ENUM|La propiedad WebMethodInfo especificada es incorrecta. El parámetro ParamValue suministrado no coincide con ParamType. El valor DTSParamValue encontrado no es de tipo EnumValue.|  
|0xC0029234|-1073573324|DTS_E_VALUE_WEBSERVICETASK_NOT_COMPLEX|La propiedad WebMethodInfo especificada es incorrecta. El parámetro ParamValue suministrado no coincide con ParamType. El valor DTSParamValue encontrado no es de tipo ComplexValue.|  
|0xC0029235|-1073573323|DTS_E_WEBSERVICETASK_VALUE_NOT_ARRAY|La propiedad WebMethodInfo especificada es incorrecta. El parámetro ParamValue suministrado no coincide con ParamType. El valor DTSParamValue encontrado no es de tipo ArrayValue.|  
|0xC0029236|-1073573322|DTS_E_WEBSERVICETASK_TYPE_NOT_PRIMITIVE|La propiedad WebMethodInfo que ha especificado es incorrecta. "%1" no es de tipo primitivo.|  
|0xC0029237|-1073573321|DTS_E_WEBSERVICETASK_ARRAY_VALUE_INVALID|Formato de ArrayValue no válido. Debe haber al menos un elemento en la matriz.|  
|0xC0029238|-1073573320|DTS_E_WEBSERVICETASK_SELECTED_VALUE_NULL|El valor de la enumeración no puede ser nulo. Seleccione un valor predeterminado para la enumeración.|  
|0xC0029239|-1073573319|DTS_E_WEBSERVICETASK_NULL_VALUE|No se puede validar un valor nulo con ningún tipo de datos.|  
|0xC002923A|-1073573318|DTS_E_WEBSERVICETASK_ENUM_VALUE_NOT_FOUND|El valor de enumeración no es correcto.|  
|0xC002923B|-1073573317|DTS_E_WEBSERVICETASK_PROP_NOT_EXISTS|La clase especificada no contiene ninguna propiedad pública con el nombre "%1".|  
|0xC002923C|-1073573316|DTS_E_WEBSERVICETASK_CONVERT_FAILED|No se pudo convertir "%1" en "%2".|  
|0xC002923D|-1073573315|DTS_E_WEBSERVICETASK_CLEANUP_FAILED|Error de limpieza. Es posible que no se haya eliminado el proxy que se creó para el servicio web.|  
|0xC002923E|-1073573314|DTS_E_WEBSERVICETASK_CREATE_INSTANCE_FAILED|No se pudo crear un objeto del tipo "%1". Compruebe si existe el constructor predeterminado.|  
|0xC002923F|-1073573313|DTS_E_WEBSERVICETASK_NOT_PRIMITIVE_TYPE|"%1" no es un tipo de valor.|  
|0xC0029240|-1073573312|DTS_E_WEBSERVICETASK_ERROR_IN_VALIDATE|No se pudo validar "%1" con "%1".|  
|0xC0029241|-1073573311|DTS_E_WEBSERVICETASK_DATATYPE_NULL|El tipo de datos no puede ser nulo. Especifique el valor del tipo de datos para validar.|  
|0xC0029242|-1073573310|DTS_E_WEBSERVICETASK_INDEX_OUT_OF_BOUNDS|No se pudo insertar ParamValue en esta posición. Puede que el índice especificado sea inferior a cero o superior a la longitud.|  
|0xC0029243|-1073573309|DTS_E_WEBSERVICETASK_WRONG_WSDL|El archivo WSDL de entrada no es válido.|  
|0xC0029244|-1073573308|DTS_E_WMIDRTASK_SYNCOBJECTFAILED|Error del objeto de sincronización.|  
|0xC0029245|-1073573307|DTS_E_WMIDRTASK_MISSINGWQLQUERY|Falta la consulta WQL.|  
|0xC0029246|-1073573306|DTS_E_WMIDRTASK_DESTINATIONMUSTBESET|Debe establecerse el destino.|  
|0xC0029247|-1073573305|DTS_E_WMIDRTASK_MISSINGCONNECTION|No hay ninguna conexión WMI establecida.|  
|0xC0029248|-1073573304|DTS_E_WMIDRTASK_INVALIDDATANODE|La tarea Lector de datos WMI recibió un nodo de datos de tarea incorrecto.|  
|0xC0029249|-1073573303|DTS_E_WMIDRTASK_FAILEDVALIDATION|Error al validar la tarea.|  
|0xC002924A|-1073573302|DTS_E_WMIDRTASK_FILEDOESNOTEXIST|El archivo "%1" no existe.|  
|0xC002924B|-1073573301|DTS_E_WMIDRTASK_CONNECTIONMNGRDOESNTEXIST|No existe el administrador de conexiones "%1".|  
|0xC002924C|-1073573300|DTS_E_WMIDRTASK_VARIABLETYPEISNOTSTRINGOROBJECT|La variable "%1" no es de tipo cadena ni objeto.|  
|0xC002924D|-1073573299|DTS_E_WMIDRTASK_CONNECTIONTYPENOTFILE|La conexión "%1" no es de tipo "FILE".|  
|0xC002924E|-1073573298|DTS_E_WMIDRTASK_CONNECTIONTYPENOTWMI|La conexión "%1" no es de tipo "WMI".|  
|0xC002924F|-1073573297|DTS_E_WMIDRTASK_FILEALREADYEXISTS|El archivo "%1" ya existe.|  
|0xC0029250|-1073573296|DTS_E_WMIDRTASK_CONNECTIONMANAGEREMPTY|El administrador de conexiones "%1" está vacío.|  
|0xC0029251|-1073573295|DTS_E_WMIDRTASK_VARNOTOBJECT|La variable "%1" debe ser de tipo objeto para poder asignarle una tabla de datos.|  
|0xC0029252|-1073573294|DTS_E_WMIDRTASK_TASKFAILURE|Error de la tarea por una consulta WMI no válida: "%1".|  
|0xC0029253|-1073573293|DTS_E_WMIDRTASK_CANTWRITETOVAR|No se puede escribir en la variable "%1" porque mantiene su valor original.|  
|0xC0029254|-1073573292|DTS_E_WMIEWTASK_SYNCOBJECTFAILED|Error del objeto de sincronización.|  
|0xC0029255|-1073573291|DTS_E_WMIEWTASK_MISSINGWQLQUERY|Falta la consulta WQL.|  
|0xC0029256|-1073573290|DTS_E_WMIEWTASK_MISSINGCONNECTION|Falta la conexión WMI.|  
|0xC0029257|-1073573289|DTS_E_WMIEWTASK_QUERYFAILURE|Error de la tarea al ejecutar la consulta WMI.|  
|0xC0029258|-1073573288|DTS_E_WMIEWTASK_INVALIDDATANODE|La tarea Monitor de eventos WMI recibió un nodo de datos de tarea no válido.|  
|0xC0029259|-1073573287|DTS_E_WMIEWTASK_CONNECTIONMNGRDOESNTEXIST|No existe el administrador de conexiones "%1".|  
|0xC002925A|-1073573286|DTS_E_WMIEWTASK_FILEDOESNOTEXIST|El archivo "%1" no existe.|  
|0xC002925B|-1073573285|DTS_E_WMIEWTASK_VARIABLETYPEISNOTSTRING|La variable "%1" no es de tipo de cadena.|  
|0xC002925C|-1073573284|DTS_E_WMIEWTASK_CONNECTIONTYPENOTFILE|La conexión "%1" no es de tipo "FILE".|  
|0xC002925D|-1073573283|DTS_E_WMIEWTASK_CONNECTIONTYPENOTWMI|La conexión "%1" no es de tipo "WMI".|  
|0xC002925E|-1073573282|DTS_E_WMIEWTASK_FILEALREADYEXISTS|El archivo "%1" ya existe.|  
|0xC002925F|-1073573281|DTS_E_WMIEWTASK_CONNECTIONMANAGEREMPTY|El administrador de conexiones "%1" está vacío.|  
|0xC0029260|-1073573280|DTS_E_WMIEWTASK_TIMEOUTOCCURRED|Se ha producido un tiempo de espera de "%1" segundos antes del evento representado por "%2".|  
|0xC0029261|-1073573279|DTS_E_WMIEWTASK_ERRMESSAGE|La supervisión de la consulta Wql provocó la siguiente excepción del sistema: "%1". Compruebe la existencia de errores en la consulta o los permisos y derechos de acceso de la conexión WMI.|  
|0xC0029262|-1073573278|DTS_E_XMLTASK_NODEFAULTOPERTION|No se han definido las operaciones especificadas.|  
|0xC0029263|-1073573277|DTS_E_XMLTASK_CONNECTIONTYPENOTFILE|El tipo de conexión no es un archivo.|  
|0xC0029264|-1073573276|DTS_E_XMLTASK_CANTGETREADERFROMSOURCE|No se puede obtener un objeto XmlReader del documento XML de origen.|  
|0xC0029265|-1073573275|DTS_E_XMLTASK_CANTGETREADERFROMDEST|No se puede obtener un objeto XmlReader del documento XML modificado.|  
|0xC0029266|-1073573274|DTS_E_XMLTASK_CANTGETREADERFROMDIFFGRAM|No se puede obtener el lector de DiffGram XDL del documento XML de DiffGram XDL.|  
|0xC0029268|-1073573272|DTS_E_XMLTASK_EMPTYNODELIST|La lista de nodos está vacía.|  
|0xC0029269|-1073573271|DTS_E_XMLTASK_NOELEMENTFOUND|No se encontró el elemento.|  
|0xC002926A|-1073573270|DTS_E_XMLTASK_UNDEFINEDOPERATION|No se han definido las operaciones especificadas.|  
|0xC002926B|-1073573269|DTS_E_XMLTASK_XPATHNAVERROR|Elemento de contenido inesperado en XPathNavigator.|  
|0xC002926C|-1073573268|DTS_E_XMLTASK_NOSCHEMAFOUND|No se encontró ningún esquema para exigir la validación.|  
|0xC002926D|-1073573267|DTS_E_XMLTASK_VALIDATIONERROR|Error de validación al validar el documento de instancia.|  
|0xC002926E|-1073573266|DTS_E_XMLTASK_SYNCOBJECTFAILED|Error del objeto de sincronización.|  
|0xC002926F|-1073573265|DTS_E_XMLTASK_ROOTNOODESNOTMATCHED|Los nodos raíz no coinciden.|  
|0xC0029270|-1073573264|DTS_E_XMLTASK_INVALIDEDITSCRIPT|El tipo de operación del script de modificación en el script de modificación final no es válido.|  
|0xC0029271|-1073573263|DTS_E_XMLTASK_CDATANODESISSUE|Los nodos CDATA deberían agregarse con la clase DiffgramAddSubtrees.|  
|0xC0029272|-1073573262|DTS_E_XMLTASK_COMMENTSNODEISSUE|Los nodos de comentario deberían agregarse con la clase DiffgramAddSubtrees.|  
|0xC0029273|-1073573261|DTS_E_XMLTASK_TEXTNODEISSUES|Los nodos de texto deberían agregarse con la clase DiffgramAddSubtrees.|  
|0xC0029274|-1073573260|DTS_E_XMLTASK_WHITESPACEISSUE|Los nodos con espacios en blanco relevantes deberían agregarse con la clase DiffgramAddSubtrees.|  
|0xC0029275|-1073573259|DTS_E_XMLTASK_DIFFENUMISSUE|Corrija la matriz OperationCost para que refleje la enumeración XmlDiffOperation.|  
|0xC0029276|-1073573258|DTS_E_XMLTASK_TASKISEMPTY|No hay operaciones en la tarea.|  
|0xC0029277|-1073573257|DTS_E_XMLTASK_DOCUMENTHASDATA|El documento ya contiene datos y no debe volverse a usar.|  
|0xC0029278|-1073573256|DTS_E_XMLTASK_INVALIDENODETYPE|Tipo de nodo no válido.|  
|0xC0029279|-1073573255|DTS_E_XMLTASK_INVALIDDATANODE|La tarea XML recibió un nodo de datos de tarea no válido.|  
|0xC002927B|-1073573253|DTS_E_XMLTASK_VARIABLETYPEISNOTSTRING|El tipo de datos de la variable no es una cadena.|  
|0xC002927C|-1073573252|DTS_E_XMLTASK_COULDNOTGETENCODINGFROMDOCUMENT|No se puede obtener codificación de XML.|  
|0xC002927D|-1073573251|DTS_E_XMLTASK_MISSINGSOURCE|No se ha especificado el origen.|  
|0xC002927E|-1073573250|DTS_E_XMLTASK_MISSINGSECONDOPERAND|No se ha especificado el segundo operando.|  
|0xC002927F|-1073573249|DTS_E_XMLTASK_INVALIDPATHDESCRIPTOR|Diffgram XDL no válido. "%1" es un descriptor de ruta de acceso no válido.|  
|0xC0029280|-1073573248|DTS_E_XMLTASK_NOMATCHINGNODE|Diffgram XDL no válido. Ningún nodo coincide con el descriptor de ruta de acceso "%1".|  
|0xC0029281|-1073573247|DTS_E_XMLTASK_EXPECTINGDIFFGRAMELEMENT|Diffgram XDL no válido. Se esperaba xd:xmldiff como elemento raíz con URI de espacio de nombres "%1".|  
|0xC0029282|-1073573246|DTS_E_XMLTASK_MISSINGSRCDOCATTRIBUTE|Diffgram XDL no válido. Falta el atributo srcDocHash en el elemento xd:xmldiff.|  
|0xC0029283|-1073573245|DTS_E_XMLTASK_MISSINGOPTIONSATTRIBUTE|Diffgram XDL no válido. Falta el atributo de opciones en el elemento xd:xmldiff.|  
|0xC0029284|-1073573244|DTS_E_XMLTASK_INVALIDSRCDOCATTRIBUTE|Diffgram XDL no válido. El atributo srcDocHash tiene un valor no válido.|  
|0xC0029285|-1073573243|DTS_E_XMLTASK_INVALIDOPTIONSATTRIBUTE|Diffgram XDL no válido. El atributo de opciones tiene un valor no válido.|  
|0xC0029286|-1073573242|DTS_E_XMLTASK_SRCDOCMISMATCH|No se puede aplicar DiffGram XDL a este documento XML. El valor rcDocHash no coincide.|  
|0xC0029287|-1073573241|DTS_E_XMLTASK_MORETHANONENODEMATCHED|Diffgram XDL no válido; más de un nodo coincide con el descriptor de ruta de acceso "%1" en el elemento xd:node o xd:change.|  
|0xC0029288|-1073573240|DTS_E_XMLTASK_XMLDECLMISMATCH|No se puede aplicar DiffGram XDL a este documento XML. No se puede agregar una nueva declaración XML.|  
|0xC0029289|-1073573239|DTS_E_XMLTASK_INTERNALERRORMORETHANONENODEINLIST|Error interno. XmlDiffPathSingleNodeList solamente puede contener un nodo.|  
|0xC002928A|-1073573238|DTS_E_XMLTASK_INTERNALERRORMORETHANONENODELEFT|Error interno. Quedan "%1" nodos después de la revisión; se esperaba 1.|  
|0xC002928B|-1073573237|DTS_E_XMLTASK_XSLTRESULTFILEISNOTXML|El archivo o texto producido por XSLT no es un XmlDocument válido y, por lo tanto, no se puede establecer como el resultado de la operación: "%1".|  
|0xC002928E|-1073573234|DTS_E_XMLTASK_FILEDOESNOTEXIST|No hay ningún archivo asociado a la conexión "%1".|  
|0xC002928F|-1073573233|DTS_E_XMLTASK_XMLTEXTEMPTY|La propiedad "%1" no tiene texto Xml de origen. El texto Xml no es válido, es de tipo nulo o es una cadena vacía.|  
|0xC0029290|-1073573232|DTS_E_XMLTASK_FILEALREADYEXISTS|El archivo "%1" ya existe.|  
|0xC0029293|-1073573229|DTS_E_TRANSFERTASKS_SRCCONNECTIONREQUIRED|Debe especificarse una conexión de origen.|  
|0xC0029294|-1073573228|DTS_E_TRANSFERTASKS_DESTCONNECTIONREQUIRED|Debe especificarse una conexión de destino.|  
|0xC0029295|-1073573227|DTS_E_TRANSFERTASKS_CONNECTIONNOTFOUND|No se encontró la conexión "%1" en el paquete.|  
|0xC0029296|-1073573226|DTS_E_TRANSFERTASKS_SERVERVERSIONNOTALLOWED|La conexión "%1" especifica una instancia de servidor SQL Server con una versión que no es compatible para la transferencia.  Solo son compatibles las versiones 7, 2000 y 2005.|  
|0xC0029297|-1073573225|DTS_E_TRANSFERTASKS_SRCSERVERLESSEQUALDESTSERVER|La conexión de origen "%1" debe especificar una instancia de SQL Server con una versión anterior o igual a la conexión de destino "%2".|  
|0xC0029298|-1073573224|DTS_E_TRANSFERTASKS_SRCDBREQUIRED|Debe especificarse una base de datos de origen.|  
|0xC0029299|-1073573223|DTS_E_TRANSFERTASKS_SRCDBMUSTEXIST|La base de datos de origen "%1" debe existir en el servidor de origen.|  
|0xC002929A|-1073573222|DTS_E_TRANSFERTASKS_DESTDBREQUIRED|Debe especificarse una base de datos de destino.|  
|0xC002929B|-1073573221|DTS_E_TRANSFERTASKS_SRCDBANDDESTDBTHESAME|La base de datos de origen y la base de datos de destino no pueden ser la misma.|  
|0xC002929C|-1073573220|DTS_E_TRANSFERDBTASK_FILENAMEREQUIRED|En la información de archivo de transferencia %1 falta el nombre de archivo.|  
|0xC002929D|-1073573219|DTS_E_TRANSFERDBTASK_FOLDERREQUIRED|En la información de archivo de transferencia %1 falta la parte de la carpeta.|  
|0xC002929E|-1073573218|DTS_E_TRANSFERTASKS_NETSHAREREQUIRED|En la información de archivo de transferencia %1 falta la parte de recursos compartidos de red.|  
|0xC002929F|-1073573217|DTS_E_TRANSFERTASKS_FILELISTSCOUNTMISMATCH|El número de archivos de transferencia de origen y el número de archivos de transferencia de destino deben ser el mismo.|  
|0xC00292A0|-1073573216|DTS_E_DOESNOTSUPPORTTRANSACTIONS|No se admite dar de alta en transacciones.|  
|0xC00292A1|-1073573215|DTS_E_TRANSFERDBTASK_OFFLINEERROR|La excepción siguiente se produjo durante una transferencia de base de datos sin conexión: %1.|  
|0xC00292A2|-1073573214|DTS_E_TRANSFERDBTASK_NETSHAREDOESNOTEXIST|No se encontró el recurso compartido de red "%1".|  
|0xC00292A3|-1073573213|DTS_E_TRANSFERDBTASK_NETSHARENOACCESS|No se pudo tener acceso al recurso compartido de red "%1".  El error es: %2.|  
|0xC00292A4|-1073573212|DTS_E_TRANSFERDBTASK_USERMUSTBEDBOORSYSADMIN|El usuario "%1" debe ser un DBO o un administrador del sistema de "%2" para poder realizar una transferencia de base de datos en línea.|  
|0xC00292A5|-1073573211|DTS_E_TRANSFERDBTASK_USERMUSTBESYSADMIN|El usuario "%1" debe ser un administrador del sistema en "%2" para realizar una transferencia de base de datos sin conexión.|  
|0xC00292A6|-1073573210|DTS_E_TRANSFERDBTASK_FTCATALOGSOFFLINEYUKONONLY|Los catálogos de texto completo solamente se pueden incluir si se realiza una transferencia de base de datos sin conexión entre 2 servidores SQL Server 2005.|  
|0xC00292A7|-1073573209|DTS_E_TRANSFERDBTASK_NOOVERWRITEDB|La base de datos "%1" ya existe en el servidor de destino "%2".|  
|0xC00292A8|-1073573208|DTS_E_TRANSFERDBTASK_MUSTHAVESOURCEFILES|Debe especificarse al menos un archivo de origen.|  
|0xC00292A9|-1073573207|DTS_E_TRANSFERDBTASKS_SRCFILENOTFOUND|No se encontró el archivo "%1" en la base de datos de origen "%2".|  
|0xC00292B3|-1073573197|DTS_E_MSMQTASK_FIPS1402COMPLIANCE|La operación solicitada no se permite en sistemas compatibles con el estándar FIPS 140-2 de EE.UU.|  
|0xC002F210|-1073548784|DTS_E_SQLTASK_ERROREXECUTINGTHEQUERY|Error al ejecutar la consulta "%1": "%2". Posibles motivos del error: problemas con la consulta, la propiedad "ResultSet" no fue establecida correctamente, parámetros no establecidos correctamente o conexión mal establecida.|  
|0xC002F300|-1073548544|DTS_E_TRANSFERSPTASK_ERRORREADINGSPNAMES|Error al leer nombres de procedimientos almacenados en el archivo xml.|  
|0xC002F301|-1073548543|DTS_E_TRANSFERSPTASK_INVALIDDATANODE|Nodo de datos no válido para la tarea Transferir procedimiento almacenado.|  
|0xC002F302|-1073548542|DTS_E_TRANSFERTASKS_CONNECTIONTYPEISNOTSMOSERVER|La conexión "%1" no es del tipo "SMOServer".|  
|0xC002F303|-1073548541|DTS_E_TRANSFERSPTASK_EXECUTIONFAILED|Error de ejecución: "%1".|  
|0xC002F304|-1073548540|DTS_E_ERROROCCURREDWITHFOLLOWINGMESSAGE|Error con el mensaje de error siguiente: "%1".|  
|0xC002F305|-1073548539|DTS_E_BITASK_EXECUTION_FAILED|Error de ejecución de la inserción masiva.|  
|0xC002F306|-1073548538|DTS_E_FSTASK_INVALIDDESTPATH|Ruta de acceso no válida.|  
|0xC002F307|-1073548537|DTS_E_FSTASK_CANTCREATEDIR|No se puede crear el directorio. El usuario eligió interrumpir la tarea si el directorio existe.|  
|0xC002F308|-1073548536|DTS_E_SQLTASK_ODBCNOSUPPORTTRANSACTION|La tarea tiene una opción de transacción "Necesaria" y la conexión "%1" es de tipo "ODBC". Las conexiones ODBC no admiten transacciones.|  
|0xC002F309|-1073548535|DTS_E_SQLTASK_ERRORASSIGINGVALUETOVAR|Error al asignar un valor a la variable "%1": "%2".|  
|0xC002F30A|-1073548534|DTS_E_FSTASK_SOURCEISEMPTY|El origen está vacío.|  
|0xC002F30B|-1073548533|DTS_E_FSTASK_DESTINATIONISEMPTY|El destino está vacío.|  
|0xC002F30C|-1073548532|DTS_E_FSTASK_FILEDIRNOTFOUND|El archivo o directorio "%1" no existe.|  
|0xC002F30D|-1073548531|DTS_E_FSTASK_VARSRCORDESTISEMPTY|La variable "%1" se utiliza como origen o destino y está vacía.|  
|0xC002F30E|-1073548530|DTS_E_FSTASK_FILEDELETED|Se eliminó el archivo o directorio "%1".|  
|0xC002F30F|-1073548529|DTS_E_FSTASK_DIRECTORYDELETED|Se eliminó el directorio "%1".|  
|0xC002F310|-1073548528|DTS_E_WMIDRTASK_VARIABLETYPEISNOTOBJECT|La variable "%1" debe ser de tipo objeto para poder asignarle una tabla de datos.|  
|0xC002F311|-1073548527|DTS_E_WMIDRTASK_VARIABLETYPEISNOTSTRING|La variable "%1" no tiene un tipo de datos de cadena.|  
|0xC002F312|-1073548526|DTS_E_FTPTASK_CANNOTACQUIRECONNECTION|Error al establecer la conexión FTP. Compruebe que se ha especificado un tipo de conexión válido en "%1".|  
|0xC002F313|-1073548525|DTS_E_FTPTASK_CONNECTIONNOTFOUND|No se encuentra el administrador de conexiones FTP "%1".|  
|0xC002F314|-1073548524|DTS_E_FTPTASK_FILEUSAGETYPEERROR|El tipo de uso de archivos de la conexión "%1" debería ser "%2" para la operación "%3".|  
|0xC002F315|-1073548523|DTS_E_TRANSFERTASKS_SOURCECANTBESAMEASDESTINATION|El servidor de origen no puede ser el mismo que el servidor de destino.|  
|0xC002F316|-1073548522|DTS_E_ERRMSGTASK_EMPTYSOURCELIST|No hay mensajes de error para transferir.|  
|0xC002F317|-1073548521|DTS_E_ERRMSGTASK_DIFFERENTMESSAGEANDLANGUAGESIZES|Las listas de mensajes de error y sus idiomas correspondientes tienen tamaños diferentes.|  
|0xC002F318|-1073548520|DTS_E_ERRMSGTASK_ERRORMESSAGEOUTOFRANGE|El id. de mensaje de error "%1" está fuera del intervalo permitido de mensajes de error definidos por el usuario. Los Id. de mensajes de error definidos por el usuario están comprendidos entre 50000 y 2147483647.|  
|0xC002F319|-1073548519|DTS_E_TRANSFERTASKS_NOTRANSACTIONSUPPORT|Esta tarea no puede participar en una transacción.|  
|0xC002F320|-1073548512|DTS_E_ERRMSGTASK_FAILEDTOTRANSFERERRORMESSAGES|Error al transferir algunos o todos los mensajes de error.|  
|0xC002F321|-1073548511|DTS_E_ERRMSGTASK_ERRORMESSAGEALREADYEXISTS|El mensaje de error "%1" ya existe en el servidor de destino.|  
|0xC002F324|-1073548508|DTS_E_ERRMSGTASK_ERRORMESSAGECANTBEFOUND|No se encuentra el mensaje de error "%1" en el servidor de origen.|  
|0xC002F325|-1073548507|DTS_E_TRANSFERTASKS_EXECUTIONFAILED|Error de ejecución: "%1".|  
|0xC002F327|-1073548505|DTS_E_JOBSTASK_FAILEDTOTRANSFERJOBS|Error al transferir los trabajos.|  
|0xC002F330|-1073548496|DTS_E_JOBSTASK_EMPTYSOURCELIST|No hay trabajos para transferir.|  
|0xC002F331|-1073548495|DTS_E_JOBSTASK_JOBEXISTSATDEST|El trabajo "%1" ya existe en el servidor de destino.|  
|0xC002F334|-1073548492|DTS_E_JOBSTASK_JOBCANTBEFOUND|No se encuentra el trabajo "%1" en el servidor de origen.|  
|0xC002F337|-1073548489|DTS_E_LOGINSTASK_EMPTYLIST|La lista de "Inicios de sesión" para transferir está vacía.|  
|0xC002F338|-1073548488|DTS_E_LOGINSTASK_CANTGETLOGINSNAMELIST|No se puede obtener la lista de "Inicios de sesión" del servidor de origen.|  
|0xC002F340|-1073548480|DTS_E_LOGINSTASK_ERRORLOGINEXISTS|El inicio de sesión "%1" ya existe en el servidor de destino.|  
|0xC002F342|-1073548478|DTS_E_LOGINSTASK_LOGINNOTFOUND|El inicio de sesión "%1" no existe en el origen.|  
|0xC002F344|-1073548476|DTS_E_LOGINSTASK_FAILEDTOTRANSFERLOGINS|Error al transferir algunos o todos los inicios de sesión.|  
|0xC002F345|-1073548475|DTS_E_STOREDPROCSTASK_FAILEDTOTRANSFERSPS|Error al transferir los procedimientos almacenados. Debería haberse producido un error más informativo.|  
|0xC002F346|-1073548474|DTS_E_STOREDPROCSTASK_STOREDPROCNOTFOUND|No se encuentra el procedimiento almacenado "%1" en el origen.|  
|0xC002F349|-1073548471|DTS_E_STOREDPROCSTASK_ERRORSTOREDPROCEDUREEXISTS|El procedimiento almacenado "%1" ya existe en el servidor de destino.|  
|0xC002F350|-1073548464|DTS_E_STOREDPROCSTASK_EMPTYSOURCELIST|No hay procedimientos almacenados para transferir.|  
|0xC002F353|-1073548461|DTS_E_TRANSOBJECTSTASK_FAILEDTOTRANSFEROBJECTS|Error al transferir los objetos.|  
|0xC002F354|-1073548460|DTS_E_TRANSOBJECTSTASK_EMPTYLIST|La lista de "Objetos" para transferir está vacía.|  
|0xC002F355|-1073548459|DTS_E_TRANSOBJECTSTASK_NOSPATSOURCE|No existe el procedimiento almacenado "%1" en el origen.|  
|0xC002F356|-1073548458|DTS_E_TRANSOBJECTSTASK_SPALREADYATDEST|El procedimiento almacenado "%1" ya existe en el destino.|  
|0xC002F357|-1073548457|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGSPS|Error al intentar obtener o establecer la lista de procedimientos almacenados para transferir: "%1".|  
|0xC002F359|-1073548455|DTS_E_TRANSOBJECTSTASK_NORULEATSOURCE|La regla "%1" no existe en el origen.|  
|0xC002F360|-1073548448|DTS_E_TRANSOBJECTSTASK_RULEALREADYATDEST|La regla "%1" ya existe en el destino.|  
|0xC002F361|-1073548447|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGRULES|Error al intentar obtener o establecer la lista de reglas para transferir: "%1".|  
|0xC002F363|-1073548445|DTS_E_TRANSOBJECTSTASK_NOTABLEATSOURCE|La tabla "%1" no existe en el origen.|  
|0xC002F364|-1073548444|DTS_E_TRANSOBJECTSTASK_TABLEALREADYATDEST|La tabla "%1" ya existe en el destino.|  
|0xC002F365|-1073548443|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGTABLES|Error al intentar obtener o establecer la lista de tablas para transferir: "%1".|  
|0xC002F367|-1073548441|DTS_E_TRANSOBJECTSTASK_NOVIEWATSOURCE|La vista "%1" no existe en el origen.|  
|0xC002F368|-1073548440|DTS_E_TRANSOBJECTSTASK_VIEWALREADYATDEST|La vista "%1" ya existe en el destino.|  
|0xC002F369|-1073548439|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGVIEWS|Error al intentar obtener o establecer la lista de vistas para transferir: "%1".|  
|0xC002F371|-1073548431|DTS_E_TRANSOBJECTSTASK_NOUDFATSOURCE|La función definida por el usuario "%1" no existe en el origen.|  
|0xC002F372|-1073548430|DTS_E_TRANSOBJECTSTASK_UDFALREADYATDEST|La función definida por el usuario "%1" ya existe en el destino.|  
|0xC002F373|-1073548429|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGUDFS|Error al intentar obtener o establecer la lista de funciones definidas por el usuario para transferir: "%1".|  
|0xC002F375|-1073548427|DTS_E_TRANSOBJECTSTASK_NODEFAULTATSOURCE|El valor predeterminado "%1" no existe en el origen.|  
|0xC002F376|-1073548426|DTS_E_TRANSOBJECTSTASK_DEFAULTALREADYATDEST|El valor predeterminado "%1" ya existe en el destino.|  
|0xC002F377|-1073548425|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGDEFAULTS|Error al intentar obtener o establecer la lista de valores predeterminados para transferir: "%1".|  
|0xC002F379|-1073548423|DTS_E_TRANSOBJECTSTASK_NOUDDTATSOURCE|El tipo de datos definido por el usuario "%1" no existe en el origen.|  
|0xC002F380|-1073548416|DTS_E_TRANSOBJECTSTASK_UDDTALREADYATDEST|El tipo de datos definido por el usuario "%1" ya existe en el destino.|  
|0xC002F381|-1073548415|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGUDDTS|Error al intentar obtener o establecer la lista de tipos de datos definidos por el usuario para transferir: "%1".|  
|0xC002F383|-1073548413|DTS_E_TRANSOBJECTSTASK_NOPFATSOURCE|La función de partición "%1" no existe en el origen.|  
|0xC002F384|-1073548412|DTS_E_TRANSOBJECTSTASK_PFALREADYATDEST|La función de partición "%1" ya existe en el destino.|  
|0xC002F385|-1073548411|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGPFS|Error al intentar obtener o establecer la lista de funciones de partición para transferir: "%1".|  
|0xC002F387|-1073548409|DTS_E_TRANSOBJECTSTASK_NOPSATSOURCE|El esquema de partición "%1" no existe en el origen.|  
|0xC002F388|-1073548408|DTS_E_TRANSOBJECTSTASK_PSALREADYATDEST|El esquema de partición "%1" ya existe en el destino.|  
|0xC002F389|-1073548407|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGPSS|Error al intentar obtener o establecer la lista de esquemas de partición para transferir: "%1".|  
|0xC002F391|-1073548399|DTS_E_TRANSOBJECTSTASK_NOSCHEMAATSOURCE|El esquema "%1" no existe en el origen.|  
|0xC002F392|-1073548398|DTS_E_TRANSOBJECTSTASK_SCHEMAALREADYATDEST|El esquema "%1" ya existe en el destino.|  
|0xC002F393|-1073548397|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGSCHEMAS|Error al intentar obtener o establecer la lista de esquemas para transferir: "%1".|  
|0xC002F395|-1073548395|DTS_E_TRANSOBJECTSTASK_NOSQLASSEMBLYATSOURCE|SqlAssembly "%1" no existe en el origen.|  
|0xC002F396|-1073548394|DTS_E_TRANSOBJECTSTASK_SQLASSEMBLYALREADYATDEST|SqlAssembly "%1" ya existe en el destino.|  
|0xC002F397|-1073548393|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGSQLASSEMBLIES|Error al intentar obtener o establecer la lista de SqlAssemblys para transferir: "%1".|  
|0xC002F399|-1073548391|DTS_E_TRANSOBJECTSTASK_NOAGGREGATEATSOURCE|El agregado definido por el usuario "%1" no existe en el origen.|  
|0xC002F400|-1073548288|DTS_E_TRANSOBJECTSTASK_AGGREGATEALREADYATDEST|El agregado definido por el usuario "%1" ya existe en el destino.|  
|0xC002F401|-1073548287|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGAGGREGATES|Error al intentar obtener o establecer la lista de agregados definidos por el usuario para transferir: "%1".|  
|0xC002F403|-1073548285|DTS_E_TRANSOBJECTSTASK_NOTYPEATSOURCE|El tipo definido por el usuario "%1" no existe en el origen.|  
|0xC002F404|-1073548284|DTS_E_TRANSOBJECTSTASK_TYPEALREADYATDEST|El tipo definido por el usuario "%1" ya existe en el destino.|  
|0xC002F405|-1073548283|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGTYPES|Error al intentar obtener o establecer la lista de tipos definidos por el usuario para transferir: "%1".|  
|0xC002F407|-1073548281|DTS_E_TRANSOBJECTSTASK_NOXMLSCHEMACOLLECTIONATSOURCE|XmlSchemaCollection "%1" no existe en el origen.|  
|0xC002F408|-1073548280|DTS_E_TRANSOBJECTSTASK_XMLSCHEMACOLLECTIONALREADYATDEST|XmlSchemaCollection "%1" ya existe en el destino.|  
|0xC002F409|-1073548279|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGXMLSCHEMACOLLECTIONS|Error al intentar obtener o establecer la lista de XmlSchemaCollections para transferir: "%1".|  
|0xC002F411|-1073548271|DTS_E_TRANSOBJECTSTASK_SUPPORTEDONYUKONONLY|Los objetos de tipo "%1" solo se admiten entre servidores SQL Server 2005 y otros más recientes.|  
|0xC002F413|-1073548269|DTS_E_LOGINSTASK_EMPTYDATABASELIST|La lista de bases de datos está vacía.|  
|0xC002F414|-1073548268|DTS_E_TRANSOBJECTSTASK_NOLOGINATSOURCE|El inicio de sesión "%1" no existe en el origen.|  
|0xC002F416|-1073548266|DTS_E_TRANSOBJECTSTASK_LOGINALREADYATDEST|El inicio de sesión "%1" ya existe en el destino.|  
|0xC002F417|-1073548265|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGLOGINS|Error al intentar obtener o establecer la lista de inicios de sesión para transferir: "%1".|  
|0xC002F419|-1073548263|DTS_E_TRANSOBJECTSTASK_NOUSERATSOURCE|El usuario "%1" no existe en el origen.|  
|0xC002F41B|-1073548261|DTS_E_TRANSOBJECTSTASK_USERALREADYATDEST|La usuario "%1" ya existe en el destino.|  
|0xC002F41C|-1073548260|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGUSERS|Error al intentar obtener o establecer la lista de usuarios para transferir: "%1".|  
|0xC002F41F|-1073548257|DTS_E_BITASK_CANNOTRETAINCONNINTRANSACTION|La tarea no puede tener un administrador de conexiones retenido en una transacción.|  
|0xC002F421|-1073548255|DTS_E_SQLTASKOUTPUTENCODINGNOTSUPPORTED|No se pueden obtener datos XML de SQL Server como Unicode porque el proveedor no admite la propiedad OUTPUTENCODING.|  
|0xC002F426|-1073548250|DTS_E_FTPTASK_FILECONNECTIONNOTFOUND|No se encuentra el administrador de conexiones de archivos "%1" para la operación FTP "%2".|  
|0xC002F428|-1073548248|DTS_E_TRANSOBJECTSTASK_CANNOTDROPOBJECTS|Los "Inicios de sesión" son objetos de nivel de servidor y no se pueden quitar primero, ya que el origen y el destino están en el mismo servidor. Si se quitan primero los objetos, se eliminarán también los inicios de sesión del origen.|  
|0xC002F429|-1073548247|DTS_E_SQLTASK_PARAMSIZEERROR|El parámetro "%1" no puede ser negativo. (-1) se usa para el valor predeterminado.|  
|0xC0040019|-1073479655|DTS_E_UNREGISTEREDPIPELINEXML_LOAD|No se pueden cargar los objetos de flujo de datos. Compruebe si el archivo Microsoft.SqlServer.PipelineXml.dll está correctamente registrado.|  
|0xC0040020|-1073479648|DTS_E_UNREGISTEREDPIPELINEXML_SAVE|No se pueden guardar los objetos de flujo de datos. Compruebe si el archivo Microsoft.SqlServer.PipelineXml.dll está correctamente registrado.|  
|0xC0040040|-1073479616|DTS_E_PIPELINE_SAVE|No se pudo guardar los objetos de flujo de datos.|  
|0xC0040041|-1073479615|DTS_E_PIPELINE_LOAD|No se pudo cargar los objetos de flujo de datos|  
|0xC0040042|-1073479614|DTS_E_SAVE_PERSTFORMAT|No se pudo guardar los objetos de flujo de datos. No se admite el formato especificado.|  
|0xC0040043|-1073479613|DTS_E_LOAD_PERSTFORMAT|No se pudo cargar los objetos de flujo de datos. No se admite el formato especificado.|  
|0xC0040044|-1073479612|DTS_E_SETPERSIST_PROPEVENTS|No se pudo establecer los eventos de persistencia XML para los objetos de flujo de datos.|  
|0xC0040045|-1073479611|DTS_E_SETPERSIST_XMLDOM|No se pudo establecer la propiedad DOM de XML de persistencia para los objetos de flujo de datos.|  
|0xC0040046|-1073479610|DTS_E_SETPERSIST_XMLNODE|No se pudo establecer la propiedad ELEMENT de XML de persistencia para los objetos de flujo de datos.|  
|0xC0040047|-1073479609|DTS_E_SETPERSISTPROP_FAILED|No se pudo establecer las propiedades de persistencia de XML para los objetos de flujo de datos.|  
|0xC0040048|-1073479608|DTS_E_NOCUSTOMPROPCOL|No se pudo obtener la colección de propiedades personalizadas para los componentes de flujo de datos.|  
|0xC0047000|-1073451008|DTS_E_CYCLEINEXECUTIONTREE|Un árbol de ejecución contiene un ciclo.|  
|0xC0047001|-1073451007|DTS_E_DISCONNECTEDOBJECT|El objeto %1 "%2" (%3!d!) se ha desconectado del diseño.|  
|0xC0047002|-1073451006|DTS_E_INVALIDOBJECTID|El Id. del objeto de diseño no es válido.|  
|0xC0047003|-1073451005|DTS_E_INPUTWITHOUTPATHS|Un objeto de entrada necesario no está conectado a un objeto de ruta.|  
|0xC0047005|-1073451003|DTS_E_INVALIDSYNCHRONOUSINPUT|%1 tiene un id. de entrada sincrónica no válido %2!d!.|  
|0xC0047006|-1073451002|DTS_E_INVALIDOUTPUTLINEAGEID|%1 tiene el id. de linaje %2!d!, pero tendría que tener %3!d!.|  
|0xC0047008|-1073451000|DTS_E_DUPLICATENAMESINCOLLECTION|El paquete contiene dos objetos con el nombre duplicado "%1" y "%2".|  
|0xC0047009|-1073450999|DTS_E_INVALIDEXCLUSIONGROUP|"%1" y "%2" pertenecen al mismo grupo de exclusión pero no tienen la misma entrada sincrónica.|  
|0xC004700A|-1073450998|DTS_E_DUPLICATELINEAGEIDSINCOLLECTION|Dos objetos de la misma colección tienen el id. de linaje duplicado: %1!d!. Son los objetos %2 y %3.|  
|0xC004700B|-1073450997|DTS_E_VALIDATIONFAILEDONLAYOUT|Error al validar el diseño.|  
|0xC004700C|-1073450996|DTS_E_VALIDATIONFAILEDONCOMPONENTS|Error al validar uno o más componentes.|  
|0xC004700D|-1073450995|DTS_E_VALIDATIONFAILED|Error al validar el diseño y uno o más componentes.|  
|0xC004700E|-1073450994|DTS_E_THREADSTARTUPFAILED|Error al iniciar el motor de la tarea Flujo de datos porque no puede crear uno o más subprocesos necesarios.|  
|0xC004700F|-1073450993|DTS_E_CANTGETMUTEX|Un subproceso no pudo crear una exclusión mutua al inicializarse.|  
|0xC0047010|-1073450992|DTS_E_CANTGETSEMAPHORE|Un subproceso no pudo crear un semáforo al inicializarse.|  
|0xC0047011|-1073450991|DTS_E_BUFFERFAILUREDETAILS|El sistema indica que hay un %1!d! por ciento de carga de memoria. Hay %2 bytes de memoria física, de los que %3 están libres. Hay %4 bytes de memoria virtual, de los que %5 están libres. El archivo de paginación tiene %6 bytes, de los que %7 están libres.|  
|0xC0047012|-1073450990|DTS_E_BUFFERALLOCFAILED|Un búfer no pudo asignar %1!d! bytes.|  
|0xC0047013|-1073450989|DTS_E_CANTCREATEBUFFERMANAGER|No se pudo crear el administrador de búfer.|  
|0xC0047015|-1073450987|DTS_E_BUFFERBADSIZE|El tipo de búfer %1!d! tenía un tamaño de %2!I64d! bytes.|  
|0xC0047016|-1073450986|DTS_E_DANGLINGWITHPATH|%1 está marcado como pendiente pero tiene una ruta de acceso adjunta.|  
|0xC0047017|-1073450985|DTS_E_INDIVIDUALVALIDATIONFAILED|Error en la validación de %1; se devolvió el código de error 0x%2!8.8X!.|  
|0xC0047018|-1073450984|DTS_E_INDIVIDUALPOSTEXECUTEFAILED|Error en la fase de ejecución posterior de %1; se devolvió el código de error 0x%2!8.8X!.|  
|0xC0047019|-1073450983|DTS_E_INDIVIDUALPREPAREFAILED|Error en la fase de preparación de %1; se devolvió el código de error 0x%2!8.8X!.|  
|0xC004701A|-1073450982|DTS_E_INDIVIDUALPREEXECUTEFAILED|Error en la fase de ejecución previa de %1; se devolvió el código de error 0x%2!8.8X!.|  
|0xC004701B|-1073450981|DTS_E_INDIVIDUALCLEANUPFAILED|Error en la fase de limpieza de %1; se devolvió el código de error 0x%2!8.8X!.|  
|0xC004701C|-1073450980|DTS_E_INVALIDINPUTLINEAGEID|%1 tiene un id. de linaje %2!d! que no se había utilizado previamente en la tarea Flujo de datos.|  
|0xC004701E|-1073450978|DTS_E_EXECUTIONTREECYCLE|No se puede establecer la conexión entre %1 y %2 porque se crearía un ciclo.|  
|0xC004701F|-1073450977|DTS_E_CANTCOMPARE|El tipo de datos "%1" no se puede comparar. No se admite la comparación de ese tipo de datos, por lo que no puede ordenarse ni utilizarse como clave.|  
|0xC0047020|-1073450976|DTS_E_REFUSEDFORSHUTDOWN|Se ha cerrado este subproceso y no acepta la entrada de búferes.|  
|0xC0047021|-1073450975|DTS_E_THREADFAILED|Código de error SSIS DTS_E_THREADFAILED.  El subproceso "%1" terminó con el código de error 0x%2!8.8X!.  Puede que haya otros mensajes de error expuestos anteriores a éste con más información sobre el motivo de que terminase el subproceso.|  
|0xC0047022|-1073450974|DTS_E_PROCESSINPUTFAILED|Código de error SSIS DTS_E_PROCESSINPUTFAILED.  Error del método ProcessInput en el componente "%1" (%2!d!). Código de error: 0x%3!8.8X! mientras se procesaba la entrada "%4" (%5!d!). El componente identificado devolvió un error del método ProcessInput. El error es específico del componente, pero es irrecuperable y detendrá la ejecución de la tarea Flujo de datos.  Puede que haya otros mensajes de error expuestos anteriores a éste con más información sobre el error.|  
|0xC0047023|-1073450973|DTS_E_CANTREALIZEVIRTUALBUFFERS|No se puede realizar un conjunto de búferes virtuales.|  
|0xC0047024|-1073450972|DTS_E_PIPELINETOOCOMPLEX|El número de subprocesos necesarios en esta canalización es %1!d!, lo que supera el límite del sistema, %2!d!. La canalización requiere demasiados de los subprocesos configurados. Hay demasiadas salidas asincrónicas o el valor de la propiedad EngineThreads es demasiado alto. Divida la canalización en varios paquetes o reduzca el valor de la propiedad EngineThreads.|  
|0xC0047028|-1073450968|DTS_E_SCHEDULERCOULDNOTCOUNTSOURCES|El programador del motor de Flujo de datos no puede obtener un recuento de los orígenes del diseño.|  
|0xC0047029|-1073450967|DTS_E_SCHEDULERCOULDNOTCOUNTDESTINATIONS|El programador del motor de Flujo de datos no puede obtener un recuento de los destinos del diseño.|  
|0xC004702A|-1073450966|DTS_E_COMPONENTVIEWISUNAVAILABLE|Vista de componentes no disponible. Asegúrese de que se ha creado la vista de componentes.|  
|0xC004702B|-1073450965|DTS_E_INCORRECTCOMPONENTVIEWID|El Id. de la vista de componentes no es correcto. Es posible que la vista de componentes no esté sincronizada. Libere la vista de componentes y vuelva a crearla.|  
|0xC004702C|-1073450964|DTS_E_BUFFERNOTLOCKED|Este búfer no está bloqueado y no puede manipularse.|  
|0xC004702D|-1073450963|DTS_E_CANTBUILDBUFFERTYPE|La tarea Flujo de datos no puede asignar memoria para generar una definición de búfer. La definición del búfer tenía %1!d! columnas.|  
|0xC004702E|-1073450962|DTS_E_CANTREGISTERBUFFERTYPE|La tarea Flujo de datos no puede registrar un tipo de búfer. El tipo tenía %1!d! columnas y correspondía al árbol de ejecución %2!d!.|  
|0xC004702F|-1073450961|DTS_E_INVALIDUSESDISPOSITIONSVALUE|No se puede cambiar el valor inicial de la propiedad UsesDispositions. Esto sucede si se edita XML y se modifica el valor de UsesDispositions. El componente establece este valor cuando se agrega al paquete y no se permite cambiarlo.|  
|0xC0047030|-1073450960|DTS_E_THREADFAILEDINITIALIZE|La tarea Flujo de datos no pudo inicializar un subproceso necesario y no puede iniciar la ejecución. El subproceso emitió anteriormente un error específico.|  
|0xC0047031|-1073450959|DTS_E_THREADFAILEDCREATE|La tarea Flujo de datos no pudo crear un subproceso necesario y no puede iniciar la ejecución. Esto suele suceder si la memoria es insuficiente.|  
|0xC0047032|-1073450958|DTS_E_EXECUTIONTREECYCLEADDINGSYNCHRONOUSINPUT|La entrada sincrónica de "%1" no puede establecerse en "%2" porque se crearía un ciclo.|  
|0xC0047033|-1073450957|DTS_E_INVALIDCUSTOMPROPERTYNAME|La propiedad personalizada "%1" no es válida porque ya hay una propiedad estándar con dicho nombre. Una propiedad personalizada no puede tener el mismo nombre que una propiedad estándar del mismo objeto.|  
|0xC0047035|-1073450955|DTS_E_BUFFERLOCKUNDERFLOW|El búfer ya estaba desbloqueado.|  
|0xC0047036|-1073450954|DTS_E_INDIVIDUALCACHEINTERFACESFAILED|%1 no pudo inicializarse y se devolvió el código de error 0x%2!8.8X!.|  
|0xC0047037|-1073450953|DTS_E_INDIVIDUALRELEASEINTERFACESFAILED|%1 no pudo cerrarse y se devolvió el código de error 0x%2!8.8X!. Un componente no pudo liberar sus interfaces.|  
|0xC0047038|-1073450952|DTS_E_PRIMEOUTPUTFAILED|Código de error SSIS DTS_E_PRIMEOUTPUTFAILED.  El método PrimeOutput en %1 devolvió el código de error 0x%2!8.8X!.  El componente devolvió un código de error cuando el motor de canalización llamó a PrimeOutput(). El componente define el significado del código de error, pero el error es grave y se ha detenido la ejecución de la canalización.  Puede que haya otros mensajes de error expuestos anteriores a éste con más información sobre el error.|  
|0xC0047039|-1073450951|DTS_E_THREADCANCELLED|Código de error SSIS DTS_E_THREADCANCELLED.  El subproceso "%1" recibió una señal de cierre y está finalizando. El usuario solicitó un cierre o un error en otro subproceso provocó el cierre de la canalización.  Puede que haya otros mensajes de error expuestos anteriores a éste con más información sobre el motivo de que se cancelase el subproceso.|  
|0xC004703A|-1073450950|DTS_E_DISTRIBUTORCANTSETPROPERTY|El distribuidor del subproceso "%1" no pudo inicializar la propiedad "%2" en el componente "%3" debido al error 0x%8.8X. El distribuidor no pudo inicializar la propiedad del componente y no puede seguir ejecutándose.|  
|0xC004703B|-1073450949|DTS_E_CANTREGISTERVIEWBUFFERTYPE|La tarea Flujo de datos no puede registrar un tipo de búfer de vista. El tipo tenía %1!d! columnas y correspondía al id. de entrada %2!d!.|  
|0xC004703F|-1073450945|DTS_E_CANTCREATEEXECUTIONTREE|No hay memoria suficiente para crear un árbol de ejecución.|  
|0xC0047040|-1073450944|DTS_E_CANTINSERTINTOHASHTABLE|No hay memoria suficiente para insertar un objeto en la tabla hash.|  
|0xC0047041|-1073450943|DTS_E_OBJECTNOTINHASHTABLE|El objeto no está incluido en la tabla hash.|  
|0xC0047043|-1073450941|DTS_E_CANTCREATECOMPONENTVIEW|No se puede crear una vista de componentes porque ya existe una. Solo puede haber una vista de componentes cada vez.|  
|0xC0047046|-1073450938|DTS_E_LAYOUTCANTSETUSAGETYPE|En la entrada "%1" (%2!d!), la colección de columnas de entrada virtual no contiene una columna de entrada virtual con el id. de linaje %3!d!.|  
|0xC0047047|-1073450937|DTS_E_WRONGOBJECTTYPE|El objeto solicitado es de un tipo de objeto incorrecto.|  
|0xC0047048|-1073450936|DTS_E_CANTCREATESPOOLFILE|El administrador de búfer no puede crear un archivo de almacenamiento temporal en cualquier ruta de la propiedad BufferTempStoragePath. Hay un nombre de archivo incorrecto, no tiene permiso o las rutas de acceso se han llenado.|  
|0xC0047049|-1073450935|DTS_E_SEEKFAILED|El administrador de búfer no pudo buscar en el desplazamiento %1!d! del archivo "%2". El archivo está dañado.|  
|0xC004704A|-1073450934|DTS_E_EXTENDFAILED|El administrador de búfer no pudo ampliar la longitud del archivo "%1" hasta %2!lu! bytes.  Espacio en disco insuficiente.|  
|0xC004704B|-1073450933|DTS_E_FILEWRITEFAILED|El administrador de búfer no puede escribir %1!d! bytes en el archivo "%2". Espacio en disco o cuota insuficientes.|  
|0xC004704C|-1073450932|DTS_E_FILEREADFAILED|El administrador de búfer no puede leer %1!d! bytes del archivo "%2". El archivo está dañado.|  
|0xC004704D|-1073450931|DTS_E_VIRTUALNOTSEQUENTIAL|El id. de búfer %1¡d! admite otros búferes virtuales y no puede colocarse en modo secuencial. Se llamó a IDTSBuffer100.SetSequentialMode en un búfer que admite búferes virtuales.|  
|0xC004704E|-1073450930|DTS_E_BUFFERISREADONLY|No se pudo realizar esta operación porque el búfer está en modo de solo lectura. No es posible modificar un búfer de solo lectura.|  
|0xC004704F|-1073450929|DTS_E_EXECUTIONTREECYCLESETTINGID|El id. %1 no puede establecerse en %2!d! porque se crearía un ciclo.|  
|0xC0047050|-1073450928|DTS_E_NOMOREBUFFERTYPES|El administrador de búfer agotó la memoria al intentar ampliar la tabla de tipos de búfer, porque no hay memoria suficiente.|  
|0xC0047051|-1073450927|DTS_E_CANTCREATENEWTYPE|El administrador de búfer no pudo crear un nuevo tipo de búfer.|  
|0xC0047053|-1073450925|DTS_E_SCHEDULERBADTREE|El programador del motor de Flujo de datos no pudo recuperar del diseño el árbol de ejecución con el índice %1!d! del diseño. El programador recibió un recuento con más árboles de ejecución que los existentes.|  
|0xC0047056|-1073450922|DTS_E_CANTCREATEPRIMEOUTPUTBUFFER|La tarea Flujo de datos no pudo crear un búfer para llamar a PrimeOutput para la salida de "%3" (%4!d!) en el componente "%1" (%2!d!). Este error suele producirse porque la memoria es insuficiente.|  
|0xC0047057|-1073450921|DTS_E_SCHEDULERTHREADMEMORY|El programador del motor de Flujo de datos no pudo crear un objeto de subproceso porque la memoria es insuficiente. porque no hay memoria suficiente.|  
|0xC004705A|-1073450918|DTS_E_SCHEDULEROBJECT|El programador del motor de Flujo de datos no puede recuperar del diseño el objeto con el id. %1!d! del diseño. El programador del motor de Flujo de datos encontró anteriormente un objeto que ya no está disponible.|  
|0xC004705B|-1073450917|DTS_E_PREPARETREENODEFAILED|La tarea Flujo de datos no pudo preparar los búferes del nodo del árbol de ejecución que empieza en la salida "%1" (%2!d!).|  
|0xC004705C|-1073450916|DTS_E_CANTCREATEVIRTUALBUFFER|La tarea Flujo de datos no puede crear un búfer virtual para preparar la ejecución.|  
|0xC004705E|-1073450914|DTS_E_NOMOREIDS|Se ha alcanzado el Id. máximo. No hay más Id. disponibles para asignar a los objetos.|  
|0xC004705F|-1073450913|DTS_E_ALREADYATTACHED|Ya se ha adjuntado %1 y no puede adjuntarse nuevamente.  Sepárelo y vuelva a intentarlo.|  
|0xC0047060|-1073450912|DTS_E_OUTPUTCOLUMNNAMECONFLICT|No se puede usar el nombre de columna "%1" en la salida "%2" porque entra en conflicto con una columna del mismo nombre en la entrada sincrónica "%3".|  
|0xC0047061|-1073450911|DTS_E_EOFANNOUNCEMENTFAILED|La tarea Flujo de Datos puede para no crear un búfer para marcar el fin del conjunto de filas.|  
|0xC0047062|-1073450910|DTS_E_USERCOMPONENTEXCEPTION|Un componente de usuario administrado ha iniciado la excepción "%1".|  
|0xC0047063|-1073450909|DTS_E_SCHEDULERMEMORY|El programador del motor de Flujo de datos no puede asignar memoria suficiente para las estructuras de ejecución. La memoria del sistema era insuficiente antes de iniciar la ejecución.|  
|0xC0047064|-1073450908|DTS_E_BUFFERNOOBJECTMEMORY|No se pudo crear el objeto de búfer porque la memoria era insuficiente.|  
|0xC0047065|-1073450907|DTS_E_BUFFERNOMAPMEMORY|No se pueden asignar los Id. de linaje de un búfer a los índices DTP_HCOL porque la memoria es insuficiente.|  
|0xC0047066|-1073450906|DTS_E_INDIVIDUALPUTVARIABLESFAILED|"%1!s!" no pudo almacenar en la caché la colección Variables y devolvió el código de error 0x%2!8.8X.|  
|0xC0047067|-1073450905|DTS_E_INDIVIDUALPUTCOMPONENTMETADATAFAILED|"%1" no pudo almacenar en la caché el objeto de metadatos del componente y devolvió el código de error 0x%2!8.8X!.|  
|0xC0047068|-1073450904|DTS_E_SORTEDOUTPUTHASINVALIDSORTKEYPOSITION|El valor de SortKeyPosition, (%2!ld!), en "%1" es distinto de cero pero es demasiado grande. Debe ser menor o igual que el número de columnas.|  
|0xC004706A|-1073450902|DTS_E_SORTEDOUTPUTHASINVALIDSORTKEYPOSITIONS|La propiedad IsSorted de %1 tiene el valor TRUE, pero los valores absolutos de SortKeyPositions de la columna de salida distinta de cero no forman una secuencia con una progresión continua empezando por uno.|  
|0xC004706B|-1073450901|DTS_E_INDIVIDUALVALIDATIONSTATUSFAILED|Error en la validación de "%1"; se devolvió el estado de validación "%2".|  
|0xC004706C|-1073450900|DTS_E_CANTCREATECOMPONENT|No se pudo crear el componente "%1!s!". Se devolvió el código de error 0x%2!8.8X! "%3!s!". Asegúrese de que el componente esté registrado correctamente.|  
|0xC004706D|-1073450899|DTS_E_COMPONENTNOTREGISTERED|El módulo que contiene "%1" no se ha registrado o instalado correctamente.|  
|0xC004706E|-1073450898|DTS_E_COMPONENTNOTFOUND|No se encuentra el módulo que contiene "%1", aunque se ha registrado.|  
|0xC004706F|-1073450897|DTS_E_BINARYCODENOTFOUND|El componente de script está configurado para precompilar el script, pero no se puede encontrar el código binario. Visite el IDE en el Editor de componentes de script haciendo clic en el botón Diseñar script para que se genere el código binario.|  
|0xC0047070|-1073450896|DTS_E_CANTCREATEBLOBFILE|El administrador de búfer no puede crear un archivo para poner en cola un objeto de tipo long en los directorios nombrados en la propiedad BLOBTempStoragePath.  Se proporcionó un nombre de archivo incorrecto, no tiene permisos o las rutas de acceso se han llenado.|  
|0xC0047071|-1073450895|DTS_E_SYNCHRONOUSIDMISMATCH|El valor de la propiedad SynchronousInputID en "%1" era %2!d! y se esperaba %3!d!.|  
|0xC0047072|-1073450894|DTS_E_OBJECTIDNOTFOUND|No existe ningún objeto con el id. %1!d!.|  
|0xC0047073|-1073450893|DTS_E_OBJECTIDLOOKUPFAILED|No se encuentra un objeto con el id. %1!d! debido al código de error 0x%2!8.8X!.|  
|0xC0047074|-1073450892|DTS_E_INVALIDCODEPAGE|La página de códigos %1!d! especificada en la columna de salida "%2" (%3!d!) no es válida. Seleccione una página de códigos distinta para la columna de salida "%2".|  
|0xC0047075|-1073450891|DTS_E_INDIVIDUALPUTEVENTINFOSFAILED|"%1" no pudo almacenar en la caché la colección EventInfos. Se devolvió el código de error 0x%2!8.8X!.|  
|0xC0047077|-1073450889|DTS_E_DUPLICATEOUTPUTCOLUMNNAMES|Nombre de "%1" duplicado.  Todos los nombres deben ser únicos.|  
|0xC0047078|-1073450888|DTS_E_NOOUTPUTCOLUMNFORINPUTCOLUMN|No hay ninguna columna de salida asociada a la columna de entrada "%1" (%2!d!).|  
|0xC0047079|-1073450887|DTS_E_EXCLGRPNOSYNCINP|"%1" tiene un búfer virtual que se extiende desde un origen raíz. Hay un grupo de exclusión distinto de cero con una entrada sincrónica con valor cero.|  
|0xC004707A|-1073450886|DTS_E_ERROROUTCANTBEONSYNCNONEXCLUSIVEOUTPUT|"%1" no puede ser una salida de error, ya que no se pueden colocar salidas de error en salidas sincrónicas no exclusivas.|  
|0xC004707B|-1073450885|DTS_E_EXPREVALDIVBYZERO|Error de división por cero. El operando de la derecha se evalúa como cero en la expresión "%1".|  
|0xC004707C|-1073450884|DTS_E_EXPREVALLITERALOVERFLOW|El literal "%1" es demasiado grande para el tipo %2. El tamaño del literal desborda el tipo.|  
|0xC004707D|-1073450883|DTS_E_EXPREVALBINARYOPNUMERICOVERFLOW|El resultado de la operación binaria "%1" en los tipos de datos %2 y %3 supera el tamaño máximo de los tipos numéricos. No se pudo convertir implícitamente los tipos de operandos en un resultado numérico (DT_NUMERIC) sin perder precisión o escala. Para realizar esta operación, deben convertirse explícitamente uno o ambos operandos, mediante un operador de conversión.|  
|0xC004707E|-1073450882|DTS_E_EXPREVALBINARYOPOVERFLOW|El resultado de la operación binaria "%1" supera el tamaño máximo del tipo de datos de resultados "%2". El tamaño del resultado de la operación desborda el tipo de resultado.|  
|0xC004707F|-1073450881|DTS_E_EXPREVALFUNCTIONOVERFLOW|El resultado de la llamada a la función "%1" es demasiado grande para el tipo "%2". El tamaño del resultado de la llamada a la función desborda el tipo de operando. Es posible que sea necesario realizar una conversión explícita a un tipo mayor.|  
|0xC0047080|-1073450880|DTS_E_EXPREVALBINARYTYPEMISMATCH|Los tipos de datos "%1" y "%2" no son compatibles con el operador binario "%3". No fue posible convertir implícitamente los tipos de operando en tipos compatibles con la operación. Para realizar esta operación, deben convertirse explícitamente uno o ambos operandos, mediante un operador de conversión.|  
|0xC0047081|-1073450879|DTS_E_EXPREVALUNSUPPORTEDBINARYTYPE|No se puede utilizar el tipo de datos "%1" con el operador binario "%2". El tipo de uno o ambos operandos no es compatible con la operación. Para realizar esta operación, deben convertirse explícitamente uno o ambos operandos, mediante un operador de conversión.|  
|0xC0047082|-1073450878|DTS_E_EXPREVALBINARYSIGNMISMATCH|Los signos del operador binario bit a bit "%1" no coinciden en la operación "%2". Ambos operandos de este operador deben ser positivos o negativos.|  
|0xC0047083|-1073450877|DTS_E_EXPREVALBINARYOPERATIONFAILED|Error de la operación binaria "%1". Código de error: 0x%2!8.8X!. Error interno o memoria insuficiente.|  
|0xC0047084|-1073450876|DTS_E_EXPREVALBINARYOPERATIONSETTYPEFAILED|No se pudo establecer el tipo de resultados de la operación binaria "%1". Código de error: 0x%2!8.8X!.|  
|0xC0047085|-1073450875|DTS_E_EXPREVALSTRINGCOMPARISONFAILED|Error al comparar "%1" con la cadena "%2".|  
|0xC0047086|-1073450874|DTS_E_EXPREVALUNSUPPORTEDUNNARYTYPE|No se puede utilizar el tipo de datos "%1" con el operador unario "%2". Este tipo de operando no es compatible con la operación. Para realizar esta operación, debe convertirse explícitamente el operando mediante un operador de conversión.|  
|0xC0047087|-1073450873|DTS_E_EXPREVALUNARYOPERATIONFAILED|Error de la operación unaria "%1". Código de error: 0x%2!8.8X!. Error interno o memoria insuficiente.|  
|0xC0047088|-1073450872|DTS_E_EXPREVALUNARYOPERATIONSETTYPEFAILED|No se pudo establecer el conjunto de resultados de la operación unaria "%1". Código de error: 0x%2!8.8X!.|  
|0xC0047089|-1073450871|DTS_E_EXPREVALPARAMTYPEMISMATCH|La función "%1" no admite el tipo de datos "%2" en el número de parámetro %3!d!. No se pudo convertir implícitamente el tipo de parámetro en un tipo compatible con la función. Para realizar esta operación, debe convertirse explícitamente el operando mediante un operador de conversión.|  
|0xC004708A|-1073450870|DTS_E_EXPREVALINVALIDFUNCTION|No se reconoció la función "%1". El nombre de la función es incorrecto o no existe.|  
|0xC004708B|-1073450869|DTS_E_EXPREVALFNSUBSTRINGINVALIDLENGTH|La longitud %1!d! no es válido para la función "%2". El parámetro de longitud no puede ser negativo. Cambie el parámetro de longitud a cero o a un valor positivo.|  
|0xC004708C|-1073450868|DTS_E_EXPREVALFNSUBSTRINGINVALIDSTARTINDEX|El índice de inicio %11d! no es válido para la función "%2". El valor del índice inicial debe ser un entero mayor que 0. El índice inicial se basa en uno y no en cero.|  
|0xC004708E|-1073450866|DTS_E_EXPREVALCHARMAPPINGFAILED|La función "%1" no puede asignar caracteres a la cadena "%2".|  
|0xC004708F|-1073450865|DTS_E_EXPREVALINVALIDDATEPART|"%1" no es una parte de fecha válida en la función "%2".|  
|0xC0047090|-1073450864|DTS_E_EXPREVALINVALIDNULLPARAM|Número de parámetro %1!d! de la función NULL con el tipo de datos "%2" no es válido. Los parámetros de NULL() deben ser estáticos y no pueden contener elementos dinámicos como columnas de entrada.|  
|0xC0047091|-1073450863|DTS_E_EXPREVALINVALIDNULLPARAMTYPE|Número de parámetro %1!d! de la función NULL con el tipo de datos "%2" no es un entero. Un parámetro de NULL() debe ser un entero o un tipo que pueda convertirse a un entero.|  
|0xC0047092|-1073450862|DTS_E_EXPREVALFUNCTIONPARAMNOTSTATIC|Número de parámetro %1!d! de la función "%2" no es estático. Este parámetro debe ser estático y no puede contener elementos dinámicos como columnas de entrada.|  
|0xC0047093|-1073450861|DTS_E_EXPREVALINVALIDCASTPARAM|Número de parámetro %1!d! de la conversión al tipo de datos "%2" no es válido. Los parámetros de los operadores de conversión deben ser estáticos y no pueden contener elementos dinámicos como columnas de entrada.|  
|0xC0047094|-1073450860|DTS_E_EXPREVALINVALIDCASTPARAMTYPE|Número de parámetro %1!d! de la conversión al tipo de datos "%2" no es un entero. Un parámetro de un operador de conversión deber ser un entero o un tipo que pueda convertirse a un entero.|  
|0xC0047095|-1073450859|DTS_E_EXPREVALINVALIDCAST|No se puede convertir la expresión "%1" del tipo de datos "%2" al tipo de datos "%3". No se admite la conversión solicitada.|  
|0xC0047096|-1073450858|DTS_E_EXPREVALINVALIDTOKEN|Error al intentar analizar la expresión "%1".  No se reconoció el token "%2" del número de línea "%3", número de carácter "%4". No se puede analizar la expresión porque contiene elementos no válidos en la ubicación especificada.|  
|0xC0047097|-1073450857|DTS_E_EXPREVALUNEXPECTEDPARSEERROR|Error al analizar la expresión "%1". No pudo analizarse la expresión por un motivo desconocido.|  
|0xC0047098|-1073450856|DTS_E_EXPREVALFAILEDTOPARSEEXPRESSIONWITHHR|Error al intentar analizar la expresión "%1". Se devolvió el código de error 0x%2!8.8X!. No puede analizarse la expresión. Es posible que contenga elementos no válidos o que no esté bien formada. También puede ser que haya un error de memoria insuficiente.|  
|0xC0047099|-1073450855|DTS_E_EXPREVALFAILEDTOPARSEEXPRESSION|La expresión "%1" no es válida y no puede analizarse. Es posible que la expresión contenga elementos no válidos o que no esté bien formada.|  
|0xC004709A|-1073450854|DTS_E_EXPREVALEXPRESSIONEMPTY|No había ninguna expresión para calcular. Se intentó calcular u obtener la cadena de una expresión vacía.|  
|0xC004709B|-1073450853|DTS_E_EXPREVALCOMPUTEFAILED|Error al intentar calcular la expresión "%1". Código de error: 0x%2!8.8X!.|  
|0xC004709C|-1073450852|DTS_E_EXPREVALBUILDSTRINGFAILED|Error al intentar generar una representación de cadena de la expresión. Código de error: 0x%1!8.8X!. Error al intentar generar una cadena que represente una expresión y que se pueda mostrar.|  
|0xC004709D|-1073450851|DTS_E_EXPREVALCANNOTCONVERTRESULT|No se puede convertir el tipo de datos de resultado de la expresión "%1" en el tipo de datos de columna "%2". El resultado de la expresión debería escribirse en una columna de entrada/salida, pero el tipo de datos de la expresión no puede convertirse al tipo de datos de la columna.|  
|0xC004709E|-1073450850|DTS_E_EXPREVALCONDITIONALOPINVALIDCONDITIONTYPE|La expresión condicional "%1" del operador condicional tiene un tipo de datos no válido de "%2". La expresión condicional del operador condicional debe devolver un booleano, que es el tipo DT_BOOL.|  
|0xC004709F|-1073450849|DTS_E_EXPREVALCONDITIONALOPTYPEMISMATCH|Los tipos de datos "%1" y "%2" no son compatibles con el operador condicional. Los tipos de operando no pueden convertirse implícitamente en tipos compatibles de la operación condicional. Para realizar esta operación, deben convertirse explícitamente uno o ambos operandos, mediante un operador de conversión.|  
|0xC00470A0|-1073450848|DTS_E_EXPREVALCONDITIONALOPSETTYPEFAILED|No se pudo establecer el tipo de resultados de la operación condicional "%1". Código de error: 0x%2!8.8X!.|  
|0xC00470A1|-1073450847|DTS_E_BUFFERORPHANED|Este búfer se convirtió en huérfano. El administrador de búfer se ha cerrado dejando un búfer pendiente que no podrá limpiarse. Puede ocasionar pérdidas de memoria y otros problemas.|  
|0xC00470A2|-1073450846|DTS_E_EXPREVALINPUTCOLUMNNAMENOTFOUND|Error al intentar buscar la columna de entrada con el nombre "%1". Código de error: 0x%2!8.8X!. No se encontró la columna de entrada especificada en la colección de columnas de entrada.|  
|0xC00470A3|-1073450845|DTS_E_EXPREVALINPUTCOLUMNIDNOTFOUND|Error al intentar encontrar la columna de entrada con id. de linaje %1!d!. Código de error 0x%2!8.8X!. No se encontró la columna de entrada en la colección de columnas de entrada.|  
|0xC00470A4|-1073450844|DTS_E_EXPREVALNOINPUTCOLUMNCOLLECTIONFORCOLUMNNAME|La expresión contiene el token desconocido "%1". Si "%1" es una variable, se debería expresar como "\@%1". El token especificado no es válido. Si el token debe ser un nombre de variable, debería tener como prefijo el símbolo \@.|  
|0xC00470A5|-1073450843|DTS_E_EXPREVALNOINPUTCOLUMNCOLLECTIONFORCOLUMNID|La expresión contiene el token desconocido "#%1!d!".|  
|0xC00470A6|-1073450842|DTS_E_EXPREVALVARIABLENOTFOUND|No se encontró la variable "%1" en la colección Variables. Es posible que la variable no exista en el ámbito correcto.|  
|0xC00470A7|-1073450841|DTS_E_EXPREVALINVALIDTOKENSTATE|Error al intentar analizar la expresión "%1". Es posible que la expresión contenga tokens no válidos o incompletos, o bien elementos no válidos. Puede que no esté bien formada o que le falte parte de un elemento necesario como, por ejemplo, un paréntesis.|  
|0xC00470A8|-1073450840|DTS_E_BLANKOUTPUTCOLUMNNAME|El nombre de "%1" está en blanco y los nombres no pueden estar en blanco.|  
|0xC00470A9|-1073450839|DTS_E_HASSIDEEFFECTSWITHSYNCINP|La propiedad HasSideEffects de "%1" tiene el valor TRUE, pero "%1" es sincrónico y no puede tener efectos secundarios. Establezca la propiedad HasSideEffects en FALSE.|  
|0xC00470AA|-1073450838|DTS_E_EXPREVALINVALIDCASTCODEPAGE|El valor %1!d! especificado para el parámetro de página de códigos de la conversión al tipo de datos "%2" no es válido. La página de códigos no está instalada en el equipo.|  
|0xC00470AB|-1073450837|DTS_E_EXPREVALINVALIDCASTPRECISION|El valor %1!d! especificado para el parámetro de precisión de la conversión al tipo de datos "%2" no es válido. La precisión debe estar en el intervalo entre %3!d! y %4!d! y el valor de precisión está fuera del intervalo de la conversión de tipos.|  
|0xC00470AC|-1073450836|DTS_E_EXPREVALINVALIDCASTSCALE|El valor %1!d! especificado para el parámetro de escala de la conversión al tipo de datos "%2" no es válido. Es necesario que la escala esté en el intervalo entre %3!d! y %4!d! y el valor de escala está fuera del intervalo de la conversión de tipos. El valor de escala no debe superar al de precisión y debe ser positivo.|  
|0xC00470AD|-1073450835|DTS_E_NONSORTEDOUTPUTHASSORTKEYPOSITIONS|La propiedad IsSorted de "%1" tiene el valor false, pero %2!lu! de los valores SortKeyPositions de sus columnas de salida son distintos de cero.|  
|0xC00470AF|-1073450833|DTS_E_EXPREVALCONDITIONALOPCODEPAGEMISMATCH|Las páginas de códigos deben coincidir en los operandos de la operación condicional "%1" del tipo "%2". La página de códigos del operando izquierdo no coincide con la página de códigos del operando derecho. Las páginas de códigos deben tener el mismo operador condicional en el tipo especificado.|  
|0xC00470B1|-1073450831|DTS_E_REFERENCEDMETADATABADCOUNT|La entrada "%1" (%2!d!) hace referencia a la entrada "%3" (%4!d!), pero ambas entradas no tienen el mismo número de columnas. La entrada %5!d! tiene %6!d! columnas y la entrada %7!¡d! tiene %8!d! columnas.|  
|0xC00470B2|-1073450830|DTS_E_OBJECTLINEAGEIDNOTFOUND|No hay ningún objeto con el id. de linaje %1!d!.|  
|0xC00470B3|-1073450829|DTS_E_FILENAMEOUTPUTCOLUMNOTFOUND|No se encuentra la columna de salida del nombre de archivo.|  
|0xC00470B4|-1073450828|DTS_E_FILENAMEOUTPUTCOLUMNINVALIDDATATYPE|La columna de salida del nombre de archivo no es una cadena de caracteres Unicode terminada en nulo, con tipo de datos DT_WSTR.|  
|0xC00470B5|-1073450827|DTS_E_DISTRIBUTORADDFAILED|Un distribuidor no pudo asignar un búfer al subproceso "%1" a causa del error 0x%2!8.8X!. Es probable que el subproceso de destino se esté cerrando.|  
|0xC00470B6|-1073450826|DTS_E_LOCALENOTINSTALLED|LocaleID %1!ld! no está instalado en este sistema.|  
|0xC00470B7|-1073450825|DTS_E_EXPREVALILLEGALHEXESCAPEINSTRINGLITERAL|El literal de cadena "%1" contiene una secuencia de escape hexadecimal no válida: "\x%2". No se admite la secuencia de escape en literales de cadena del evaluador de expresiones. Las secuencias de escape hexadecimales deben tener la forma \xhhhh, donde h es un dígito hexadecimal válido.|  
|0xC00470B8|-1073450824|DTS_E_EXPREVALILLEGALESCAPEINSTRINGLITERAL|El literal de cadena "%1" contiene una secuencia de escape no válida: "\\%2!c!". No se admite la secuencia de escape en literales de cadena del evaluador de expresiones. Si necesita incluir una barra diagonal inversa en la cadena, use una doble barra diagonal inversa, "\\\\".|  
|0xC00470B9|-1073450823|DTS_E_NOOUTPUTCOLUMNS|"%1" no contiene columnas de salida. Una salida asincrónica debe contener columnas de salida.|  
|0xC00470BA|-1073450822|DTS_E_LOBDATATYPENOTSUPPORTED|"%1" tiene un tipo de datos de objeto long, DT_TEXT, DT_NTEXT o DT_IMAGE, que no es compatible.|  
|0xC00470BB|-1073450821|DTS_E_OUTPUTWITHMULTIPLEERRORS|Error al insertar el id. de salida tiene varias configuraciones de salida de error. Primero %2!d! y %3!d!, luego %4!d! y %5!d!.|  
|0xC00470BC|-1073450820|DTS_E_FAILEDDURINGOLEDBDATATYPECONVERSIONCHECK|El proveedor OLE DB no pudo comprobar la conversión de tipo de datos de "%1".|  
|0xC00470BD|-1073450819|DTS_E_BUFFERISEOR|Este búfer representa el final del conjunto de filas y no se puede alterar su recuento de filas.  Se intentó llamar a AddRow o RemoveRow en un búfer que contiene el final de la marca de conjunto de filas.|  
|0xC00470BE|-1073450818|DTS_E_EXPREVALUNSUPPORTEDTYPE|El tipo de datos "%1" no se admite en una expresión. El tipo especificado no es compatible o no es válido.|  
|0xC00470BF|-1073450817|DTS_E_PRIMEOUTPUTNOEOR|El método PrimeOutput se ejecutó correctamente en "%1" pero no indicó un final del conjunto de filas. Hay un error en el componente. Debería haber indicado un final de fila. La canalización cerrará la ejecución para evitar resultados imprevisibles.|  
|0xC00470C0|-1073450816|DTS_E_EXPREVALDATACONVERSIONOVERFLOW|Se produjo un desbordamiento al convertir del tipo de datos "%1" al tipo de datos "%2". El tipo de origen es demasiado grande para el tipo de destino.|  
|0xC00470C1|-1073450815|DTS_E_EXPREVALDATACONVERSIONNOTSUPPORTED|No se admite la conversión del tipo de datos "%1" al tipo de datos "%2". El tipo de origen no puede convertirse al tipo de destino.|  
|0xC00470C2|-1073450814|DTS_E_EXPREVALDATACONVERSIONFAILED|Código de error: 0x%1!8.8X! al intentar convertir del tipo de datos %2 al tipo de datos %3.|  
|0xC00470C3|-1073450813|DTS_E_EXPREVALCONDITIONALOPERATIONFAILED|Error de la operación condicional "%1". Código de error: 0x%2!8.8X!. Error interno o error de memoria insuficiente.|  
|0xC00470C4|-1073450812|DTS_E_EXPREVALCASTFAILED|Error al convertir la expresión "%1" del tipo de datos "%2" al tipo de datos "%3". Código de error: 0x%4!8.8X!.|  
|0xC00470C5|-1073450811|DTS_E_EXPREVALFUNCTIONCOMPUTEFAILED|No se pudo evaluar la función "%1". Código de error: 0x%2!8.8X!.|  
|0xC00470C6|-1073450810|DTS_E_EXPREVALFUNCTIONCONVERTPARAMTOMEMBERFAILED|Número de parámetro %1!d! de la función “%2" no puede convertirse a un valor estático.|  
|0xC00470C7|-1073450809|DTS_E_REDIRECTROWUNAVAILABLEWITHFASTLOADANDZEROMAXINSERTCOMMITSIZE|No es posible establecer que la disposición de filas de error en "%1" redirija la fila cuando se active la opción de carga rápida y el tamaño máximo de confirmación de inserción establecido sea cero.|  
|0xC00470CE|-1073450802|DTS_E_EXPREVALBINARYOPERATORCODEPAGEMISMATCH|Las páginas de códigos de los operandos del operador binario "%1"" del tipo "%2" deben coincidir. Actualmente, la página de códigos del operando izquierdo no coincide con la página de códigos del operando derecho. El operador binario especificado en el tipo especificado debe tener las mismas páginas de códigos.|  
|0xC00470CF|-1073450801|DTS_E_EXPREVALVARIABLECOMPUTEFAILED|No se pudo recuperar el valor de la variable "%1". Código de error: 0x%2!8.8X!.|  
|0xC00470D0|-1073450800|DTS_E_EXPREVALVARIABLETYPENOTSUPPORTED|El tipo de datos de la variable "%1" no se admite en una expresión.|  
|0xC00470D1|-1073450799|DTS_E_EXPREVALCASTCODEPAGEMISMATCH|No se puede convertir la expresión "%1" del tipo de datos "%2" al tipo de datos "%3" porque la página de códigos del valor que se convierte (%4!d!) no coincide con la página de códigos de resultados solicitada (%5!d!). La página de códigos del origen debe coincidir con la página de códigos solicitada para el destino.|  
|0xC00470D2|-1073450798|DTS_E_BUFFERSIZEOUTOFRANGE|El tamaño de búfer predeterminado debe estar entre %1!d! y %2!d! bytes. Se intentó establecer un valor demasiado pequeño o demasiado grande para la propiedad DefaultBufferSize.|  
|0xC00470D3|-1073450797|DTS_E_BUFFERMAXROWSIZEOUTOFRANGE|El número máximo predeterminado de filas del búfer debe ser superior a %1!d! filas. Se intentó establecer un valor demasiado pequeño para la propiedad DefaultBufferMaxRows.|  
|0xC00470D4|-1073450796|DTS_E_EXTERNALCOLUMNMETADATACODEPAGEMISMATCH|La página de códigos de %1 es %2!d! y debe ser %3!d!.|  
|0xC00470D5|-1073450795|DTS_E_THREADCOUNTOUTOFRANGE|No se pudo asignar %3!d! a la propiedad EngineThreads de la tarea Flujo de datos. El valor debe estar entre %1!d! y %2!d!.|  
|0xC00470D6|-1073450794|DTS_E_EXPREVALINVALIDTOKENSINGLEQUOTE|Error al analizar la expresión "%1". No se esperaba una comilla simple en el número de línea "%2", número de carácter "%3".|  
|0xC00470D7|-1073450793|DTS_E_EXPREVALINVALIDTOKENSINGLEEQUAL|Error al analizar la expresión "%1". No se esperaba el signo igual (=) en el número de línea "%2", número de carácter "%3". Es posible que se necesite un signo igual doble (==) en la ubicación especificada.|  
|0xC00470DA|-1073450790|DTS_E_INDIVIDUALPUTREFTRACKERFAILED|El componente "%1" no pudo almacenar en la caché la colección de rastreadores de referencias de objetos en tiempo de ejecución y devolvió el código de error 0x%2!8.8X!.|  
|0xC00470DB|-1073450789|DTS_E_EXPREVALAMBIGUOUSINPUTCOLUMNNAME|Hay varias columnas de entrada con el nombre "%1". La columna de entrada deseada debe especificarse de forma única como [Nombre de componente].[%2] o debe hacerse referencia a ella mediante el id. de linaje. Actualmente, la columna de entrada especificada existe en más de un componente.|  
|0xC00470DC|-1073450788|DTS_E_EXPREVALDOTTEDINPUTCOLUMNNAMENOTFOUND|Error al buscar la columna de entrada con el nombre "[%1].[%2]". Código de error: 0x%3!8.8X!. No se encontró la columna de entrada en la colección de columnas de entrada.|  
|0xC00470DD|-1073450787|DTS_E_EXPREVALAMBIGUOUSVARIABLENNAME|Hay varias variables con el nombre "%1". El nombre de variable debe de forma única como \@[Namespace::%2]. La variable existe en más de un espacio de nombres.|  
|0xC00470DE|-1073450786|DTS_E_REDUCTIONFAILED|El programador del motor de Flujo de datos no pudo reducir el plan de ejecución de la canalización. Establezca el valor false en la propiedad OptimizedMode.|  
|0xC00470DF|-1073450785|DTS_E_EXPREVALSQRTINVALIDPARAM|La función SQRT no puede ejecutarse con valores negativos y se ha pasado un valor negativo a la función SQRT.|  
|0xC00470E0|-1073450784|DTS_E_EXPREVALLNINVALIDPARAM|La función LN no puede ejecutarse con valores negativos o cero, y se ha pasado un cero o un valor negativo a la función LN.|  
|0xC00470E1|-1073450783|DTS_E_EXPREVALLOGINVALIDPARAM|La función LOG no puede ejecutarse con valores negativos o cero, y se ha pasado un cero o un valor negativo a la función LOG.|  
|0xC00470E2|-1073450782|DTS_E_EXPREVALPOWERINVALIDPARAM|Los parámetros pasados a la función POWER no pueden evaluarse y han producido un resultado indeterminado. |  
|0xC00470E3|-1073450781|DTS_E_NOCANCELEVENT|El objeto de tiempo de ejecución no puede proporcionar un evento de cancelación a causa del error 0x%1!8.8X!.|  
|0xC00470E4|-1073450780|DTS_E_CANCELRECEIVED|La canalización recibió una solicitud de cancelación y se está cerrando.|  
|0xC00470E5|-1073450779|DTS_E_EXPREVALUNARYOPOVERFLOW|El resultado de la operación de negación unaria "%1" supera el tamaño máximo del tipo de datos de resultados "%2". El tamaño del resultado de la operación desborda el tipo de resultado.|  
|0xC00470E6|-1073450778|DTS_E_EXPREVALPLACEHOLDERINEXPRESSION|Se encontró el marcador de posición "%1" en una expresión. Debe sustituirse por un parámetro u operando real.|  
|0xC00470E7|-1073450777|DTS_E_EXPREVALFNRIGHTINVALIDLENGTH|La longitud %1!d! especificada para la función "%2 " es negativa y no es válida. El parámetro de longitud debe ser positivo.|  
|0xC00470E8|-1073450776|DTS_E_EXPREVALFNREPLICATEINVALIDREPEATCOUNT|El número de repeticiones %1!d! es negativo y no es válido para la función "%2". El parámetro de número de repeticiones no puede ser negativo.|  
|0xC00470EA|-1073450774|DTS_E_EXPREVALVARIABLECOULDNOTBEREAD|Error al leer la variable "%1". Código de error: 0x%2!8.8X!.|  
|0xC00470EC|-1073450772|DTS_E_EXPREVALBINARYOPDTSTRNOTSUPPORTED|En los operandos de una operación binaria, el tipo de datos DT_STR solamente se admite en columnas de entrada y operaciones de conversión. La expresión "%1" tiene un operando DT_STR que no es una columna de entrada ni el resultado de una conversión y no puede utilizarse en una operación binaria. Para realizar esta operación, debe convertirse explícitamente el operando mediante un operador de conversión.|  
|0xC00470ED|-1073450771|DTS_E_EXPREVALCONDITIONALOPDTSTRNOTSUPPORTED|En los operandos de la operación condicional, el tipo de datos DT_STR solamente se admite en columnas de entrada y operaciones de conversión. La expresión "%1" tiene un operando DT_STR que no es una columna de entrada ni el resultado de una conversión y no puede utilizarse en la operación condicional. Para realizar esta operación, debe convertirse explícitamente el operando mediante un operador de conversión.|  
|0xC00470EE|-1073450770|DTS_E_EXPREVALFNFINDSTRINGINVALIDOCCURRENCECOUNT|El recuento de repeticiones %1!d! no es válido para la función "%2". Este parámetro debe ser mayor que cero.|  
|0xC00470EF|-1073450769|DTS_E_INDIVIDUALPUTLOGENTRYINFOS|"%1" no pudo almacenar en la caché la colección LogEntryInfos y devolvió el código de error 0x%2!8.8X!.|  
|0xC00470F0|-1073450768|DTS_E_EXPREVALINVALIDDATEPARTNODE|El parámetro de parte de fecha especificado para la función "%1" no es válido. Debe ser una cadena estática.  El parámetro de parte de fecha no puede contener elementos dinámicos, como columnas de entrada, y debe ser del tipo DT_WSTR.|  
|0xC00470F1|-1073450767|DTS_E_EXPREVALINVALIDCASTLENGTH|El valor %1!d! especificado para el parámetro de longitud de la conversión al tipo de datos %2 es negativo y no es válido. La longitud debe ser positiva.|  
|0xC00470F2|-1073450766|DTS_E_EXPREVALINVALIDNULLCODEPAGE|El valor %1!d! especificado para el parámetro de página de códigos de la función NULL con el tipo de datos "%2" no es válido. La página de códigos no está instalada en el equipo.|  
|0xC00470F3|-1073450765|DTS_E_EXPREVALINVALIDNULLPRECISION|El valor %1!d! especificado para el parámetro de precisión de la función NULL con el tipo de datos "%2" está fuera del intervalo. La precisión debe estar en el intervalo entre %3!d! y %4!d!.|  
|0xC00470F4|-1073450764|DTS_E_EXPREVALINVALIDNULLSCALE|El valor %1!d! especificado para el parámetro de escala de la función NULL con el tipo de datos %2 está fuera del intervalo. La escala debe estar en el intervalo entre %3!d! y %4!d!. El valor de escala no debe superar al de precisión ni ser negativo.|  
|0xC00470F5|-1073450763|DTS_E_EXPREVALINVALIDNULLLENGTH|El valor %1!d! especificado para el parámetro de longitud de la función "NULL" con el tipo de datos %2 es negativo y no es válido. La longitud debe ser positiva.|  
|0xC00470F6|-1073450762|DTS_E_NEGATIVESNOTALLOWED|%1 no puede tener asignado un valor negativo.|  
|0xC00470F7|-1073450761|DTS_E_FASTPARSENOTALLOWED|El valor de la propiedad personalizada "%1" para "%2" no puede ser true.  El tipo de datos de columna debe ser uno de los siguientes:  DT_I1, DT_I2, DT_I4, DT_I8, DT_UI1, DT_UI2, DT_UI4, DT_UI8, DT_DBTIMESTAMP, DT_DBTIMESTAMP2, DT_DBTIMESTAMPOFFSET, DT_DATE, DT_DBDATE, DT_DBTIME, DT_DBTIME2 o DT_FILETIME.|  
|0xC00470F8|-1073450760|DTS_E_CANNOTREATTACHPATH|No se puede volver a adjuntar "%1". Elimine la ruta de acceso, agregue una nueva y adjúntela.|  
|0xC00470F9|-1073450759|DTS_E_EXPREVALINVALIDNUMBEROFPARAMSPLURALSINGULAR|La función "%1" requiere %2!d! parámetros, no %3!d! parámetro. Se reconoció el nombre de la función pero el número de parámetros no es válido.|  
|0xC00470FA|-1073450758|DTS_E_EXPREVALINVALIDNUMBEROFPARAMSSINGULARPLURAL|La función "%1" requiere %2!d! parámetro, no %3!d! parámetros. Se reconoció el nombre de la función pero el número de parámetros no es válido.|  
|0xC00470FB|-1073450757|DTS_E_EXPREVALINVALIDNUMBEROFPARAMSPLURALPLURAL|La función "%1" requiere %2!d! parámetros, no %3!d! parámetros. Se reconoció el nombre de la función pero el número de parámetros no es válido.|  
|0xC00470FC|-1073450756|DTS_E_EXPREVALFAILEDTOPARSEEXPRESSIONOUTOFMEMORY|Error al intentar analizar la expresión "%1" porque la memoria es insuficiente.|  
|0xC00470FD|-1073450755|DTS_E_INDIVIDUALCHECKPRODUCTLEVELFAILED|%1 no pudo realizar su comprobación de nivel de producto necesario y se devolvió el código de error 0x%2!8.8X!.|  
|0xC00470FE|-1073450754|DTS_E_PRODUCTLEVELTOLOW|Código de error SSIS DTS_E_PRODUCTLEVELTOLOW.  No se puede ejecutar la tarea %1 en la instalación %2 de Integration Services. Requiere %3 o una edición de nivel superior.|  
|0xC00470FF|-1073450753|DTS_E_EXPREVALSTRINGLITERALTOOLONG|Un literal de cadena de la expresión supera la longitud máxima permitida de %1!d! caracteres.|  
|0xC0047100|-1073450752|DTS_E_EXPREVALSTRINGVARIABLETOOLONG|La variable %1 contiene una cadena que supera la longitud máxima permitida de %2!d! caracteres.|  
|0xC0047101|-1073450751|DTS_E_COMPONENT_NOINTERFACE|Se encontró %1, pero no admite una interfaz de Integration Services necesaria (IDTSRuntimeComponent100).  Obtenga una versión actualizada de este componente del proveedor de componentes.|  
|0xC0048000|-1073446912|DTS_E_CANNOTOPENREGISTRYKEY|No se puede abrir la clave del Registro "%1".|  
|0xC0048001|-1073446911|DTS_E_INVALIDCOMPONENTFILENAME|No se puede obtener el nombre de archivo del componente con el CLSID "%1". Compruebe si el componente se ha registrado correctamente o si el CLSID proporcionado es correcto.|  
|0xC0048002|-1073446910|DTS_E_UNKNOWNCOMPONENTHASINVALIDCLSID|El CLSID de uno de los componentes no es válido. Compruebe si todos los componentes de la canalización tienen CLSID válidos.|  
|0xC0048003|-1073446909|DTS_E_COMPONENTHASINVALIDCLSID|El CLSID de uno de los componentes, con el id. %1!d!, no es válida.|  
|0xC0048004|-1073446908|DTS_E_INVALIDINDEX|El índice no es válido.|  
|0xC0048005|-1073446907|DTS_E_CANNOTACCESSDTSAPPLICATIONOBJECT|No se puede obtener acceso al objeto Application. Compruebe si SSIS se ha instalado correctamente.|  
|0xC0048006|-1073446906|DTS_E_ERROROCCURREDWHILERETRIEVINGFILENAME|Error al recuperar el nombre de archivo de un componente. Código de error: 0x%1!8.8X!.|  
|0xC0048007|-1073446905|DTS_E_CANNOTRETRIEVEPROPERTYFORCOMPONENT|No se puede recuperar la propiedad "%1" del componente con el id. %2!d!.|  
|0xC0048008|-1073446904|DTS_E_DUPLICATEIDFOUND|Se intentó utilizar el id. %1!d! más de una vez en la tarea Flujo de datos.|  
|0xC0048009|-1073446903|DTS_E_CANNOTRETRIEVEBYLINEAGE|No se puede recuperar por el Id. de linaje un elemento de una colección que no contiene columnas.|  
|0xC004800B|-1073446901|DTS_E_CANNOTMAPRUNTIMECONNECTIONMANAGER|No se encuentra el administrador de conexiones con el id. "%1" en la colección de administradores de conexión, a causa de un error con el código 0x%2!8.8X!. "%3" necesita que el administrador de conexiones se incluya en la colección de administradores de conexión de "%4". Compruebe si se ha creado un administrador de conexiones con ese Id. en la colección de administradores de conexión, Connections.|  
|0xC004800E|-1073446898|DTS_E_INPUTNOTKNOWN|El subproceso "%1" recibió un búfer para la entrada %2!d!, pero este subproceso no es responsable de dicha entrada. Se produjo un error que provocó que el programador del motor de Flujo de datos generara un plan de ejecución incorrecto.|  
|0xC004800F|-1073446897|DTS_E_GETRTINTERFACEFAILED|El componente "%1" (%2!d!) no puede proporcionar una interfaz IDTSRuntimeComponent100.|  
|0xC0048011|-1073446895|DTS_E_CANTGIVEAWAYBUFFER|El motor de la tarea Flujo de datos intentó copiar un búfer para asignar otro subproceso pero no lo consiguió.|  
|0xC0048012|-1073446894|DTS_E_CANTCREATEVIEWBUFFER|El motor de la tarea Flujo de datos no pudo crear un búfer de vista del tipo %1!d! sobre el tipo %2!d! del búfer %3!d.|  
|0xC0048013|-1073446893|DTS_E_UNUSABLETEMPORARYPATH|El administrador de búfer no pudo crear un archivo temporal en la ruta de acceso "%1". La ruta de acceso no volverá a tenerse en cuenta para su almacenamiento temporal.|  
|0xC0048014|-1073446892|DTS_E_DIRECTTONONERROROUTPUT|El administrador de búfer intentó insertar una fila de error en una salida que no estaba registrada como salida de error. Se produjo una llamada a DirectErrorRow en una salida que no tiene la propiedad IsErrorOut establecida en TRUE.|  
|0xC0048015|-1073446891|DTS_E_BUFFERISPRIVATE|Se realizó una llamada a un método de búfer en un búfer privado y los búferes privados no admiten esta operación.|  
|0xC0048016|-1073446890|DTS_E_BUFFERISFLAT|Los búferes de modo privado no admiten esta operación.|  
|0xC0048017|-1073446889|DTS_E_BUFFERISPRIMEOUTPUT|Esta operación no puede llamarse en un búfer pasado a PrimeOutput. Se realizó una llamada a un método de búfer durante PrimeOutput, pero esta llamada no se permite durante PrimeOutput.|  
|0xC0048018|-1073446888|DTS_E_BUFFERISPROCESSINPUT|No se puede llamar a esta operación en un búfer pasado a ProcessInput. Se realizó una llamada a un método de búfer durante ProcessInput, pero esta llamada no se permite durante ProcessInput.|  
|0xC0048019|-1073446887|DTS_E_BUFFERGETTEMPFILENAME|El administrador de búfer no pudo obtener un nombre de archivo temporal.|  
|0xC004801A|-1073446886|DTS_E_REFERENCECOLUMNTOOWIDE|El código encontró una columna demasiado ancha.|  
|0xC004801B|-1073446885|DTS_E_CANNOTGETRUNTIMECONNECTIONMANAGERID|No se puede obtener el id. del administrador de conexiones en tiempo de ejecución especificado por "%1" en la colección de administradores de conexión, en Conexiones de "%2", debido al código de error 0x%3!8.8X!. Compruebe que se ha establecido en el componente la propiedad ConnectionManager.ID del objeto de conexión en tiempo de ejecución.|  
|0xC004801C|-1073446884|DTS_E_EMPTYRUNTIMECONNECTIONMANAGERID|El "%1" de la colección de administradores de conexión, Connections, de "%2" no tiene ningún valor en la propiedad id. Compruebe si se ha establecido en el componente la propiedad ConnectionManagerID del objeto de conexión en tiempo de ejecución.|  
|0xC004801D|-1073446883|DTS_E_METADATAREADONLY|Los metadatos no pueden modificarse durante su ejecución.|  
|0xC004801F|-1073446881|DTS_E_UPGRADEFAILED|Los metadatos del componente para "%1" no pudieron actualizarse a la nueva versión del componente. Error en el método PerformUpgrade.|  
|0xC0048020|-1073446880|DTS_E_COMPONENTVERSIONMISMATCH|La versión de %1 no es compatible con esta versión de DataFlow.|  
|0xC0048021|-1073446879|DTS_E_ERRORCOMPONENT|Falta el componente, no está registrado, no puede actualizarse o faltan interfaces necesarias. La información de contacto de este componente es "%1".|  
|0xC0048022|-1073446878|DTS_E_BUFFERISNOTPRIMEOUTPUT|Se llamó al método en el búfer incorrecto. Los búferes que no se utilizan para la salida del componente no admiten esta operación.|  
|0xC0049014|-1073442796|DTS_E_EXPREVALSTATIC_COMPUTATIONFAILED|Error durante el cálculo de la expresión.|  
|0xC0049030|-1073442768|DTS_E_EXPREVALSTATIC_DIVBYZERO|Se produjo una división por cero en la expresión.|  
|0xC0049031|-1073442767|DTS_E_EXPREVALSTATIC_LITERALOVERFLOW|El tamaño del valor literal era demasiado grande para el tipo solicitado.|  
|0xC0049032|-1073442766|DTS_E_EXPREVALSTATIC_BINARYOPNUMERICOVERFLOW|El resultado de la operación binaria supera el tamaño máximo de los tipos numéricos. No se pudo convertir implícitamente los tipos de operandos en un resultado numérico (DT_NUMERIC) sin perder precisión o escala. Para realizar esta operación, deben convertirse explícitamente uno o ambos operandos, mediante un operador de conversión.|  
|0xC0049033|-1073442765|DTS_E_EXPREVALSTATIC_BINARYOPOVERFLOW|El tamaño del resultado de una operación binaria desborda el tamaño máximo del tipo de datos de resultado.|  
|0xC0049034|-1073442764|DTS_E_EXPREVALSTATIC_FUNCTIONOVERFLOW|El tamaño del resultado de una llamada a una función es demasiado grande para el tipo de resultado y desborda el tipo del operando. Es posible que sea necesario realizar una conversión explícita a un tipo mayor.|  
|0xC0049035|-1073442763|DTS_E_EXPREVALSTATIC_BINARYTYPEMISMATCH|Se utilizaron tipos de datos no compatibles con un operador binario. No fue posible convertir implícitamente los tipos de operando en tipos compatibles con la operación. Para realizar esta operación, deben convertirse explícitamente uno o ambos operandos, mediante un operador de conversión.|  
|0xC0049036|-1073442762|DTS_E_EXPREVALSTATIC_UNSUPPORTEDBINARYTYPE|Se utilizó un tipo de datos no compatible con un operador binario. El tipo de uno o de ambos operandos no es compatible con la operación. Para realizar esta operación, deben convertirse explícitamente uno o ambos operandos, mediante un operador de conversión.|  
|0xC0049037|-1073442761|DTS_E_EXPREVALSTATIC_BINARYSIGNMISMATCH|El signo del operador binario bit a bit no coincide. Ambos operandos de este operador deben ser positivos o negativos.|  
|0xC0049038|-1073442760|DTS_E_EXPREVALSTATIC_BINARYOPERATIONFAILED|Error en una operación binaria. Memoria insuficiente o error interno.|  
|0xC0049039|-1073442759|DTS_E_EXPREVALSTATIC_BINARYOPERATIONSETTYPEFAILED|Error al establecer el tipo de resultado de una operación binaria.|  
|0xC004903A|-1073442758|DTS_E_EXPREVALSTATIC_STRINGCOMPARISONFAILED|No se pueden comparar dos cadenas.|  
|0xC004903B|-1073442757|DTS_E_EXPREVALSTATIC_UNSUPPORTEDUNNARYTYPE|Se utiliza un tipo de datos no compatible con un operador unario. El tipo de operando no es compatible con la operación. Para realizar esta operación, debe convertirse explícitamente el operando mediante un operador de conversión.|  
|0xC004903C|-1073442756|DTS_E_EXPREVALSTATIC_UNARYOPERATIONFAILED|Error en una operación unaria. Memoria insuficiente o error interno.|  
|0xC004903D|-1073442755|DTS_E_EXPREVALSTATIC_UNARYOPERATIONSETTYPEFAILED|Error al establecer el tipo de resultado de una operación binaria.|  
|0xC004903E|-1073442754|DTS_E_EXPREVALSTATIC_PARAMTYPEMISMATCH|Una función tiene un parámetro con un tipo de datos no compatible. El tipo de parámetro no puede convertirse implícitamente en un tipo compatible con la función. Para realizar esta operación, debe convertirse explícitamente el operando mediante un operador de conversión.|  
|0xC004903F|-1073442753|DTS_E_EXPREVALSTATIC_INVALIDFUNCTION|Nombre de función no válido en la expresión. Compruebe si el nombre de función existe y es correcto.|  
|0xC0049040|-1073442752|DTS_E_EXPREVALSTATIC_FNSUBSTRINGINVALIDLENGTH|Parámetro de longitud no válido para la función SUBSTRING. El parámetro de longitud no puede ser negativo.|  
|0xC0049041|-1073442751|DTS_E_EXPREVALSTATIC_FNSUBSTRINGINVALIDSTARTINDEX|Índice inicial no válido para la función SUBSTRING. El valor del índice inicial debe ser un entero mayor que cero. El índice inicial se basa en uno y no en cero.|  
|0xC0049042|-1073442750|DTS_E_EXPREVALSTATIC_INVALIDNUMBEROFPARAMS|Se asignó a una función un número incorrecto de parámetros. Se reconoció el nombre de función pero el número de parámetros no era correcto.|  
|0xC0049043|-1073442749|DTS_E_EXPREVALSTATIC_CHARMAPPINGFAILED|Error en una función de asignación de caracteres.|  
|0xC0049044|-1073442748|DTS_E_EXPREVALSTATIC_INVALIDDATEPART|Se especificó para una función de fecha un parámetro de parte de fecha desconocido.|  
|0xC0049045|-1073442747|DTS_E_EXPREVALSTATIC_INVALIDNULLPARAM|Se asignó un parámetro no válido a la función NULL. Los parámetros de NULL deben ser estáticos y no pueden contener elementos dinámicos como columnas de entrada.|  
|0xC0049046|-1073442746|DTS_E_EXPREVALSTATIC_INVALIDNULLPARAMTYPE|Se asignó un parámetro no válido a la función NULL. Un parámetro de NULL debe ser un entero o un tipo que pueda convertirse a un entero.|  
|0xC0049047|-1073442745|DTS_E_EXPREVALSTATIC_FUNCTIONPARAMNOTSTATIC|Se asignó un parámetro no válido a una función. Este parámetro debe ser estático y no puede contener elementos dinámicos como columnas de entrada.|  
|0xC0049048|-1073442744|DTS_E_EXPREVALSTATIC_INVALIDCASTPARAM|Se asignó un parámetro no válido a una operación de conversión. Los parámetros de los operadores de conversión deben ser estáticos y no pueden contener elementos dinámicos como columnas de entrada.|  
|0xC0049049|-1073442743|DTS_E_EXPREVALSTATIC_INVALIDCASTPARAMTYPE|Se asignó un parámetro no válido a una operación de conversión. Un parámetro de un operador de conversión deber ser un entero o un tipo que pueda convertirse a un entero.|  
|0xC004904A|-1073442742|DTS_E_EXPREVALSTATIC_INVALIDCAST|La expresión contenía una conversión de tipos no compatible.|  
|0xC004904B|-1073442741|DTS_E_EXPREVALSTATIC_INVALIDTOKEN|La expresión contenía un token desconocido. La expresión no pudo analizarse porque contiene elementos no válidos.|  
|0xC004904C|-1073442740|DTS_E_EXPREVALSTATIC_FAILEDTOPARSEEXPRESSION|La expresión no es válida y no pudo analizarse. Es posible que contenga elementos no válidos o que no esté bien formada.|  
|0xC004904D|-1073442739|DTS_E_EXPREVALSTATIC_UNARYOPOVERFLOW|El resultado de una operación de negación unaria desborda el tamaño máximo del tipo de datos de resultados. El tamaño del resultado de la operación desborda el tipo de resultado.|  
|0xC004904E|-1073442738|DTS_E_EXPREVALSTATIC_COMPUTEFAILED|Error al intentar calcular la expresión.|  
|0xC004904F|-1073442737|DTS_E_EXPREVALSTATIC_BUILDSTRINGFAILED|Error al intentar generar una representación de cadena de la expresión.|  
|0xC0049050|-1073442736|DTS_E_EXPREVALSTATIC_CANNOTCONVERTRESULT|No se puede convertir el tipo de datos de resultado de la expresión al tipo de datos de columna. El resultado de la expresión debería escribirse en una columna de entrada/salida, pero el tipo de datos de la expresión no puede convertirse al tipo de datos de la columna.|  
|0xC0049051|-1073442735|DTS_E_EXPREVALSTATIC_CONDITIONALOPINVALIDCONDITIONTYPE|La expresión condicional del operador condicional tiene un tipo de datos no válido. La expresión condicional debe ser de tipo DT_BOOL.|  
|0xC0049052|-1073442734|DTS_E_EXPREVALSTATIC_CONDITIONALOPTYPEMISMATCH|Tipos de datos de los operandos del operador condicional no compatibles. No se pudo convertir implícitamente los tipos de operando en tipos compatibles con la operación condicional. Para realizar esta operación, deben convertirse explícitamente uno o ambos operandos, mediante un operador de conversión.|  
|0xC0049053|-1073442733|DTS_E_EXPREVALSTATIC_CONDITIONALOPSETTYPEFAILED|Error al establecer el tipo de resultado de una operación binaria.|  
|0xC0049054|-1073442732|DTS_E_EXPREVALSTATIC_INPUTCOLUMNNAMENOTFOUND|No se encontró la columna de entrada especificada en la colección de columnas de entrada.|  
|0xC0049055|-1073442731|DTS_E_EXPREVALSTATIC_INPUTCOLUMNIDNOTFOUND|Error al intentar buscar una columna de entrada por Id. de linaje. No se encontró la columna de entrada en la colección de columnas de entrada.|  
|0xC0049056|-1073442730|DTS_E_EXPREVALSTATIC_NOINPUTCOLUMNCOLLECTION|La expresión contiene un token desconocido que parece ser una referencia de columna de entrada pero la colección de columnas de entrada no está disponible para procesar columnas de entrada. No se ha proporcionado la colección de columnas de entrada al evaluador de expresiones pero se incluyó una columna de entrada en la expresión.|  
|0xC0049057|-1073442729|DTS_E_EXPREVALSTATIC_VARIABLENOTFOUND|No se encontró una variable especificada en la colección. Es posible que no exista en el ámbito correcto. Compruebe si la variable existe y si el ámbito es correcto.|  
|0xC0049058|-1073442728|DTS_E_EXPREVALSTATIC_INVALIDTOKENSTATE|Error al intentar analizar la expresión. La expresión contiene un token no válido o incompleto. Puede ser que contenga elementos no válidos, que le falte un elemento necesario, como un paréntesis de cierre, o que no esté bien formada.|  
|0xC0049059|-1073442727|DTS_E_EXPREVALSTATIC_INVALIDCASTCODEPAGE|El valor especificado para el parámetro de página de códigos de la conversión al tipo de datos DT_STR o DT_TEXT no es válido. La página de códigos especificada no está instalada en el equipo.|  
|0xC004905A|-1073442726|DTS_E_EXPREVALSTATIC_INVALIDCASTPRECISION|El valor especificado para el parámetro de precisión de una operación de conversión está fuera del intervalo de la conversión de tipos.|  
|0xC004905B|-1073442725|DTS_E_EXPREVALSTATIC_INVALIDCASTSCALE|El valor especificado para el parámetro de escala de una operación de conversión está fuera del intervalo de la conversión de tipos. El valor de escala no debe superar al de precisión ni ser negativo.|  
|0xC004905C|-1073442724|DTS_E_EXPREVALSTATIC_CONDITIONALOPCODEPAGEMISMATCH|Las páginas de códigos no coinciden en una operación condicional. La página de códigos del operando izquierdo no coincide con la página de códigos del operando derecho. El operador condicional de ese tipo debe tener las mismas páginas de códigos.|  
|0xC004905D|-1073442723|DTS_E_EXPREVALSTATIC_ILLEGALHEXESCAPEINSTRINGLITERAL|Un literal de cadena contiene una secuencia de escape hexadecimal no válida. No se admite la secuencia de escape en literales de cadena del evaluador de expresiones. Las secuencias de escape hexadecimales deben tener la forma \xhhhh, donde h es un dígito hexadecimal válido.|  
|0xC004905E|-1073442722|DTS_E_EXPREVALSTATIC_ILLEGALESCAPEINSTRINGLITERAL|El literal de cadena contiene una secuencia de escape no válida. No se admite la secuencia de escape en literales de cadena del evaluador de expresiones. Si necesita incluir una barra diagonal inversa en la cadena, use una doble barra diagonal inversa, "\\\\".|  
|0xC004905F|-1073442721|DTS_E_EXPREVALSTATIC_UNSUPPORTEDTYPE|Se utilizó en la expresión un tipo de datos no compatible o desconocido.|  
|0xC0049060|-1073442720|DTS_E_EXPREVALSTATIC_DATACONVERSIONOVERFLOW|Se produjo un desbordamiento al convertir tipos de datos. El tipo de origen es demasiado grande para el tipo de destino.|  
|0xC0049061|-1073442719|DTS_E_EXPREVALSTATIC_DATACONVERSIONNOTSUPPORTED|La expresión contiene una conversión de tipo de datos no compatible. El tipo de origen no puede convertirse al tipo de destino.|  
|0xC0049062|-1073442718|DTS_E_EXPREVALSTATIC_DATACONVERSIONFAILED|Error al intentar realizar la conversión de datos. El tipo de origen no pudo convertirse al tipo de destino.|  
|0xC0049063|-1073442717|DTS_E_EXPREVALSTATIC_CONDITIONALOPERATIONFAILED|Error en la operación condicional.|  
|0xC0049064|-1073442716|DTS_E_EXPREVALSTATIC_CASTFAILED|Error al intentar realizar una conversión de tipos.|  
|0xC0049065|-1073442715|DTS_E_EXPREVALFAILEDTOCONVERTSTRCOLUMNTOWSTR|Error al convertir "%1" del tipo DT_STR al tipo DT_WSTR. Código de error: 0x%2!8.8X!. Error al realizar la conversión implícita en la columna de entrada.|  
|0xC0049066|-1073442714|DTS_E_EXPREVALSTATIC_FAILEDTOCONVERTSTRCOLUMNTOWSTR|Error al convertir una columna de entrada del tipo DT_STR al tipo DT_WSTR. Error al realizar la conversión implícita en la columna de entrada.|  
|0xC0049067|-1073442713|DTS_E_EXPREVALSTATIC_FUNCTIONCOMPUTEFAILED|Error al evaluar la función.|  
|0xC0049068|-1073442712|DTS_E_EXPREVALSTATIC_FUNCTIONCONVERTPARAMTOMEMBERFAILED|Un parámetro de función no puede convertirse a un valor estático. El parámetro debe ser estático y no puede contener elementos dinámicos como columnas de entrada.|  
|0xC0049088|-1073442680|DTS_E_EXPREVALSTATIC_FNRIGHTINVALIDLENGTH|Parámetro de longitud no válido para la función RIGHT. El parámetro de longitud no puede ser negativo.|  
|0xC0049089|-1073442679|DTS_E_EXPREVALSTATIC_FNREPLICATEINVALIDREPEATCOUNT|Parámetro de recuento de repeticiones no válido para la función REPLICATE. Este parámetro no puede ser negativo.|  
|0xC0049096|-1073442666|DTS_E_EXPREVALSTATIC_BINARYOPERATORCODEPAGEMISMATCH|Las páginas de códigos no coinciden en una operación binaria. La página de códigos del operando izquierdo no coincide con la página de códigos del operando derecho. Esta operación binaria debe tener las mismas páginas de códigos.|  
|0xC0049097|-1073442665|DTS_E_EXPREVALSTATIC_VARIABLECOMPUTEFAILED|Error al recuperar el valor de una variable.|  
|0xC0049098|-1073442664|DTS_E_EXPREVALSTATIC_VARIABLETYPENOTSUPPORTED|La expresión contiene una variable con un tipo de datos no compatible.|  
|0xC004909B|-1073442661|DTS_E_EXPREVALSTATIC_CASTCODEPAGEMISMATCH|No se puede convertir la expresión porque la página de códigos del valor que se convierte no coincide con la página de códigos de resultado solicitada. La página de códigos del origen debe coincidir con la página de códigos solicitada para el destino.|  
|0xC004909C|-1073442660|DTS_E_EXPREVALSTATIC_INVALIDTOKENSINGLEQUOTE|La expresión contiene una comilla sencilla inesperada. Es posible que se necesiten comillas dobles.|  
|0xC004909D|-1073442659|DTS_E_EXPREVALSTATIC_INVALIDTOKENSINGLEEQUAL|La expresión contiene un signo igual (=) inesperado. Este error suele producirse si se necesita un signo igual doble (==).|  
|0xC00490AA|-1073442646|DTS_E_EXPREVALSTATIC_AMBIGUOUSINPUTCOLUMNNAME|Se especificó un nombre de columna de entrada ambiguo.  La columna debe calificarse como [Nombre de componente].[Nombre de columna] o debe hacerse referencia a ella mediante el id. de linaje. Este error se produce si la columna de entrada existe en más de un componente y debe diferenciarse agregando el nombre del componente o utilizando el id. de linaje.|  
|0xC00490AB|-1073442645|DTS_E_EXPREVALSTATIC_PLACEHOLDERINEXPRESSION|Se encontró un operando o parámetro de función de marcador de posición en una expresión. Debe sustituirse por un parámetro u operando real.|  
|0xC00490AC|-1073442644|DTS_E_EXPREVALSTATIC_AMBIGUOUSVARIABLENNAME|Se especificó un nombre de variable ambiguo. El nombre de variable debe calificarse como \@[Namespace::Variable]. Este error se produce si la variable existe en más de un espacio de nombres.|  
|0xC00490D3|-1073442605|DTS_E_EXPREVALSTATIC_BINARYOPDTSTRNOTSUPPORTED|En los operandos de las operaciones binarias, el tipo de datos DT_STR solamente se admite para las columnas de entrada y operaciones de conversión. Un operando DT_STR que no sea una columna de entrada o el resultado de una conversión no puede utilizarse con una operación binaria. Para realizar esta operación, debe convertirse explícitamente el operando mediante un operador de conversión.|  
|0xC00490D4|-1073442604|DTS_E_EXPREVALSTATIC_CONDITIONALOPDTSTRNOTSUPPORTED|En los operandos del operador condicional, el tipo de datos DT_STR solamente se admite para las columnas de entrada y operaciones de conversión. Un operando DT_STR que no sea una columna de entrada o el resultado de una conversión no puede utilizarse con la operación condicional. Para realizar esta operación, debe convertirse explícitamente el operando mediante un operador de conversión.|  
|0xC00490D5|-1073442603|DTS_E_EXPREVALSTATIC_FNFINDSTRINGINVALIDOCCURRENCECOUNT|El parámetro de recuento de coincidencias no es válido para la función FINDSTRING. Este parámetro debe ser mayor que cero.|  
|0xC00490DD|-1073442595|DTS_E_EXPREVALSTATIC_INVALIDDATEPARTNODE|El parámetro de parte de fecha especificado para una función de fecha no es válido. Los parámetros de parte de fecha deben ser cadenas estáticas y no pueden contener elementos dinámicos, como columnas de entrada. Deben ser del tipo DT_WSTR.|  
|0xC00490DE|-1073442594|DTS_E_EXPREVALSTATIC_INVALIDCASTLENGTH|El valor especificado para el parámetro de longitud de una operación de conversión no es válido. La longitud debe ser positiva. La longitud especificada para la conversión de tipos es negativa. Sustituya el valor por uno positivo.|  
|0xC00490DF|-1073442593|DTS_E_EXPREVALSTATIC_INVALIDNULLLENGTH|El valor especificado para el parámetro de longitud de una función NULL no es válido. La longitud debe ser positiva. La longitud especificada para la función NULL es negativa. Sustituya el valor por uno positivo.|  
|0xC00490E0|-1073442592|DTS_E_EXPREVALSTATIC_INVALIDNULLCODEPAGE|El valor especificado para el parámetro de página de códigos de la función NULL con el tipo de datos DT_STR o DT_TEXT no es válido. La página de códigos especificada no está instalada en el equipo. Cambie la página de códigos especificada o instale la página de códigos en el equipo.|  
|0xC00490E1|-1073442591|DTS_E_EXPREVALSTATIC_INVALIDNULLPRECISION|El valor especificado para el parámetro de precisión de una función NULL no es válido. La precisión que se especificó está fuera del intervalo de la función NULL.|  
|0xC00490E2|-1073442590|DTS_E_EXPREVALSTATIC_INVALIDNULLSCALE|El valor especificado para el parámetro de escala de una función NULL no es válido. La escala que se especificó está fuera del intervalo de la función NULL. El valor de escala no debe superar al de precisión y debe ser positivo.|  
|0xC00490E8|-1073442584|DTS_E_XMLSRCERRORSETTINGERROROUTPUTCOLUMNDATA|Error de %1 al intentar escribir datos en %2 en %3. %4|  
|0xC00490F5|-1073442571|DTS_E_TXLOOKUP_CANCEL_REQUESTED|El usuario solicitó la cancelación de la transformación de búsquedas.|  
|0xC00490F6|-1073442570|DTS_E_LOBLENGTHLIMITEXCEEDED|El procesamiento de los datos de caracteres u objetos binarios grandes (LOB) se ha detenido porque se ha alcanzado el límite de 4 GB.|  
|0xC00490F7|-1073442569|DTS_E_CANNOTLOADCOMPONENT|No se pudo cargar el componente de canalización administrado "%1".  Excepción: %2.|  
|0xC00F9304|-1072721148|DTS_E_OLEDB_EXCEL_NOT_SUPPORTED|Código de error SSIS DTS_E_OLEDB_EXCEL_NOT_SUPPORTED: El Administrador de conexiones con Excel no es compatible con la versión de 64 bits de SSIS debido a que no hay ningún proveedor OLE DB disponible.|  
|0xC00F9310|-1072721136|DTS_E_CACHEBADHEADER|El archivo caché está dañado o no se creó mediante el administrador de conexiones de caché.  Proporcione un archivo caché válido.|  
|0xC0202001|-1071636479|DTS_E_MISSINGSQLCOMMAND|El comando SQL no se ha establecido correctamente. Compruebe la propiedad SQLCommand.|  
|0xC0202002|-1071636478|DTS_E_COMERROR|Información del objeto de error COM disponible.  Origen: "%1" Código de error: 0x%2!8.8X!  Descripción: "%3".|  
|0xC0202003|-1071636477|DTS_E_ACQUIREDCONNECTIONUNAVAILABLE|No se puede obtener acceso a las conexiones adquiridas.|  
|0xC0202004|-1071636476|DTS_E_INCORRECTCOLUMNCOUNT|El número de columnas es incorrecto.|  
|0xC0202005|-1071636475|DTS_E_COLUMNNOTFOUND|La columna "%1" no se encuentra en el origen de datos.|  
|0xC0202007|-1071636473|DTS_E_OLEDBRECORD|Hay un registro OLE DB disponible.  Origen: "%1" Hresult: 0x%2!8.8X!  Descripción: "%3".|  
|0xC0202009|-1071636471|DTS_E_OLEDBERROR|Código de error SSIS DTS_E_OLEDBERROR.  Error de OLE DB. Código de error: 0x%1!8.8X!.|  
|0xC020200A|-1071636470|DTS_E_ALREADYCONNECTED|El componente ya está conectado. Es necesario desconectar el componente antes de intentar conectarlo.|  
|0xC020200B|-1071636469|DTS_E_INCORRECTSTOCKPROPERTYVALUE|El valor de la propiedad "%1" no es correcto.|  
|0xC020200E|-1071636466|DTS_E_CANNOTOPENDATAFILE|No se puede abrir el archivo de datos "%1".|  
|0xC0202010|-1071636464|DTS_E_DESTINATIONFLATFILEREQUIRED|No se proporcionó ningún nombre de archivo plano de destino. Asegúrese de que el administrador de conexiones de archivos planos está configurado con una cadena sin conexión. Si el administrador de conexiones de archivos planos se utiliza en varios componentes, asegúrese de que la cadena de conexión contiene suficientes nombres de archivo.|  
|0xC0202011|-1071636463|DTS_E_TEXTQUALIFIERNOTFOUND|No se encuentra el calificador de texto de la columna "%1".|  
|0xC0202014|-1071636460|DTS_E_CANNOTCONVERTTYPES|No se admite la conversión de "%1" a "%2".|  
|0xC0202015|-1071636459|DTS_E_PROBLEMDETECTINGTYPECOMPATIBILITY|Se devolvió el código de error 0x%1!8.8X! al validar la conversión de tipos de %2 a %3.|  
|0xC0202016|-1071636458|DTS_E_CANNOTMAPINPUTCOLUMNTOOUTPUTCOLUMN|No se encuentra la columna de entrada con el id. de linaje "%1!d!" que necesita "%2". Compruebe la propiedad personalizada SourceInputColumnLineageID de la columna de salida.|  
|0xC0202017|-1071636457|DTS_E_INCORRECTMINIMUMNUMBEROFOUTPUTS|El número de salidas es incorrecto. Debe haber al menos %1!d! salidas.|  
|0xC0202018|-1071636456|DTS_E_INCORRECTEXACTNUMBEROFOUTPUTS|El número de salidas es incorrecto. Debe haber exactamente %1!d! salidas.|  
|0xC0202019|-1071636455|DTS_E_STRINGCONVERSIONTOOLONG|Una cadena era demasiado larga para convertirla.|  
|0xC020201A|-1071636454|DTS_E_INCORRECTEXACTNUMBEROFINPUTS|El número de entradas es incorrecto. Debe haber exactamente %1!d! entradas.|  
|0xC020201B|-1071636453|DTS_E_CANNOTHAVEZEROINPUTCOLUMNS|El número de columnas de entrada de %1 no puede ser cero.|  
|0xC020201C|-1071636452|DTS_E_CANNOTHAVEINPUTS|Este componente tiene %1!d! entradas.  No se permite ninguna entrada en este componente.|  
|0xC020201D|-1071636451|DTS_E_PROCESSINPUTCALLEDWITHINVALIDINPUTID|Se llamó a ProcessInput con un identificador de entrada de %1!d! no válido.|  
|0xC020201F|-1071636449|DTS_E_INCORRECTCUSTOMPROPERTYTYPE|La propiedad personalizada "%1" debe ser del tipo %2.|  
|0xC0202020|-1071636448|DTS_E_INVALIDBUFFERTYPE|El tipo de búfer no es válido. Asegúrese de que el diseño de canalización y todos los componentes pasen la validación.|  
|0xC0202021|-1071636447|DTS_E_INCORRECTCUSTOMPROPERTYVALUE|El valor de la propiedad personalizada "%1" no es correcto.|  
|0xC0202022|-1071636446|DTS_E_CONNECTIONREQUIREDFORMETADATA|Error por falta de conexión. Se requiere una conexión para solicitar metadatos. Si está trabajando sin conexión, desactive Trabajar sin conexión en el menú SSIS para habilitar la conexión.|  
|0xC0202023|-1071636445|DTS_E_CANTCREATECUSTOMPROPERTY|No se puede crear la propiedad personalizada "%1".|  
|0xC0202024|-1071636444|DTS_E_CANTGETCUSTOMPROPERTYCOLLECTION|No se puede recuperar la colección de propiedades personalizadas para inicializarse.|  
|0xC0202025|-1071636443|DTS_E_CANNOTCREATEACCESSOR|No se puede crear un descriptor de acceso de OLE DB. Compruebe si los metadatos de columna son válidos.|  
|0xC0202026|-1071636442|DTS_E_PRIMEOUTPUTCALLEDWITHINVALIDOUTPUTID|Se llamó a PrimeOutput con un id. de salida de %1!d! no válido.|  
|0xC0202027|-1071636441|DTS_E_INCORRECTSTOCKPROPERTY|El valor de la propiedad "%1" en "%2" no es válido.|  
|0xC0202028|-1071636440|DTS_E_CONNECTIONREQUIREDFORREAD|Se necesita una conexión para leer los datos.|  
|0xC020202C|-1071636436|DTS_E_ERRORWHILEREADINGHEADERROWS|Error al leer filas de encabezados.|  
|0xC020202D|-1071636435|DTS_E_DUPLICATECOLUMNNAME|Nombre de columna duplicado "%1".|  
|0xC0202030|-1071636432|DTS_E_CANNOTGETCOLUMNNAME|No se puede obtener el nombre de la columna con el id. %1!d!.|  
|0xC0202031|-1071636431|DTS_E_CANTDIRECTROW|Error al dirigir la fila a la salida "%1" (%2!d!).|  
|0xC020203A|-1071636422|DTS_E_CANNOTCREATEBULKINSERTHREAD|No se puede crear el subproceso de inserción masiva debido al error "%1".|  
|0xC020203B|-1071636421|DTS_E_BULKINSERTHREADINITIALIZATIONFAILED|El subproceso de la tarea Inserción masiva de SSIS no pudo inicializarse.|  
|0xC020203E|-1071636418|DTS_E_BULKINSERTTHREADALREADYRUNNING|El subproceso de la tarea Inserción masiva de SSIS ya se está ejecutando.|  
|0xC020203F|-1071636417|DTS_E_BULKINSERTTHREADABNORMALCOMPLETION|El subproceso de la tarea Inserción masiva de SSIS terminó con errores o advertencias.|  
|0xC0202040|-1071636416|DTS_E_CANNOTGETIROWSETFASTLOAD|Error al abrir el conjunto de filas de carga rápida de "%1". Compruebe que el objeto existe en la base de datos.|  
|0xC0202041|-1071636415|DTS_E_CONNECTREQUIREDFORMETADATAVALIDATION|Error por falta de conexión. Se necesita una conexión para proceder con la validación de metadatos.|  
|0xC0202042|-1071636414|DTS_E_DESTINATIONTABLENAMENOTPROVIDED|No se ha proporcionado un nombre de tabla de destino.|  
|0xC0202043|-1071636413|DTS_E_ICONVERTTYPEUNAVAILABLE|El proveedor OLE DB que utiliza el adaptador OLE DB no admite IConvertType. Establezca la propiedad ValidateColumnMetaData del adaptador en FALSE.|  
|0xC0202044|-1071636412|DTS_E_OLEDBPROVIDERDATATYPECONVERSIONUNSUPPORTED|El proveedor OLE DB que utiliza el adaptador OLE DB no puede realizar conversiones entre los tipos "%1" y "%2" de "%3".|  
|0xC0202045|-1071636411|DTS_E_VALIDATECOLUMNMETADATAFAILED|Error en la validación de metadatos de columna.|  
|0xC0202047|-1071636409|DTS_E_ATTEMPTINGTOINSERTINTOAROWIDCOLUMN|"%1" es una columna con id. de fila y no puede incluirse en una operación de inserción de datos.|  
|0xC0202048|-1071636408|DTS_E_ATTEMPTINGTOINSERTINTOAROWVERCOLUMN|Se intentó una inserción en la columna de versión de fila "%1". No se puede insertar en una columna de versión de fila.|  
|0xC0202049|-1071636407|DTS_E_ATTEMPTINGTOINSERTINTOAREADONLYCOLUMN|Error de inserción en la columna de solo lectura "%1".|  
|0xC020204A|-1071636406|DTS_E_UNABLETORETRIEVECOLUMNINFO|No se puede recuperar la información de columna del origen de datos. Asegúrese de que la tabla de destino de la base de datos está disponible.|  
|0xC020204B|-1071636405|DTS_E_CANTLOCKBUFFER|No se pudo bloquear un búfer. El sistema no tiene memoria suficiente o el administrador de búfer ha alcanzado su cuota.|  
|0xC020204C|-1071636404|DTS_E_INVALIDCOMPARISONFLAGS|%1 tiene una propiedad ComparisonFlags que incluye marcas adicionales con el valor %2!d!.|  
|0xC020204D|-1071636403|DTS_E_COLUMNMETADATAUNAVAILABLEFORVALIDATION|Metadatos de columna no disponibles para la validación.|  
|0xC0202053|-1071636397|DTS_E_CANNOTWRITETODATAFILE|No se puede escribir en el archivo de datos.|  
|0xC0202055|-1071636395|DTS_E_COLUMNDELIMITERNOTFOUND|No se encontró el delimitador de columnas de la columna "%1".|  
|0xC0202058|-1071636392|DTS_E_COLUMNPARSEFAILED|Error al analizar la columna "%1" en el archivo de datos.|  
|0xC020205A|-1071636390|DTS_E_RAWFILENAMEREQUIRED|No se ha establecido correctamente el nombre de archivo.  Proporcione la ruta de acceso y el nombre del archivo sin formato directamente en la propiedad FileName o bien especificando una variable en la propiedad FileNameVariable.|  
|0xC020205B|-1071636389|DTS_E_RAWFILECANTOPEN|No se puede abrir el archivo "%1" para escribir en él. El error puede producirse si no hay privilegios de archivo o si el disco está lleno.|  
|0xC020205C|-1071636388|DTS_E_RAWFILECANTBUFFER|No se puede crear un búfer de E/S para el archivo de salida. El error puede producirse si no hay privilegios de archivo o si el disco está lleno.|  
|0xC020205D|-1071636387|DTS_E_RAWCANTWRITE|No se pueden escribir %1!d! bytes en el archivo "%2". Consulte los mensajes de error anteriores para obtener detalles.|  
|0xC020205E|-1071636386|DTS_E_RAWBADHEADER|Se encontraron metadatos erróneos en el encabezado de archivo. El archivo está dañado o no es un archivo de datos sin procesar producidos por SSIS.|  
|0xC020205F|-1071636385|DTS_E_RAWEXISTSCREATEONCE|Se produjo un error porque el archivo de salida ya existe y la propiedad WriteOption está establecida en Crear una vez. Establezca la propiedad WriteOption en Crear siempre o elimine el archivo.|  
|0xC0202060|-1071636384|DTS_E_RAWCANTAPPENDTRUNCATE|Error por un conflicto en la configuración de propiedades. Las propiedades AllowAppend y ForceTruncate están establecidas en TRUE. Ambas propiedades no pueden establecerse en TRUE. Establezca una de las dos propiedades en FALSE.|  
|0xC0202061|-1071636383|DTS_E_RAWBADVERSION|La información de versión y de marcas del archivo era errónea. El archivo está dañado o no es un archivo de datos sin procesar producidos por SSIS.|  
|0xC0202062|-1071636382|DTS_E_RAWVERSIONINCOMPATIBLEAPPEND|El archivo de salida se escribió con una versión no compatible y no puede anexarse. Es posible que el archivo tenga un formato antiguo y ya no pueda utilizarse.|  
|0xC0202064|-1071636380|DTS_E_RAWMETADATAMISMATCH|No se puede anexar el archivo de salida porque ninguna columna del archivo existente coincide con la columna "%1" de la entrada. El archivo anterior no coincide en los metadatos.|  
|0xC0202065|-1071636379|DTS_E_RAWMETADATACOUNTMISMATCH|No se puede anexar el archivo de salida porque el número de columnas del archivo de salida no coincide con el número de columnas de este destino. El archivo anterior no coincide en los metadatos.|  
|0xC0202067|-1071636377|DTS_E_ERRORRETRIEVINGCOLUMNCODEPAGE|Error al recuperar la información de página de códigos de la columna.|  
|0xC0202068|-1071636376|DTS_E_RAWCANTREAD|No se pueden leer %1!d! bytes del archivo "%2". Debería haberse comunicado anteriormente la causa del error.|  
|0xC0202069|-1071636375|DTS_E_RAWUNEXPECTEDEOF|Se encontró un final de archivo inesperado al leer %1!d! bytes del archivo "%2". El archivo finalizó antes de tiempo porque el formato de archivo no era válido.|  
|0xC020206A|-1071636374|DTS_E_RAWNOLONGTYPES|No se puede usar la columna %1. Los adaptadores sin procesar no admiten datos de tipo image, text y ntext.|  
|0xC020206B|-1071636373|DTS_E_RAWUNEXPECTEDTYPE|El adaptador encontró un tipo de datos de %1!d! no reconocido. Podría deberse a un archivo de entrada dañado (origen) o a un tipo de búfer no válido (destino).|  
|0xC020206C|-1071636372|DTS_E_RAWSTRINGTOOLONG|Cadena demasiado larga. El adaptador leyó una cadena de %1!d! bytes y esperaba una cadena de %2!d! en el desplazamiento %3!d!. Podría deberse a un archivo de entrada dañado. El archivo muestra una longitud de cadena demasiado grande para la columna de búfer.|  
|0xC020206E|-1071636370|DTS_E_RAWSKIPFAILED|El adaptador sin formato intentó omitir %1!d! bytes en el archivo de entrada de la columna "%2" sin referencia, con el id. de linaje %3!d!, pero se produjo un error. El error devuelto por el sistema operativo debería haberse comunicado previamente.|  
|0xC020206F|-1071636369|DTS_E_RAWREADFAILED|El adaptador sin formato intentó leer %1!d! bytes en el archivo de entrada de la columna "%2" con el id. de linaje %3!d!, pero se produjo un error. El error devuelto por el sistema operativo debería haberse comunicado previamente.|  
|0xC0202070|-1071636368|DTS_E_RAWFILENAMEINVALID|La propiedad de nombre de archivo no es válida. El nombre de archivo es un dispositivo o contiene caracteres no válidos.|  
|0xC0202071|-1071636367|DTS_E_BULKINSERTAPIPREPARATIONFAILED|No se puede preparar la inserción masiva de SSIS para la inserción de datos.|  
|0xC0202072|-1071636366|DTS_E_INVALIDDATABASEOBJECTNAME|El nombre de objeto "%1" no es válido.|  
|0xC0202073|-1071636365|DTS_E_INVALIDORDERCLAUSE|Cláusula Order no válida.|  
|0xC0202074|-1071636364|DTS_E_RAWFILECANTOPENREAD|No se puede abrir el archivo "%1" para lectura. Puede producirse un error si no hay privilegios o si no se encuentra el archivo. La causa exacta se comunica en un mensaje de error anterior.|  
|0xC0202075|-1071636363|DTS_E_TIMEGENCANTCREATE|No se puede crear Microsoft.AnalysisServices.TimeDimGenerator.TimeDimGenerator.|  
|0xC0202076|-1071636362|DTS_E_TIMEGENCANTCONFIGURE|No se puede configurar Microsoft.AnalysisServices.TimeDimGenerator.|  
|0xC0202077|-1071636361|DTS_E_TIMEGENCANTCONVERT|Tipo de datos no compatible para la columna %1!d!.|  
|0xC0202079|-1071636359|DTS_E_TIMEGENCANTREAD|Error al intentar leer Microsoft.AnalysisServices.TimeDimGenerator. Código de error: 0x%1!8.8X!.|  
|0xC020207A|-1071636358|DTS_E_TIMEGENCANTREADCOLUMN|Error al tratar de leer los datos de la columna "%2!d!" de Microsoft.AnalysisServices.TimeDimGenerator. Código de error: 0x%2!8.8X!.|  
|0xC020207B|-1071636357|DTS_E_RSTDESTBADVARIABLENAME|No se ha establecido un nombre de variable válido en la propiedad VariableName. Debe escribirse un nombre de variable en tiempo de ejecución.|  
|0xC020207C|-1071636356|DTS_E_RSTDESTRSTCONFIGPROBLEM|No se puede crear o configurar el objeto ADODB.Recordset.|  
|0xC020207D|-1071636355|DTS_E_RSTDESTRSTWRITEPROBLEM|Error al escribir en el objeto ADODB.Recordset.|  
|0xC020207E|-1071636354|DTS_E_FILENAMEINVALID|El nombre de archivo no es válido. El nombre de archivo es un dispositivo o contiene caracteres no válidos.|  
|0xC020207F|-1071636353|DTS_E_FILENAMEINVALIDWITHPARAM|El nombre de archivo "%1" no es válido. El nombre de archivo es un dispositivo o contiene caracteres no válidos.|  
|0xC0202080|-1071636352|DTS_E_CMDDESTNOPARAMS|No se pueden recuperar las descripciones de columnas de destino de los parámetros del comando SQL.|  
|0xC0202081|-1071636351|DTS_E_CMDDESTNOTBOUND|Parámetros no enlazados. Todos los parámetros del comando SQL deben estar enlazados a columnas de entrada.|  
|0xC0202082|-1071636350|DTS_E_TXPIVOTBADUSAGE|El valor PivotUsage de la columna de entrada "%1" (%2!d!) no es válido.|  
|0xC0202083|-1071636349|DTS_E_TXPIVOTTOOMANYPIVOTKEYS|Se encontraron demasiadas claves dinámicas. Solo puede utilizarse una columna de entrada como clave dinámica.|  
|0xC0202084|-1071636348|DTS_E_TXPIVOTNOPIVOTKEY|No se encontró ninguna clave dinámica. Debe utilizarse una columna de entrada como clave dinámica.|  
|0xC0202085|-1071636347|DTS_E_TXPIVOTINPUTALREADYMAPPED|Se ha asignado más de una columna de salida (como "%1" (%2!d!)) a la columna de entrada "%3" (%4!d!).|  
|0xC0202086|-1071636346|DTS_E_TXPIVOTCANTMAPPIVOTKEY|La columna de salida "%1" (%2!d!) no puede asignarse a la columna de entrada PivotKey.|  
|0xC0202087|-1071636345|DTS_E_TXPIVOTCANTMAPPINGNOTFOUND|La columna de salida "%1" (%2!d!) tiene una SourceColumn %3!d! que no es un id. de linaje de columna de entrada válido.|  
|0xC0202088|-1071636344|DTS_E_TXPIVOTEMPTYPIVOTKEYVALUE|Se ha asignado la columna de salida "%1" (%2!d!) a una columna de entrada de valor dinamizado, pero falta el valor de su propiedad PivotKeyValue.|  
|0xC0202089|-1071636343|DTS_E_TXPIVOTDUPLICATEPIVOTKEYVALUE|Se ha asignado la columna de salida "%1" (%2!d!) a una columna de entrada de valor dinamizado con un valor de propiedad PivotKeyValue no único.|  
|0xC020208A|-1071636342|DTS_E_TXPIVOTOUTPUTNOTMAPPED|La columna de entrada "%1" (%2!d!) no se ha asignado a ninguna columna de salida.|  
|0xC020208B|-1071636341|DTS_E_TXPIVOTCANTCOMPARESETKEYS|Error al comparar los valores de las claves fijas.|  
|0xC020208D|-1071636339|DTS_E_TXPIVOTNOBLOB|La columna de entrada "%1" (%2!d!) no puede utilizarse como clave fija, clave dinámica ni valor dinámico porque contiene datos de tipo long.|  
|0xC020208E|-1071636338|DTS_E_TXPIVOTBADOUTPUTTYPE|Tipo de salida incorrecto. La columna de salida "%1" (%2!d!) debe tener el mismo tipo de datos y metadatos que la columna de entrada a la que está asignada.|  
|0xC020208F|-1071636337|DTS_E_TXPIVOTPROCESSERROR|Error al intentar dinamizar los registros de origen.|  
|0xC0202090|-1071636336|DTS_E_TXPIVOTBADPIVOTKEYVALUE|El valor de clave dinámica "%1" no es válido.|  
|0xC0202091|-1071636335|DTS_E_ERRORWHILESKIPPINGDATAROWS|Error al omitir filas de datos.|  
|0xC0202092|-1071636334|DTS_E_ERRORWHILEREADINGDATAROWS|Error al procesar el archivo "%1" en la fila de datos %2!I64d!.|  
|0xC0202093|-1071636333|DTS_E_FAILEDTOINITIALIZEFLATFILEPARSER|Error al inicializar al analizador de archivos planos.|  
|0xC0202094|-1071636332|DTS_E_UNABLETORETRIEVECOLUMNINFOFROMFLATFILECONNECTIONMANAGER|No se puede recuperar la información de columna del administrador de conexiones de archivos planos.|  
|0xC0202095|-1071636331|DTS_E_FAILEDTOWRITEOUTCOLUMNNAME|Error al escribir el nombre de la columna "%1".|  
|0xC0202096|-1071636330|DTS_E_INVALIDFLATFILECOLUMNTYPE|El tipo de la columna "%1" es incorrecto. Es del tipo "%2". Solo puede ser "%3" o "%4".|  
|0xC0202097|-1071636329|DTS_E_DISKIOBUFFEROVERFLOW|Error al intentar escribir datos de %1!d! bytes en la E/S de disco. El búfer de E/S de disco tiene %2!d! bytes libres.|  
|0xC0202098|-1071636328|DTS_E_FAILEDTOWRITEOUTHEADER|Error al escribir el encabezado de archivo.|  
|0xC0202099|-1071636327|DTS_E_FAILEDTOGETFILESIZE|Error al obtener el tamaño del archivo "%1".|  
|0xC020209A|-1071636326|DTS_E_FAILEDTOSETFILEPOINTER|Error al establecer el puntero de archivo para el archivo "%1".|  
|0xC020209B|-1071636325|DTS_E_UNABLETOSETUPDISKIOBUFFER|Error al establecer el búfer de E/S de disco.|  
|0xC020209C|-1071636324|DTS_E_COLUMNDATAOVERFLOWDISKIOBUFFER|Desbordamiento de los datos de la columna "%1" en el búfer de E/S de disco.|  
|0xC020209D|-1071636323|DTS_E_DISKIOFAILED|Error de E/S de disco inesperado al leer el archivo.|  
|0xC020209E|-1071636322|DTS_E_DISKIOTIMEDOUT|Se agotó el tiempo de espera de E/S de disco al leer el archivo.|  
|0xC020209F|-1071636321|DTS_E_INPUTSNOTREADONLY|No se puede leer el tipo de uso especificado para las columnas de entrada de esta transformación ni se puede escribir en él. Cambie el tipo de uso para que sea de solo lectura.|  
|0xC02020A0|-1071636320|DTS_E_CANNOTCOPYORCONVERTFLATFILEDATA|No se pueden copiar o convertir los datos de archivo plano de la columna "%1".|  
|0xC02020A1|-1071636319|DTS_E_FAILEDCOLUMNDATACONVERSIONSTATUS|Error en la conversión de datos. La conversión de datos en la columna "%1" devolvió el valor de estado %2!d! y el texto de estado "%3".|  
|0xC02020A2|-1071636318|DTS_E_VARIABLESCOLLECTIONUNAVAILABLE|La colección Variables no está disponible.|  
|0xC02020A3|-1071636317|DTS_E_TXUNPIVOTDUPLICATEPIVOTKEYVALUE|PivotKeyValue duplicado. Se ha asignado la columna de entrada "%1" (%2!d!) a una columna de salida de valor dinamizado que tiene un valor PivotKeyValue no único.|  
|0xC02020A4|-1071636316|DTS_E_TXUNPIVOTNOUNPIVOTDESTINATION|No se encontró ningún destino de anulación de dinamización. Debe asignarse al menos una columna de entrada con un PivotKeyValue a una DestinationColumn de la salida.|  
|0xC02020A5|-1071636315|DTS_E_TXUNPIVOTBADKEYLIST|PivotKeyValue no es válido. En una transformación UnPivot con más de una DestinationColumn de anulación de dinamización, los PivotKeyValues establecidos por cada destino deben coincidir exactamente.|  
|0xC02020A6|-1071636314|DTS_E_TXUNPIVOTBADUNPIVOTMETADATA|Metadatos UnPivot incorrectos. En una transformación UnPivot, todas las columnas de entrada con un PivotKeyValue establecido que apuntan a una misma DestinationColumn deben tener metadatos que coincidan exactamente con la DestinationColumn.|  
|0xC02020A7|-1071636313|DTS_E_TXPIVOTBADPIVOTKEYCONVERT|No se puede convertir el valor de clave dinámica "%1" al tipo de datos de la columna de clave dinámica.|  
|0xC02020A8|-1071636312|DTS_E_TXUNPIVOTTOOMANYPIVOTKEYS|Se han especificado demasiadas claves dinámicas. Solo puede utilizarse una columna de salida como clave dinámica.|  
|0xC02020A9|-1071636311|DTS_E_TXUNPIVOTUNMAPPEDOUTPUT|La columna de salida "%1" (%2!d!) no ha sido asignada por ninguna propiedad DestinationColumn de ninguna columna de entrada.|  
|0xC02020AA|-1071636310|DTS_E_TXUNPIVOTNOPIVOT|No se ha marcado ninguna columna de salida como PivotKey.|  
|0xC02020AB|-1071636309|DTS_E_TXUNPIVOTNOTINPUTMAP|El valor de la propiedad DestinationColumn de la columna de entrada "%1" (%2!d!) no hace referencia a un LineageID de columna de salida válido.|  
|0xC02020AC|-1071636308|DTS_E_TXUNPIVOTDUPLICATEDESTINATION|Error de destino duplicado. Se ha asignado más de una columna de entrada no dinamizada a una misma columna de salida de destino.|  
|0xC02020AD|-1071636307|DTS_E_TOTALINPUTCOLSCANNOTBEZERO|No se encontró ninguna columna de entrada. Debe asignarse al menos una columna de entrada a una columna de salida.|  
|0xC02020AE|-1071636306|DTS_E_TXMERGEJOINMUSTHAVESAMENUMBEROFINPUTANDOUTPUTCOLS|El número de columnas de entrada y de salida no es igual. El número total de columnas de entrada en todas las entradas debe ser el mismo que el número total de columnas de salida.|  
|0xC02020AF|-1071636305|DTS_E_INPUTMUSTBESORTED|La entrada no está ordenada. "%1" debe estar ordenada.|  
|0xC02020B0|-1071636304|DTS_E_TXMERGEJOININVALIDJOINTYPE|La propiedad personalizada JoinType de %1 contiene un valor de %2!ld!, que no es válido. Los valores válidos son 0 (completa), 1 (izquierda) o 2 (interna).|  
|0xC02020B1|-1071636303|DTS_E_TXMERGEJOININVALIDNUMKEYCOLS|El valor de NumKeyColumns no es válido. En %1, el valor de la propiedad personalizada NumKeyColumns debe estar entre 1 y %2!lu!.|  
|0xC02020B2|-1071636302|DTS_E_NOKEYCOLS|No se encuentra ninguna columna de clave. %1 debe tener al menos una columna con un valor de SortKeyPosition distinto de cero.|  
|0xC02020B3|-1071636301|DTS_E_TXMERGEJOINNOTENOUGHKEYCOLS|No hay suficientes columnas de clave. %1 debe tener al menos %2!ld! columnas con valores de SortKeyPosition distintos de cero.|  
|0xC02020B4|-1071636300|DTS_E_TXMERGEJOINDATATYPEMISMATCH|Los tipos de datos no coinciden. Los tipos de datos de las columnas con el valor %1!ld! de SortKeyPosition no coinciden.|  
|0xC02020B5|-1071636299|DTS_E_TXMERGEJOININVALIDSORTKEYPOS|La columna con el valor %1!ld! de SortKeyPosition no es válida. Debería ser %2!ld!.|  
|0xC02020B6|-1071636298|DTS_E_TXMERGEJOINSORTDIRECTIONMISMATCH|La dirección de ordenación no coincide. Las direcciones de ordenación de las columnas con el valor %1!ld! de SortKeyPosition no coinciden.|  
|0xC02020B7|-1071636297|DTS_E_TXMERGEJOINOUTPUTCOLMUSTHAVEASSOCIATEDINPUTCOL|Falta una columna. %1 debe tener una columna de entrada asociada.|  
|0xC02020B8|-1071636296|DTS_E_TXMERGEJOINREADONLYINPUTCOLSWITHNOOUTPUTCOL|Las columnas de entrada deben tener columnas de salida. Algunas columnas de entrada con un tipo de uso de solo lectura no tienen columnas de salida asociadas.|  
|0xC02020B9|-1071636295|DTS_E_TXMERGEJOINNONSTRINGCOMPARISONFLAGSNOTZERO|Marcas de comparación distintas de cero. Las marcas de comparación de las columnas que no son cadenas deben ser cero.|  
|0xC02020BA|-1071636294|DTS_E_TXMERGEJOINCOMPARISONFLAGSMISMATCH|Las marcas de comparación de las columnas con el valor %1!ld! de SortKeyPosition no coinciden.|  
|0xC02020BB|-1071636293|DTS_E_TXPIVOTBADPIVOTKEYVALUENOSTRING|Valor de clave dinámica desconocido.|  
|0xC02020BC|-1071636292|DTS_E_TXLINEAGEINVALIDLINEAGEITEM|El valor de elemento de linaje %1!ld! no es válida. El intervalo válido está entre %2!ld! y %3!ld!.|  
|0xC02020BD|-1071636291|DTS_E_CANNOTHAVEANYINPUTCOLUMNS|No se permiten columnas de entrada. El número de columnas de entrada debe ser cero.|  
|0xC02020BE|-1071636290|DTS_E_TXLINEAGEDATATYPEMISMATCH|El tipo de datos de "%1" no es válido para el elemento de linaje especificado.|  
|0xC02020BF|-1071636289|DTS_E_TXLINEAGEINVALIDLENGTH|La longitud de "%1" no es válida para el elemento de linaje especificado.|  
|0xC02020C1|-1071636287|DTS_E_METADATAMISMATCHWITHOUTPUTCOLUMN|Los metadatos de "%1" no coinciden con los metadatos de la columna de salida asociada.|  
|0xC02020C3|-1071636285|DTS_E_TXMERGESORTKEYPOSMISMATCH|Los valores de SortKeyPosition de algunas columnas de salida no coinciden con los valores de SortKeyPosition de las columnas de entrada asociadas.|  
|0xC02020C4|-1071636284|DTS_E_ADDROWTOBUFFERFAILED|Error al intentar agregar una fila al búfer de la tarea Flujo de datos. Código de error: 0x%1!8.8X!.|  
|0xC02020C5|-1071636283|DTS_E_DATACONVERSIONFAILED|Error en la conversión de datos al convertir la columna "%1" (%2!d!) a la columna "%3" (%4!d!).  La conversión devolvió el valor de estado %5!d! y el texto de estado "%6".|  
|0xC02020C6|-1071636282|DTS_E_FAILEDTOALLOCATEROWHANDLEBUFFER|Error al intentar asignar un búfer de identificador de fila. Código de error: 0x%1!8.8X!.|  
|0xC02020C7|-1071636281|DTS_E_FAILEDTOSENDROWTOSQLSERVER|Error al intentar enviar una fila a SQL Server. Código de error: 0x%1!8.8X!.|  
|0xC02020C8|-1071636280|DTS_E_FAILEDTOPREPAREBUFFERSTATUS|Error al intentar preparar el estado del búfer. Código de error: 0x%1!8.8X!.|  
|0xC02020C9|-1071636279|DTS_E_FAILEDTOBUFFERROWSTARTS|Error al intentar recuperar el inicio de la fila de búfer. Código de error: 0x%1!8.8X!.|  
|0xC02020CA|-1071636278|DTS_E_BULKINSERTTHREADTERMINATED|El subproceso de Inserción masiva de SSIS ya no se está ejecutando.  No se pueden insertar más filas. Intente aumentar el tiempo de espera del subproceso de inserción masiva.|  
|0xC02020CB|-1071636277|DTS_E_RAWTOOMANYCOLUMNS|El archivo de origen no es válido. El archivo de origen está devolviendo más de 131.072 columnas. Esto suele suceder si el archivo de origen no se crea por el destino de archivo sin formato.|  
|0xC02020CC|-1071636276|DTS_E_TXUNIONALL_EXTRADANGLINGINPUT|%1 es una entrada adicional no adjunta y se quitará.|  
|0xC02020CD|-1071636275|DTS_E_TXUNIONALL_NONDANGLINGUNATTACHEDINPUT|%1 no está adjunta pero no está marcada como pendiente.  Se marcará como pendiente.|  
|0xC02020CF|-1071636273|DTS_E_TXPIVOTRUNTIMEDUPLICATEPIVOTKEYVALUE|Valor de clave dinámica "%1" duplicado.|  
|0xC02020D0|-1071636272|DTS_E_TXPIVOTRUNTIMEDUPLICATEPIVOTKEYVALUENOSTRING|Valor de clave dinámica "__" duplicado.|  
|0xC02020D1|-1071636271|DTS_E_FAILEDTOGETCOMPONENTLOCALEID|Error al recuperar el id. de configuración regional del componente. Código de error: 0x%1!8.8X!.|  
|0xC02020D2|-1071636270|DTS_E_MISMATCHCOMPONENTCONNECTIONMANAGERLOCALEID|Los Id. de configuración regional no coinciden. El id. de configuración regional del componente (%1!d!) no coincide con el id. de configuración regional del administrador de conexiones (%2!d!).|  
|0xC02020D3|-1071636269|DTS_E_LOCALEIDNOTSET|No se ha establecido el Id. de configuración regional del componente. Los adaptadores de archivos planos deben tener establecido el Id. de configuración regional en el administrador de conexiones de archivos planos.|  
|0xC02020D4|-1071636268|DTS_E_RAWBYTESTOOLONG|El campo binario es demasiado grande. El adaptador intentó leer un campo binario de %1!d! bytes de longitud, pero esperaba un campo de %2!d! bytes como máximo en el desplazamiento %3!d!. Esto suele suceder si el archivo de entrada no es válido. El archivo contiene una longitud de cadena demasiado grande para la columna de búfer.|  
|0xC02020D5|-1071636267|DTS_E_TXSAMPLINGINVALIDPCT|El porcentaje %2!ld! no es válido para la propiedad "%1". Debe estar entre 1 y 100.|  
|0xC02020D6|-1071636266|DTS_E_TXSAMPLINGINVALIDROWS|El número de filas %2!ld! no es válido para la propiedad "%1". Debe ser mayor que 0.|  
|0xC02020D7|-1071636265|DTS_E_RAWSTRINGINPUTTOOLONG|Se pidió al adaptador que escribiera una cadena de %1!I64d! bytes de longitud, pero todos los datos deben tener menos de 4294967295 bytes de longitud.|  
|0xC02020D9|-1071636263|DTS_E_ATLEASTONEINPUTMUSTBEMAPPEDTOOUTPUT|No se asignó ninguna entrada a una salida. "%1" debe tener al menos una columna de entrada asignada a una columna de salida.|  
|0xC02020DB|-1071636261|DTS_E_CANNOTCONVERTDATATYPESWITHDIFFERENTCODEPAGES|La conversión de "%1" con página de códigos %2!d! en "%3" con página de códigos %4!d! no se admite.|  
|0xC02020DC|-1071636260|DTS_E_COLUMNNOTMAPPEDTOEXTERNALMETADATACOLUMN|La asignación de columna de metadatos externos a %1 no es válida.  El Id. de columna de metadatos externos no puede ser cero.|  
|0xC02020DD|-1071636259|DTS_E_COLUMNMAPPEDTONONEXISTENTEXTERNALMETADATACOLUMN|Se ha asignado %1 a una columna de metadatos externa que no existe.|  
|0xC02020E5|-1071636251|DTS_E_UNABLETOWRITELOBDATATOBUFFER|Error al escribir datos de objeto long de tipo DT_TEXT, DT_NTEXT o DT_IMAGE en el búfer de la tarea Flujo de datos para la columna "%1".|  
|0xC02020E8|-1071636248|DTS_E_CANNOTGETIROWSET|Error al abrir un conjunto de filas de "%1". Compruebe que el objeto existe en la base de datos.|  
|0xC02020E9|-1071636247|DTS_E_VARIABLEACCESSFAILED|Error al obtener acceso a la variable "%1". Código de error: 0x%1!8.8X!.|  
|0xC02020EA|-1071636246|DTS_E_CONNECTIONMANAGERNOTFOUND|No se encuentra el administrador de conexiones "%1". Uno de los componentes no pudo encontrar el administrador de conexiones en la colección Connections.|  
|0xC02020EB|-1071636245|DTS_E_VERSIONUPGRADEFAILED|Error al actualizar de la versión "%1" a la versión %2!d!.|  
|0xC02020EC|-1071636244|DTS_E_RSTDESTBIGBLOB|Un valor de una columna de entrada es demasiado grande para almacenarse en el objeto ADODB.Recordset.|  
|0xC02020ED|-1071636243|DTS_E_CANNOTCONVERTBETWEENUNICODEANDNONUNICODESTRINGCOLUMNS|Las columnas "%1" y "%2" no pueden realizar conversiones entre tipos de datos de cadena Unicode y no Unicode.|  
|0xC02020EE|-1071636242|DTS_E_ROWCOUNTBADVARIABLENAME|La variable "%1" especificada por la propiedad VariableName no es una variable válida. Es necesario un nombre de variable válida para escribir en ella.|  
|0xC02020EF|-1071636241|DTS_E_ROWCOUNTBADVARIABLETYPE|La variable "%1" especificada por la propiedad VariableName no es un entero. Cambie la variable por VT_I4, VT_UI4, VT_I8 o VT_UI8.|  
|0xC02020F0|-1071636240|DTS_E_NOCOLUMNADVANCETHROUGHFILE|No se especificó ninguna columna para permitir al componente avanzar por el archivo.|  
|0xC02020F1|-1071636239|DTS_E_MERGEJOINSORTEDOUTPUTHASNOSORTKEYPOSITIONS|La propiedad IsSorted de "%1" está establecida en TRUE, pero el valor de SortKeyPosition en todas las columnas de salida es cero. Cambie el valor de IsSorted por FALSE o seleccione al menos una columna de salida que contenga un valor de SortKeyPosition distinto de cero.|  
|0xC02020F2|-1071636238|DTS_E_METADATAMISMATCHWITHINPUTCOLUMN|Los metadatos de "%1" no coinciden con los metadatos de la columna de entrada.|  
|0xC02020F3|-1071636237|DTS_E_RSTDESTBADVARIABLE|El valor de la variable especificada no puede encontrarse, bloquearse ni establecerse.|  
|0xC02020F4|-1071636236|DTS_E_CANTPROCESSCOLUMNTYPECODEPAGE|No se puede procesar la columna "%1" porque se ha especificado más de una página de códigos (%2!d! y %3!d!) para ella.|  
|0xC02020F5|-1071636235|DTS_E_CANTINSERTCOLUMNTYPE|No se puede insertar la columna "%1" porque no se admite la conversión entre los tipos %2 y %3.|  
|0xC02020F6|-1071636234|DTS_E_CANNOTCONVERTBETWEENUNICODEANDNONUNICODESTRINGCOLUMN|No se puede convertir la columna "%1" entre los tipos de datos de cadena Unicode y no Unicode.|  
|0xC02020F8|-1071636232|DTS_E_COULDNOTFINDINPUTBUFFERCOLUMNBYLINEAGE|%1 no encuentra la columna con que tiene el LineageID %2!ld! en su búfer de entrada.|  
|0xC02020F9|-1071636231|DTS_E_COULDNOTGETCOLUMNINFOFORINPUTBUFFER|%1 no puede obtener información de la columna %2!lu! de su búfer de entrada.|  
|0xC02020FA|-1071636230|DTS_E_COULDNOTGETCOLUMNINFOFORCOPYBUFFER|%1 no puede obtener información de la columna "%2!lu!" de su búfer de copia.|  
|0xC02020FB|-1071636229|DTS_E_COULDNOTREGISTERCOPYBUFFER|%1 no puede registrar un tipo de búfer para su búfer de copia.|  
|0xC02020FC|-1071636228|DTS_E_COULDNOTCREATECOPYBUFFER|%1 no puede crear un búfer para copiar en él sus datos para ordenarlos.|  
|0xC02020FD|-1071636227|DTS_E_DATAREADERDESTREADFAILED|Error del cliente DataReader al llamar a Read o ha cerrado DataReader.|  
|0xC02020FE|-1071636226|DTS_E_NOSCHEMAINFOFOUND|El comando SQL no devolvió ninguna información de columna.|  
|0xC02020FF|-1071636225|DTS_E_GETSCHEMATABLEFAILED|%1 no pudo recuperar la información de columna del comando SQL. Se produjo el siguiente error: %2|  
|0xC0202100|-1071636224|DTS_E_SOURCETABLENAMENOTPROVIDED|No se ha proporcionado un nombre de tabla de origen.|  
|0xC0203110|-1071632112|DTS_E_CACHE_INVALID_INDEXPOS|La posición del índice de caché, %1!d!, no es válido. Para las columnas que no son de índice, la posición del índice debe ser 0. Para las columnas de índice, la posición del índice debe ser un número positivo consecutivo.|  
|0xC0203111|-1071632111|DTS_E_CACHE_DUPLICATE_INDEXPOS|La posición del índice, %1!d!, está duplicada. Para las columnas que no son de índice, la posición del índice debe ser 0. Para las columnas de índice, la posición del índice debe ser un número positivo consecutivo.|  
|0xC0203112|-1071632110|DTS_E_CACHE_TOO_FEW_INDEX_COLUMNS|Debe especificarse al menos una columna de índice para el administrador de conexiones de caché. Para especificar una columna de índice, establezca la propiedad Index Position de la columna de caché.|  
|0xC0203113|-1071632109|DTS_E_CACHE_INDEXPOS_NOT_CONTINUOUS|Las posiciones de índice de caché deben ser consecutivas. Para las columnas que no son de índice, la posición del índice debe ser 0. Para las columnas de índice, la posición del índice debe ser un número positivo consecutivo.|  
|0xC0204000|-1071628288|DTS_E_PROPERTYNOTSUPPORTED|No se puede establecer la propiedad "%1" en "%2". La propiedad establecida no se admite en el objeto especificado. Compruebe el nombre de la propiedad, el uso de mayúsculas y minúsculas y la ortografía.|  
|0xC0204002|-1071628286|DTS_E_CANTCHANGEPROPERTYTYPE|No se puede cambiar el tipo de propiedad que estableció el componente.|  
|0xC0204003|-1071628285|DTS_E_CANTADDOUTPUTID|Error al insertar el id. de salida %1!d!. No se creó la nueva salida.|  
|0xC0204004|-1071628284|DTS_E_CANTDELETEOUTPUTID|No se puede eliminar el id. de salida %1!d! de la colección de salida.  Es posible que el Id. no sea válido o que sea la salida predeterminada o una salida de error.|  
|0xC0204006|-1071628282|DTS_E_FAILEDTOSETPROPERTY|Error al establecer la propiedad "%1" en "%2".|  
|0xC0204007|-1071628281|DTS_E_FAILEDTOSETOUTPUTCOLUMNTYPE|Error al establecer el tipo de %1 en el tipo: "%2", longitud: %3!d!, precisión: %4!d!, escala: %5!d!, página de códigos: %6!d!.|  
|0xC0204008|-1071628280|DTS_E_MORETHANONEERROROUTPUTFOUND|Se encontró más de una salida de error en el componente y solamente puede haber una.|  
|0xC020400A|-1071628278|DTS_E_CANTSETOUTPUTCOLUMNPROPERTY|No se puede establecer la propiedad en una columna de salida.|  
|0xC020400B|-1071628277|DTS_E_CANTMODIFYERROROUTPUTCOLUMNDATATYPE|El tipo de datos de "%1" no puede modificarse en el error "%2".|  
|0xC020400E|-1071628274|DTS_E_CANONLYSETISSORTEDONSOURCE|La propiedad IsSorted de "%1" no puede tener el valor TRUE porque no es una salida de origen. Una salida de origen tiene el valor cero en SynchronousInputID.|  
|0xC020400F|-1071628273|DTS_E_CANONLYSETSORTKEYONSOURCE|La propiedad SortKeyPosition de "%1" no puede ser distinta de cero porque "%2" no es una salida de origen. La columna de salida "colname" (identificador) no puede tener un valor distinto de cero en la propiedad SortKeyPosition porque su "outputname" (identificador) de salida no es una salida de origen.|  
|0xC0204010|-1071628272|DTS_E_CANONLYSETCOMPFLAGSONSOURCE|El valor de la propiedad ComparisonFlags de "%1" no puede ser distinto de cero porque "%2" es una salida de origen. La columna de salida "colname" (identificador) no puede tener un valor distinto de cero en la propiedad ComparisonFlags porque su "outputname" (identificador) de salida no es una salida de origen.|  
|0xC0204011|-1071628271|DTS_E_NONSTRINGCOMPARISONFLAGSNOTZERO|Las marcas de comparación de "%1" deben ser cero porque no son de tipo cadena. El valor de ComparisonFlags solo puede ser distinto de cero en las columnas de tipo cadena.|  
|0xC0204012|-1071628270|DTS_E_COMPFLAGSONLYONSORTCOL|El valor de la propiedad ComparisonFlags de "%1" no puede ser distinto de cero porque SortKeyPosition tiene el valor cero. El valor de ComparisonFlags de una columna de salida solo puede ser distinto de cero si el valor de SortKeyPosition también es distinto de cero.|  
|0xC0204013|-1071628269|DTS_E_READONLYSTOCKPROPERTY|La propiedad es de solo lectura.|  
|0xC0204014|-1071628268|DTS_E_INVALIDDATATYPE|%1 tenía establecido un valor de tipo de datos no válido (%2!ld!).|  
|0xC0204015|-1071628267|DTS_E_CODEPAGEREQUIRED|"%1" requiere el establecimiento de una página de códigos pero el valor pasado es cero.|  
|0xC0204016|-1071628266|DTS_E_INVALIDSTRINGLENGTH|La longitud de "%1" no es válida. La longitud debe estar entre %2!ld! y %3!ld!.|  
|0xC0204017|-1071628265|DTS_E_INVALIDSCALE|La escala de "%1" no es válida. La escala debe estar entre %2!ld! y %3!ld!.|  
|0xC0204018|-1071628264|DTS_E_INVALIDPRECISION|La precisión de "%1" no es válida. La precisión debe estar entre %2!ld! y %3!ld!.|  
|0xC0204019|-1071628263|DTS_E_PROPVALUEIGNORED|Uno de los valores de longitud, precisión, escala o página de códigos de "%1" es distinto de cero, pero el tipo de datos requiere que el valor sea cero.|  
|0xC020401A|-1071628262|DTS_E_CANTSETOUTPUTCOLUMNDATATYPEPROPERTIES|%1 no permite establecer propiedades de tipos de datos de columnas de salida.|  
|0xC020401B|-1071628261|DTS_E_INVALIDDATATYPEFORERRORCOLUMNS|"%1" contiene un tipo de datos no válido. "%1" es una columna de error especial y el único tipo de datos válido es DT_I4.|  
|0xC020401C|-1071628260|DTS_E_NOERRORDESCFORCOMPONENT|El componente no suministra descripciones de códigos de error.|  
|0xC020401D|-1071628259|DTS_E_UNRECOGNIZEDERRORCODE|El código de error especificado no está asociado a este componente.|  
|0xC020401F|-1071628257|DTS_E_TRUNCATIONTRIGGEREDREDIRECTION|Un truncamiento provocó el redireccionamiento de una fila a partir de la configuración de disposición de truncamiento.|  
|0xC0204020|-1071628256|DTS_E_CANTSETUSAGETYPETOREADWRITE|"%1" no puede convertir la columna con id. de linaje %2!d! en columna de lectura/escritura porque ese tipo de uso no se permite en esta columna. Se intentó cambiar el tipo de uso de una columna de entrada por el tipo UT_READWRITE, que no se admite en este componente.|  
|0xC0204023|-1071628253|DTS_E_CANTSETUSAGETYPE|%1 ha prohibido el uso solicitado para la columna de entrada con id. de linaje %2!d!.|  
|0xC0204024|-1071628252|DTS_E_FAILEDTOSETUSAGETYPE|"%1" no pudo realizar el cambio solicitado en la columna de entrada con id. de linaje %2!d!. Error en la solicitud. Código de error: 0x%3!8.8X!. El error especificado se produjo al intentar establecer el tipo de uso de una columna de entrada.|  
|0xC0204025|-1071628251|DTS_E_FAILEDTOSETOUTPUTCOLUMNDATATYPEPROPERTIES|Error al intentar establecer las propiedades de tipo de datos en "%1". Código de error: 0x%2!8.8X!. El error se produjo al intentar establecer una o varias propiedades de tipo de datos de la columna de salida.|  
|0xC0204026|-1071628250|DTS_E_UNABLETORETRIEVEMETADATA|No se pueden recuperar los metadatos de "%1". Asegúrese de que el nombre de objeto es correcto y de que el objeto existe.|  
|0xC0204027|-1071628249|DTS_E_CANNOTMAPOUTPUTCOLUMN|No se puede asignar la columna de salida a una columna de metadatos externos.|  
|0xC0204028|-1071628248|DTS_E_UNSUPPORTEDVARIABLETYPE|La variable %1 debe ser de tipo "%2".|  
|0xC020402A|-1071628246|DTS_E_CANTSETEXTERNALMETADATACOLUMNDATATYPEPROPERTIES|%1 no permite establecer propiedades de tipos de datos de columnas de metadatos externas.|  
|0xC020402B|-1071628245|DTS_E_IDNOTINPUTNOROUTPUT|El id. %1!lu! no es un id. de entrada ni un id. de salida. El id. especificado debe ser el id. de entrada o el id. de salida asociado a la recopilación de metadatos externos.|  
|0xC020402C|-1071628244|DTS_E_METADATACOLLECTIONNOTUSED|La recopilación de metadatos externos en "%1" está marcada como no utilizada, de modo que no puede realizarse en ella ninguna operación.|  
|0xC020402D|-1071628243|DTS_E_NOBUFFERTYPEONSYNCOUTPUT|%1 es una salida sincrónica y el tipo de búfer no se puede recuperar para una salida sincrónica.|  
|0xC0207000|-1071616000|DTS_E_INPUTCOLUMNUSAGETYPENOTREADONLY|La columna de entrada "%1" debe ser de solo lectura. El tipo de uso de la columna de entrada no es de solo lectura, lo cual no se permite.|  
|0xC0207001|-1071615999|DTS_E_MISSINGCUSTOMPROPERTY|Falta la propiedad "%1" requerida en "%2". El objeto debe tener la propiedad personalizada especificada.|  
|0xC0207002|-1071615998|DTS_E_ILLEGALCUSTOMOUTPUTPROPERTY|La salida %1 no puede tener la propiedad "%2", pero actualmente tiene asignada dicha propiedad.|  
|0xC0207003|-1071615997|DTS_E_INVALIDOUTPUTEXCLUSIONGROUP|%1 debe estar en el grupo de exclusión %2!d!. Todas las salidas deben estar en el grupo de exclusión especificado.|  
|0xC0207004|-1071615996|DTS_E_PROPERTYISEMPTY|La propiedad "%1" está vacía. Esta propiedad no puede estar vacía.|  
|0xC0207005|-1071615995|DTS_E_CREATEEXPRESSIONOBJECTFAILED|No se puede asignar memoria para la expresión "%1". Error de memoria insuficiente al crear un objeto interno para que contenga la expresión.|  
|0xC0207006|-1071615994|DTS_E_EXPRESSIONPARSEFAILED|No se puede analizar la expresión "%1". Expresión no válida o error de memoria insuficiente.|  
|0xC0207007|-1071615993|DTS_E_EXPRESSIONCOMPUTEFAILED|Error al calcular la expresión "%1". Código de error: 0x%2!8.8X!. Es posible que la expresión tenga errores, como la división por cero, que no puedan detectarse durante el análisis o puede haber un error de memoria insuficiente.|  
|0xC0207008|-1071615992|DTS_E_FAILEDTOCREATEEXPRESSIONARRAY|No se puede asignar memoria para los objetos Expression. Error de memoria insuficiente al crear la matriz de punteros del objeto Expression.|  
|0xC020700A|-1071615990|DTS_E_FAILEDTOCREATEEXPRESSIONMANANGER|Error de %1 al crear el administrador de expresiones. Código de error: 0x%2!8.8X!.|  
|0xC020700B|-1071615989|DTS_E_SPLITEXPRESSIONNOTBOOLEAN|La expresión "%1" no es booleana. El tipo de resultado de la expresión debe ser booleano.|  
|0xC020700C|-1071615988|DTS_E_EXPRESSIONVALIDATIONFAILED|La expresión "%1" de "%2" no es válida.|  
|0xC020700E|-1071615986|DTS_E_COLUMNNOTMATCHED|No puede establecerse una coincidencia entre la columna "%1" (%2!d!) y ninguna columna de archivo de entrada. El nombre de columna de salida o el nombre de columna de entrada no se encuentran en el archivo.|  
|0xC020700F|-1071615985|DTS_E_SETRESULTCOLUMNFAILED|Error al intentar establecer la columna de resultados de la expresión "%1" en %2. Código de error: 0x%3!8.8X!. No se puede determinar la columna de entrada o de salida que debía recibir el resultado de la expresión o no se puede convertir el resultado de la expresión al tipo de columna.|  
|0xC0207011|-1071615983|DTS_E_FAILEDTOGETLOCALEIDFROMPACKAGE|%1 no pudo obtener el id. de configuración regional del paquete.|  
|0xC0207012|-1071615982|DTS_E_INCORRECTPARAMETERMAPPINGFORMAT|La cadena de asignación de parámetros no tiene el formato correcto.|  
|0xC0207013|-1071615981|DTS_E_NOTENOUGHPARAMETERSPROVIDED|El comando SQL requiere %1!d! parámetros pero la asignación de parámetros solo tiene %2!d! parámetros.|  
|0xC0207014|-1071615980|DTS_E_PARAMETERNOTFOUNDINMAPPING|El comando SQL requiere un parámetro llamado "%1", que no se encuentra en la asignación de parámetros.|  
|0xC0207015|-1071615979|DTS_E_DUPLICATEDATASOURCECOLUMNNAME|Hay más de una columna de origen de datos con el nombre "%1".  Los nombres de columnas de origen de datos deben ser únicos.|  
|0xC0207016|-1071615978|DTS_E_DATASOURCECOLUMNWITHNONAMEFOUND|Una de las columnas de origen de datos no tiene nombre.  Todas las columnas de origen de datos deben tener un nombre.|  
|0xC0208001|-1071611903|DTS_E_DISCONNECTEDCOMPONENT|Hay un componente desconectado del diseño.|  
|0xC0208002|-1071611902|DTS_E_INVALIDCOMPONENTID|El Id. del componente de diseño no es válido.|  
|0xC0208003|-1071611901|DTS_E_INVALIDINPUTCOUNT|Uno de los componentes tiene un número no válido de entradas.|  
|0xC0208004|-1071611900|DTS_E_INVALIDOUTPUTCOUNT|Uno de los componentes tiene un número no válido de salidas.|  
|0xC0208005|-1071611899|DTS_E_NOINPUTSOROUTPUTS|Uno de los componentes no tiene entradas ni salidas.|  
|0xC0208007|-1071611897|DTS_E_CANTALLOCATECOLUMNINFO|No había memoria suficiente para asignar una lista a las columnas manipuladas por este componente.|  
|0xC0208008|-1071611896|DTS_E_OUTPUTCOLUMNNOTININPUT|La columna de salida "%1" (%2!d!) hace referencia a la columna de entrada con el id. de linaje %3!d!, pero no se encontró ninguna entrada con dicho id. de linaje.|  
|0xC0208009|-1071611895|DTS_E_SORTNEEDSONEKEY|Al menos una columna de entrada debe estar marcada como criterio de ordenación, pero no se encontraron criterios.|  
|0xC020800A|-1071611894|DTS_E_SORTDUPLICATEKEYWEIGHT|Tanto la columna "%1" (%2!d!) como la columna "%3" (%4!d!) se marcaron con el criterio de ordenación de peso %5!d!.|  
|0xC020800D|-1071611891|DTS_E_CANTMODIFYINVALID|El componente no puede realizar el cambio de metadatos solicitado hasta que se solucione el problema de validación.|  
|0xC020800E|-1071611890|DTS_E_CANTADDINPUT|No se puede agregar una entrada a la colección de entradas.|  
|0xC020800F|-1071611889|DTS_E_CANTADDOUTPUT|No se puede agregar una salida a la colección de salidas.|  
|0xC0208010|-1071611888|DTS_E_CANTDELETEINPUT|No se puede quitar una entrada de la colección de entradas.|  
|0xC0208011|-1071611887|DTS_E_CANTDELETEOUTPUT|No se puede quitar una salida de la colección de salidas.|  
|0xC0208014|-1071611884|DTS_E_CANTCHANGEUSAGETYPE|No se puede cambiar el tipo de uso de la columna.|  
|0xC0208016|-1071611882|DTS_E_INVALIDUSAGETYPEFORCUSTOMPROPERTY|%1 debe ser de lectura/escritura para tener la propiedad personalizada "%2". La columna de entrada o de salida tiene la propiedad personalizada especificada pero no es de lectura/escritura. Quite la propiedad o convierta la columna en columna de lectura/escritura.|  
|0xC0208017|-1071611881|DTS_E_READWRITECOLUMNMISSINGREQUIREDCUSTOMPROPERTY|%1 es de lectura/escritura y debe tener la propiedad personalizada "%2". Agregue la propiedad o quite el atributo de lectura/escritura de la columna.|  
|0xC0208018|-1071611880|DTS_E_CANTDELETECOLUMN|No se puede eliminar la columna. El componente no permite la eliminación de columnas de esta entrada o salida.|  
|0xC0208019|-1071611879|DTS_E_CANTADDCOLUMN|El componente no permite la adición de columnas a esta entrada o salida.|  
|0xC020801A|-1071611878|DTS_E_CANNOTTFINDRUNTIMECONNECTIONOBJECT|No se encuentra la conexión "%1". Compruebe si el administrador de conexiones tiene una conexión con dicho nombre.|  
|0xC020801B|-1071611877|DTS_E_CANNOTFINDRUNTIMECONNECTIONMANAGER|No se encuentra el administrador de conexiones en tiempo de ejecución con el id. "%1". Compruebe si la colección de administradores de conexión tiene un administrador de conexiones con dicho Id.|  
|0xC020801C|-1071611876|DTS_E_CANNOTACQUIRECONNECTIONFROMCONNECTIONMANAGER|Código de error SSIS DTS_E_CANNOTACQUIRECONNECTIONFROMCONNECTIONMANAGER.  Error de la llamada del método AcquireConnection al administrador de conexiones "%1". Código de error: 0x%2!8.8X!.  Puede que haya otros mensajes de error expuestos anteriores a éste con más información sobre el motivo del error del método AcquireConnection.|  
|0xC020801D|-1071611875|DTS_E_ACQUIREDCONNECTIONISINVALID|La conexión adquirida del administrador de conexiones "%1" no es válida.|  
|0xC020801E|-1071611874|DTS_E_INCORRECTCONNECTIONMANAGERTYPE|El administrador de conexiones "%1" es de un tipo incorrecto.  El tipo requerido es "%2". El tipo disponible para el componente es "%3".|  
|0xC020801F|-1071611873|DTS_E_CANNOTACQUIREMANAGEDCONNECTIONFROMCONNECTIONMANAGER|No se puede adquirir una conexión administrada del administrador de conexiones en tiempo de ejecución.|  
|0xC0208020|-1071611872|DTS_E_CANTINITINPUT|No se puede crear una entrada para inicializar la colección de entradas.|  
|0xC0208021|-1071611871|DTS_E_CANTINITOUTPUT|No se puede crear una salida para inicializar la colección de salidas.|  
|0xC0208023|-1071611869|DTS_E_EXTRACTORCANTWRITE|Error al escribir en el archivo "%1". Código de error: 0x%2!8.8X!.|  
|0xC0208024|-1071611868|DTS_E_INCORRECTCONNECTIONOBJECTTYPE|El administrador de conexiones "%1" devolvió un objeto de un tipo incorrecto desde el método AcquireConnection.|  
|0xC0208025|-1071611867|DTS_E_INPUTCOLPROPERTYNOTFOUND|Se requiere la propiedad "%3" en la columna de entrada "%1" (%2!d!), pero no se encuentra. Debe agregarse la propiedad que falta.|  
|0xC0208026|-1071611866|DTS_E_EXTRACTORUNREFERENCED|"%1" se ha marcado como de solo lectura pero no se hace referencia a ella desde ninguna otra columna. No se permiten las columnas sin referencia.|  
|0xC0208027|-1071611865|DTS_E_EXTRACTORREFERENCEDCOLUMNNOTFOUND|"%1" hace referencia al id. de columna %2!d! y no se encuentra dicha columna en la entrada. Hay una referencia que apunta a una columna que no existe.|  
|0xC0208028|-1071611864|DTS_E_EXTRACTORDATACOLUMNNOTBLOB|"%1" hace referencia a "%2" y dicha columna no es de tipo BLOB.|  
|0xC0208029|-1071611863|DTS_E_INSERTERREFERENCEDCOLUMNNOTFOUND|"%1" hace referencia al id. de columna de salida %2!d! y no se encuentra dicha columna en la salida.|  
|0xC020802A|-1071611862|DTS_E_INSERTERCANTREAD|Error al leer del archivo "%1". Código de error: 0x%2!8.8X!.|  
|0xC020802B|-1071611861|DTS_E_TXSCD_NOTYPEDCOLUMNSATINPUT|Debe haber al menos una columna de tipo Fixed, Changing o Historical en la entrada de una transformación Dimensión de variación lenta. Compruebe que al menos una de las columnas es FixedAttribute, ChangingAttribute o HistoricalAttribute.|  
|0xC020802C|-1071611860|DTS_E_TXSCD_INVALIDINPUTCOLUMNTYPE|La propiedad ColumnType de "%1" no es válida. El valor actual está fuera del intervalo de valores aceptables.|  
|0xC020802D|-1071611859|DTS_E_TXSCD_CANNOTMAPDIFFERENTTYPES|No se puede asignar la columna de entrada "%1" a la columna externa "%2" porque tienen tipos de datos distintos. La transformación Dimensión de variación lenta no permite la asignación entre columnas de distintos tipos, excepto DT_STR y DT_WSTR.|  
|0xC020802E|-1071611858|DTS_E_NTEXTDATATYPENOTSUPPORTEDWITHANSIFILES|El tipo de datos de "%1" es DT_NTEXT, que no es compatible con archivos ANSI. Utilice DT_TEXT en su lugar y convierta los datos a DT_NTEXT mediante el componente de conversión de datos.|  
|0xC020802F|-1071611857|DTS_E_TEXTDATATYPENOTSUPPORTEDWITHUNICODEFILES|El tipo de datos de "%1" es DT_NTEXT, que no es compatible con archivos Unicode. Utilice DT_NTEXT en su lugar y convierta los datos a DT_TEXT mediante el componente de conversión de datos.|  
|0xC0208030|-1071611856|DTS_E_IMAGEDATATYPENOTSUPPORTED|El tipo de datos de "%1" es DT_IMAGE, que no es compatible. Utilice DT_TEXT o DT_NTEXT en su lugar y convierta los datos DT_IMAGE mediante el componente de conversión de datos.|  
|0xC0208031|-1071611855|DTS_E_FLATFILEFORMATNOTSUPPORTED|El formato "%1" no es compatible con el administrador de conexiones de archivos planos. Los formatos compatibles son Delimited, FixedWidth, RaggedRight y Mixed.|  
|0xC0208032|-1071611854|DTS_E_EXTRACTORFILENAMECOLUMNNOTSTRING|"%1" debería contener un nombre de archivo, pero no es de tipo cadena.|  
|0xC0208033|-1071611853|DTS_E_EXTRACTORCANTAPPENDTRUNCATE|Error por un conflicto en la configuración de propiedades. Las propiedades AllowAppend y ForceTruncate de "%1" están establecidas en TRUE. Ambas propiedades no pueden establecerse en TRUE. Establezca una de las dos propiedades en FALSE.|  
|0xC0208034|-1071611852|DTS_E_EXTRACTORCOLUMNALREADYREFERENCED|%1 hace referencia al id. de columna %2!d!, pero %3 ya hace referencia a dicha columna. Quite una de las dos referencias a la columna.|  
|0xC0208035|-1071611851|DTS_E_CONNECTIONMANANGERNOTASSIGNED|No se ha asignado un administrador de conexiones a %1.|  
|0xC0208036|-1071611850|DTS_E_INSERTERCOLUMNALREADYREFERENCED|%1 hace referencia a la columna de salida con el id. %2!d!, pero %3 ya hace referencia a dicha columna.|  
|0xC0208037|-1071611849|DTS_E_INSERTERCOLUMNNOTREFERENCED|Ninguna columna de entrada hace referencia a "%1". Exactamente una columna de entrada debe hacer referencia a cada columna de salida.|  
|0xC0208038|-1071611848|DTS_E_INSERTERDATACOLUMNNOTBLOB|"%1" hace referencia a "%2" y dicha columna no tiene el tipo correcto. Debe ser DT_TEXT, DT_NTEXT o DT_IMAGE. Hay una referencia que apunta a una columna que debe ser BLOB.|  
|0xC0208039|-1071611847|DTS_E_INSERTERFILENAMECOLUMNNOTSTRING|"%1" debería contener un nombre de archivo, pero no es de tipo cadena.|  
|0xC020803A|-1071611846|DTS_E_INSERTEREXPECTBOMINVALIDTYPE|El valor de la propiedad ExpectBOM de "%1" es TRUE para %2, pero la columna no es de tipo NT_NTEXT. ExpectBOM especifica que la transformación Importar columna espera una marca de orden de bytes (BOM). Establezca el valor False en la propiedad ExpectBOM o cambie el tipo de datos de columna de salida por DT_NTEXT.|  
|0xC020803B|-1071611845|DTS_E_INSERTERINVALIDDATACOLUMNSETTYPE|Las columnas de salida de datos deben ser DT_TEXT, DT_NTEXT o DT_IMAGE. Solo puede establecerse un tipo BLOB en la columna de salida de datos.|  
|0xC020803C|-1071611844|DTS_E_TXSCD_FIXEDATTRIBUTECHANGE|Si el valor de la propiedad FailOnFixedAttributeChange es TRUE, se producirá un error en la transformación si se detecta un cambio de atributo fijo. Para enviar filas a la salida de atributos fijos, establezca el valor FALSE en la propiedad FailOnFixedAttributeChange.|  
|0xC020803D|-1071611843|DTS_E_TXSCD_LOOKUPFAILURE|La transformación de búsquedas no pudo recuperar ninguna fila. La transformación produce un error si se establece el valor TRUE en FailOnLookupFailure y no se recupera ninguna fila.|  
|0xC020803E|-1071611842|DTS_E_TXSCD_INVALIDNUMBERSOFPARAMETERS|Debe haber al menos un tipo de columna Key en la entrada de una transformación Dimensión de variación lenta. Establezca al menos un tipo de columna Key.|  
|0xC020803F|-1071611841|DTS_E_TXSCD_CANNOTFINDEXTERNALCOLUMN|No se encuentra la columna externa con el nombre "%1".|  
|0xC0208040|-1071611840|DTS_E_TXSCD_INFFEREDINDICATORNOTBOOL|La columna de indicador deducido "%1" debe ser de tipo DT_BOOL.|  
|0xC0208107|-1071611641|DTS_E_ERRORROWDISPMUSTBENOTUSED|%1 debe tener RD_NotUsed como valor de disposición de filas de error.|  
|0xC0208108|-1071611640|DTS_E_TRUNCROWDISPMUSTBENOTUSED|%1 debe tener RD_NotUsed como valor de disposición de filas de truncamiento.|  
|0xC0208201|-1071611391|DTS_E_TXAGG_INPUTNOTFOUNDFOROUTPUT|No se encuentra la columna de entrada con el id. de linaje %1!d! necesaria para la columna de salida con el id. de linaje %2!d!.|  
|0xC0208202|-1071611390|DTS_E_TXAGG_INVALIDOUTPUTDATATYPEFORAGGREGATE|Tipo de datos de salida no válido para el tipo de agregado especificado en el id. de columna de salida %1!d!.|  
|0xC0208203|-1071611389|DTS_E_TXAGG_INVALIDINPUTDATATYPEFORAGGREGATE|Se ha utilizado un tipo de datos de entrada no válido para %1 en el agregado especificado en %2.|  
|0xC0208204|-1071611388|DTS_E_TXAGG_INPUTOUTPUTDATATYPEMISMATCH|Los tipos de datos del id. de linaje de columna de entrada %1!d! y el id. de columna de salida %2!d! no coinciden.|  
|0xC0208205|-1071611387|DTS_E_UNABLETOGETINPUTBUFFERHANDLE|No se puede obtener el identificador de búfer de entrada para el id. de entrada %1!d!.|  
|0xC0208206|-1071611386|DTS_E_UNABLETOGETOUTPUTBUFFERHANDLE|No se puede obtener el identificador de búfer de salida para el id. de salida %1!d!.|  
|0xC0208207|-1071611385|DTS_E_UNABLETOFINDCOLUMNHANDLEINOUTPUTBUFFER|No se encuentra la columna con el id. de linaje %1!d! en el búfer de salida.|  
|0xC0208208|-1071611384|DTS_E_UNABLETOFINDCOLUMNHANDLEININPUTBUFFER|No se encuentra la columna con el id. de linaje %1!d! en el búfer de entrada.|  
|0xC0208209|-1071611383|DTS_E_CANNOTHAVEZEROOUTPUTCOLUMNS|El número de columnas de salida de %1 no puede ser cero.|  
|0xC020820A|-1071611382|DTS_E_CONNECTIONMANAGERCOLUMNCOUNTMISMATCH|El número de columnas del administrador de conexiones de archivos planos debe ser el mismo que el número de columnas del adaptador de archivos planos. El número de columnas del administrador de conexiones de archivos planos es %1!d!, mientras que el número de columnas del adaptador de archivos planos es %2!d!.|  
|0xC020820B|-1071611381|DTS_E_MISMATCHCONNECTIONMANAGERCOLUMN|No se encuentra la columna "%1" del índice %2!d! del administrador de conexiones de archivos planos en el índice %3!d! de la colección de columnas del adaptador de archivos planos.|  
|0xC020820D|-1071611379|DTS_E_EXTERNALMETADATACOLUMNISALREADYMAPPED|La columna de metadatos externos con id. %1!d! ya se ha asignado a %2.|  
|0xC020820E|-1071611378|DTS_E_TXAGG_STRING_TOO_LONG|La transformación encontró una columna de clave de más de %1!u! caracteres.|  
|0xC020820F|-1071611377|DTS_E_DERIVEDRESULT_TOO_LONG|La transformación encontró un valor de resultado de más de %1!u! bytes.|  
|0xC0208210|-1071611376|DTS_E_TXAGG_MEMALLOCERROUTPUTDESCRIPTORS|No se puede asignar memoria.|  
|0xC0208211|-1071611375|DTS_E_TXAGG_MEMALLOCERRWORKSPACEDESCRIPTORS|No se puede asignar memoria.|  
|0xC0208212|-1071611374|DTS_E_TXAGG_MEMALLOCERRSORTORDERDESCRIPTORS|No se puede asignar memoria.|  
|0xC0208213|-1071611373|DTS_E_TXAGG_MEMALLOCERRNUMERICDESCRIPTORS|No se puede asignar memoria.|  
|0xC0208214|-1071611372|DTS_E_TXAGG_MEMALLOCERRCOUNTDISTINCTDESCRIPTOR|No se puede asignar memoria.|  
|0xC0208215|-1071611371|DTS_E_TXAGG_MEMALLOCERRWORKSPACESORTORDERDESCRIPTORS|No se puede asignar memoria.|  
|0xC0208216|-1071611370|DTS_E_TXAGG_MEMALLOCERRWORKSPACENUMERICDESCRIPTORS|No se puede asignar memoria.|  
|0xC0208217|-1071611369|DTS_E_TXAGG_MEMALLOCERRWORKSPACEBUFFCOLS|No se puede asignar memoria.|  
|0xC0208218|-1071611368|DTS_E_UNREFERENCEDINPUTCOLUMN|No se hace referencia a la columna de entrada "%1".|  
|0xC0208219|-1071611367|DTS_E_CANTBUILDTHREADPOOL|La transformación Ordenar no pudo crear un grupo de subprocesos con %1!d! subprocesos. No hay suficiente memoria disponible.|  
|0xC020821A|-1071611366|DTS_E_QUEUEWORKITEMFAILED|La transformación Ordenar no puede poner un elemento de trabajo en la cola de su grupo de subprocesos. No hay memoria suficiente.|  
|0xC020821B|-1071611365|DTS_E_SORTTHREADSTOPPED|Se detuvo un subproceso de trabajo de la transformación Ordenar. Código de error: 0x%1!8.8X!. Se encontró un error grave al ordenar un búfer.|  
|0xC020821E|-1071611362|DTS_E_SORTBADTHREADCOUNT|El valor de MaxThreads era %1!ld! y debería estar entre 1 y %2!ld!, ambos incluidos, o ser -1 para usar como valor predeterminado el número de CPU.|  
|0xC020821F|-1071611361|DTS_E_DTPXMLLOADFAILURE|No se puede cargar desde XML.|  
|0xC0208220|-1071611360|DTS_E_DTPXMLSAVEFAILURE|No se puede guardar en XML.|  
|0xC0208221|-1071611359|DTS_E_DTPXMLINT32CONVERTERR|No se puede convertir el valor "%1" a un entero.|  
|0xC0208222|-1071611358|DTS_E_DTPXMLBOOLCONVERTERR|No se puede convertir el valor "%1" a un booleano.|  
|0xC0208223|-1071611357|DTS_E_DTPXMLPARSEERRORNEARID|Se encontró un error de carga cerca del objeto con el id. %1!d!.|  
|0xC0208226|-1071611354|DTS_E_DTPXMLPROPERTYTYPEERR|El valor "%1" no es válido para el atributo "%2".|  
|0xC0208228|-1071611352|DTS_E_DTPXMLSETUSAGETYPEERR|El valor "%1" no es válido para el atributo "%2".|  
|0xC0208229|-1071611351|DTS_E_DTPXMLDATATYPEERR|El valor "%1" no es válido para el atributo "%2".|  
|0xC020822A|-1071611350|DTS_E_UNMAPPEDINPUTCOLUMN|%1 no está asignado a una columna de salida.|  
|0xC020822B|-1071611349|DTS_E_INPUTCOLUMNBADMAP|%1 tiene una asignación no válida.  No existe una columna de salida con el id. %2!ld! en este componente.|  
|0xC020822D|-1071611347|DTS_E_MULTIPLYMAPPEDOUTCOL|Se ha asignado %1 a una columna de salida que ya tiene una asignación en esta entrada.|  
|0xC020822E|-1071611346|DTS_E_TXAGG_STRINGPROMOTIONFAILED|No se pudo convertir a DT_WSTR la columna de entrada con el id. de linaje %1!ld!, a causa del error 0x%2!8.8X!.|  
|0xC0208230|-1071611344|DTS_E_DTPXMLIDLOOKUPERR|No se encontró en el paquete el objeto con el id. %1!d! al que se hace referencia.|  
|0xC0208231|-1071611343|DTS_E_DTPXMLINVALIDXMLPERSISTPROPERTY|No se puede leer una propiedad de persistencia necesaria para el módulo pipelinexml. La canalización no proporcionó la propiedad.|  
|0xC0208232|-1071611342|DTS_E_DTPXMLPROPERTYSTATEERR|El valor "%1" no es válido para el atributo "%2".|  
|0xC0208233|-1071611341|DTS_E_CANTGETCUSTOMPROPERTY|No se puede recuperar la propiedad personalizada "%1".|  
|0xC0208234|-1071611340|DTS_E_UNABLETOLOCATEINPUTCOLUMNID|En la colección de columnas de entrada no se encuentra una columna de entrada con el id. de linaje %1!d!, a la que se hace referencia en la propiedad personalizada ParameterMap con el parámetro en el número de posición %2!d!.|  
|0xC0208235|-1071611339|DTS_E_TXLOOKUP_UNABLETOLOCATEREFCOLUMN|No se encuentra la columna de referencia "%1".|  
|0xC0208236|-1071611338|DTS_E_TXLOOKUP_INCOMPATIBLEDATATYPES|Los tipos de datos de %1 y de la columna de referencia con el nombre "%2" no son compatibles.|  
|0xC0208237|-1071611337|DTS_E_TXLOOKUP_PARAMMETADATAMISMATCH|La instrucción SQL con parámetros produce metadatos que no coinciden con la instrucción SQL principal.|  
|0xC0208238|-1071611336|DTS_E_TXLOOKUP_INCORRECTNUMOFPARAMETERS|La instrucción SQL con parámetros contiene un número de parámetros incorrecto. Se esperaba %1!d! pero se encontró %2!d!.|  
|0xC0208239|-1071611335|DTS_E_TXLOOKUP_INVALIDJOINTYPE|%1 tiene un tipo de datos que no puede combinarse.|  
|0xC020823A|-1071611334|DTS_E_TXLOOKUP_INVALIDCOPYTYPE|%1 tiene un tipo de datos que no puede copiarse.|  
|0xC020823B|-1071611333|DTS_E_INSERTERINVALIDCOLUMNDATATYPE|%1 tiene un tipo de datos no compatible. Debe ser DT_STR o DT_WSTR.|  
|0xC020823C|-1071611332|DTS_E_EXTRACTORINVALIDCOLUMNDATATYPE|%1 tiene un tipo de datos no compatible. Debe ser DT_STR, DT_WSTR, DT_TEXT, DT_NTEXT o DT_IMAGE.|  
|0xC020823D|-1071611331|DTS_E_TXCHARMAPINVALIDCOLUMNDATATYPE|%1 tiene un tipo de datos no compatible. Debe ser DT_STR, DT_WSTR, DT_TEXT o DT_NTEXT.|  
|0xC020823E|-1071611330|DTS_E_SORTCANTCREATEEVENT|La transformación Ordenar no puede crear un evento para comunicarse con sus subprocesos de trabajo. No hay suficientes identificadores del sistema para la transformación Ordenar.|  
|0xC020823F|-1071611329|DTS_E_SORTCANTCREATETHREAD|La transformación Ordenar no puede crear un subproceso de trabajo. No hay memoria suficiente para la transformación Ordenar.|  
|0xC0208240|-1071611328|DTS_E_SORTCANTCOMPARE|La transformación Ordenar no pudo comparar la fila %1!d! en el id. de búfer %2!d! con la fila %3!d! en el id. de búfer %4!d!.|  
|0xC0208242|-1071611326|DTS_E_TXLOOKUP_TOOFEWREFERENCECOLUMNS|Los metadatos de referencia a la transformación de búsquedas contienen muy pocas columnas. Compruebe la propiedad SQLCommand. La instrucción SELECT debe devolver al menos una columna.|  
|0xC0208243|-1071611325|DTS_E_TXLOOKUP_MALLOCERR_REFERENCECOLUMNINFO|No se puede asignar memoria para una matriz de estructuras ColumnInfo.|  
|0xC0208244|-1071611324|DTS_E_TXLOOKUP_MALLOCERR_REFERENCECOLUMNPAIR|No se pudo asignar memoria para una matriz de estructuras ColumnPair.|  
|0xC0208245|-1071611323|DTS_E_TXLOOKUP_MALLOCERR_BUFFCOL|No se puede asignar memoria para una matriz de estructuras BUFFCOL con el fin de crear un área de trabajo principal.|  
|0xC0208246|-1071611322|DTS_E_TXLOOKUP_MAINWORKSPACE_CREATEERR|No se puede crear un búfer de área de trabajo principal.|  
|0xC0208247|-1071611321|DTS_E_TXLOOKUP_HASHTABLE_MALLOCERR|No se puede asignar memoria para la tabla hash.|  
|0xC0208248|-1071611320|DTS_E_TXLOOKUP_HASHNODEHEAP_CREATEERR|No se puede asignar memoria para crear un montón de nodos hash.|  
|0xC0208249|-1071611319|DTS_E_TXLOOKUP_HASHNODEHEAP_MALLOCERR|No se puede asignar memoria para un montón de nodos hash.|  
|0xC020824A|-1071611318|DTS_E_TXLOOKUP_LRUNODEHEAP_CREATEERR|No se puede crear un montón de nodos LRU. Memoria insuficiente.|  
|0xC020824B|-1071611317|DTS_E_TXLOOKUP_LRUNODEHEAP_MALLOCERR|No se puede asignar memoria para el motón de nodos LRU. Memoria insuficiente.|  
|0xC020824C|-1071611316|DTS_E_TXLOOKUP_OLEDBERR_LOADCOLUMNMETADATA|Error de OLE DB al cargar metadatos de columna. Compruebe las propiedades SQLCommand y SqlCommandParam.|  
|0xC020824D|-1071611315|DTS_E_TXLOOKUP_OLEDBERR_GETIROWSET|Error de OLE DB al capturar conjunto de filas. Compruebe las propiedades SQLCommand y SqlCommandParam.|  
|0xC020824E|-1071611314|DTS_E_TXLOOKUP_OLEDBERR_FILLBUFFER|Error de OLE DB al llenar la caché interna. Compruebe las propiedades SQLCommand y SqlCommandParam.|  
|0xC020824F|-1071611313|DTS_E_TXLOOKUP_OLEDBERR_BINDPARAMETERS|Error de OLE DB al enlazar parámetros. Compruebe las propiedades SQLCommand y SqlCommandParam.|  
|0xC0208250|-1071611312|DTS_E_TXLOOKUP_OLEDBERR_CREATEBINDING|Error de OLE DB al crear enlaces. Compruebe las propiedades SQLCommand y SqlCommandParam.|  
|0xC0208251|-1071611311|DTS_E_TXLOOKUP_INVALID_CASE|Se encontró un escenario no válido en una instrucción switch en tiempo de ejecución.|  
|0xC0208252|-1071611310|DTS_E_TXLOOKUP_MAINWORKSPACE_MALLOCERR|No se puede asignar memoria para una nueva fila del búfer de área de trabajo principal. Memoria insuficiente.|  
|0xC0208253|-1071611309|DTS_E_TXLOOKUP_OLEDBERR_GETPARAMIROWSET|Error de OLE DB al capturar conjunto de filas con parámetros. Compruebe las propiedades SQLCommand y SqlCommandParam.|  
|0xC0208254|-1071611308|DTS_E_TXLOOKUP_OLEDBERR_GETPARAMSINGLEROW|Error de OLE DB al capturar fila con parámetros. Compruebe las propiedades SQLCommand y SqlCommandParam.|  
|0xC0208255|-1071611307|DTS_E_TXAGG_MAINWORKSPACE_MALLOCERR|No se puede asignar memoria para una nueva fila del búfer de área de trabajo principal. Memoria insuficiente.|  
|0xC0208256|-1071611306|DTS_E_TXAGG_MAINWORKSPACE_CREATEERR|No se puede crear un búfer de área de trabajo principal.|  
|0xC0208257|-1071611305|DTS_E_TXAGG_HASHTABLE_MALLOCERR|No se puede asignar memoria para la tabla hash.|  
|0xC0208258|-1071611304|DTS_E_TXAGG_HASHNODEHEAP_CREATEERR|No se puede asignar memoria para crear un montón de nodos hash.|  
|0xC0208259|-1071611303|DTS_E_TXAGG_HASHNODEHEAP_MALLOCERR|No se puede asignar memoria para el motón de nodos hash.|  
|0xC020825A|-1071611302|DTS_E_TXAGG_CDNODEHEAP_CREATEERR|No se puede asignar memoria para crear un montón de nodos CountDistinct.|  
|0xC020825B|-1071611301|DTS_E_TXAGG_CDNODEHEAP_MALLOCERR|No se puede asignar memoria para el montón de nodos CountDistinct.|  
|0xC020825C|-1071611300|DTS_E_TXAGG_CDCHAINHEAP_CREATEERR|No se puede asignar memoria para crear un montón de cadenas CountDistinct.|  
|0xC020825D|-1071611299|DTS_E_TXAGG_CDHASHTABLE_CREATEERR|No se puede asignar memoria para la tabla hash CountDistinct.|  
|0xC020825E|-1071611298|DTS_E_TXAGG_CDWORKSPACE_MALLOCERR|No se puede asignar memoria para una nueva fila del búfer de área de trabajo CountDistinct.|  
|0xC020825F|-1071611297|DTS_E_TXAGG_CDWORKSPACE_CREATEERR|No se puede crear un búfer de área de trabajo CountDistinct.|  
|0xC0208260|-1071611296|DTS_E_TXAGG_CDCOLLASSEARRAY_MALLOCERR|No se puede asignar memoria a la matriz para contraer CountDistinct.|  
|0xC0208261|-1071611295|DTS_E_TXAGG_CDCHAINHEAP_MALLOCERR|No se puede asignar memoria para cadenas CountDistinct.|  
|0xC0208262|-1071611294|DTS_E_TXCOPYMAP_MISMATCHED_COLUMN_METADATA|Los metadatos de las columnas con los id. de linaje %1!d! y %2!d! tienen metadatos no coincidentes. La columna de entrada asignada a una columna de salida para una asignación de copia no tiene los mismos metadatos (tipo de datos, precisión, escala, longitud o página de códigos).|  
|0xC0208263|-1071611293|DTS_E_TXCOPYMAP_INCORRECT_OUTPUT_COLUMN_MAPPING|La columna de salida con el id. de linaje "%1!d!" se ha asignado incorrectamente a una columna de entrada. La propiedad CopyColumnId de la columna de salida no es correcta.|  
|0xC0208265|-1071611291|DTS_E_CANTGETBLOBDATA|Error al recuperar datos long para la columna "%1".|  
|0xC0208266|-1071611290|DTS_E_CANTADDBLOBDATA|Se recuperaron datos de tipo long para una columna, pero no se pueden agregar al búfer de la tarea Flujo de datos.|  
|0xC0208267|-1071611289|DTS_E_MCASTOUTPUTCOLUMNS|La salida "%1" (%2!d!) tiene columnas de salida pero las salidas de multidifusión no declaran columnas. El paquete está dañado.|  
|0xC0208273|-1071611277|DTS_E_UNABLETOGETLOCALIZEDRESOURCE|No se puede cargar un id. de recurso %1!d! localizado. Compruebe si el archivo RLL está presente.|  
|0xC0208274|-1071611276|DTS_E_DTPXMLEVENTSCACHEERR|No se puede adquirir la interfaz de eventos. Se pasó una interfaz de eventos no válida al módulo de flujo de datos para almacenarla en XML.|  
|0xC0208275|-1071611275|DTS_E_DTPXMLPATHLOADERR|Error al establecer un objeto de ruta durante la carga de XML.|  
|0xC0208276|-1071611274|DTS_E_DTPXMLINPUTLOADERR|Error al establecer un objeto de entrada durante la carga de XML.|  
|0xC0208277|-1071611273|DTS_E_DTPXMLOUTPUTLOADERR|Error al establecer un objeto de salida durante la carga de XML.|  
|0xC0208278|-1071611272|DTS_E_DTPXMLINPUTCOLUMNLOADERR|Error al establecer un objeto de columna de entrada durante la carga de XML.|  
|0xC0208279|-1071611271|DTS_E_DTPXMLOUTPUTCOLUMNLOADERR|Error al establecer un objeto de columna de salida durante la carga de XML.|  
|0xC0208280|-1071611264|DTS_E_DTPXMLPROPERTYLOADERR|Error al establecer un objeto de propiedad durante la carga de XML.|  
|0xC0208281|-1071611263|DTS_E_DTPXMLCONNECTIONLOADERR|Error al establecer un objeto de conexión durante la carga de XML.|  
|0xC0208282|-1071611262|DTS_E_FG_MISSING_OUTPUT_COLUMNS|Faltan algunas columnas especiales específicas de la transformación o tienen tipos incorrectos.|  
|0xC0208283|-1071611261|DTS_E_FG_PREPARE_TABLES_AND_ACCESSORS|La transformación Agrupación aproximada no pudo crear las tablas y descriptores de acceso requeridos.|  
|0xC0208284|-1071611260|DTS_E_FG_COPY_INPUT|La transformación Agrupación aproximada no pudo copiar la entrada.|  
|0xC0208285|-1071611259|DTS_E_FG_GENERATE_GROUPS|La transformación Agrupación aproximada no pudo generar grupos.|  
|0xC0208286|-1071611258|DTS_E_FG_LEADING_TRAILING|Error inesperado en la agrupación aproximada al aplicar la configuración de la propiedad '%1'.|  
|0xC0208287|-1071611257|DTS_E_FG_PICK_CANONICAL|La transformación Agrupación aproximada no pudo seleccionar una fila canónica de datos para utilizarse en la estandarización de los datos.|  
|0xC0208288|-1071611256|DTS_E_FG_NOBLOBS|La agrupación aproximada no admite columnas de entrada de tipo IMAGE, TEXT o NTEXT.|  
|0xC0208289|-1071611255|DTS_E_FG_FUZZY_MATCH_ON_NONSTRING|Se ha especificado una coincidencia parcial en la columna "%1" (%2!d!) que no es un tipo de datos DT_STR o DT_WSTR.|  
|0xC020828A|-1071611254|DTS_E_FUZZYGROUPINGINTERNALPIPELINEERROR|Error de canalización de la transformación Agrupación aproximada. Código de error: 0x%1!8.8X!: "%2"|  
|0xC020828B|-1071611253|DTS_E_CODE_PAGE_NOT_SUPPORTED|La página de códigos %1!d! especificada en la columna "%2" (%3!d!) no se admite.  Primero debe convertir esta columna en DT_WSTR, lo que se puede hacer insertando una transformación de conversión de datos antes de ésta.|  
|0xC0208294|-1071611244|DTS_E_SETEODFAILED|Se encontró un error al establecer el final de la marca de datos para la salida "%1" (%2!d!) que conduce al búfer.|  
|0xC0208296|-1071611242|DTS_E_CANTCLONE|No se pudo clonar el búfer de entrada. Memoria insuficiente o error interno.|  
|0xC02082F9|-1071611143|DTS_E_TXCHARMAP_CANTKATAKANAHIRAGANA|La columna "%1" solicita la producción simultánea de caracteres Katakana y Hiragana.|  
|0xC02082FA|-1071611142|DTS_E_TXCHARMAP_CANTSIMPLECOMPLEX|La columna "%1" solicita la producción simultánea de caracteres de chino simplificado y chino tradicional.|  
|0xC02082FB|-1071611141|DTS_E_TXCHARMAP_CANTFULLHALF|La columna "%1" solicita que las operaciones generen caracteres de formato completo y formato medio.|  
|0xC02082FC|-1071611140|DTS_E_TXCHARMAP_CANTCHINAJAPAN|La columna "%1" combina operaciones en caracteres japoneses con operaciones de caracteres chinos.|  
|0xC02082FD|-1071611139|DTS_E_TXCHARMAP_CANTCASECHINESE|La columna "%1" combina operaciones en caracteres chinos con operaciones en mayúsculas y minúsculas.|  
|0xC02082FE|-1071611138|DTS_E_TXCHARMAP_CANTCASEJAPANESE|La columna "%1" combina operaciones en caracteres japoneses con operaciones en mayúsculas y minúsculas.|  
|0xC02082FF|-1071611137|DTS_E_TXCHARMAP_CANTBOTHCASE|La columna "%1" asigna la columna tanto en mayúsculas como en minúsculas.|  
|0xC0208300|-1071611136|DTS_E_TXCHARMAP_CANTLINGUISTIC|La columna "%1" combina marcas que no sean de mayúsculas y minúsculas con la utilización lingüística de mayúsculas y minúsculas.|  
|0xC0208301|-1071611135|DTS_E_TXCHARMAP_INVALIDMAPFLAGANDDATATYPE|El tipo de datos de la columna "%1" no puede asignarse de la forma especificada.|  
|0xC0208302|-1071611134|DTS_E_TXFUZZYLOOKUP_UNSUPPORTED_MATCH_INDEX_VERSION|La versión (%1) del índice de coincidencia existente "%2" no es compatible. La versión esperada es "%3". Este error se produce si la versión almacenada en los metadatos de índice no coincide con la versión para la cual se generó el código actual. Para solucionar el error, vuelva a generar el índice con la versión actual del código.|  
|0xC0208303|-1071611133|DTS_E_TXFUZZYLOOKUP_INVALID_MATCH_INDEX|Aparentemente la tabla "%1" no es un índice de coincidencia pregenerado válido. Este error se produce si no se puede cargar el registro de metadatos del índice pregenerado especificado.|  
|0xC0208304|-1071611132|DTS_E_TXFUZZYLOOKUP_UNABLE_TO_READ_MATCH_INDEX|No se puede leer el índice de coincidencia pregenerado "%1" especificado.  Código de error de OLEDB: 0x%2! 8.8X!.|  
|0xC0208305|-1071611131|DTS_E_TXFUZZYLOOKUP_NO_JOIN_COLUMNS|No hay ninguna columna de entrada válida que tenga una combinación válida con una columna de tabla de referencia.  Asegúrese de que exista al menos una combinación definida con las propiedades de columna de entrada JoinToReferenceColumn y JoinType.|  
|0xC0208306|-1071611130|DTS_E_TXFUZZYLOOKUP_INDEX_DOES_NOT_CONTAIN_COLUMN|El índice de coincidencia existente "%1" especificado no se generó originalmente con información de coincidencias parciales para la columna "%2".  Debe volver a generarse para incluir esta información. Este error se produce si se generó el índice con una columna que no era de combinación parcial.|  
|0xC0208307|-1071611129|DTS_E_TXFUZZYLOOKUP_IDENTIFIER_PROPERTY|El nombre "%1" asignado a la propiedad "%2" no es un nombre de identificador de SQL válido. Esto sucede si el nombre de la propiedad no cumple las especificaciones de los nombres de identificadores de SQL válidos.|  
|0xC0208309|-1071611127|DTS_E_TXFUZZYLOOKUP_MINSIMILARITY_INVALID|La propiedad umbral MinSimilarity en la transformación Búsqueda aproximada debe tener un valor mayor o igual que 0,0 pero menor que 1,0.|  
|0xC020830A|-1071611126|DTS_E_TXFUZZYLOOKUP_INVALID_PROPERTY_VALUE|El valor "%1" de la propiedad "%2" no es válido.|  
|0xC020830B|-1071611125|DTS_E_TXFUZZYLOOKUP_INCOMPATIBLE_FUZZY_JOIN_DATATYPES|La búsqueda aproximada especificada entre la columna de entrada "%1" y la columna de referencia "%2" no es válida porque las combinaciones parciales solo se admiten entre columnas de cadena de los tipos DT_STR y DT_WSTR.|  
|0xC020830C|-1071611124|DTS_E_TXFUZZYLOOKUP_INCOMPATIBLE_EXACT_JOIN_DATATYPES|Las columnas de búsquedas exactas "%1" y "%2" no tienen los mismos tipos de datos o no son tipos de cadenas comparables. Las combinaciones parciales se admiten entre columnas con los mismos tipos de datos o con una combinación de DT_STR y DT_WSTR.|  
|0xC020830D|-1071611123|DTS_E_TXFUZZYLOOKUP_INCOMPATIBLE_COPYCOLUMN_DATATYPES|Las columnas de búsquedas exactas "%1" y "%2" no tienen los mismos tipos de datos o no son tipos de cadenas que puedan convertirse trivialmente. Esto sucede porque se puede copiar de una columna de referencia a una columna de salida si ambas tienen los mismos tipos de datos o una combinación de DT_STR y DT_WSTR, pero no se admiten otros tipos.|  
|0xC020830E|-1071611122|DTS_E_TXFUZZYLOOKUP_INCOMPATIBLE_PASSTHRUCOLUMN_DATATYPES|Las columnas de paso a través "%1" y "%2" no tienen los mismos tipos de datos. Solo se admiten columnas con los mismos tipos de datos como columnas de paso a través de la entrada a la salida.|  
|0xC020830F|-1071611121|DTS_E_TXFUZZYLOOKUP_UNABLETOLOCATEREFCOLUMN|No se encuentra la columna de referencia "%1".|  
|0xC0208311|-1071611119|DTS_E_TXFUZZYLOOKUP_OUTPUT_COLUMN_MUST_BE_PASSTHRU_COLUMN_OR_A_COPY_COLUMN|Una columna de salida debe tener especificada exactamente una propiedad CopyColumn o PassThruColumn. Este error se produce si ni la propiedad CopyColumn ni la propiedad PassThruColumn, o ambas propiedades, tienen establecidos valores no vacíos.|  
|0xC0208312|-1071611118|DTS_E_TXFUZZYLOOKUP_PASSTHRU_COLUMN_NOT_FOUND|El id. de linaje de origen "%1!d!" especificado para la propiedad "%2 "de la columna de salida "%3" no se encontró en la colección de columnas de entrada. Esto sucede si no se encuentra en el conjunto de entradas el Id. de columna de entrada especificado en una columna de salida como columna de paso a través.|  
|0xC0208313|-1071611117|DTS_E_TXFUZZYLOOKUP_INDEXED_COLUMN_NOT_FOUND_IN_REF_TABLE|No se encontró en la tabla o consulta de referencia la columna "%1" del índice pregenerado "%2". Esto sucede si el esquema o consulta de la tabla de referencia ha cambiado desde que se generó el índice de coincidencia existente.|  
|0xC0208314|-1071611116|DTS_E_TXFUZZYLOOKUP_TOKEN_TOO_LONG|El componente encontró un token de más de 2147483647 caracteres.|  
|0xC0208315|-1071611115|DTS_E_RAWMETADATAMISMATCHTYPE|No se puede anexar el archivo de salida. El nombre de la columna "%1" coincide, pero la columna del archivo tiene el tipo %2 y la columna de entrada tiene el tipo %3. Los tipos de datos de los metadatos de la columna no coinciden.|  
|0xC0208316|-1071611114|DTS_E_RAWMETADATAMISMATCHSIZE|No se puede anexar el archivo de salida. El nombre de la columna "%1" coincide, pero la longitud máxima de la columna del archivo es %2!d! y la de la columna de entrada es %3!d!. La longitud de los metadatos de la columna no coincide.|  
|0xC0208317|-1071611113|DTS_E_RAWMETADATAMISMATCHCODEPAGE|No se puede anexar el archivo de salida. El nombre de la columna "%1" coincide, pero la columna del archivo tiene la página de códigos %2!d! y la columna de entrada tiene la página de códigos %3!d!. Las páginas de códigos de los metadatos de la columna indicada no coinciden.|  
|0xC0208318|-1071611112|DTS_E_RAWMETADATAMISMATCHPRECISION|No se puede anexar el archivo de salida. El nombre de la columna "%1" coincide, pero la columna del archivo tiene el valor de precisión %2!d! y la columna de entrada tiene el valor de precisión %3!d!. La precisión de los metadatos de la columna indicada no coincide.|  
|0xC0208319|-1071611111|DTS_E_RAWMETADATAMISMATCHSCALE|No se puede anexar el archivo de salida. El nombre de la columna "%1" coincide, pero la columna del archivo tiene el valor de escala %2!d! y la columna de entrada tiene el valor de escala %3!d!.  La escala de los metadatos de la columna indicada no coincide.|  
|0xC020831A|-1071611110|DTS_E_COULD_NOT_DETERMINE_DATASOURCE_DBMSNAME|No se puede determinar el nombre DBMS y la versión en "%1". Esto sucede si IDBProperties en la conexión no devolvió la información necesaria para comprobar el nombre DBMS y la versión.|  
|0xC020831B|-1071611109|DTS_E_INCORRECT_SQL_SERVER_VERSION|El tipo DBMS o la versión de "%1" no es compatible.  Se requiere una conexión a Microsoft SQL Server 8.0 o posterior. Esto sucede si IDBProperties en la conexión no devolvió la versión correcta.|  
|0xC020831D|-1071611107|DTS_E_CANTDELETEERRORCOLUMNS|%1 es una columna de salida de error especial y no puede eliminarse.|  
|0xC020831E|-1071611106|DTS_E_UNEXPECTEDCOLUMNDATATYPE|El tipo de datos especificado para la columna "%1" no es el tipo esperado "%2".|  
|0xC020831F|-1071611105|DTS_E_INPUTCOLUMNNOTFOUND|No se pudo localizar en la colección de columnas de entrada el id. de linaje de columna de entrada "%1" al que hace referencia la propiedad "%2" en la columna de salida "%3".|  
|0xC0208320|-1071611104|DTS_E_TXGROUPDUPS_INPUTCOLUMNNOTJOINED|La columna de entrada "%1" a la que hace referencia la propiedad "%2" en la columna de salida "%3" debe tener la propiedad ToBeCleaned=True y tener un valor de propiedad ExactFuzzy válido.|  
|0xC0208322|-1071611102|DTS_E_TXFUZZYLOOKUP_REF_TABLE_MISSING_IDENTITY_INDEX|La tabla de referencia '%1' no tiene un índice clúster en una columna de identidad de tipo entero que se necesita si la propiedad 'CopyRefTable' está establecida en FALSE. Si el valor de CopyRefTable es False, la tabla de referencia debe tener un índice clúster en una columna de identidad de tipo entero.|  
|0xC0208323|-1071611101|DTS_E_TXFUZZYLOOKUP_REF_CONTAINS_NON_INTEGER_IDENT_COLUMN|La tabla de referencia '%1' contiene una columna de identidad de tipo no entero que no es compatible. Utilice una vista de la tabla sin la columna '%2'.  Este error se produce porque, si se copia la tabla de referencia, se agrega una columna de identidad de tipo entero y solamente se permite una columna de identidad por tabla.|  
|0xC0208324|-1071611100|DTS_E_TXFUZZY_MATCHCONTRIBUTION_AND_HIERARCHY_SPECIFIED|No pueden especificarse al mismo tiempo MatchContribution y la información de jerarquía. No se permite porque ambas propiedades son pesos de la puntuación.|  
|0xC0208325|-1071611099|DTS_E_TXFUZZY_HIERARCHY_INCORRECT|Los niveles de la jerarquía deberían ser números únicos. El nivel válido en los valores de jerarquía son los enteros mayores o iguales que 1. Cuanto más pequeño es el número, más baja es la columna en la jerarquía. El valor predeterminado es 0, que indica que la columna no forma parte de una jerarquía. No se permiten superposiciones ni espacios.|  
|0xC0208326|-1071611098|DTS_E_TXFUZZYGROUPING_INSUFFICIENT_FUZZY_JOIN_COLUMNS|No se definió ninguna columna con agrupación aproximada.  Debe existir al menos una columna de entrada definida con las propiedades de columna ToBeCleaned=true y ExactFuzzy=2.|  
|0xC0208329|-1071611095|DTS_E_TXFUZZYLOOKUP_COLUMNINVALID|La columna con el id. "%1!d!" no era válido por un motivo indeterminado.|  
|0xC020832A|-1071611094|DTS_E_TXFUZZYLOOKUP_UNSUPPORTEDDATATYPE|No se admite el tipo de datos de la columna '%1'.|  
|0xC020832C|-1071611092|DTS_E_TXFUZZYLOOKUP_OUTPUTLENGTHMISMATCH|La longitud de la columna de salida '%1' es menor que la de la columna de origen '%2'.|  
|0xC020832F|-1071611089|DTS_E_TERMEXTRACTION_INCORRECTEXACTNUMBEROFINPUTCOLUMNS|Solo debería haber una columna de entrada.|  
|0xC0208330|-1071611088|DTS_E_TERMEXTRACTION_INCORRECTEXACTNUMBEROFOUTPUTCOLUMNS|Debería haber exactamente dos columnas de salida.|  
|0xC0208331|-1071611087|DTS_E_TERMEXTRACTION_INCORRECTDATATYPEOFINPUTCOLUMN|La columna de entrada solo puede tener el tipo de datos DT_WSTR o DT_NTEXT.|  
|0xC0208332|-1071611086|DTS_E_TERMEXTRACTION_INCORRECTDATATYPEOFOUTPUTCOLUMN|La columna de salida [%1!d!] solo puede tener el tipo de datos '%2'.|  
|0xC0208333|-1071611085|DTS_E_TERMEXTRACTION_INCORRECTDATATYPEOFREFERENCECOLUMN|La columna de referencia solo puede tener el tipo de datos DT_STR o DT_WSTR.|  
|0xC0208334|-1071611084|DTS_E_TERMEXTRACTION_UNABLETOLOCATEREFCOLUMN|Error al buscar la columna de referencia '%1'.|  
|0xC0208335|-1071611083|DTS_E_TERMEXTRACTION_INCORRECTTERMTYPE|El tipo de término de la transformación solamente puede ser WordOnly, PhraseOnly o WordPhrase.|  
|0xC0208336|-1071611082|DTS_E_TERMEXTRACTION_INCORRECTFREQUENCYTHRESHOLD|El valor del umbral de frecuencia no debe ser inferior a '%1!d!'.|  
|0xC0208337|-1071611081|DTS_E_TERMEXTRACTION_INCORRECTMAXLENOFTERM|El valor de longitud máxima del término no debe ser inferior a '%1!d!'.|  
|0xC0208338|-1071611080|DTS_E_TERMEXTRACTION_TOOFEWREFERENCECOLUMNS|Los metadatos de referencia de extracción de términos contienen muy pocas columnas.|  
|0xC0208339|-1071611079|DTS_E_TERMEXTRACTION_MALLOCERR_REFERENCECOLUMNINFO|Error al asignar memoria.|  
|0xC020833A|-1071611078|DTS_E_TERMEXTRACTION_MAINWORKSPACE_CREATEERR|Error al crear un búfer de área de trabajo.|  
|0xC020833B|-1071611077|DTS_E_TERMEXTRACTION_OLEDBERR_CREATEBINDING|Error de OLEDB al crear enlaces.|  
|0xC020833C|-1071611076|DTS_E_TERMEXTRACTION_OLEDBERR_GETIROWSET|Error de OLEDB al capturar conjuntos de filas.|  
|0xC020833D|-1071611075|DTS_E_TERMEXTRACTION_OLEDBERR_FILLBUFFER|Error de OLEDB al llenar la caché interna.|  
|0xC020833E|-1071611074|DTS_E_TERMEXTRACTION_PROCESSERR|Error al extraer términos en la fila %1!ld!, columna %2!ld!. Se devolvió el código de error 0x%3!8.8X!. Quítelo de la entrada para solucionar el problema.|  
|0xC020833F|-1071611073|DTS_E_TERMEXTRACTIONORLOOKUP_PROCESSERR_DEPOSITFULL|El número de términos candidatos supera el límite de 4G.|  
|0xC0208340|-1071611072|DTS_E_TERMEXTRACTION_INVALIDOUTTERMTABLEORCOLUMN|La tabla, vista o columna de referencia que se utiliza en los términos de exclusión no es válida.|  
|0xC0208341|-1071611071|DTS_E_TXFUZZYLOOKUP_STRINGCOLUMNTOOLONG|La longitud de la columna de cadena '%1' supera los 4000 caracteres.  Es necesario realizar la conversión de DT_STR a DT_WSTR, por lo que se producirá un truncamiento.  Reduzca el ancho de columna o utilice solamente tipos de columna DT_WSTR.|  
|0xC0208342|-1071611070|DTS_E_TERMEXTRACTION_OUTTERMTABLEANDCOLUMNNOTSET|No se ha establecido la tabla, vista o columna de referencia que se utiliza en los términos de exclusión.|  
|0xC0208343|-1071611069|DTS_E_TERMLOOKUP_TOOFEWOUTPUTCOLUMNS|La búsqueda de términos contiene muy pocas columnas de salida.|  
|0xC0208344|-1071611068|DTS_E_TERMLOOKUP_INCORRECTDATATYPEOFREFERENCECOLUMN|La columna de referencia solo puede tener el tipo de datos DT_STR o DT_WSTR.|  
|0xC0208345|-1071611067|DTS_E_TERMLOOKUP_UNABLETOLOCATEREFCOLUMN|Error al buscar la columna de referencia '%1'.|  
|0xC0208346|-1071611066|DTS_E_TERMLOOKUP_TOOFEWREFERENCECOLUMNS|Los metadatos de referencia de búsqueda de términos contienen muy pocas columnas.|  
|0xC0208347|-1071611065|DTS_E_TERMEXTRACTIONORLOOKUP_TESTOFFSETERROR|Error al normalizar palabras.|  
|0xC0208348|-1071611064|DTS_E_TERMLOOKUP_MAINWORKSPACE_CREATEERR|Error al crear un búfer de área de trabajo.|  
|0xC0208349|-1071611063|DTS_E_TERMLOOKUP_OLEDBERR_CREATEBINDING|Error de OLEDB al crear enlaces.|  
|0xC020834A|-1071611062|DTS_E_TERMLOOKUP_OLEDBERR_GETIROWSET|Error de OLEDB al capturar conjuntos de filas.|  
|0xC020834B|-1071611061|DTS_E_TERMLOOKUP_OLEDBERR_FILLBUFFER|Error de OLEDB al llenar la caché interna.|  
|0xC020834C|-1071611060|DTS_E_TERMLOOKUP_PROCESSERR|Error al buscar términos en la fila %1!ld!, columna %2!ld!. Se devolvió el código de error 0x%3!8.8X!. Quítelo de la entrada para solucionar el problema.|  
|0xC020834D|-1071611059|DTS_E_TERMLOOKUP_TEXTIDINPUTCOLUMNNOTMAPPEDWITHOUTPUTCOLUMN|Al menos una columna de paso a través no se ha asignado a una columna de salida.|  
|0xC020834E|-1071611058|DTS_E_TERMLOOKUP_INCORRECTEXACTNUMBEROFTEXTCOLUMNS|Debería haber exactamente una columna de entrada asignada a una columna de referencia.|  
|0xC020834F|-1071611057|DTS_E_TERMLOOKUP_TEXTINPUTCOLUMNHAVEINCORRECTDATATYPE|La columna de entrada asignada a una columna de referencia solo puede tener los tipos de datos DT_NTXT o DT_WSTR.|  
|0xC0208354|-1071611052|DTS_E_TXFUZZYLOOKUP_INVALID_MATCH_INDEX_NAME|El nombre de la tabla de referencia "%1" no es un identificador de SQL válido. Esto sucede si no puede analizarse el nombre de la tabla desde la cadena de entrada. Debe de haber espacios sin comillas en el nombre. Compruebe si el nombre se ha escrito correctamente entre comillas.|  
|0xC0208355|-1071611051|DTS_E_TERMEXTRACTION_TERMFILTERSTARTITERATIONERROR|Error al iniciar la iteración del filtro de términos.|  
|0xC0208356|-1071611050|DTS_E_TERMEXTRACTION_EMPTYTERMRESULTERROR|Error al reclamar el búfer que se utiliza para almacenar los términos en la caché. Se devolvió el código de error 0x%1!8.8X!.|  
|0xC0208357|-1071611049|DTS_E_TERMEXTRACTION_STDLENGTHERROR|Error std::length_error de los contenedores STL.|  
|0xC0208358|-1071611048|DTS_E_TERMLOOKUP_SAVEWORDWITHPUNCTERROR|Error al guardar palabras con caracteres de puntuación. Se devolvió el código de error 0x%1!8.8X!.|  
|0xC0208359|-1071611047|DTS_E_TERMLOOKUP_ADDREFERENCETERM|Error al procesar el término de referencia %1!ld!th. Se devolvió el código de error 0x%2!8.8X!. Para solucionarlo, quite el término de referencia de la tabla de referencia.|  
|0xC020835A|-1071611046|DTS_E_TERMLOOKUP_SORREFERENCETERM|Error al ordenar términos de referencia. Se devolvió el código de error 0x%1!8.8X!.|  
|0xC020835B|-1071611045|DTS_E_TERMLOOKUP_COUNTTERM|Error al contar términos candidatos. Se devolvió el código de error 0x%1!8.8X!.|  
|0xC020835C|-1071611044|DTS_E_FUZZYLOOKUP_REFERENCECACHEFULL|La búsqueda aproximada no pudo cargar toda la tabla de referencia en la memoria principal tal como se precisa cuando la propiedad Exhaustive está habilitada.  La memoria del sistema es insuficiente o bien se especificó un límite para MaxMemoryUsage que no fue suficiente para cargar la tabla de referencia.  Establezca el valor de MaxMemoryUsage en 0 o auméntelo significativamente.  Como alternativa, deshabilite Exhaustive.|  
|0xC020835D|-1071611043|DTS_E_TERMLOOKUP_INITIALIZE|Error al inicializar el motor de búsqueda de términos. Se devolvió el código de error 0x%1!8.8X!.|  
|0xC020835E|-1071611042|DTS_E_TERMLOOKUP_PROCESSSENTENCE|Error al procesar frases. Se devolvió el código de error 0x%1!8.8X!.|  
|0xC020835F|-1071611041|DTS_E_TEXTMININGBASE_APPENDTOTEMPBUFFER|Error al agregar cadenas a un búfer interno. Se devolvió el código de error 0x%1!8.8X!.|  
|0xC0208360|-1071611040|DTS_E_TERMEXTRACTION_SAVEPOSTAG|Error al guardar etiquetas de funciones de sintaxis de un búfer interno. Se devolvió el código de error 0x%1!8.8X!.|  
|0xC0208361|-1071611039|DTS_E_TERMEXTRACTION_COUNTTERM|Error al contar términos candidatos. Se devolvió el código de error 0x%1!8.8X!.|  
|0xC0208362|-1071611038|DTS_E_TERMEXTRACTION_INITPOSPROCESSOR|Error al inicializar el procesador de funciones de sintaxis. Se devolvió el código de error 0x%1!8.8X!.|  
|0xC0208363|-1071611037|DTS_E_TERMEXTRACTION_INITFSA|Error al cargar autómatas de estado finito. Se devolvió el código de error 0x%1!8.8X!.|  
|0xC0208364|-1071611036|DTS_E_TERMEXTRACTION_INITIALIZE|Error al inicializar el motor de extracción de términos. Se devolvió el código de error 0x%1!8.8X!.|  
|0xC0208365|-1071611035|DTS_E_TERMEXTRACTION_PROCESSSENTENCE|Error al procesar dentro de una frase. Se devolvió el código de error 0x%1!8.8X!.|  
|0xC0208366|-1071611034|DTS_E_TERMEXTRACTION_INITPOSTAGVECTOR|Error al inicializar el procesador de funciones de sintaxis. Se devolvió el código de error 0x%1!8.8X!.|  
|0xC0208367|-1071611033|DTS_E_TERMEXTRACTION_SAVEPTRSTRING|Error al agregar cadenas a un búfer interno. Se devolvió el código de error 0x%1!8.8X!.|  
|0xC0208368|-1071611032|DTS_E_TERMEXTRACTION_ADDWORDTODECODER|Error al agregar palabras a un descodificador estático. Se devolvió el código de error 0x%1!8.8X!.|  
|0xC0208369|-1071611031|DTS_E_TERMEXTRACTION_DECODE|Error al descodificar una frase. Se devolvió el código de error 0x%1!8.8X!.|  
|0xC020836A|-1071611030|DTS_E_TERMEXTRACTION_SETEXCLUDEDTERM|Error al establecer términos de exclusión. Se devolvió el código de error 0x%1!8.8X!.|  
|0xC020836B|-1071611029|DTS_E_TERMEXTRACTION_PROCESSDOCUMENT|Error al procesar un documento en la entrada. Se devolvió el código de error 0x%1!8.8X!.|  
|0xC020836C|-1071611028|DTS_E_TEXTMININGBASE_TESTPERIOD|Error al probar si un punto forma parte de un acrónimo. Se devolvió el código de error 0x%1!8.8X!.|  
|0xC020836D|-1071611027|DTS_E_TERMLOOKUP_ENGINEADDREFERENCETERM|Error al establecer términos de referencia. Se devolvió el código de error 0x%1!8.8X!.|  
|0xC020836E|-1071611026|DTS_E_TERMLOOKUP_PROCESSDOCUMENT|Error al procesar un documento en la entrada. Se devolvió el código de error 0x%1!8.8X!.|  
|0xC020836F|-1071611025|DTS_E_INVALIDBULKINSERTPROPERTYVALUE|El valor de la propiedad %1 es %2!d!, que no está permitido.  El valor debe ser mayor o igual que %3!d!.|  
|0xC0208370|-1071611024|DTS_E_INVALIDBULKINSERTFIRSTROWLASTROWVALUES|El valor de la propiedad %1 es %2!d!, que debe ser menor o igual que el valor %3!d! de la propiedad %4.|  
|0xC0208371|-1071611023|DTS_E_FUZZYLOOKUPUNABLETODELETEEXISTINGMATCHINDEX|Error al intentar eliminar el índice de coincidencia parcial existente con el nombre "%1". Es posible que esta tabla no fuera creada mediante búsqueda aproximada (o esta versión de búsqueda aproximada), que se haya dañado o que haya otro problema. Intente eliminar manualmente la tabla con el nombre "%2" o especifique un nombre distinto para la propiedad MatchIndexName.|  
|0xC0208372|-1071611022|DTS_E_TERMEXTRACTION_INCORRECTSCORETYPE|El tipo de puntuación de la transformación solo puede ser Frequency o TFIDF.|  
|0xC0208373|-1071611021|DTS_E_FUZZYLOOKUPREFTABLETOOBIG|La tabla de referencia especificada tiene demasiadas filas. La búsqueda aproximada solo funciona con tablas de referencia de menos de mil millones de filas. Considere la posibilidad de utilizar una vista más pequeña de la tabla de referencia.|  
|0xC0208374|-1071611020|DTS_E_FUZZYLOOKUPUNABLETODETERMINEREFERENCETABLESIZE|No se puede determinar el tamaño de la tabla de referencia '%1'.  Es posible que este objeto sea una vista y no una tabla.  La búsqueda aproximada no admite vistas si CopyReferentaceTable=false.  Asegúrese de que la tabla existe y de que CopyReferenceTable=true.|  
|0xC0208377|-1071611017|DTS_E_XMLSRCOUTPUTCOLUMNDATATYPENOTSUPPORTED|El tipo de datos "%1" de la tarea Flujo de datos SSIS de %2 no es compatible con %3.|  
|0xC0208378|-1071611016|DTS_E_XMLSRCCANNOTFINDCOLUMNTOSETDATATYPE|No se pueden establecer las propiedades de tipos de datos de la columna de salida con el id. %1!d! en la salida con el id. %2!d!. No se encontró la salida o la columna.|  
|0xC0208379|-1071611015|DTS_E_CUSTOMPROPERTYISREADONLY|No se puede cambiar el valor de la propiedad personalizada "%1" en %2.|  
|0xC020837A|-1071611014|DTS_E_OUTPUTCOLUMNHASNOERRORCOLUMN|%1 en la salida no de error no tiene ninguna columna de salida correspondiente en la salida de error.|  
|0xC020837B|-1071611013|DTS_E_ERRORCOLUMNHASNOOUTPUTCOLUMN|%1 en la salida de error no tiene ninguna columna de salida correspondiente en la salida de no error.|  
|0xC020837C|-1071611012|DTS_E_ERRORCOLUMNHASINCORRECTPROPERTIES|%1 en la salida de error tiene propiedades que no coinciden con las propiedades de su columna de origen de datos correspondiente.|  
|0xC020837D|-1071611011|DTS_E_ADOSRCOUTPUTCOLUMNDATATYPECANNOTBECHANGED|El tipo de datos de las columnas de salida de %1 no se puede cambiar, excepto el de las columnas DT_WSTR y DT_NTEXT.|  
|0xC020837F|-1071611009|DTS_E_ADOSRCDATATYPEMISMATCH|El tipo de datos de "%1" no coincide con el tipo de datos "%2" de la columna de origen "%3".|  
|0xC0208380|-1071611008|DTS_E_ADOSRCCOLUMNNOTINSCHEMAROWSET|%1 no tiene una columna de origen coincidente en el esquema.|  
|0xC0208381|-1071611007|DTS_E_TERMLOOKUP_INVALIDREFERENCETERMTABLEORCOLUMN|La tabla o vista de referencia, o la columna que se utiliza para los términos de referencia no es válida.|  
|0xC0208382|-1071611006|DTS_E_TERMLOOKUP_REFERENCETERMTABLEANDCOLUMNNOTSET|La tabla o vista de referencia, o la columna que se utiliza para los términos de referencia no se ha establecido.|  
|0xC0208383|-1071611005|DTS_E_COLUMNMAPPEDTOALREADYMAPPEDEXTERNALMETADATACOLUMN|%1 está asignado a la columna de metadatos externos con el id. %2!ld!, que ya está asignada a otra columna.|  
|0xC0208384|-1071611004|DTS_E_TXFUZZYLOOKUP_TOOMANYPREFIXES|El nombre del objeto SQL '%1' especificado para la propiedad '%2' supera el número máximo de prefijos.  El máximo es 2.|  
|0xC0208385|-1071611003|DTS_E_MGDSRCSTATIC_OVERFLOW|El valor era demasiado grande para caber en la columna.|  
|0xC0208386|-1071611002|DTS_E_DATAREADERDESTREADERISCLOSED|IDataReader de SSIS está cerrada.|  
|0xC0208387|-1071611001|DTS_E_DATAREADERDESTREADERISATEND|IDataReader de SSIS se encuentra más allá del final del conjunto de resultados.|  
|0xC0208388|-1071611000|DTS_E_DATAREADERDESTINVALIDCOLUMNORDINAL|La posición ordinal de la columna no es válida.|  
|0xC0208389|-1071610999|DTS_E_DATAREADERDESTCANNOTCONVERT|No se puede convertir el valor %1 del tipo de datos "%2" en el tipo de datos "%3".|  
|0xC020838A|-1071610998|DTS_E_DATAREADERDESTINVALIDCODEPAGE|%1 tiene la página de códigos no compatible %2!d!.|  
|0xC020838B|-1071610997|DTS_E_XMLSRCEXTERNALMETADATACOLUMNNOTINSCHEMA|%1 no tiene ninguna asignación al esquema XML.|  
|0xC020838D|-1071610995|DTS_E_TXTERMLOOKUP_MISMATCHED_COLUMN_METADATA|Los metadatos de las columnas con los id. de linaje %1!d! y %2!d! tienen metadatos no coincidentes. La columna de entrada asignada a una columna de salida no tiene los mismos metadatos (tipo de datos, precisión, escala, longitud o página de códigos).|  
|0xC020838E|-1071610994|DTS_E_DATAREADERDESTREADERTIMEOUT|IDataReader de SSIS está cerrada. El tiempo de espera de lectura ha expirado.|  
|0xC020838F|-1071610993|DTS_E_ADOSRCINVALIDSQLCOMMAND|Error al ejecutar el comando SQL proporcionado: "%1". %2|  
|0xC0208390|-1071610992|DTS_E_JOINTYPEDOESNTMATCHETI|La propiedad JoinType especificada para la columna de entrada '%1' es distinta de la propiedad JoinType especificada para la columna de tabla de referencia correspondiente cuando se creó por primera vez el índice de coincidencias.  Vuelva a generar el índice de coincidencias con la propiedad JoinType especificada o cambie la propiedad JoinType de forma que coincida con el tipo que se utilizó al crear el índice de coincidencias.|  
|0xC0208392|-1071610990|DTS_E_SQLCEDESTDATATYPENOTSUPPORTED|El tipo de datos "%1" de la columna "%2" no es compatible con %3|  
|0xC0208393|-1071610989|DTS_E_DATAREADERDESTDATATYPENOTSUPPORTED|El tipo de datos "%1" de la columna %2 no es compatible con %3.|  
|0xC0208394|-1071610988|DTS_E_RECORDSETDESTDATATYPENOTSUPPORTED|El tipo de datos %1 no es compatible con %2.|  
|0xC0208446|-1071610810|DTS_E_TXSCRIPTMIGRATIONCOULDNOTADDREFERENCE|No se pudo agregar la referencia de proyecto "%1" durante la migración de %2. Puede que sea necesario completar la migración manualmente.|  
|0xC0208447|-1071610809|DTS_E_TXSCRIPTMIGRATIONMULTIPLEENTRYPOINTSFOUND|Se encontraron varios puntos de entrada con el nombre "%1" durante la migración de %2. Puede que sea necesario completar la migración manualmente.|  
|0xC0208448|-1071610808|DTS_E_TXSCRIPTMIGRATIONNOENTRYPOINTFOUND|No se encontró ningún punto de entrada durante la migración de %1. Puede que sea necesario completar la migración manualmente.|  
|0xC020844B|-1071610805|DTS_E_ADODESTINSERTIONFAILURE|Excepción durante la inserción de datos. El mensaje devuelto por el proveedor es: %1|  
|0xC020844C|-1071610804|DTS_E_ADODESTCONNECTIONTYPENOTSUPPORTED|No se pudo recuperar el nombre invariable del proveedor en %1. Actualmente, no es compatible con el componente de destino de ADO NET.|  
|0xC020844D|-1071610803|DTS_E_ADODESTARGUMENTEXCEPTION|Excepción de argumento cuando el proveedor de datos intenta insertar datos en el destino. El mensaje devuelto es: %1|  
|0xC020844E|-1071610802|DTS_E_ADODESTWRONGBATCHSIZE|La propiedad BatchSize debe ser un entero no negativo|  
|0xC020844F|-1071610801|DTS_E_ADODESTERRORUPDATEROW|Error al enviar esta fila al origen de datos de destino.|  
|0xC0208450|-1071610800|DTS_E_ADODESTEXECUTEREADEREXCEPTION|Excepción al ejecutar el comando SQL. El mensaje es: %1|  
|0xC0208451|-1071610799|DTS_E_ADODESTDATATYPENOTSUPPORTED|El tipo de datos "%1" de la columna "%2" no es compatible con %3|  
|0xC0208452|-1071610798|DTS_E_ADODESTFAILEDTOACQUIRECONNECTION|El destino de ADO NET no ha podido adquirir la conexión %1. Puede que la conexión esté dañada.|  
|0xC0208453|-1071610797|DTS_E_ADODESTNOTMANAGEDCONNECTION|La conexión especificada %1 no está administrada. Use la conexión administrada del destino de ADO NET.|  
|0xC0208454|-1071610796|DTS_E_ADODESTNOERROROUTPUT|El componente de destino no tiene una salida de error. Puede que esté dañada.|  
|0xC0208455|-1071610795|DTS_E_ADODESTNOLINEAGEID|El identificador lineageID %1 asociado con la columna externa %2 no existe en tiempo de ejecución.|  
|0xC0208456|-1071610794|DTS_E_ADODESTEXTERNALCOLNOTEXIST|%1 no existe en la base de datos. Puede que se haya quitado o cambiado de nombre.|  
|0xC0208457|-1071610793|DTS_E_ADODESTGETSCHEMATABLEFAILED|No se pudieron obtener las propiedades de columnas externas. Puede que el nombre de tabla que especificó no exista o que no tenga permiso SELECT en el objeto de tabla y se haya producido un error en un intento alternativo de obtener las propiedades de columna mediante la conexión. Los mensajes de error detallados son: %1|  
|0xC0208458|-1071610792|DTS_E_ADODESTCOLUMNERRORDISPNOTSUPPORTED|La disposición de errores de columnas de entrada no es compatible con el componente de destino de ADO NET.|  
|0xC0208459|-1071610791|DTS_E_ADODESTCOLUMNTRUNDISPNOTSUPPORTED|La disposición de truncamiento de columnas de entrada no es compatible con el componente de destino de ADO NET.|  
|0xC020845A|-1071610790|DTS_E_ADODESTINPUTTRUNDISPNOTSUPPORTED|La disposición de truncamiento de filas de entrada no es compatible con el componente de destino de ADO NET.|  
|0xC020845B|-1071610789|DTS_E_ADODESTTABLENAMEERROR|No se espera el nombre de tabla o vista. \n\t Si se especifica el nombre de tabla, use el prefijo %1 y el sufijo %2 del proveedor de datos seleccionado. \n\t Si usa un nombre con varias partes, use tres partes como máximo para el nombre de tabla.|  
|0xC0209001|-1071607807|DTS_E_FAILEDTOFINDCOLUMNINBUFFER|No se encontró la columna "%1" con el id. de linaje %2!d! en el búfer. El administrador de búfer devolvió el código de error 0x%3!8.8X!.|  
|0xC0209002|-1071607806|DTS_E_FAILEDTOGETCOLUMNINFOFROMBUFFER|Error al obtener información para la columna "%1" (%2!d!) desde el búfer. Se devolvió el código de error 0x%3!8.8X!.|  
|0xC0209011|-1071607791|DTS_E_TXAGG_ARITHMETICOVERFLOW|Se encontró un desbordamiento aritmético al agregar "%1".|  
|0xC0209012|-1071607790|DTS_E_FAILEDTOGETCOLINFO|Error al obtener información para la fila "%1!ld!", columna "%2!ld!", del búfer. Se devolvió el código de error 0x%3!8.8X!.|  
|0xC0209013|-1071607789|DTS_E_FAILEDTOSETCOLINFO|Error al establecer información para la fila "%1!ld!", columna "%2!ld!", en el búfer. Se devolvió el código de error 0x%3!8.8X!.|  
|0xC0209015|-1071607787|DTS_E_REQUIREDBUFFERISNOTAVAILBLE|El búfer necesario no está disponible.|  
|0xC0209016|-1071607786|DTS_E_FAILEDTOGETBUFFERBOUNDARYINFO|Error al intentar obtener la información de límite de búfer. Código de error: 0x%1!8.8X!.|  
|0xC0209017|-1071607785|DTS_E_FAILEDTOSETBUFFERENDOFROWSET|Error al establecer el final del conjunto de filas del búfer. Código de error: 0x%1!8.8X!.|  
|0xC0209018|-1071607784|DTS_E_FAILEDTOGETDATAFORERROROUTPUTBUFFER|Error al obtener datos para el búfer de salida de error.|  
|0xC0209019|-1071607783|DTS_E_FAILEDTOREMOVEROWFROMBUFFER|Error al quitar una fila del búfer. Código de error: 0x%1!8.8X!.|  
|0xC020901B|-1071607781|DTS_E_FAILEDTOSETBUFFERERRORINFO|Error al intentar establecer la información de error del búfer. Código de error: 0x%1!8.8X!.|  
|0xC020901C|-1071607780|DTS_E_COLUMNSTATUSERROR|Error con %1 en %2. Se devolvió el estado de columna: "%3".|  
|0xC020901D|-1071607779|DTS_E_TXLOOKUP_METADATAXMLCACHEERR|No se pueden almacenar en la caché los metadatos de referencia.|  
|0xC020901E|-1071607778|DTS_E_TXLOOKUP_ROWLOOKUPERROR|La fila no produjo ninguna coincidencia durante la búsqueda.|  
|0xC020901F|-1071607777|DTS_E_INVALIDERRORDISPOSITION|%1 tiene una disposición no válida de filas de truncamiento o error.|  
|0xC0209022|-1071607774|DTS_E_FAILEDTODIRECTERRORROW|Error al dirigir las filas a la salida de error. Código de error: 0x%1!8.8X!.|  
|0xC0209023|-1071607773|DTS_E_FAILEDTOPREPARECOLUMNSTATUSESFORINSERT|Error al preparar los estados de columna para la inserción. Código de error: 0x%1!8.8X!.|  
|0xC0209024|-1071607772|DTS_E_FAILEDTOFINDCOLUMNBYLINEAGEID|Error al intentar buscar %1 con el id. de linaje %2!d! en el búfer de la tarea Flujo de datos. Código de error: 0x%3!8.8X!.|  
|0xC0209025|-1071607771|DTS_E_FAILEDTOFINDNONSPECIALERRORCOLUMN|No se encontró ninguna columna de error no especial en %1.|  
|0xC0209029|-1071607767|DTS_E_INDUCEDTRANSFORMFAILUREONERROR|Código de error SSIS DTS_E_INDUCEDTRANSFORMFAILUREONERROR.  Error de "%1" a causa de un error con el código 0x%2!8.8X!. y a la especificación de un error en la disposición de filas de error en "%3". Error en el objeto especificado del componente especificado.  Puede que haya otros mensajes de error expuestos anteriores a éste con más información sobre el error.|  
|0xC020902A|-1071607766|DTS_E_INDUCEDTRANSFORMFAILUREONTRUNCATION|Error de "%1" a causa de un truncamiento y a la especificación de un error de truncamiento en la disposición de filas de truncamiento en "%2". Error de truncamiento en el objeto especificado del componente especificado.|  
|0xC020902B|-1071607765|DTS_E_TXSPLITEXPRESSIONEVALUATEDTONULL|La expresión "%1" de "%2" se evaluó como NULL, pero "%3" requiere resultados booleanos. Modifique la disposición de filas de error en la salida para tratar el resultado como False (Omitir error) o para redirigir esta fila a la salida de error (Redirigir fila).  Los resultados de la expresión deben ser booleanos en una división condicional.  El resultado NULL de la expresión es un error.|  
|0xC020902C|-1071607764|DTS_E_TXSPLITSTATIC_EXPRESSIONEVALUATEDTONULL|La expresión se evaluó como NULL, pero se requiere un resultado booleano. Modifique la disposición de filas de error en la salida para tratar el resultado como False (Omitir error) o para redirigir esta fila a la salida de error (Redirigir fila). Los resultados de la expresión deben ser booleanos en una división condicional.  El resultado NULL de la expresión es un error.|  
|0xC020902D|-1071607763|DTS_E_UTF16BIGENDIANFORMATNOTSUPPORTED|El formato de archivo UTF-16 big endian no es compatible.  Solo se admite el formato UTF-16 little endian.|  
|0xC020902E|-1071607762|DTS_E_UTF8FORMATNOTSUPPORTEDASUNICODE|El formato de archivo UTF-8 no se admite como Unicode.|  
|0xC020902F|-1071607761|DTS_E_DTPXMLCANTREADIDATTR|No se puede leer el atributo de Id.|  
|0xC020903E|-1071607746|DTS_E_TXLOOKUP_INDEXCOLUMNREUSED|Hay varias columnas de entrada de búsqueda que hacen referencia a la columna de índice de la caché %1.|  
|0xC020903F|-1071607745|DTS_E_TXLOOKUP_INDEXCOLUMNSMISMATCH|La búsqueda no hace referencia a todas las columnas de índice del administrador de conexiones de caché. Número de columnas unidas en la búsqueda: %1!d!. Número de columnas de índice: %2!d!.|  
|0xC0209069|-1071607703|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_CANTCONVERTVALUE|El valor de los datos no se pudo convertir por motivos distintos a un error de coincidencia de signos o desbordamiento de datos.|  
|0xC020906A|-1071607702|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_SCHEMAVIOLATION|El valor de los datos infringió la restricción de esquema.|  
|0xC020906B|-1071607701|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_TRUNCATED|Se truncaron los datos.|  
|0xC020906C|-1071607700|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_SIGNMISMATCH|Error de conversión porque el valor de los datos tenía signo y el tipo utilizado por el proveedor no tenía signo.|  
|0xC020906D|-1071607699|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_DATAOVERFLOW|Error de conversión porque el valor de los datos desbordó el tipo utilizado por el proveedor.|  
|0xC020906E|-1071607698|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_UNAVAILABLE|No hay ningún estado disponible.|  
|0xC020906F|-1071607697|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_PERMISSIONDENIED|El usuario no tenía los permisos correctos para escribir en la columna.|  
|0xC0209070|-1071607696|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_INTEGRITYVIOLATION|El valor de los datos infringió las restricciones de integridad para la columna.|  
|0xC0209071|-1071607695|DTS_E_OLEDBSOURCEADAPTERSTATIC_UNAVAILABLE|No hay ningún estado disponible.|  
|0xC0209072|-1071607694|DTS_E_OLEDBSOURCEADAPTERSTATIC_CANTCONVERTVALUE|El valor de los datos no se pudo convertir por motivos distintos a un error de coincidencia de signos o desbordamiento de datos.|  
|0xC0209073|-1071607693|DTS_E_OLEDBSOURCEADAPTERSTATIC_TRUNCATED|Se truncaron los datos.|  
|0xC0209074|-1071607692|DTS_E_OLEDBSOURCEADAPTERSTATIC_SIGNMISMATCH|Error de conversión porque el valor de los datos tenía signo y el tipo utilizado por el proveedor no tenía signo.|  
|0xC0209075|-1071607691|DTS_E_OLEDBSOURCEADAPTERSTATIC_DATAOVERFLOW|Error de conversión porque el valor de los datos desbordó el tipo utilizado por el proveedor.|  
|0xC0209076|-1071607690|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_SCHEMAVIOLATION|El valor de los datos infringió la restricción de esquema.|  
|0xC0209077|-1071607689|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_CANTCONVERTVALUE|El valor de los datos no se pudo convertir por motivos distintos a un error de coincidencia de signos o desbordamiento de datos.|  
|0xC0209078|-1071607688|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_TRUNCATED|Se truncaron los datos.|  
|0xC0209079|-1071607687|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_SIGNMISMATCH|Error de conversión porque el valor de los datos tenía signo y el tipo utilizado por el proveedor no tenía signo.|  
|0xC020907A|-1071607686|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_DATAOVERFLOW|Error de conversión porque el valor de los datos desbordó el tipo utilizado por el proveedor.|  
|0xC020907B|-1071607685|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_UNAVAILABLE|No hay ningún estado disponible.|  
|0xC020907C|-1071607684|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_PERMISSIONDENIED|El usuario no tenía los permisos correctos para escribir en la columna.|  
|0xC020907D|-1071607683|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_INTEGRITYVIOLATION|El valor de los datos infringe las restricciones de integridad.|  
|0xC020907F|-1071607681|DTS_E_TXDATACONVERTSTATIC_CANTCONVERTVALUE|El valor de los datos no se pudo convertir por motivos distintos a un error de coincidencia de signos o desbordamiento de datos.|  
|0xC0209080|-1071607680|DTS_E_TXDATACONVERTSTATIC_TRUNCATED|Se truncaron los datos.|  
|0xC0209081|-1071607679|DTS_E_TXDATACONVERTSTATIC_SIGNMISMATCH|Error de conversión porque el valor de los datos tenía signo y el tipo utilizado por el proveedor no tenía signo.|  
|0xC0209082|-1071607678|DTS_E_TXDATACONVERTSTATIC_DATAOVERFLOW|Error de conversión porque el valor de los datos desbordó el tipo utilizado por la transformación de conversión de datos.|  
|0xC0209083|-1071607677|DTS_E_FLATFILESOURCEADAPTERSTATIC_UNAVAILABLE|No hay ningún estado disponible.|  
|0xC0209084|-1071607676|DTS_E_FLATFILESOURCEADAPTERSTATIC_CANTCONVERTVALUE|El valor de los datos no se pudo convertir por motivos distintos a un error de coincidencia de signos o desbordamiento de datos.|  
|0xC0209085|-1071607675|DTS_E_FLATFILESOURCEADAPTERSTATIC_TRUNCATED|Se truncaron los datos.|  
|0xC0209086|-1071607674|DTS_E_FLATFILESOURCEADAPTERSTATIC_SIGNMISMATCH|Error de conversión porque el valor de los datos tenía signo y el tipo utilizado por el adaptador de origen de archivos planos no tenía signo.|  
|0xC0209087|-1071607673|DTS_E_FLATFILESOURCEADAPTERSTATIC_DATAOVERFLOW|Error de conversión porque el valor de los datos desbordó el tipo utilizado por el adaptador de origen de archivos planos.|  
|0xC020908E|-1071607666|DTS_E_TXDATACONVERTSTATIC_UNAVAILABLE|No hay ningún estado disponible.|  
|0xC0209090|-1071607664|DTS_E_FILEOPENERR_FORREAD|Error al abrir el archivo "%1" para leerlo. Código de error: 0x%2!8.8X!.|  
|0xC0209091|-1071607663|DTS_E_TXFILEINSERTERSTATIC_FILEOPENERR_FORREAD|Error al abrir el archivo para leerlo.|  
|0xC0209092|-1071607662|DTS_E_FILEOPENERR_FORWRITE|Error al abrir el archivo "%1" para escribir en él. Código de error: 0x%2!8.8X!.|  
|0xC0209093|-1071607661|DTS_E_TXFILEEXTRACTORSTATIC_FILEOPENERR_FORWRITE|Error al abrir el archivo para escribir en él.|  
|0xC0209094|-1071607660|DTS_E_TXFILEINSERTERSTATIC_INSERTERCANTREAD|Error al leer el archivo.|  
|0xC0209095|-1071607659|DTS_E_TXFILEEXTRACTORSTATIC_EXTRACTORCANTWRITE|Error al escribir en el archivo.|  
|0xC0209099|-1071607655|DTS_E_DTPXMLINVALIDPROPERTYARRAYTOOMANYVALUES|Se encontraron demasiados elementos de matriz al analizar una propiedad de la matriz de tipo. El valor de elementCount es menor que el número de elementos de matriz encontrados.|  
|0xC020909A|-1071607654|DTS_E_DTPXMLINVALIDPROPERTYARRAYNOTENOUGHVALUES|Se encontraron muy pocos elementos de matriz al analizar una propiedad de la matriz de tipo. El valor de elementCount es mayor que el número de elementos de matriz encontrados.|  
|0xC020909E|-1071607650|DTS_E_FILEOPENERR_FORWRITE_FILENOTFOUND|Error al abrir el archivo "%1" para escribir en él. No se encuentra el archivo.|  
|0xC020909F|-1071607649|DTS_E_TXFILEEXTRACTORSTATIC_FILEOPENERR_FORWRITE_FILENOTFOUND|Error al abrir el archivo para escribir en él. No se encuentra el archivo.|  
|0xC02090A0|-1071607648|DTS_E_FILEOPENERR_FORWRITE_PATHNOTFOUND|Error al abrir el archivo "%1" para escribir en él. No se encuentra la ruta de acceso.|  
|0xC02090A1|-1071607647|DTS_E_TXFILEEXTRACTORSTATIC_FILEOPENERR_FORWRITE_PATHNOTFOUND|Error al abrir el archivo para escribir en él. No se encuentra la ruta de acceso.|  
|0xC02090A2|-1071607646|DTS_E_FILEOPENERR_FORWRITE_TOOMANYOPENFILES|Error al abrir el archivo "%1" para escribir en él. Hay demasiados archivos abiertos.|  
|0xC02090A3|-1071607645|DTS_E_TXFILEEXTRACTORSTATIC_FILEOPENERR_FORWRITE_TOOMANYOPENFILES|Error al abrir el archivo para escribir en él. Hay demasiados archivos abiertos.|  
|0xC02090A4|-1071607644|DTS_E_FILEOPENERR_FORWRITE_ACCESSDENIED|Error al abrir el archivo "%1" para escribir en él. No tiene los permisos correctos.|  
|0xC02090A5|-1071607643|DTS_E_TXFILEEXTRACTORSTATIC_FILEOPENERR_FORWRITE_ACCESSDENIED|Error al abrir el archivo para escribir en él. No tiene los permisos correctos.|  
|0xC02090A6|-1071607642|DTS_E_FILEOPENERR_FORWRITE_FILEEXISTS|Error al abrir el archivo "%1" para escribir en él. El archivo existe y no puede sobrescribirse. Si el valor de la propiedad AllowAppend es FALSE y la propiedad ForceTruncate se establece en FALSE, la existencia del archivo provocará este error.|  
|0xC02090A7|-1071607641|DTS_E_TXFILEEXTRACTORSTATIC_FILEOPENERR_FORWRITE_FILEEXISTS|Error al abrir un archivo para escribir en él. El archivo ya existe y no puede sobrescribirse. Si las propiedades AllowAppend y ForceTruncate se establecen en FALSE, la existencia del archivo provocará este error.|  
|0xC02090A8|-1071607640|DTS_E_INCORRECTCUSTOMPROPERTYVALUEFOROBJECT|El valor de la propiedad personalizada "%1" en %2 no es correcto.|  
|0xC02090A9|-1071607639|DTS_E_COLUMNSHAVEINCOMPATIBLEMETADATA|Las columnas "%1" y "%2" tienen metadatos no compatibles.|  
|0xC02090AD|-1071607635|DTS_E_FILEWRITEERR_DISKFULL|Error al abrir el archivo "%1" para escribir en él porque el disco está lleno. No hay suficiente espacio en disco para guardar este archivo.|  
|0xC02090AE|-1071607634|DTS_E_TXFILEEXTRACTORSTATIC_FILEWRITEERR_DISKFULL|Error al intentar abrir el archivo para escribir en él porque el disco está lleno.|  
|0xC02090B9|-1071607623|DTS_E_TXAGG_SORTKEYGENFAILED|No se pudo generar un criterio de ordenación. Error: 0x%1!8.8X!. ComparisonFlags está habilitado y se produjo un error al generar un criterio de ordenación con LCMapString.|  
|0xC02090BA|-1071607622|DTS_E_TXCHARMAPLCMAPFAILED|La transformación no pudo asignar una cadena y devolvió el error 0x%1!8.8X!. Error de LCMapString.|  
|0xC02090BB|-1071607621|DTS_E_FILEOPENERR_FORREAD_FILENOTFOUND|Error al abrir el archivo "%1" para leerlo. No se encontró el archivo.|  
|0xC02090BC|-1071607620|DTS_E_TXFILEINSERTERSTATIC_FILEOPENERR_FORREAD_FILENOTFOUND|Error al abrir un archivo para leerlo. No se encontró el archivo.|  
|0xC02090BD|-1071607619|DTS_E_FILEOPENERR_FORREAD_PATHNOTFOUND|Error al abrir el archivo "%1" para leerlo. No se encuentra la ruta de acceso.|  
|0xC02090BE|-1071607618|DTS_E_TXFILEINSERTERSTATIC_FILEOPENERR_FORREAD_PATHNOTFOUND|Error al abrir un archivo para leerlo. No se encontró la ruta de acceso.|  
|0xC02090BF|-1071607617|DTS_E_FILEOPENERR_FORREAD_TOOMANYOPENFILES|Error al abrir el archivo "%1" para leerlo. Hay demasiados archivos abiertos.|  
|0xC02090C0|-1071607616|DTS_E_TXFILEINSERTERSTATIC_FILEOPENERR_FORREAD_TOOMANYOPENFILES|Error al abrir el archivo para leerlo. Hay demasiados archivos abiertos.|  
|0xC02090C1|-1071607615|DTS_E_FILEOPENERR_FORREAD_ACCESSDENIED|Error al intentar abrir el archivo "%1" para leerlo. Acceso denegado.|  
|0xC02090C2|-1071607614|DTS_E_TXFILEINSERTERSTATIC_FILEOPENERR_FORREAD_ACCESSDENIED|Error al abrir el archivo para leerlo. No tiene los permisos correctos.|  
|0xC02090C3|-1071607613|DTS_E_INSERTERINVALIDBOM|El valor de la marca de orden de bytes (BOM) del archivo "%1" es 0x%2!4.4X!, pero se esperaba el valor 0x%3!4.4X!. Se estableció la propiedad ExpectBOM para este archivo pero falta el valor BOM o no es válido.|  
|0xC02090C4|-1071607612|DTS_E_TXFILEINSERTERSTATIC_INSERTERINVALIDBOM|El valor de marca de orden de bytes (BOM) del archivo no es válido. Se estableció la propiedad ExpectBOM para este archivo pero falta el valor BOM o no es válido.|  
|0xC02090C5|-1071607611|DTS_E_NOCOMPONENTATTACHED|%1 no se ha adjuntado a un componente.  Es necesario adjuntar un componente.|  
|0xC02090C9|-1071607607|DTS_E_TXLOOKUP_INVALIDMAXMEMORYPROP|El valor de la propiedad personalizada %1 no es correcto.  Debería ser un número entre %2!d! y %3!I64d!.|  
|0xC02090CA|-1071607606|DTS_E_TXAGG_COMPFLAGS_BADAGGREGATIONTYPE|No se puede especificar la propiedad personalizada "%1" para el tipo de agregación seleccionado para esta columna. La propiedad personalizada de marcas de comparación solo puede especificarse para los tipos de agregación Group by y Count Distinct.|  
|0xC02090CB|-1071607605|DTS_E_TXAGG_COMPFLAGS_BADDATATYPE|La propiedad personalizada de marcas de comparación "%1" solo puede especificarse para columnas con los tipos de datos DT_STR o DT_WSTR.|  
|0xC02090CD|-1071607603|DTS_E_TXAGG_AGGREGATION_FAILURE|Error en la agregación en %1. Código de error: 0x%2!8.8X!.|  
|0xC02090CF|-1071607601|DTS_E_MAPPINGSETUPERROR|Error al configurar la asignación. %1|  
|0xC02090D0|-1071607600|DTS_E_XMLSRCUNABLETOREADXMLDATA|%1 no pudo leer los datos XML.|  
|0xC02090D1|-1071607599|DTS_E_XMLSRCUNABLETOGETXMLDATAVARIABLE|%1 no pudo obtener la variable especificada por la propiedad "%2".|  
|0xC02090D2|-1071607598|DTS_E_NODATATABLEMATCHROWID|%1 contiene RowsetID con un valor de %2 que no hace referencia a una tabla de datos del esquema.|  
|0xC02090D6|-1071607594|DTS_E_TXAGG_BADKEYSVALUE|La propiedad %1 debe estar vacía o tener como valor un número entre %2!u! y %3!u!. La propiedad Keys o CountDistinctKeys tiene un valor no válido. La propiedad debería tener como valor un número entre 0 y ULONG_MAX, ambos incluidos, o no estar establecida.|  
|0xC02090D7|-1071607593|DTS_E_TXAGG_TOOMANYKEYS|El componente de agregado encontró demasiadas combinaciones de claves distintas. No puede contener más de %1!u! valores de claves distintas. Hay más de ULONG_MAX valores de claves distintas en el área de trabajo principal.|  
|0xC02090D8|-1071607592|DTS_E_TXAGG_TOOMANYCOUNTDISTINCTVALUES|El componente de agregado encontró demasiados valores distintos al calcular la agregación Count Distinct. No puede contener más de %1!u! valores distintos. Al calcular la agregación Count Distinct se encontraron más de ULONG_MAX valores distintos.|  
|0xC02090D9|-1071607591|DTS_E_FAILEDTOWRITETOTHEFILENAMECOLUMN|Error al intentar escribir en la columna de nombre de archivo. Código de error: 0x%1!8.8X!.|  
|0xC02090DC|-1071607588|DTS_E_FAILEDTOFINDERRORCOLUMN|Se produjo un error, pero no se puede determinar la columna que provocó el error.|  
|0xC02090E3|-1071607581|DTS_E_TXLOOKUP_FAILEDUPGRADE_BAD_VERSION|No se pueden actualizar los metadatos de búsqueda de la versión %1!d! a %2!d!. La transformación de búsquedas no pudo actualizar el número de versión de metadatos existente en una llamada a PerformUpgrade().|  
|0xC02090E5|-1071607579|DTS_E_TERMEXTRACTIONORLOOKUP_NTEXTSPLITED|No se encuentra el límite final de una frase.|  
|0xC02090E6|-1071607578|DTS_E_TERMEXTRACTION_EXCEED_MAXWORDNUM|La transformación Extracción de términos no puede procesar el texto de entrada porque una de las frases del texto de entrada es demasiado larga. La frase está segmentada en varias frases.|  
|0xC02090E7|-1071607577|DTS_E_XMLSRCFAILEDTOCREATEREADER|%1 no pudo leer los datos XML. %2|  
|0xC02090F0|-1071607568|DTS_E_TXLOOKUP_REINITMETADATAFAILED|Error al llamar al método de transformación de búsquedas ReinitializeMetadata.|  
|0xC02090F1|-1071607567|DTS_E_TXLOOKUP_NOJOINS|La transformación de búsquedas debe contener al menos una columna de entrada combinada con una columna de referencia y no se ha especificado ninguna de las dos. Debe especificar al menos una columna de combinación.|  
|0xC02090F2|-1071607566|DTS_E_MANAGEDERR_BADFORMATSPECIFICATION|La cadena de mensaje expuesta por la infraestructura de errores administrados contiene una especificación de formato errónea. Código de error interno.|  
|0xC02090F3|-1071607565|DTS_E_MANAGEDERR_UNSUPPORTEDTYPE|Al dar formato a una cadena de mensaje mediante la infraestructura de errores administrados, se encontró un tipo de variante al que no se puede dar formato. Código de error interno.|  
|0xC02090F5|-1071607563|DTS_E_DATAREADERSRCUNABLETOPROCESSDATA|%1 no pudo procesar los datos. %2|  
|0xC02090F6|-1071607562|DTS_E_XMLSRCEMPTYPROPERTY|La propiedad "%1" de %2 estaba vacía.|  
|0xC02090F7|-1071607561|DTS_E_XMLSRCINVALIDOUTPUTNAME|Error al intentar crear una salida con el nombre "%1" para la tabla XML con la ruta de acceso "%2" porque el nombre no es válido.|  
|0xC02090F8|-1071607560|DTS_E_MGDSRC_OVERFLOW|El valor era demasiado grande para caber en %1.|  
|0xC02090F9|-1071607559|DTS_E_DATAREADERDESTUNABLETOPROCESSDATA|%1 no pudo procesar los datos.|  
|0xC02090FA|-1071607558|DTS_E_XMLSRC_INDUCEDTRANSFORMFAILUREONTRUNCATION|Error de "%1" debido a un truncamiento, y la disposición de filas de truncamiento de "%2" en "%3" especifica un error de truncamiento. Error de truncamiento en el objeto especificado del componente especificado.|  
|0xC02090FB|-1071607557|DTS_E_XMLSRC_INDUCEDTRANSFORMFAILUREONERROR|Error de "%1" a causa de un error con el código 0x%2!8.8X!. La disposición de filas de error de "%3" en "%4" especifica la anulación al producirse un error. Error en el objeto especificado del componente especificado.|  
|0xC0209291|-1071607151|DTS_E_SQLCEDESTSTATIC_FAILEDTOSETVALUES|El destino SQLCE no pudo establecer los valores de columna de la fila.|  
|0xC0209292|-1071607150|DTS_E_SQLCEDESTSTATIC_FAILEDTOINSERT|El destino SQLCE no pudo insertar la fila.|  
|0xC0209293|-1071607149|DTS_E_TXFUZZYLOOKUP_OLEDBERR_LOADCOLUMNMETADATA|Se encontró un error de OLEDB al cargar los metadatos de columna.|  
|0xC0209294|-1071607148|DTS_E_TXFUZZYLOOKUP_TOOFEWREFERENCECOLUMNS|Los metadatos de referencia de búsqueda contienen muy pocas columnas.|  
|0xC0209295|-1071607147|DTS_E_TXSCD_OLEDBERR_LOADCOLUMNMETADATA|Se encontró un error de OLEDB al cargar los metadatos de columna.|  
|0xC0209296|-1071607146|DTS_E_TXSCD_TOOFEWREFERENCECOLUMNS|Los metadatos de referencia de búsqueda contienen muy pocas columnas.|  
|0xC0209297|-1071607145|DTS_E_TXSCD_MALLOCERR_REFERENCECOLUMNINFO|No se puede asignar memoria.|  
|0xC0209298|-1071607144|DTS_E_TXSCD_MALLOCERR_BUFFCOL|No se puede asignar memoria.|  
|0xC0209299|-1071607143|DTS_E_TXSCD_MAINWORKSPACE_CREATEERR|No se ha podido crear el búfer de área de trabajo.|  
|0xC020929A|-1071607142|DTS_E_DTPXMLDOMCREATEERROR|No se puede crear una instancia del documento DOM XML. Compruebe si los binarios MSXML se han instalado y registrado correctamente.|  
|0xC020929B|-1071607141|DTS_E_DTPXMLDOMLOADERROR|No se pueden cargar datos XML en un DOM local para procesarlos.|  
|0xC020929C|-1071607140|DTS_E_RSTDESTBADVARIABLETYPE|El tipo de la variable en tiempo de ejecución "%1" no es correcto. El tipo de la variable en tiempo de ejecución debe ser Object.|  
|0xC020929E|-1071607138|DTS_E_XMLDATAREADERMULTIPLEINLINEXMLSCHEMASNOTSUPPORTED|El Adaptador de origen XML no pudo procesar los datos XML. No se admiten esquemas insertados múltiples.|  
|0xC020929F|-1071607137|DTS_E_XMLDATAREADERANYTYPENOTSUPPORTED|El Adaptador de origen XML no pudo procesar los datos XML. El contenido de un elemento no se puede declarar como anyType.|  
|0xC02092A0|-1071607136|DTS_E_XMLDATAREADERGROUPREFNOTSUPPORTED|El Adaptador de origen XML no pudo procesar los datos XML. El contenido de un elemento no puede contener una referencia (ref) a un grupo.|  
|0xC02092A1|-1071607135|DTS_E_XMLDATAREADERMIXEDCONTENTFORCOMPLEXTYPESNOTSUPPORTED|El Adaptador de origen XML no admite el modelo de contenido mixto en tipos complejos.|  
|0xC02092A2|-1071607134|DTS_E_XMLDATAREADERINLINESCHEMAFOUNDINSOURCEXML|El Adaptador de origen XML no pudo procesar los datos XML. Un esquema insertado debe ser el primer nodo secundario del documento de origen Xml.|  
|0xC02092A3|-1071607133|DTS_E_XMLDATAREADERNOINLINESCHEMAFOUND|El Adaptador de origen XML no pudo procesar los datos XML. No se encontró ningún esquema insertado en el XML de origen, pero la propiedad "UseInlineSchema" se estableció en True.|  
|0xC02092A4|-1071607132|DTS_E_CONNECTIONMANAGERTRANSACTEDANDRETAINEDINBULKINSERT|El componente no puede utilizar un administrador de conexiones que conserve su conexión en una transacción con carga rápida o inserción masiva.|  
|0xC02092A5|-1071607131|DTS_E_OUTPUTREDIRECTINTRANSACTIONNOTALLOWED|No se puede establecer el redireccionamiento de %1 en caso de error, mediante una conexión en una transacción.|  
|0xC02092A6|-1071607130|DTS_E_FOUNDORPHANEDEXTERNALMETADATACOLUMN|%1 no tiene una columna de entrada o de salida correspondiente.|  
|0xC02092A9|-1071607127|DTS_E_RAWDESTNOINPUTCOLUMNS|No hay ninguna columna seleccionada para escribirla en el archivo.|  
|0xC02092AA|-1071607126|DTS_E_RAWDESTBLOBDATATYPE|%1 tiene un tipo de datos no válido. Las columnas con los tipos de datos DT_IMAGE, DT_TEXT y DT_NTEXT no se pueden escribir en los archivos sin formato.|  
|0xC02092AB|-1071607125|DTS_E_RAWDESTWRONGEXTERNALMETADATAUSAGE|Este componente utiliza la recopilación de metadatos externos de forma incorrecta. El componente debería utilizar metadatos externos al anexar o truncar un archivo existente. De lo contrario, los metadatos externos no son necesarios.|  
|0xC02092AC|-1071607124|DTS_E_RAWDESTMAPPEDINPUTCOLUMN|%1 está asignado a una columna de metadatos externos con el id. %2!d!. Las columnas de entrada no deberían asignarse a columnas de metadatos externos cuando el valor seleccionado de la opción de escritura es Crear siempre.|  
|0xC02092AD|-1071607123|DTS_E_RAWFILECANTOPENFORMETADATA|No se puede abrir el archivo para leer los metadatos. Si el archivo no existe, y el componente ya ha definido los metadatos externos, se puede establecer el valor "False" para la propiedad "ValidateExternalMetadata" y se creará el archivo en tiempo de ejecución.|  
|0xC02092AE|-1071607122|DTS_E_FAILEDTOACCESSLOBCOLUMN|Error al tener acceso a los datos LOB desde el búfer de flujo de datos para la columna de origen de datos "%1" con el código de error 0x%2!8.8X!.|  
|0xC02092AF|-1071607121|DTS_E_XMLSRCUNABLETOPROCESSXMLDATA|%1 no pudo procesar los datos XML. %2|  
|0xC02092B0|-1071607120|DTS_E_XMLSRCSTATIC_UNABLETOPROCESSXMLDATA|El Adaptador de origen XML no pudo procesar los datos XML.|  
|0xC02092B1|-1071607119|DTS_E_RAWINVALIDACCESSMODE|El valor %1!d! no se reconoce como modo de acceso válido.|  
|0xC02092B2|-1071607118|DTS_E_INCOMPLETEDATASOURCECOLUMNFOUND|No está disponible toda la información de metadatos para la columna de origen de datos "%1".  Asegúrese de que la columna esté definida correctamente en el origen de datos.|  
|0xC02092B3|-1071607117|DTS_E_TXAUDIT_ONLYSTRINGLENGTHCHANGEALLOWED|Solo se puede modificar la longitud de las columnas Nombre de usuario, Nombre del paquete, Nombre de tarea y Nombre del equipo.  Toda la demás información de tipo de datos de columna de auditoría es de solo lectura.|  
|0xC02092B4|-1071607116|DTS_E_ROWSETUNAVAILABLE|El proveedor OLE DB no ha devuelto un conjunto de filas basado en el comando SQL.|  
|0xC02092B5|-1071607115|DTS_E_COMMITFAILED|Error de confirmación.|  
|0xC02092B6|-1071607114|DTS_E_USEBINARYFORMATREQUIRESANSIFILE|La propiedad personalizada "%1" de %2 solo se puede utilizar con archivos ANSI.|  
|0xC02092B7|-1071607113|DTS_E_USEBINARYFORMATREQUIRESBYTES|La propiedad personalizada "%1" de %2 solo se puede utilizar con DT_BYTES.|  
|0xC0209302|-1071607038|DTS_E_OLEDB_NOPROVIDER_ERROR|Código de error SSIS DTS_E_OLEDB_NOPROVIDER_ERROR.  El proveedor OLE DB solicitado %2 no está registrado. Código de error: 0x%1!8.8X!.|  
|0xC0209303|-1071607037|DTS_E_OLEDB_NOPROVIDER_64BIT_ERROR|Código de error SSIS DTS_E_OLEDB_NOPROVIDER_64BIT_ERROR.  El proveedor OLE DB solicitado %2 no está registrado; es posible que no haya ningún proveedor de 64 bits disponible.  Código de error: 0x%1!8.8X!.|  
|0xC0209306|-1071607034|DTS_E_MULTICACHECOLMAPPINGS|La columna de caché, "%1", está asignada a varias columnas. Quite las asignaciones de columna duplicadas.|  
|0xC0209307|-1071607033|DTS_E_COLNOTMAPPEDTOCACHECOL|%1 no está asignada a una columna de caché válida.|  
|0xC0209308|-1071607032|DTS_E_CACHECOLDATATYPEINCOMPAT|No se puede asignar la columna de entrada, %1, y la columna de caché, "%2", porque los tipos de datos no coinciden.|  
|0xC0209309|-1071607031|DTS_E_INCORRECTINPUTCACHECOLCOUNT|El mismo número de columnas de entrada no coincide con el número de columnas de caché.|  
|0xC020930A|-1071607030|DTS_E_INVALIDCACHEFILENAME|No se ha especificado el nombre de archivo caché o el nombre especificado no es válido. Proporcione un nombre de archivo caché válido.|  
|0xC020930B|-1071607029|DTS_E_CACHECOLINDEXPOSMISMATCH|La posición del índice de la columna, "%1", es diferente de la posición del índice de la columna del administrador de conexiones de caché, "%2".|  
|0xC020930C|-1071607028|DTS_E_FAILEDTOLOADCACHE|Error al cargar la caché del archivo, "%1".|  
|0xC020930D|-1071607027|DTS_E_TXLOOKUP_REFCOLUMNISNOTINDEX|La columna de entrada de búsqueda %1 hace referencia a una columna de caché que no es de índice %2.|  
|0xC020930E|-1071607026|DTS_E_FAILEDTOGETCONNECTIONSTRING|Error al obtener la cadena de conexión.|  
|0xC020930F|-1071607025|DTS_E_CACHECOLDATATYPEPROPINCOMPAT|No se puede asignar la columna de entrada, "%1", y la columna de caché, "%2", porque una o más propiedades de tipo de datos no coinciden.|  
|0xC0209311|-1071607023|DTS_E_CACHECOLUMNOTFOUND|No se encontró la columna de caché "%1" en la caché.|  
|0xC0209312|-1071607022|DTS_E_CACHECOLUMNMAPPINGFAILED|Error al asignar %1 a una columna de caché. El código de hresult es 0x%2!8.8X!.|  
|0xC0209313|-1071607021|DTS_E_CACHELOADEDFROMFILE|%1 no puede escribir en la caché porque %2 ha cargado la caché desde un archivo.|  
|0xC0209314|-1071607020|DTS_E_CACHERELOADEDDIFFERENTFILES|%1 no puede cargar la caché desde el archivo "%2" porque la caché ya se ha cargado desde el archivo "%3".|  
|0xC0209316|-1071607018|DTS_E_OUTPUTNOTUSED|Ningún componente utiliza la salida con el id. %1!d! de componente de agregado. Elimínela o asóciela con la salida de algún componente.|  
|0xC0209317|-1071607017|DTS_E_CACHEFILEWRITEFAILED|%1 no pudo escribir la caché en el archivo "%2". El código de hresult es 0x%3!8.8X!.|  
|0xC0209318|-1071607016|DTS_E_XMLDATATYPECHANGED|Ha cambiado la información de tipo de datos del esquema XML para "%1" en el elemento "%2".  Reinicialice los metadatos para este componente y revise las asignaciones de columna.|  
|0xC0209319|-1071607015|DTS_E_TXLOOKUP_UNUSEDINPUTCOLUMN|%1 no se utiliza en combinación o copia. Elimine la columna no utilizada de la lista de columnas de salida.|  
|0xC020931A|-1071607014|DTS_E_SORTSTACKOVERFLOW|Se produjo un error en la ordenación debido a un desbordamiento de la pila mientras se ordenaba un búfer de entrada.  Reduzca la propiedad DefaultBufferMaxRows en la tarea Flujo de datos.|  
|0xC020F42A|-1071582166|DTS_E_OLEDB_OLDPROVIDER_ERROR|Considere la posibilidad de cambiar el valor de PROVIDER en la cadena de conexión por %1 o visite http://www.microsoft.com/downloads para buscar e instalar compatibilidad para %2.|  
|||DTS_E_INITTASKOBJECTFAILED|Error al inicializar el objeto de la tarea "%1!s!", tipo "%2!s!" debido al error 0x%3!8.8X! "%4!s!".|  
|||DTS_E_GETCATMANAGERFAILED|Error al crear el administrador de categorías del componente COM debido al error 0x%1!8.8X! "%2!s!".|  
|||DTS_E_COMPONENTINITFAILED|Componente %1!s! no se pudo inicializar debido al error 0x%2!8.8X! "%3!s!".|  
  
##  <a name="msgWarning"></a> Mensajes de advertencia  
 Los nombres simbólicos de los mensajes de advertencia de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] comienzan con `DTS_W_`.  
  
|Código hexadecimal|Código decimal|Nombre simbólico|Descripción|  
|----------------------|------------------|-------------------|-----------------|  
|0x80000036|-2147483594|DTS_W_COUNTDOWN|La evaluación expirará en %1!lu! días. Cuando expire, no podrán ejecutarse los paquetes.|  
|0x80010015|-2147418091|DTS_W_GENERICWARNING|Se han producido advertencias. Debe haber más advertencias específicas anteriores donde se expliquen los detalles de estas advertencias.|  
|0x80012010|-2147409904|DTS_W_FAILEDXMLDOCCREATION|No se puede crear una instancia de objeto de documento XML. Compruebe que MSXML se ha instalado y registrado correctamente.|  
|0x80012011|-2147409903|DTS_W_FAILEDCONFIGLOAD|No se puede cargar el archivo de configuración XML. Es posible que sea incorrecto o que no sea válido.|  
|0x80012012|-2147409902|DTS_W_CONFIGFILENAMEINVALID|El nombre de archivo de configuración "%1" no es válido. Compruebe el nombre del archivo de configuración.|  
|0x80012013|-2147409901|DTS_W_CONFIGFILEINVALID|Se cargó el archivo de configuración, pero no es válido. El archivo no tiene el formato correcto, puede estar dañado o faltarle un elemento.|  
|0x80012014|-2147409900|DTS_W_CONFIGFILENOTFOUND|No se encuentra el archivo de configuración "%1". Compruebe el directorio y el nombre de archivo.|  
|0x80012015|-2147409899|DTS_W_CONFIGKEYNOTFOUND|No se encontró la clave del Registro de configuración "%1". Hay una entrada de configuración referida a una clave del Registro no disponible. Compruebe el Registro para asegurarse de que contiene la clave.|  
|0x80012016|-2147409898|DTS_W_CONFIGTYPEINVALID|El tipo de configuración de una de las entradas de configuración no es válido. Los tipos válidos son los de la enumeración DTSConfigurationType.|  
|0x80012017|-2147409897|DTS_W_CANNOTFINDOBJECT|La ruta de acceso del paquete hizo referencia a un objeto que no se encuentra: "%1". Esto sucede si se intenta resolver una ruta de acceso del paquete de un objeto que no se encuentra.|  
|0x80012018|-2147409896|DTS_W_CONFIGFORMATINVALID_PACKAGEDELIMITER|La entrada de configuración "%1" tiene un formato incorrecto porque no comienza por un delimitador de paquete. Agregue el prefijo "\package" a la ruta del paquete.|  
|0x80012019|-2147409895|DTS_W_CONFIGFORMATINVALID|El formato de la entrada de configuración "%1" no es correcto. Es posible que falte un delimitador o que haya errores de formato, por ejemplo, un delimitador de matriz no válido.|  
|0x8001201A|-2147409894|DTS_W_NOPARENTVARIABLES|No se pudo configurar a partir de una variable primaria "%1" porque no había ninguna colección de variables primarias.|  
|0x8001201B|-2147409893|DTS_W_CONFIGFILEFAILEDIMPORT|Error al importar el archivo de configuración: "%1".|  
|0x8001201C|-2147409892|DTS_W_PARENTVARIABLENOTFOUND|No se pudo configurar a partir de una variable primaria "%1" porque no había ninguna variable primaria. Código de error: 0x%2!8.8X!.|  
|0x8001201D|-2147409891|DTS_W_CONFIGFILEEMPTY|El archivo de configuración estaba vacío y no contenía ninguna entrada de configuración.|  
|0x80012023|-2147409885|DTS_W_INVALIDCONFIGURATIONTYPE|El tipo de configuración de "%1" no es válido. Puede suceder si se intenta establecer un tipo de configuración no válido en la propiedad Type de un objeto de configuración.|  
|0x80012025|-2147409883|DTS_W_REGISTRYCONFIGURATIONTYPENOTFOUND|No se encontró en la clave "%1" el tipo de configuración para el Registro. Agregue un valor ConfigType a la clave del Registro y asígnele el valor de cadena "Variable", "Property", "ConnectionManager", "LoggingProvider" o "ForEachEnumerator".|  
|0x80012026|-2147409882|DTS_W_REGISTRYCONFIGURATIONVALUENOTFOUND|No se encontró en la clave "%1" el valor de configuración para el Registro. Agregue un valor Value a la clave del Registro de tipo DWORD o String.|  
|0x80012028|-2147409880|DTS_W_PROCESSCONFIGURATIONFAILEDSET|En la configuración del proceso no se pudo establecer como destino la ruta de acceso del paquete de "%1". Esto sucede si no se puede establecer la variable o propiedad de destino. Compruebe la variable o propiedad de destino.|  
|0x80012032|-2147409870|DTS_W_CONFIGUREDVALUESECTIONEMPTY|Error al recuperar el valor del archivo .ini. La sección ConfiguredValue está vacía o no existe: "%1".|  
|0x80012033|-2147409869|DTS_W_CONFIGUREDTYPESECTIONEMPTY|Error al recuperar el valor del archivo .ini. La sección ConfiguredType está vacía o no existe: "%1".|  
|0x80012034|-2147409868|DTS_W_PACKAGEPATHSECTIONEMPTY|Error al recuperar el valor del archivo .ini. La sección PackagePath está vacía o no existe: "%1".|  
|0x80012035|-2147409867|DTS_W_CONFIGUREDVALUETYPE|Error al recuperar el valor del archivo .ini. La sección ConfiguredValueType está vacía o no existe: "%1".|  
|0x80012051|-2147409839|DTS_W_SQLSERVERFAILEDIMPORT|La configuración de SQL Server no se importó correctamente: "%1".|  
|0x80012052|-2147409838|DTS_W_INICONFIGURATIONPROBLEM|El archivo de configuración .ini no es válido porque faltan campos o están vacíos.|  
|0x80012054|-2147409836|DTS_W_NORECORDSFOUNDINTABLE|La tabla "%1" no contiene registros de configuración. Esto sucede si se configura a partir de una tabla de SQL Server que no tiene registros de configuración.|  
|0x80012055|-2147409835|DTS_W_DUPLICATECUSTOMEVENT|Error al utilizar el mismo nombre en distintos eventos personalizados. Diversos elementos secundarios de este contenedor definieron de forma diferente el evento personalizado "%1". Es posible que haya un error al ejecutar el controlador de eventos.|  
|0x80012057|-2147409833|DTS_W_CONFIGREADONLYVARIABLE|La configuración intentó cambiar una variable de solo lectura. La variable se encuentra en la ruta de acceso del paquete "%1".|  
|0x80012058|-2147409832|DTS_W_CONFIGPROCESSCONFIGURATIONFAILED|Error al llamar a ProcessConfiguration en el paquete. La configuración intentó cambiar la propiedad en la ruta de acceso del paquete "%1".|  
|0x80012059|-2147409831|DTS_W_ONEORMORECONFIGLOADFAILED|Error al cargar al menos una de las entradas de configuración del paquete. Compruebe las entradas de configuración de "%1" y las advertencias anteriores para ver una descripción de los errores de configuración.|  
|0x8001205A|-2147409830|DTS_W_CONFIGNODEINVALID|Entrada de configuración "%1" no válida en el archivo de configuración o error al configurar la variable.  El nombre indica la entrada errónea. En algunos casos no se proporciona el nombre.|  
|0x80014058|-2147401640|DTS_W_FAILURENOTRESTARTABLE|Error en esta tarea o contenedor; el paquete continuará porque el valor de la propiedad FailPackageOnFailure es FALSE. Esta advertencia se expone cuando el valor de la propiedad SaveCheckpoints del paquete es TRUE y hay un error en la tarea o el contenedor.|  
|0x80017101|-2147389183|DTS_W_EMPTYPATH|La ruta de acceso está vacía.|  
|0x80019002|-2147381246|DTS_W_MAXIMUMERRORCOUNTREACHED|Código de error SSIS DTS_W_MAXIMUMERRORCOUNTREACHED.  El método Execution se ejecutó correctamente pero el número de errores (%1!d!) alcanzó el máximo permitido (%2!d!) y se produjo un error. Esto sucede si el número de errores alcanza el número especificado en MaximumErrorCount. Cambie el valor de MaximumErrorCount o corrija los errores.|  
|0x80019003|-2147381245|DTS_W_CONFIGENVVARNOTFOUND|No se encontró la variable de entorno de configuración.  La variable de entorno era "%1". Esto sucede si un paquete especifica una variable de entorno para un valor de configuración pero no se encuentra. Compruebe la colección de valores de configuración del paquete y compruebe que la variable de entorno especificada es válida y está disponible.|  
|0x80019316|-2147380458|DTS_W_CONNECTIONPROVIDERCHANGE|El nombre de proveedor del administrador de conexiones "%1" ha cambiado de "%2" a "%3".|  
|0x80019317|-2147380457|DTS_W_READEXTMAPFAILED|Se produjo una excepción al leer los archivos de asignación de actualizaciones. La excepción es "%1".|  
|0x80019318|-2147380456|DTS_W_DUPLICATEMAPPINGKEY|Hay una asignación duplicada en el archivo, "%1". La etiqueta es "%2", y la clave es "%3".|  
|0x80019319|-2147380455|DTS_W_IMPLICITUPGRADEMAPPING|La extensión, "%1", se actualizó implícitamente a "%2". Agregue una asignación para esta extensión en el directorio UpgradeMappings.|  
|0x8001931A|-2147380454|DTS_W_INVALIDEXTENSIONMAPPING|Una asignación del archivo, "%1", no es válida. Los valores no pueden ser null ni estar vacíos. La etiqueta es "%2", la clave es "%3" y el valor es "%4".|  
|0x8001931C|-2147380452|DTS_W_ADOCONNECTIONDATATYPECOMPATCHANGE|La propiedad DataTypeCompatibility del administrador de conexiones de tipo ADO "%1"se estableció en 80 por las razones de compatibilidad con versiones anteriores.|  
|0x8001C004|-2147368956|DTS_W_FILEENUMEMPTY|El enumerador Foreach File está vacío. El enumerador Foreach File no encontró ningún archivo coincidente con el patrón de archivo o el directorio especificado estaba vacío.|  
|0x8001F02F|-2147356625|DTS_W_COULDNOTRESOLVEPACKAGEPATH|No se puede resolver la ruta de acceso de un paquete a un objeto del paquete "%1". Compruebe si la ruta de acceso del paquete es válida.|  
|0x8001F203|-2147356157|DTS_W_ITERATIONEXPRESSIONISNOTASSIGNMENT|La expresión de iteración no es de asignación: "%1". Este error suele producirse si la expresión de ForLoop no es de asignación.|  
|0x8001F204|-2147356156|DTS_W_INITIALIZATIONEXPRESSIONISNOTASSIGNMENT|La expresión de inicialización no es de asignación: "%1". Este error suele producirse si la expresión que hay en las expresiones de iteración de ForLoop no es de asignación.|  
|0x8001F205|-2147356155|DTS_W_LOGPROVIDERNOTDEFINED|El ejecutable "%1" se pegó correctamente. Sin embargo, no se encontró en la colección "LogProviders" el proveedor de registro asociado al ejecutable.  El ejecutable se pegó sin la información del proveedor de registro.|  
|0x8001F300|-2147355904|DTS_W_PACKAGEUPGRADED|Actualización correcta del paquete.|  
|0x8001F42B|-2147355605|DTS_W_LEGACYPROGID|El ProgID "%1" está obsoleto. Debe utilizarse en su lugar el nuevo ProgID de este componente "%2".|  
|0x80020918|-2147350248|DTS_W_FTPTASK_OPERATIONFAILURE|No se pudo realizar la operación "%1".|  
|0x800283A5|-2147318875|DTS_W_MSMQTASK_USE_WEAK_ENCRYPTION|El algoritmo de cifrado "%1" usa cifrado débil.|  
|0x80029164|-2147315356|DTS_W_FSTASK_OPERATIONFAILURE|La tarea no pudo ejecutar la operación "%1".|  
|0x80029185|-2147315323|DTS_W_EXECPROCTASK_FILENOTINPATH|El archivo o proceso "%1" no se encuentra en la ruta de acceso.|  
|0x800291C6|-2147315258|DTS_W_SENDMAILTASK_SUBJECT_MISSING|El asunto está vacío.|  
|0x800291C7|-2147315257|DTS_W_SENDMAILTASK_ERROR_IN_TO_LINE|La dirección de la línea "Para" es incorrecta. Falta el símbolo "\@" o no es válida.|  
|0x800291C8|-2147315256|DTS_W_SENDMAILTASK_AT_MISSING_IN_FROM|La dirección de la línea "De" es incorrecta. Falta el símbolo "\@" o no es válida.|  
|0x8002927A|-2147315078|DTS_W_XMLTASK_DIFFFAILURE|Los dos documentos XML son diferentes.|  
|0x8002928C|-2147315060|DTS_W_XMLTASK_DTDVALIDATIONWARNING|La validación DTD utilizará el archivo DTD definido en la línea DOCTYPE del documento XML. No utilizará lo asignado a la propiedad "%1".|  
|0x8002928D|-2147315059|DTS_W_XMLTASK_VALIDATIONFAILURE|Error al validar la tarea "%1".|  
|0x80029291|-2147315055|DTS_W_TRANSFERDBTASK_ACTIONSETTOCOPY|El valor de la acción de transferencia no era válido.  Se está estableciendo para copiar.|  
|0x80029292|-2147315054|DTS_W_TRANSFERDBTASK_METHODSETTOONLINE|El valor del método de transferencia no era válido.  Se está estableciendo para una transferencia en línea.|  
|0x8002F304|-2147290364|DTS_W_PROBLEMOCCURREDWITHFOLLOWINGMESSAGE|Problema con los mensajes siguientes: "%1".|  
|0x8002F322|-2147290334|DTS_W_ERRMSGTASK_ERRORMESSAGEALREADYEXISTS|El mensaje de error "%1" ya existe en el servidor de destino.|  
|0x8002F331|-2147290319|DTS_W_JOBSTASK_JOBEXISTSATDEST|El trabajo "%1" ya existe en el servidor de destino.|  
|0x8002F332|-2147290318|DTS_W_JOBSTASK_SKIPPINGJOBEXISTSATDEST|Omitiendo la transferencia del trabajo "%1" porque ya existe en el destino.|  
|0x8002F333|-2147290317|DTS_W_JOBSTASK_OVERWRITINGJOB|Sobrescribiendo el trabajo "%1" en el servidor de destino.|  
|0x8002F339|-2147290311|DTS_W_LOGINSTASK_ENUMVALUEINCORRECT|Ha cambiado el valor de enumeración almacenado de la propiedad "FailIfExists", por lo que ya no es válida. Restableciendo el valor predeterminado.|  
|0x8002F343|-2147290301|DTS_W_LOGINSTASK_OVERWRITINGLOGINATDEST|Sobrescribiendo el inicio de sesión "%1" en el destino.|  
|0x8002F356|-2147290282|DTS_W_TRANSOBJECTSTASK_SPALREADYATDEST|El procedimiento almacenado "%1" ya existe en el destino.|  
|0x8002F360|-2147290272|DTS_W_TRANSOBJECTSTASK_RULEALREADYATDEST|La regla "%1" ya existe en el destino.|  
|0x8002F364|-2147290268|DTS_W_TRANSOBJECTSTASK_TABLEALREADYATDEST|La tabla "%1" ya existe en el destino.|  
|0x8002F368|-2147290264|DTS_W_TRANSOBJECTSTASK_VIEWALREADYATDEST|La vista "%1" ya existe en el destino.|  
|0x8002F372|-2147290254|DTS_W_TRANSOBJECTSTASK_UDFALREADYATDEST|La función definida por el usuario "%1" ya existe en el destino.|  
|0x8002F376|-2147290250|DTS_W_TRANSOBJECTSTASK_DEFAULTALREADYATDEST|El valor predeterminado "%1" ya existe en el destino.|  
|0x8002F380|-2147290240|DTS_W_TRANSOBJECTSTASK_UDDTALREADYATDEST|El tipo de datos definido por el usuario "%1" ya existe en el destino.|  
|0x8002F384|-2147290236|DTS_W_TRANSOBJECTSTASK_PFALREADYATDEST|La función de partición "%1" ya existe en el destino.|  
|0x8002F388|-2147290232|DTS_W_TRANSOBJECTSTASK_PSALREADYATDEST|El esquema de partición "%1" ya existe en el destino.|  
|0x8002F391|-2147290223|DTS_W_TRANSOBJECTSTASK_SCHEMAALREADYATDEST|El esquema "%1" ya existe en el destino.|  
|0x8002F396|-2147290218|DTS_W_TRANSOBJECTSTASK_SQLASSEMBLYALREADYATDEST|SqlAssembly "%1" ya existe en el destino.|  
|0x8002F400|-2147290112|DTS_W_TRANSOBJECTSTASK_AGGREGATEALREADYATDEST|El agregado definido por el usuario "%1" ya existe en el destino.|  
|0x8002F404|-2147290108|DTS_W_TRANSOBJECTSTASK_TYPEALREADYATDEST|El tipo definido por el usuario "%1" ya existe en el destino.|  
|0x8002F408|-2147290104|DTS_W_TRANSOBJECTSTASK_XMLSCHEMACOLLECTIONALREADYATDEST|XmlSchemaCollection "%1" ya existe en el destino.|  
|0x8002F412|-2147290094|DTS_W_TRANSOBJECTSTASK_NOELEMENTSPECIFIEDTOTRANSFER|No hay ningún elemento especificado para transferir.|  
|0x8002F415|-2147290091|DTS_W_TRANSOBJECTSTASK_LOGINALREADYATDEST|El inicio de sesión "%1" ya existe en el destino.|  
|0x8002F41A|-2147290086|DTS_W_TRANSOBJECTSTASK_USERALREADYATDEST|La usuario "%1" ya existe en el destino.|  
|0x80047007|-2147192825|DTS_W_NOLINEAGEVALIDATION|No se pueden validar los Id. de linaje de las columnas de entrada porque los árboles de ejecución contienen ciclos.|  
|0x80047034|-2147192780|DTS_W_EMPTYDATAFLOW|La tarea DataFlow no tiene componentes. Agregue componentes o quite la tarea.|  
|0x80047069|-2147192727|DTS_W_SORTEDOUTPUTHASNOSORTKEYPOSITIONS|El valor de la propiedad IsSorted de %1 es TRUE, pero todos los valores SortKeyPositions de sus columnas de salida son cero.|  
|0x8004706F|-2147192721|DTS_W_SOURCEREMOVED|No se leerá el origen "%1" (%2!d!) porque ninguno de sus datos puede verse fuera de la tarea Flujo de datos.|  
|0x80047076|-2147192714|DTS_W_UNUSEDOUTPUTDATA|La columna de salida "%1" (%2!d!) de la salida "%3" (%4!d!) y el componente "%5" (%6!d!) no se utilizará posteriormente en la tarea Flujo de datos. Si se quita esta columna de salida que no se utiliza, se aumentará el rendimiento de la tarea Flujo de datos.|  
|0x800470AE|-2147192658|DTS_W_COMPONENTREMOVED|Se ha quitado el componente "%1" (%2!d!) de la tarea Flujo de datos porque no se utiliza su salida y sus entradas no tienen efectos secundarios o no están conectadas a las salidas de otros componentes. Si se necesita el componente, debe establecerse el valor True en la propiedad HasSideEffects de al menos una de las entradas, o bien debe conectarse la salida.|  
|0x800470B0|-2147192656|DTS_W_NOWORKTODO|Se asignó un subproceso a las filas, pero el subproceso no realiza ningún trabajo. El diseño tiene una salida desconectada. Para evitar esta advertencia y acelerar el proceso, ejecute la canalización con la propiedad RunInOptimizedMode establecida en TRUE. ¡|  
|0x800470C8|-2147192632|DTS_W_EXTERNALMETADATACOLUMNSOUTOFSYNC|Las columnas externas para %1 no están sincronizadas con las columnas de orígenes de datos. %2|  
|0x800470C9|-2147192631|DTS_W_EXTERNALMETADATACOLUMNCOLLECTIONNEEDSADDITION|Es necesario agregar la columna "%1" a la colección de columnas externas.|  
|0x800470CA|-2147192630|DTS_W_EXTERNALMETADATACOLUMNCOLLECTIONNEEDSUPDATE|Es necesario actualizar la columna "%1".|  
|0x800470CB|-2147192629|DTS_W_EXTERNALMETADATACOLUMNCOLLECTIONNEEDSREMOVAL|Es necesario quitar %1 de las columnas externas.|  
|0x800470D8|-2147192616|DTS_W_EXPREVALPOTENTIALSTRINGTRUNCATION|La cadena de resultado de la expresión "%1" puede truncarse si supera la longitud máxima de %2!d! caracteres. La expresión podría tener un valor de resultado superior al tamaño máximo de un DT_WSTR.|  
|0x800470E9|-2147192599|DTS_W_COMPONENTLEAKPROCESSINPUT|Una llamada al método ProcessInput de la entrada %1!d! en %2 conservó de forma inesperada una referencia al búfer al que se pasó. El recuento de referencias en dicho búfer era %3!d! antes de la llamada y %4!d! tras devolver la llamada.|  
|0x800470EB|-2147192597|DTS_W_EXPREVALUNREFERENCEDINPUTCOLUMN|"%1" en "%2" tiene el tipo de uso READONLY, pero ninguna expresión le hace referencia. Quite la columna de la lista de columnas de entrada disponibles, o hágale referencia en una expresión.|  
|0x8004801E|-2147188706|DTS_W_COULDNOTFINDCURRENTVERSION|No se encuentra el valor "%1" del componente %2. No se encuentra el valor CurrentVersion del componente. Este error se produce si el componente no ha establecido la información del Registro de forma que contenga un valor CurrentVersion en la sección DTSInfo. Este mensaje aparece durante el desarrollo de componentes o cuando se utiliza el componente en un paquete, si el componente no se ha registrado correctamente.|  
|0x80049300|-2147183872|DTS_W_BUFFERGETTEMPFILENAME|El administrador de búfer no pudo obtener un nombre de archivo temporal.|  
|0x80049301|-2147183871|DTS_W_UNUSABLETEMPORARYPATH|El administrador de búfer no pudo crear un archivo temporal en la ruta de acceso "%1". La ruta de acceso no volverá a tenerse en cuenta para su almacenamiento temporal.|  
|0x80049304|-2147183868|DTS_W_DF_PERFCOUNTERS_DISABLED|Advertencia: no se pudo abrir la memoria compartida global para comunicar con la DLL de rendimiento; los contadores de rendimiento del flujo de datos no están disponibles.  Para resolver este problema, ejecute el paquete como administrador o en la consola del sistema.|  
|0x8020200F|-2145378289|DTS_W_PARTIALROWFOUNDATENDOFFILE|Hay una fila parcial al final del archivo.|  
|0x8020202B|-2145378261|DTS_W_ENDOFFILEREACHWHILEREADINGHEADERROWS|Se alcanzó el final del archivo de datos mientras se leían las filas de encabezados. Asegúrese de que el delimitador de filas de encabezados y el número de filas de encabezados que se omitirán son correctos.|  
|0x80202066|-2145378202|DTS_W_CANTRETRIEVECODEPAGEFROMOLEDBPROVIDER|No se puede recuperar la información de página de códigos de columna del proveedor OLE DB.  Si el componente admite la propiedad "%1", se utilizará la página de códigos de dicha propiedad.  Cambie el valor de la propiedad si los valores de la página de códigos de la cadena actual no son correctos.  Si el componente no admite la propiedad, se utilizará la página de códigos del Id. de configuración regional del componente.|  
|0x802020F7|-2145378057|DTS_W_TXSORTSORTISTHESAME|Los datos ya se han ordenado del modo especificado; puede quitarse la transformación.|  
|0x8020400D|-2145370099|DTS_W_NOPIPELINEDATATYPEMAPPINGAVAILABLE|%1 hace referencia a un tipo de datos externo que no puede asignarse a un tipo de datos de la tarea Flujo de datos. En su lugar, se utilizará el tipo de datos DT_WSTR de la tarea Flujo de datos.|  
|0x802070CC|-2145357620|DTS_W_STATICTRUNCATIONINEXPRESSION|La expresión "%1" producirá siempre un truncamiento de datos. La expresión contiene un truncamiento estático (truncamiento de un valor fijo).|  
|0x8020820C|-2145353204|DTS_W_UNMAPPEDINPUTCOLUMN|No se ha asignado la columna de entrada "%1" con el id. %2!d! en el índice %3!d!. El Id. de linaje de la columna es cero.|  
|0x80208305|-2145352955|DTS_W_TXFUZZYLOOKUP_DELIMITERS_DONT_MATCH|Los delimitadores especificados no coinciden con los delimitadores que se utilizan para crear el índice de coincidencias "%1" preexistente. Este error se produce si los delimitadores que se utilizan para acortar campos no coinciden. Puede provocar efectos desconocidos en las coincidencias o en los resultados.|  
|0x80208308|-2145352952|DTS_W_TXFUZZYLOOKUP_MAXRESULTS_IS_ZERO|El valor de la propiedad MaxOutputMatchesPerInput en la transformación Búsqueda aproximada es cero. No se producirán resultados.|  
|0x80208310|-2145352944|DTS_W_TXFUZZYLOOKUP_NO_FUZZY_JOIN_COLUMNS|No hay ninguna columna de entrada válida con la propiedad de columna JoinType establecida en Aproximada.  El rendimiento de las combinaciones exactas puede mejorarse si se usa la transformación Búsqueda en lugar de la transformación Búsqueda aproximada.|  
|0x8020831C|-2145352932|DTS_W_TXFUZZYLOOKUP_TIMESTAMPCAVEAT|La columna de referencia "%1" puede ser una columna de marca de tiempo de SQL. Cuando se cree el índice de coincidencias aproximadas y una copia de la tabla de referencia, todas las marcas de tiempo de la tabla de referencia reflejarán el estado actual de la tabla en el momento de la copia. Puede producirse un comportamiento inesperado si se establece el valor False en CopyReferenceTable.|  
|0x80208321|-2145352927|DTS_W_MATCHINDEXALREADYEXISTS|Ya existe una tabla con el nombre '%1' asignado a MatchIndexName y DropExistingMatchIndex tiene el valor FALSE.  No se podrá ejecutar la transformación a menos que se quite la tabla, se especifique otro nombre o se establezca el valor TRUE a DropExisitingMatchIndex.|  
|0x8020832B|-2145352917|DTS_W_TXFUZZYLOOKUP_JOINLENGTHMISMATCH|La longitud de la columna de entrada '%1' no es igual a la longitud de la columna de referencia '%2' en la que se buscan coincidencias.|  
|0x8020832D|-2145352915|DTS_W_TXFUZZYLOOKUP_CODEPAGE_MISMATCH|Las páginas de códigos de la columna de origen DT_STR "%1" y la columna de destino DT_STR "%2" no coinciden.  Puede provocar resultados inesperados.|  
|0x8020832E|-2145352914|DTS_W_FUZZYLOOKUP_TOOMANYEXACTMATCHCOLUMNS|Hay más de 16 combinaciones de coincidencias exactas, de forma que es posible que el rendimiento no sea óptimo. Reduzca el número de combinaciones de coincidencias exactas para mejorar el rendimiento. SQL Server tiene un límite de 16 columnas por índice; el índice invertido se utilizará en todas las búsquedas.|  
|0x80208350|-2145352880|DTS_W_FUZZYLOOKUP_MEMLIMITANDEXHAUSTIVESPECIFIED|La opción Exhaustiva requiere que se cargue toda la referencia en la memoria principal.  Dado que se ha especificado un límite de memoria para la propiedad MaxMemoryUsage, es posible que toda la tabla de referencia no quepa dentro de este límite y que se produzca un error en tiempo de ejecución durante la operación de coincidencia.|  
|0x80208351|-2145352879|DTS_W_FUZZYLOOKUP_EXACTMATCHCOLUMNSEXCEEDBYTELIMIT|La longitud acumulada de las columnas especificadas en las combinaciones de coincidencias exactas supera el límite de 900 bytes para las claves de índice.  La búsqueda aproximada crea un índice en las columnas de coincidencias exactas para aumentar el rendimiento de la búsqueda y existe la posibilidad de que este índice no se cree correctamente y que la búsqueda retroceda a un método de búsqueda de coincidencias alternativo, posiblemente más lento. Si el rendimiento supone un problema, quite algunas columnas de combinaciones de coincidencias exactas o reduzca la longitud máxima de las columnas de coincidencias exactas de longitud variable.|  
|0x80208352|-2145352878|DTS_W_FUZZYLOOKUP_EXACTMATCHINDEXCREATIONFAILED|Error al crear un índice de columnas de coincidencias exactas. Revirtiendo al método alternativo de búsqueda aproximada.|  
|0x80208353|-2145352877|DTS_W_FUZZYGROUPINGINTERNALPIPELINEWARNING|La siguiente advertencia de canalización interna de agrupación aproximada produjo el código de error 0x%1!8.8X!: "%2".|  
|0x80208375|-2145352843|DTS_W_XMLSRCOUTPUTCOLUMNLENGTHSETTODEFAULT|No se especificó ninguna longitud máxima para %1 con el tipo de datos externo %2. Se utilizará el tipo de datos "%3" de la tarea Flujo de datos de SSIS con una longitud de %6!d!.|  
|0x80208376|-2145352842|DTS_W_XMLSRCOUTPUTCOLUMNDATATYPEMAPPEDTOSTRING|%1 hace referencia al tipo de datos externo %2, que no puede asignarse a un tipo de datos de la tarea Flujo de datos de SSIS.  Se utilizará el tipo de datos DT_WSTR de la tarea Flujo de datos de SSIS con una longitud de %4!d! en su lugar.|  
|0x80208385|-2145352827|DTS_W_NOREDIRECTWITHATTACHEDERROROUTPUTS|No se enviarán filas a los resultados de error. Configure las disposiciones de truncamiento o error para redirigir las filas a las salidas de error, o bien elimine los destinos o transformaciones de flujo de datos adjuntos a las salidas de error.|  
|0x80208386|-2145352826|DTS_W_REDIRECTWITHNOATTACHEDERROROUTPUTS|Se perderán las filas enviadas a las salidas de error. Agregue nuevos destinos o transformaciones de flujo de datos para recibir filas de error, o bien reconfigure el componente para dejar de redirigir filas a las salidas de error.|  
|0x80208391|-2145352815|DTS_W_XMLSRCOUTPUTCOLUMNLENGTHSETTOMAXIMUM|Para %1 con el tipo de datos externo %2, el esquema XML especificó una restricción maxLength de %3!d!, que supera la longitud de columna máxima permitida de %4!d!. Se utilizará el tipo de datos "%5" de la tarea Flujo de datos de SSIS con una longitud de %6!d!.|  
|0x802090E4|-2145349404|DTS_W_TXLOOKUP_DUPLICATE_KEYS|%1 encontró valores de clave de referencia duplicados al almacenar en caché los datos de referencia. Este error se produce solo en el modo de caché completa. Quite los valores de clave duplicados o cambie el modo de caché a PARTIAL o NO_CACHE.|  
|0x802092A7|-2145348953|DTS_W_POTENTIALTRUNCATIONFROMDATAINSERTION|Puede producirse un truncamiento debido a la inserción de datos de la columna de flujo de datos "%1" con una longitud de %2!d! en la columna de base de datos "%3" con una longitud de %4!d!.|  
|0x802092A8|-2145348952|DTS_W_POTENTIALTRUNCATIONFROMDATARETRIEVAL|Puede producirse un truncamiento debido a la recuperación de datos de la columna de base de datos "%1" con una longitud de %2!d! en la columna de flujo de datos "%3" con una longitud de %4!d!.|  
|0x802092AA|-2145348950|DTS_W_ADODESTBATCHNOTSUPPORTEDFORERRORDISPOSITION|Actualmente no se admite el modo por lotes cuando se usa la disposición de filas de errores. La propiedad BatchSize se establecerá en 1.|  
|0x802092AB|-2145348949|DTS_W_ADODESTNOROWSINSERTED|No se insertó correctamente ninguna línea en el destino. Puede deberse a que los tipos de datos entre columnas no coinciden o que se usa un tipo de datos no compatible con el proveedor ADO.NET. Puesto que la disposición de errores para este componente no es "Error de componente", aquí no se muestran mensajes de error; establezca la disposición de errores en "Error de componente" para ver aquí los mensajes de error.|  
|0x802092AC|-2145348948|DTS_W_ADODESTPOTENTIALDATALOSS|Pueden perderse datos si se insertan datos de la columna de entrada "%1" con el tipo de datos "%2" en la columna externa "%3" con el tipo de datos "%4". Si la intención es ésta, una forma alternativa de realizar la conversión consiste en usar un componente de conversión de datos antes que el componente de destino de ADO NET.|  
|0x802092AD|-2145348947|DTS_W_ADODESTEXTERNALCOLNOTMATCHSCHEMACOL|%1 no está sincronizado con la columna de base de datos.  La columna más reciente tiene %2. Use el editor avanzado para actualizar las columnas de destino disponibles si es necesario.|  
|0x802092AE|-2145348946|DTS_W_ADODESTEXTERNALCOLNOTEXIST|%1 no existe en la base de datos. Puede que se haya quitado o cambiado de nombre. Use el editor avanzado para actualizar las columnas de destino disponibles si es necesario.|  
|0x802092AF|-2145348945|DTS_W_ADODESTNEWEXTCOL|Se ha agregado una nueva columna con el nombre %1 a la tabla de base de datos externa. Use el editor avanzado para actualizar las columnas de destino disponibles si es necesario.|  
|0x8020930C|-2145348852|DTS_W_NOMATCHOUTPUTGETSNOROWS|No se envió ninguna fila a la salida de entradas no coincidentes. Configure la transformación para enviar las filas sin entradas coincidentes a la salida de entradas no coincidentes, o elimine las transformaciones del flujo de datos o los destinos adjuntos a la salida de entradas no coincidentes.|  
|0x8020931B|-2145348837|DTS_W_ADODESTINVARIANTEXCEPTION|Se recibió una excepción al enumerar los proveedores de ADO.Net. El nombre invariable era "%1". El mensaje de excepción es: %2|  
|0xC020822C|-1071611348|DTS_W_UNMAPPEDOUTPUTCOLUMN|No se ha asignado ninguna columna de entrada a %1.|  
|0x930D|37645|DTS_W_EXTERNALTABLECOLSOUTOFSYNC|La tabla "%1" ha cambiado. Es posible que se hayan agregado nuevas columnas a la tabla.|  
  
##  <a name="msgInfo"></a> Mensajes informativos  
 Los nombres simbólicos de los mensajes de informativos de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] comienzan con `DTS_I_`.  
  
|Código hexadecimal|Código decimal|Nombre simbólico|Descripción|  
|----------------------|------------------|-------------------|-----------------|  
|0x4001100A|1073811466|DTS_I_STARTINGTRANSACTION|Iniciando transacción distribuida para este contenedor.|  
|0x4001100B|1073811467|DTS_I_COMMITTINGTRANSACTION|Confirmando la transacción distribuida iniciada por este contenedor.|  
|0x4001100C|1073811468|DTS_I_ABORTINGTRANSACTION|Anulando la transacción distribuida actual.|  
|0x40013501|1073820929|DTS_I_GOTMUTEXFROMWAIT|Se adquirió correctamente la exclusión mutua "%1".|  
|0x40013502|1073820930|DTS_I_RELEASEACQUIREDMUTEX|Se liberó correctamente la exclusión mutua "%1".|  
|0x40013503|1073820931|DTS_I_NEWMUTEXCREATED|Se creó correctamente la exclusión mutua "%1".|  
|0x40015101|1073828097|DTS_I_DUMP_ON_ANY_ERR|Se generarán archivos de volcado de depuración para cualquier evento de error.|  
|0x40015102|1073828098|DTS_I_DUMP_ON_CODES|Se generarán archivos de volcado de depuración para los siguientes códigos de evento: "%1"|  
|0x40015103|1073828099|DTS_I_START_DUMP|El código de evento 0x%1!8.8X! desencadenó la generación de archivos de depuración de volcado en la carpeta "%2".|  
|0x40015104|1073828100|DTS_I_SSIS_INFO_DUMP|Creando archivo de volcado de información SSIS "%1".|  
|0x40015106|1073828102|DTS_I_FINISH_DUMP|Archivos de volcado de depuración creados correctamente.|  
|0x40016019|1073831961|DTS_I_PACKAGEMIGRATED|El formato de paquete se migró de la versión %1!d! a la versión %2!d!. Debe guardarse para conservar los cambios de migración.|  
|0x4001601A|1073831962|DTS_I_SCRIPTSMIGRATED|Los scripts del paquete se migraron correctamente. El paquete debe guardarse para retener los cambios de migración.|  
|0x40016025|1073831973|DTS_I_FTPRECEIVEFILE|Recibiendo el archivo "%1".|  
|0x40016026|1073831974|DTS_I_FTPSENDFILE|Enviando el archivo "%1".|  
|0x40016027|1073831975|DTS_I_FTPFILEEXISTS|El archivo "%1" ya existe.|  
|0x40016028|1073831976|DTS_I_FTPERRORLOADINGMSG|No se puede obtener información de error adicional debido a un error interno.|  
|0x40016036|1073831990|DTS_I_FTPDELETEFILE|Error al intentar eliminar el archivo "%1". Esto puede suceder si el archivo no existe, si la ortografía del nombre de archivo no es correcta o si no tiene permisos para eliminar el archivo.|  
|0x40016037|1073831991|DTS_I_CONFIGFROMREG|El paquete está intentando configurar desde una entrada del Registro mediante la clave del Registro "%1".|  
|0x40016038|1073831992|DTS_I_CONFIGFROMENVVAR|El paquete se está intentando configurar desde la variable de entorno "%1".|  
|0x40016039|1073831993|DTS_I_CONFIGFROMINIFILE|El paquete se está intentando configurar desde el archivo .ini "%1".|  
|0x40016040|1073832000|DTS_I_CONFIGFROMSQLSERVER|El paquete se está intentando configurar desde SQL Server mediante la cadena de configuración "%1".|  
|0x40016041|1073832001|DTS_I_CONFIGFROMFILE|El paquete se está intentando configurar desde el archivo XML "%1".|  
|0x40016042|1073832002|DTS_I_CONFIGFROMPARENTVARIABLE|El paquete se está intentando configurar desde la variable primaria "%1".|  
|0x40016043|1073832003|DTS_I_ATTEMPTINGUPGRADEOFDTS|Intentando actualizar el SSIS de la versión "%1" a la versión "%2". El paquete está intentando actualizar el objeto de tiempo de ejecución.|  
|0x40016044|1073832004|DTS_I_ATTEMPTINGUPGRADEOFANEXTOBJ|Intentando actualizar "%1". El paquete está intentando actualizar un objeto extensible.|  
|0x40016045|1073832005|DTS_I_SAVECHECKPOINTSTOFILE|El paquete guardará puntos de comprobación en el archivo "%1" durante la ejecución. El paquete está configurado para guardar puntos de comprobación.|  
|0x40016046|1073832006|DTS_I_RESTARTFROMCHECKPOINTFILE|Se reinició el paquete desde el archivo de punto de comprobación "%1". El paquete se configuró para reiniciarse desde el punto de comprobación.|  
|0x40016047|1073832007|DTS_I_CHECKPOINTSAVEDTOFILE|El archivo de punto de comprobación "%1" se actualizó para registrar la finalización de este contenedor.|  
|0x40016048|1073832008|DTS_I_CHECKPOINTFILEDELETED|El archivo de punto de comprobación "%1" se eliminó tras finalizar correctamente el paquete.|  
|0x40016049|1073832009|DTS_I_CHECKPOINTSAVINGTOFILE|Iniciando la actualización del archivo de punto de comprobación "%1".|  
|0x40016051|1073832017|DTS_I_CHOSENMAXEXECUTABLES|Según la configuración del sistema, el número máximo de ejecutables simultáneos es %1!d!.|  
|0x40016052|1073832018|DTS_I_MAXEXECUTABLES|El número máximo de ejecutables simultáneos establecido es %1!d!.|  
|0x40016053|1073832019|DTS_I_PACKAGESTART|Inicio de la ejecución del paquete.|  
|0x40016054|1073832020|DTS_I_PACKAGEEND|Fin de la ejecución del paquete.|  
|0x40029161|1073910113|DTS_I_FSTASK_DIRECTORYDELETED|Se eliminó el directorio "%1".|  
|0x40029162|1073910114|DTS_I_FSTASK_FILEDELETED|Se eliminó el archivo o directorio "%1".|  
|0x400292A8|1073910440|DTS_I_TRANSFERDBTASK_OVERWRITEDB|Sobrescribiendo la base de datos "%1" en el servidor de destino "%2".|  
|0x4002F304|1073935108|DTS_I_SOMETHINGHAPPENED|"%1".|  
|0x4002F323|1073935139|DTS_I_ERRMSGTASK_SKIPPINGERRORMESSAGEALREADYEXISTS|Omitiendo el mensaje de error "%1" porque ya existe en el servidor de destino.|  
|0x4002F326|1073935142|DTS_I_ERRMSGTASK_TRANSFEREDNERRORMESSAGES|Se transfirieron "%1" mensajes de error.|  
|0x4002F351|1073935185|DTS_I_STOREDPROCSTASKS_TRANSFEREDNSPS|La tarea ha transferido "%1" procedimientos almacenados.|  
|0x4002F352|1073935186|DTS_I_TRANSOBJECTSTASK_TRANSFEREDNOBJECTS|"%1" objetos transferidos.|  
|0x4002F358|1073935192|DTS_I_TRANSOBJECTSTASK_NOSPSTOTRANSFER|No hay procedimientos almacenados para transferir.|  
|0x4002F362|1073935202|DTS_I_TRANSOBJECTSTASK_NORULESTOTRANSFER|No hay reglas para transferir.|  
|0x4002F366|1073935206|DTS_I_TRANSOBJECTSTASK_NOTABLESTOTRANSFER|No hay tablas para transferir.|  
|0x4002F370|1073935216|DTS_I_TRANSOBJECTSTASK_NOVIEWSTOTRANSFER|No hay vistas para transferir.|  
|0x4002F374|1073935220|DTS_I_TRANSOBJECTSTASK_NOUDFSTOTRANSFER|No hay funciones definidas por el usuario para transferir.|  
|0x4002F378|1073935224|DTS_I_TRANSOBJECTSTASK_NODEFAULTSTOTRANSFER|No hay valores predeterminados para transferir.|  
|0x4002F382|1073935234|DTS_I_TRANSOBJECTSTASK_NOUDDTSTOTRANSFER|No hay tipos de datos definidos por el usuario para transferir.|  
|0x4002F386|1073935238|DTS_I_TRANSOBJECTSTASK_NOPFSTOTRANSFER|No hay funciones de partición para transferir.|  
|0x4002F390|1073935248|DTS_I_TRANSOBJECTSTASK_NOPSSTOTRANSFER|No hay esquemas de partición para transferir.|  
|0x4002F394|1073935252|DTS_I_TRANSOBJECTSTASK_NOSCHEMASTOTRANSFER|No hay esquemas para transferir.|  
|0x4002F398|1073935256|DTS_I_TRANSOBJECTSTASK_NOSQLASSEMBLIESTOTRANSFER|No hay SqlAssemblies para transferir.|  
|0x4002F402|1073935362|DTS_I_TRANSOBJECTSTASK_NOAGGREGATESTOTRANSFER|No hay agregados definidos por el usuario para transferir.|  
|0x4002F406|1073935366|DTS_I_TRANSOBJECTSTASK_NOTYPESTOTRANSFER|No hay tipos definidos por el usuario para transferir.|  
|0x4002F410|1073935376|DTS_I_TRANSOBJECTSTASK_NOXMLSCHEMACOLLECTIONSTOTRANSFER|No hay XmlSchemaCollections para transferir.|  
|0x4002F418|1073935384|DTS_I_TRANSOBJECTSTASK_NOLOGINSTOTRANSFER|No hay inicios de sesión para transferir.|  
|0x4002F41D|1073935389|DTS_I_TRANSOBJECTSTASK_NOUSERSTOTRANSFER|No hay usuarios para transferir.|  
|0x4002F41E|1073935390|DTS_I_TRANSOBJECTSTASK_TRUNCATINGTABLE|Truncando la tabla "%1"|  
|0x40043006|1074016262|DTS_I_EXECUTIONPHASE_PREPAREFOREXECUTE|Se está iniciando la fase de preparación de la ejecución.|  
|0x40043007|1074016263|DTS_I_EXECUTIONPHASE_PREEXECUTE|Se está iniciando la fase de ejecución previa.|  
|0x40043008|1074016264|DTS_I_EXECUTIONPHASE_POSTEXECUTE|Se está iniciando la fase de ejecución posterior.|  
|0x40043009|1074016265|DTS_I_EXECUTIONPHASE_CLEANUP|Se está iniciando la fase de limpieza.|  
|0x4004300A|1074016266|DTS_I_EXECUTIONPHASE_VALIDATE|Se está iniciando la fase de validación.|  
|0x4004300B|1074016267|DTS_I_ROWS_WRITTEN|"%1" ha escrito %2!ld! filas.|  
|0x4004300C|1074016268|DTS_I_EXECUTIONPHASE_EXECUTE|Se está iniciando la fase de ejecución.|  
|0x4004800C|1074036748|DTS_I_CANTRELIEVEPRESSURE|El administrador de búfer detectó que el sistema tenía poca memoria virtual pero no pudo intercambiar ningún búfer. Se tuvieron en cuenta %1!d! búferes y %2!d! estaban bloqueados. No había memoria suficiente en la canalización porque la instalada no era suficiente o la estaban utilizando otros procesos, o había demasiados búferes bloqueados.|  
|0x4004800D|1074036749|DTS_I_CANTALLOCATEMEMORYPRESSURE|El administrador de búfer no pudo realizar una llamada de asignación de memoria de %3!d! bytes y no pudo intercambiar ningún búfer para aliviar la presión de memoria. Se tuvieron en cuenta %1!d! búferes y %2!d! estaban bloqueados. No había memoria suficiente en la canalización porque la instalada no era suficiente o la estaban utilizando otros procesos, o había demasiados búferes bloqueados.|  
|0x4004800E|1074036750|DTS_I_ALLOCATEDDURINGMEMORYPRESSURE|El administrador de búfer ha asignado %1!d! bytes, aunque se ha detectado presión de memoria y ninguno de los intentos reiterados para intercambiar búferes se ha realizado correctamente.|  
|0x400490F4|1074041076|DTS_I_TXLOOKUP_CACHE_PROGRESS|%1 ha almacenado en la caché %2!d! filas.|  
|0x400490F5|1074041077|DTS_I_TXLOOKUP_CACHE_FINAL|%1 ha almacenado en la caché un total de %2!d! filas.|  
|0x4020206D|1075847277|DTS_I_RAWSOURCENOCOLUMNS|El adaptador de origen sin procesar abrió un archivo pero el archivo no contiene ninguna columna. El adaptador no producirá datos. Esto podría indicar que hay un archivo dañado o que hay cero columnas y, por lo tanto, no hay datos.|  
|0x402020DA|1075847386|DTS_I_OLEDBINFORMATIONALMESSAGE|Hay un mensaje de información de OLE DB disponible.|  
|0x40208327|1075872551|DTS_I_TXFUZZYLOOKUP_EXACT_MATCH_PERF_COLLATIONS_DONT_MATCH|Es posible mejorar el rendimiento de las coincidencias aproximadas si se establece una correspondencia entre la combinación exacta FuzzyComparisonFlags en la columna de entrada "%1" y la intercalación SQL predeterminada para la columna de tabla de referencia "%2".  También es necesario no establecer marcas de subconjuntos en FuzzyComparisonFlagsEx.|  
|0x40208328|1075872552|DTS_I_TXFUZZYLOOKUP_EXACT_MATCH_PERF_INDEX_MISSING|Es posible mejorar el rendimiento de las coincidencias aproximadas si se crea un índice sobre la tabla de referencia en todas las columnas de coincidencias exactas especificadas.|  
|0x40208387|1075872647|DTS_I_DISPSNOTREVIEWED|No se revisaron las disposiciones de truncamiento y error. Asegúrese de que este componente está configurado para redirigir filas a salidas de error, si desea seguir transformando dichas filas.|  
|0x402090DA|1075876058|DTS_I_TXAGG_WORKSPACE_REHASH|La transformación Agregado ha encontrado %1!d! combinaciones de claves. Debe volver a aplicar el algoritmo hash a los datos porque el número de combinaciones de claves es superior al esperado. Es posible configurar el componente para evitar tener que volver a aplicar el algoritmo hash a los datos, mediante el ajuste de las propiedades Keys, KeyScale y AutoExtendFactor.|  
|0x402090DB|1075876059|DTS_I_TXAGG_COUNTDISTINCT_REHASH|La transformación Agregado ha encontrado %1!d! valores distintos al ejecutar una agregación "Count Distinct" en "%2". La transformación volverá a aplicar el algoritmo hash a los datos porque el número de valores distintos es superior al esperado. Es posible configurar el componente para evitar tener que volver a aplicar el algoritmo hash a los datos, mediante el ajuste de las propiedades CountDistinctKeys, CountDistinctKeyScale y AutoExtendFactor.|  
|0x402090DC|1075876060|DTS_I_STARTPROCESSINGFILE|Se inició el procesamiento del archivo "%1".|  
|0x402090DD|1075876061|DTS_I_FINISHPROCESSINGFILE|Finalizó el procesamiento del archivo "%1".|  
|0x402090DE|1075876062|DTS_I_TOTALDATAROWSPROCESSEDFORFILE|El número total de filas de datos procesadas para el archivo "%1" es %2!I64d!.|  
|0x402090DF|1075876063|DTS_I_FINALCOMMITSTARTED|Se inició la confirmación final de la inserción de datos en "%1".|  
|0x402090E0|1075876064|DTS_I_FINALCOMMITENDED|Finalizó la confirmación final de la inserción de datos en "%1".|  
|0x402090E1|1075876065|DTS_I_BEGINHASHINGCACHE|Se agregaron %1!u! filas a la caché. El sistema está procesando las filas.|  
|0x402090E2|1075876066|DTS_I_SUCCEEDEDHASHINGCACHE|%1 procesó %2!u! filas en la caché. El tiempo de procesamiento fue de %3 segundos. La caché utilizó %4!I64u! bytes de memoria.|  
|0x402090E3|1075876067|DTS_I_FAILEDHASHINGCACHE|%1 no pudo procesar las filas en la caché.  El tiempo de procesamiento fue de %2 segundos.|  
|0x402090E4|1075876068|DTS_I_SUCCEEDEDPREPARINGCACHE|%1 logró preparar la caché correctamente. El tiempo de preparación fue de %2 segundos.|  
|0x40209314|1075876628|DTS_I_TXLOOKUP_PARTIALPERF|%1 ha realizado las siguientes operaciones: ha procesado %2!I64u! filas, ha emitido %3!I64u! comandos de base de datos en la base de datos de referencia y ha realizado %4!I64u! búsquedas usando la caché parcial.|  
|0x40209315|1075876629|DTS_I_TXLOOKUP_PARTIALPERF2|%1 ha realizado las siguientes operaciones: ha procesado %2!I64u! filas, ha emitido %3!I64u! comandos de base de datos en la base de datos de referencia, ha realizado %4!I64u! búsquedas usando la caché parcial y %5!I64u! búsquedas usando la caché para las filas sin entradas coincidentes en la búsqueda inicial.|  
|0x40209316|1075876630|DTS_I_CACHEFILEWRITESTARTED|%1 está escribiendo la caché en el archivo "%2".|  
|0x40209317|1075876631|DTS_I_CACHEFILEWRITESUCCEEDED|%1 ha escrito la caché en el archivo "%2".|  
|0x4020F42C|1075901484|DTS_I_OLEDBDESTZEROMAXCOMMITSIZE|La propiedad de tamaño máximo de confirmación de inserción del destino de OLE DB "%1" está establecida en 0. Este valor de la propiedad puede hacer que el paquete en ejecución deje de responder. Para obtener más información, vea el tema de Ayuda F1 del Editor de destino de OLE DB (página Administrador de conexiones).|  
  
##  <a name="msgGeneral"></a> Mensajes generales y de eventos  
 Los nombres simbólicos de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] mensajes de error que comienzan por `DTS_MSG_`.  
  
|Código hexadecimal|Código decimal|Nombre simbólico|Descripción|  
|----------------------|------------------|-------------------|-----------------|  
|0x1|1|DTS_MSG_CATEGORY_SERVICE_CONTROL|Función incorrecta.|  
|0x2|2|DTS_MSG_CATEGORY_RUNNING_PACKAGE_MANAGEMENT|El sistema no encuentra el archivo especificado.|  
|0x100|256|DTS_MSG_SERVER_STARTING|Iniciando el servicio SSIS de Microsoft.<br /><br /> Versión de servidor %1|  
|0x101|257|DTS_MSG_SERVER_STARTED|Servicio SSIS de Microsoft iniciado.<br /><br /> Versión de servidor %1|  
|0x102|258|DTS_MSG_SERVER_STOPPING|Se agotó el tiempo de espera de la operación de espera.|  
|0x103|259|DTS_MSG_SERVER_STOPPED|No más datos disponibles.|  
|0x104|260|DTS_MSG_SERVER_START_FAILED|Error al iniciar el Servicio SSIS de Microsoft.<br /><br /> Error: %1|  
|0x105|261|DTS_MSG_SERVER_STOP_ERROR|Error al detener el Servicio SSIS de Microsoft.<br /><br /> Error: %1|  
|0x110|272|DTS_MSG_SERVER_MISSING_CONFIG|El archivo de configuración del Servicio SSIS de Microsoft no existe.<br /><br /> Cargando la configuración predeterminada.|  
|0x111|273|DTS_MSG_SERVER_BAD_CONFIG|El archivo de configuración del Servicio SSIS de Microsoft es incorrecto.<br /><br /> Error al leer el archivo de configuración: %1<br /><br /> Cargando la configuración predeterminada del servidor.|  
|0x112|274|DTS_MSG_SERVER_MISSING_CONFIG_REG|Servicio SSIS de Microsoft:<br /><br /> La configuración del Registro que especifica el archivo de configuración no existe.<br /><br /> Intentando cargar el archivo de configuración.|  
|0x150|336|DTS_MSG_SERVER_STOPPING_PACKAGE|Servicio SSIS de Microsoft: deteniendo el paquete en ejecución.<br /><br /> Id. de instancia del paquete: %1<br /><br /> Id. del paquete: %2<br /><br /> Nombre del paquete: %3<br /><br /> Descripción del paquete: %4<br /><br /> Paquete iniciado por: %5|  
|0x40013000|1073819648|DTS_MSG_PACKAGESTART|Paquete "%1" iniciado.|  
|0x40013001|1073819649|DTS_MSG_PACKAGESUCCESS|El paquete "%1" finalizó correctamente.|  
|0x40013002|1073819650|DTS_MSG_PACKAGECANCEL|Se ha cancelado el paquete "%1".|  
|0x40013003|1073819651|DTS_MSG_PACKAGEFAILURE|Error en el paquete "%1".|  
|0x40013004|1073819652|DTS_MSG_CANTDELAYLOADDLL|El módulo %1 no puede cargar la DLL %2 para llamar al punto de entrada %3 por el error %4. El producto requiere la ejecución de la DLL pero no se encontró la DLL en la ruta.|  
|0x40013005|1073819653|DTS_MSG_CANTDELAYLOADDLLFUNCTION|El módulo %1 cargó la DLL %2, pero no encuentra el punto de entrada %3 por el error %4. No se encuentra la DLL indicada en la ruta y el producto requiere la ejecución de dicha DLL.|  
|0x40103100|1074802944|DTS_MSG_EVENTLOGENTRY|Nombre del evento: %1<br /><br /> Mensaje: %9<br /><br /> Operador: %2<br /><br /> Nombre de origen: %3<br /><br /> Id. de origen: %4<br /><br /> Id. de ejecución: %5<br /><br /> Hora de inicio: %6<br /><br /> Hora de finalización: %7<br /><br /> Código de datos: %8|  
|0x40103101|1074802945|DTS_MSG_EVENTLOGENTRY_PREEXECUTE|Nombre del evento: %1<br /><br /> Mensaje: %9<br /><br /> Operador: %2<br /><br /> Nombre de origen: %3<br /><br /> Id. de origen: %4<br /><br /> Id. de ejecución: %5<br /><br /> Hora de inicio: %6<br /><br /> Hora de finalización: %7<br /><br /> Código de datos: %8|  
|0x40103102|1074802946|DTS_MSG_EVENTLOGENTRY_POSTEXECUTE|Nombre del evento: %1<br /><br /> Mensaje: %9<br /><br /> Operador: %2<br /><br /> Nombre de origen: %3<br /><br /> Id. de origen: %4<br /><br /> Id. de ejecución: %5<br /><br /> Hora de inicio: %6<br /><br /> Hora de finalización: %7<br /><br /> Código de datos: %8|  
|0x40103103|1074802947|DTS_MSG_EVENTLOGENTRY_PREVALIDATE|Nombre del evento: %1<br /><br /> Mensaje: %9<br /><br /> Operador: %2<br /><br /> Nombre de origen: %3<br /><br /> Id. de origen: %4<br /><br /> Id. de ejecución: %5<br /><br /> Hora de inicio: %6<br /><br /> Hora de finalización: %7<br /><br /> Código de datos: %8|  
|0x40103104|1074802948|DTS_MSG_EVENTLOGENTRY_POSTVALIDATE|Nombre del evento: %1<br /><br /> Mensaje: %9<br /><br /> Operador: %2<br /><br /> Nombre de origen: %3<br /><br /> Id. de origen: %4<br /><br /> Id. de ejecución: %5<br /><br /> Hora de inicio: %6<br /><br /> Hora de finalización: %7<br /><br /> Código de datos: %8|  
|0x40103105|1074802949|DTS_MSG_EVENTLOGENTRY_WARNING|Nombre del evento: %1<br /><br /> Mensaje: %9<br /><br /> Operador: %2<br /><br /> Nombre de origen: %3<br /><br /> Id. de origen: %4<br /><br /> Id. de ejecución: %5<br /><br /> Hora de inicio: %6<br /><br /> Hora de finalización: %7<br /><br /> Código de datos: %8|  
|0x40103106|1074802950|DTS_MSG_EVENTLOGENTRY_ERROR|Nombre del evento: %1<br /><br /> Mensaje: %9<br /><br /> Operador: %2<br /><br /> Nombre de origen: %3<br /><br /> Id. de origen: %4<br /><br /> Id. de ejecución: %5<br /><br /> Hora de inicio: %6<br /><br /> Hora de finalización: %7<br /><br /> Código de datos: %8|  
|0x40103107|1074802951|DTS_MSG_EVENTLOGENTRY_TASKFAILED|Nombre del evento: %1<br /><br /> Mensaje: %9<br /><br /> Operador: %2<br /><br /> Nombre de origen: %3<br /><br /> Id. de origen: %4<br /><br /> Id. de ejecución: %5<br /><br /> Hora de inicio: %6<br /><br /> Hora de finalización: %7<br /><br /> Código de datos: %8|  
|0x40103108|1074802952|DTS_MSG_EVENTLOGENTRY_PROGRESS|Nombre del evento: %1<br /><br /> Mensaje: %9<br /><br /> Operador: %2<br /><br /> Nombre de origen: %3<br /><br /> Id. de origen: %4<br /><br /> Id. de ejecución: %5<br /><br /> Hora de inicio: %6<br /><br /> Hora de finalización: %7<br /><br /> Código de datos: %8|  
|0x40103109|1074802953|DTS_MSG_EVENTLOGENTRY_EXECSTATCHANGE|Nombre del evento: %1<br /><br /> Mensaje: %9<br /><br /> Operador: %2<br /><br /> Nombre de origen: %3<br /><br /> Id. de origen: %4<br /><br /> Id. de ejecución: %5<br /><br /> Hora de inicio: %6<br /><br /> Hora de finalización: %7<br /><br /> Código de datos: %8|  
|0x4010310A|1074802954|DTS_MSG_EVENTLOGENTRY_VARVALCHANGE|Nombre del evento: %1<br /><br /> Mensaje: %9<br /><br /> Operador: %2<br /><br /> Nombre de origen: %3<br /><br /> Id. de origen: %4<br /><br /> Id. de ejecución: %5<br /><br /> Hora de inicio: %6<br /><br /> Hora de finalización: %7<br /><br /> Código de datos: %8|  
|0x4010310B|1074802955|DTS_MSG_EVENTLOGENTRY_CUSTOMEVENT|Nombre del evento: %1<br /><br /> Mensaje: %9<br /><br /> Operador: %2<br /><br /> Nombre de origen: %3<br /><br /> Id. de origen: %4<br /><br /> Id. de ejecución: %5<br /><br /> Hora de inicio: %6<br /><br /> Hora de finalización: %7<br /><br /> Código de datos: %8|  
|0x4010310C|1074802956|DTS_MSG_EVENTLOGENTRY_PACKAGESTART|Nombre del evento: %1<br /><br /> Mensaje: %9<br /><br /> Operador: %2<br /><br /> Nombre de origen: %3<br /><br /> Id. de origen: %4<br /><br /> Id. de ejecución: %5<br /><br /> Hora de inicio: %6<br /><br /> Hora de finalización: %7<br /><br /> Código de datos: %8|  
|0x4010310D|1074802957|DTS_MSG_EVENTLOGENTRY_PACKAGEEND|Nombre del evento: %1<br /><br /> Mensaje: %9<br /><br /> Operador: %2<br /><br /> Nombre de origen: %3<br /><br /> Id. de origen: %4<br /><br /> Id. de ejecución: %5<br /><br /> Hora de inicio: %6<br /><br /> Hora de finalización: %7<br /><br /> Código de datos: %8|  
|0x4010310E|1074802958|DTS_MSG_EVENTLOGENTRY_INFORMATION|Nombre del evento: %1<br /><br /> Mensaje: %9<br /><br /> Operador: %2<br /><br /> Nombre de origen: %3<br /><br /> Id. de origen: %4<br /><br /> Id. de ejecución: %5<br /><br /> Hora de inicio: %6<br /><br /> Hora de finalización: %7<br /><br /> Código de datos: %8|  
  
##  <a name="msgSuccess"></a> Mensajes de aprobación  
 Los nombres simbólicos de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] mensajes de aprobación que comienzan por `DTS_S_`.  
  
|Código hexadecimal|Código decimal|Nombre simbólico|Descripción|  
|----------------------|------------------|-------------------|-----------------|  
|0x40003|262147|DTS_S_NULLDATA|El valor es nulo.|  
|0x40005|262149|DTS_S_TRUNCATED|El valor de cadena se ha truncado. El búfer recibió una cadena demasiado larga para la columna y truncó la cadena.|  
|0x200001|2097153|DTS_S_EXPREVALTRUNCATIONOCCURRED|Se produjo un truncamiento al evaluar la expresión. El truncamiento se produjo durante la evaluación, que puede incluir cualquier punto de un paso intermedio.|  
  
##  <a name="msgPipeline"></a> Mensajes de error de componentes de flujo de datos  
 Los nombres simbólicos de mensajes de error de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] comienzan con `DTSBC_E_`, donde "BC" hace referencia a la clase base nativa de la que se derivan la mayoría de los componentes de flujo de datos de Microsoft.  
  
|Código hexadecimal|Código decimal|Nombre simbólico|Descripción|  
|----------------------|------------------|-------------------|-----------------|  
|0xC8000002|-939524094|DTSBC_E_INCORRECTEXACTNUMBEROFTOTALOUTPUTS|El número total de salidas y salidas de error, %1!lu!, no es correcto. Debe haber exactamente %2!lu!.|  
|0xC8000003|-939524093|DTSBC_E_FAILEDTOGETOUTPUTBYINDEX|No se puede recuperar la salida con el índice %1!lu!.|  
|0xC8000005|-939524091|DTSBC_E_INCORRECTEXACTNUMBEROFERROROUTPUTS|El número de salidas de error, %1!lu!, no es correcto. Debe haber exactamente %2!lu!.|  
|0xC8000006|-939524090|DTSBC_E_INVALIDVALIDATIONSTATUSVALUE|Valor de estado de validación "%1!lu! incorrecto. ".  Debe ser uno de los valores encontrados en la enumeración DTSValidationStatus.|  
|0xC8000007|-939524089|DTSBC_E_INPUTHASNOOUTPUT|La entrada "%1!lu!" no tiene una salida sincrónica.|  
|0xC8000008|-939524088|DTSBC_E_INPUTHASNOERROROUTPUT|La entrada "%1!lu!" no tiene una salida de error sincrónica.|  
|0xC8000009|-939524087|DTSBC_E_INVALIDHTPIVALUE|El valor de HowToProcessInput, %1!lu!, no es válido. Debe ser uno de los valores de la enumeración HowToProcessInput.|  
|0xC800000A|-939524086|DTSBC_E_FAILEDTOGETCOLINFO|Error al obtener información para la fila "%1!ld!", columna "%2!ld!" del búfer.  Se devolvió el código de error 0x%3!8.8X!.|  
|0xC800000B|-939524085|DTSBC_E_FAILEDTOSETCOLINFO|Error al establecer información para la fila "%1!ld!", columna "%2!ld!" en el búfer.  Se devolvió el código de error 0x%3!8.8X!.|  
|0xC800000C|-939524084|DTSBC_E_INVALIDPROPERTY|La propiedad "%1" no es válida.|  
|0xC800000D|-939524083|DTSBC_E_PROPERTYNOTFOUND|No se encontró la propiedad "%1".|  
|0xC8000010|-939524080|DTSBC_E_READONLYPROPERTY|Error al asignar un valor de solo lectura a la propiedad "%1".|  
|0xC8000011|-939524079|DTSBC_E_CANTINSERTOUTPUTCOLUMN|%1 no permite la inserción de columnas de salida.|  
|0xC8000012|-939524078|DTSBC_E_OUTPUTCOLUMNSMETADATAMISMATCH|Los metadatos de las columnas de salida no coinciden con los metadatos de las columnas de entrada asociadas.  Se actualizarán los metadatos de las columnas de salida.|  
|0xC8000013|-939524077|DTSBC_E_OUTPUTCOLUMNSMISSING|Hay columnas de entrada que no tienen columnas de salida asociadas. Se agregarán las columnas de salida.|  
|0xC8000014|-939524076|DTSBC_E_TOOMANYOUTPUTCOLUMNS|Hay columnas de salida que no tienen columnas de entrada asociadas. Se quitarán las columnas de salida.|  
|0xC8000015|-939524075|DTSBC_E_OUTPUTCOLUMNSMETADATAMISMATCHUNMAP|Los metadatos de las columnas de salida no coinciden con los metadatos de las columnas de entrada asociadas.  Se quitará la asignación de las columnas de entrada.|  
|0xC8000016|-939524074|DTSBC_E_UNMAPINPUTCOLUMNS|Hay columnas de entrada que no tienen columnas de salida asociadas. Se quitará la asignación de las columnas de entrada.|  
|0xC8000017|-939524073|DTSBC_E_MULTIPLEINCOLSTOOUTCOL|Hay una columna de entrada asociada a una columna de salida que, a su vez, ya está asociada a otra columna de entrada de la misma entrada.|  
|0xC8000018|-939524072|DTSBC_E_CANTINSERTEXTERNALMETADATACOLUMN|%1 no permite la inserción de columnas de metadatos externas.|  
  
  
