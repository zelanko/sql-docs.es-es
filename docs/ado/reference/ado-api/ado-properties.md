---
title: Propiedades de ADO | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- properties [ADO]
- ADO properties
ms.assetid: 0ac0d1a7-6c7a-4f4c-b115-428935e0f98b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d3ddf4e26d015067c0b5bf06f6e2adeecd39f041
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "67920893"
---
# <a name="ado-properties"></a>Propiedades de ADO

|||  
|-|-|  
|[AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md)|Indica en qué página reside el registro actual.|  
|[AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md)|Indica la posición ordinal del registro actual de un objeto de **conjunto de registros** .|  
|[ActiveCommand](../../../ado/reference/ado-api/activecommand-property-ado.md)|Indica el objeto de **comando** que creó el objeto de **conjunto de registros** asociado.|  
|[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)|Indica a qué objeto de **conexión** pertenece actualmente el objeto de **comando**, **conjunto de registros**o **registro** especificado.|  
|[ActualSize](../../../ado/reference/ado-api/actualsize-property-ado.md)|Indica la longitud real del valor de un campo.|  
|[Atributos](../../../ado/reference/ado-api/attributes-property-ado.md)|Indica una o más características de un objeto.|  
|[BOF y EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)|**BOF** indica que la posición del registro actual es anterior al primer registro de un objeto de conjunto de registros.<br /><br /> **EOF** indica que la posición del registro actual es posterior al último registro de un objeto de conjunto de registros.|  
|[Marcador](../../../ado/reference/ado-api/bookmark-property-ado.md)|Indica un marcador que identifica de forma única el registro actual en un objeto de **conjunto de registros** o establece el registro actual de un objeto de **conjunto de registros** en el registro identificado por un marcador válido.|  
|[CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md)|Indica el número de registros de un objeto de **conjunto de registros** que se almacenan en caché localmente en la memoria.|  
|[Capítulo](../../../ado/reference/ado-api/chapter-property-ado.md)|Obtiene o establece un objeto **Chapter** de OLE DB de/en un objeto **ADORecordsetConstruction** .|  
|[CharSet](../../../ado/reference/ado-api/charset-property-ado.md)|Indica el juego de caracteres en el que se debe traducir el contenido de una **secuencia** de texto.|  
|[CommandStream](../../../ado/reference/ado-api/commandstream-property-ado.md)|Indica la secuencia que se usa como entrada para un objeto de **comando** .|  
|[CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)|Indica el texto de un comando que se va a emitir en un proveedor.|  
|[CommandTimeout](../../../ado/reference/ado-api/commandtimeout-property-ado.md)|Indica cuánto tiempo se debe esperar mientras se ejecuta un comando antes de terminar el intento y generar un error.|  
|[CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md)|Indica el tipo de un objeto de **comando** .|  
|[Propiedad ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)|Indica la información utilizada para establecer una conexión con un origen de datos.|  
|[ConnectionTimeout](../../../ado/reference/ado-api/connectiontimeout-property-ado.md)|Indica cuánto tiempo se debe esperar mientras se establece una conexión antes de terminar el intento y generar un error.|  
|[Recuento](../../../ado/reference/ado-api/count-property-ado.md)|Indica el número de objetos de una colección.|  
|[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)|Indica la ubicación del servicio de cursor.|  
|[CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md)|Indica el tipo de cursor utilizado en un objeto de **conjunto de registros** .|  
|[DataMember](../../../ado/reference/ado-api/datamember-property.md)|Indica el nombre del miembro de datos que se recuperará del objeto al que hace referencia la propiedad **DataSource** .|  
|[DataSource](../../../ado/reference/ado-api/datasource-property-ado.md)|Indica un objeto que contiene los datos que se van a representar como un objeto de **conjunto de registros** .|  
|[DefaultDatabase](../../../ado/reference/ado-api/defaultdatabase-property.md)|Indica la base de datos predeterminada para un objeto de **conexión** .|  
|[DefinedSize](../../../ado/reference/ado-api/definedsize-property.md)|Indica la capacidad de los datos de un objeto de **campo** .|  
|[Descripción](../../../ado/reference/ado-api/description-property.md)|Describe un objeto de **error** .|  
|[Dialecto](../../../ado/reference/ado-api/dialect-property.md)|Indica la sintaxis y las reglas generales que utilizará el proveedor para analizar las propiedades **CommandText** o **CommandStream** .|  
|[Dirección](../../../ado/reference/ado-api/direction-property.md)|Indica si el **parámetro** representa un parámetro de entrada, un parámetro de salida o ambos, o si el parámetro es el valor devuelto de un procedimiento almacenado.|  
|[EditMode](../../../ado/reference/ado-api/editmode-property.md)|Indica el estado de edición del registro actual.|  
|[OCASIONA](../../../ado/reference/ado-api/eos-property.md)|Indica si la posición actual está al final de la secuencia.|  
|[Filter](../../../ado/reference/ado-api/filter-property.md)|Indica un filtro para los datos de un **conjunto de registros**.|  
|[HelpContext y HelpFile](../../../ado/reference/ado-api/helpcontext-helpfile-properties.md)|Indica el archivo de ayuda y el tema asociados a un objeto de **error** .<br /><br /> **HelpContextID** devuelve un identificador de contexto, como un valor **largo** , para un tema de un archivo de ayuda.<br /><br /> **HelpFile** devuelve un valor de **cadena** que se evalúa como una ruta de acceso totalmente resuelta de un archivo de ayuda.|  
|[Ajustar](../../../ado/reference/ado-api/index-property.md)|Indica el nombre del índice actualmente activo para un objeto de **conjunto de registros** .|  
|[IsolationLevel](../../../ado/reference/ado-api/isolationlevel-property.md)|Indica el nivel de aislamiento para un objeto de **conexión** .|  
|[Elemento](../../../ado/reference/ado-api/item-property-ado.md)|Indica un miembro específico de una colección, por nombre o número ordinal.|  
|[LineSeparator](../../../ado/reference/ado-api/lineseparator-property-ado.md)|Indica el carácter binario que se va a utilizar como separador de línea en los objetos de **flujo** de texto.|  
|[LockType](../../../ado/reference/ado-api/locktype-property-ado.md)|Indica el tipo de bloqueos colocados en los registros durante la edición.|  
|[MarshalOptions](../../../ado/reference/ado-api/marshaloptions-property-ado.md)|Indica qué registros deben calcularse de nuevo en el servidor.|  
|[MaxRecords](../../../ado/reference/ado-api/maxrecords-property-ado.md)|Indica el número máximo de registros que se van a devolver a un **conjunto** de registros desde una consulta.|  
|[Modo](../../../ado/reference/ado-api/mode-property-ado.md)|Indica los permisos disponibles para modificar los datos de un objeto de **conexión**, **registro**o **secuencia** .|  
|[Nombre](../../../ado/reference/ado-api/name-property-ado.md)|Indica el nombre de un objeto.|  
|[NativeError](../../../ado/reference/ado-api/nativeerror-property-ado.md)|Indica el código de error específico del proveedor para un objeto de **error** determinado.|  
|[número](../../../ado/reference/ado-api/number-property-ado.md)|Indica el número que identifica de forma única un objeto de **error** .|  
|[NumericScale](../../../ado/reference/ado-api/numericscale-property-ado.md)|Indica la escala de valores numéricos en un **parámetro** o un objeto de **campo** .|  
|[OriginalValue](../../../ado/reference/ado-api/originalvalue-property-ado.md)|Indica el valor de un **campo** que existía en el registro antes de que se realizaran cambios.|  
|[NúmeroDePáginas](../../../ado/reference/ado-api/pagecount-property-ado.md)|Indica el número de páginas de datos que contiene el objeto de **conjunto de registros** .|  
|[PageSize](../../../ado/reference/ado-api/pagesize-property-ado.md)|Indica el número de registros que representan una página en el **conjunto de registros**.|  
|[ParentRow](../../../ado/reference/ado-api/parentrow-property-ado.md)|Establece el contenedor de un objeto de **fila** OLE DB en un objeto **ADORecordConstruction** , de modo que el elemento primario de la fila se convierta en un objeto **Record** de ADO.|  
|[ParentURL](../../../ado/reference/ado-api/parenturl-property-ado.md)|Indica una cadena de dirección URL absoluta que apunta al **registro** primario del objeto de **registro** actual.|  
|[Localización](../../../ado/reference/ado-api/position-property-ado.md)|Indica la posición actual dentro de un objeto de **flujo** .|  
|[Precisión](../../../ado/reference/ado-api/precision-property-ado.md)|Indica el grado de precisión de los valores numéricos de un objeto de **parámetro** o de los objetos de **campo** numérico.|  
|[Prepared](../../../ado/reference/ado-api/prepared-property-ado.md)|Indica si se debe guardar una versión compilada de un comando antes de la ejecución.|  
|[Proveedor](../../../ado/reference/ado-api/provider-property-ado.md)|Indica el nombre del proveedor de un objeto de **conexión** .|  
|[RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md)|Indica el número de registros de un objeto de **conjunto de registros** .|  
|[RecordType](../../../ado/reference/ado-api/recordtype-property-ado.md)|Indica el tipo de objeto de **registro** .|  
|[Columna](../../../ado/reference/ado-api/row-property-ado.md)|Obtiene o establece un objeto de **fila** OLE DB de/en un objeto **ADORecordConstruction** .|  
|[RowPosition](../../../ado/reference/ado-api/rowposition-property-ado.md)|Obtiene o establece un objeto **RowPosition** OLE DB de/en un objeto **ADORecordsetConstruction** .|  
|[Conjunto de filas](../../../ado/reference/ado-api/rowset-property-ado.md)|Obtiene o establece un objeto de **conjunto de filas** OLE DB de/en un objeto **ADORecordsetConstruction** .|  
|[Origen (error de ADO)](../../../ado/reference/ado-api/source-property-ado-error.md)|Indica el nombre del objeto o la aplicación que originalmente generó un error.|  
|[Source (registro de ADO)](../../../ado/reference/ado-api/source-property-ado-record.md)|Indica la entidad representada por el objeto de **registro** .|  
|[Source (conjunto de registros ADO)](../../../ado/reference/ado-api/source-property-ado-recordset.md)|Indica el origen de los datos de un objeto de **conjunto de registros**|  
|[SQLState](../../../ado/reference/ado-api/sqlstate-property.md)|Indica el estado de SQL para un objeto de **error** específico.|  
|[State](../../../ado/reference/ado-api/state-property-ado.md)|Indica para todos los objetos aplicables si el estado del objeto es abierto o cerrado. Indica para todos los objetos aplicables que ejecutan un método asincrónico, si el estado actual del objeto es conexión, ejecución o recuperación.|  
|[Status (campo de ADO)](../../../ado/reference/ado-api/status-property-ado-field.md)|Indica el estado de un objeto de **campo** .|  
|[Status (conjunto de registros ADO)](../../../ado/reference/ado-api/status-property-ado-recordset.md)|Indica el estado del registro actual en relación con las actualizaciones por lotes u otras operaciones masivas.|  
|[StayInSync](../../../ado/reference/ado-api/stayinsync-property.md)|Indica, en un objeto de **conjunto de registros** jerárquico, si la referencia a los registros secundarios subyacentes (es decir, el *capítulo*) cambia cuando cambia la posición de la fila primaria.|  
|[Propiedad de la secuencia](../../../ado/reference/ado-api/stream-property.md)|Obtiene o establece un objeto de **flujo** de OLE DB de/en un objeto **ADOStreamConstruction** .|  
|[Type](../../../ado/reference/ado-api/type-property-ado.md)|Indica el tipo operativo o el tipo de datos de un **parámetro**, **campo**o objeto de **propiedad** .|  
|[Type (secuencia de ADO)](../../../ado/reference/ado-api/type-property-ado-stream.md)|Indica el tipo de datos contenidos en la **secuencia** (binario o de texto).|  
|[UnderlyingValue](../../../ado/reference/ado-api/underlyingvalue-property.md)|Indica el valor actual de la base de datos para un objeto de **campo** .|  
|[Valor](../../../ado/reference/ado-api/value-property-ado.md)|Indica el valor asignado a un **campo**, un **parámetro**o un objeto de **propiedad** .|  
|[Versión](../../../ado/reference/ado-api/version-property-ado.md)|Indica el número de versión de ADO.|  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de la API de ADO](../../../ado/reference/ado-api/ado-api-reference.md)   
 [Colecciones de ADO](../../../ado/reference/ado-api/ado-collections.md)   
 [Propiedades dinámicas de ADO](../../../ado/reference/ado-api/ado-dynamic-properties.md)   
 [Constantes enumeradas de ADO](../../../ado/reference/ado-api/ado-enumerated-constants.md)   
 [Apéndice B: errores de ADO](../../../ado/guide/appendixes/appendix-b-ado-errors.md)   
 [Eventos de ADO](../../../ado/reference/ado-api/ado-events.md)   
 [Métodos de ADO](../../../ado/reference/ado-api/ado-methods.md)   
 [Modelo de objetos ADO](../../../ado/reference/ado-api/ado-object-model.md)   
 [Interfaces y objetos ADO](../../../ado/reference/ado-api/ado-objects-and-interfaces.md)
