---
title: Constantes enumeradas de ADO | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: enumerated constants [ADO]
ms.assetid: c97ed131-1a93-463c-9e61-22f029b0c474
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: fb606a366746b09d7ba6303b0cb11bb1b96f6164
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="ado-enumerated-constants"></a>Constantes enumeradas de ADO
Para ayudar en la depuración, las enumeraciones ADO muestran un valor para cada constante. Sin embargo, este valor es puramente informativo y puede cambiar de una versión de ADO a otro. El código sólo debería depender del nombre, no el valor real, de cada constante enumerada.  
  
|||  
|-|-|  
|[ADCPROP_ASYNCTHREADPRIORITY_ENUM](../../../ado/reference/ado-api/adcprop-asyncthreadpriority-enum.md)|Para un RDS **Recordset** de objetos, especifica la prioridad de ejecución del subproceso asincrónico que recupera los datos.|  
|[ADCPROP_AUTORECALC_ENUM](../../../ado/reference/ado-api/adcprop-autorecalc-enum.md)|Especifica cuándo la **MSDataShape** proveedor vuelve a calcular las columnas agregadas y calculadas en jerárquica **conjunto de registros**.|  
|[ADCPROP_UPDATECRITERIA_ENUM](../../../ado/reference/ado-api/adcprop-updatecriteria-enum.md)|Especifica los campos que se pueden usar para detectar conflictos durante una actualización optimista de una fila del origen de datos con un **Recordset** objeto.|  
|[ADCPROP_UPDATERESYNC_ENUM](../../../ado/reference/ado-api/adcprop-updateresync-enum.md)|Especifica si el **UpdateBatch** método va seguido de un modo implícito **Resync** operación del método y si es así, el ámbito de esa operación.|  
|[AffectEnum](../../../ado/reference/ado-api/affectenum.md)|Especifica que los registros se ven afectados por una operación.|  
|[BookmarkEnum](../../../ado/reference/ado-api/bookmarkenum.md)|Especifica un marcador que indica dónde debe comenzar la operación.|  
|[CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)|Especifica cómo se debe interpretar un argumento de comando.|  
|[CompareEnum](../../../ado/reference/ado-api/compareenum.md)|Especifica la posición relativa de dos registros representados por sus marcadores.|  
|[ConnectModeEnum](../../../ado/reference/ado-api/connectmodeenum.md)|Especifica los permisos disponibles para modificar datos en un **conexión**, abra un **registro**, o especificar valores para la **modo** propiedad de la  **Registro** y **flujo** objetos.|  
|[ConnectOptionEnum](../../../ado/reference/ado-api/connectoptionenum.md)|Especifica si el **abiertos** método de un **conexión** objeto debe devolver después (sincrónicamente) o antes (asincrónicamente) se establece la conexión.|  
|[ConnectPromptEnum](../../../ado/reference/ado-api/connectpromptenum.md)|Especifica si se debe mostrar un cuadro de diálogo para solicitar parámetros que faltan al abrir una conexión a un origen de datos ODBC.|  
|[CopyRecordOptionsEnum](../../../ado/reference/ado-api/copyrecordoptionsenum.md)|Especifica el comportamiento de la **CopyRecord** método.|  
|[CursorLocationEnum](../../../ado/reference/ado-api/cursorlocationenum.md)|Especifica la ubicación del motor de cursor.|  
|[CursorOptionEnum](../../../ado/reference/ado-api/cursoroptionenum.md)|Especifica qué funcionalidad el **admite** debe probar el método de.|  
|[CursorTypeEnum](../../../ado/reference/ado-api/cursortypeenum.md)|Especifica el tipo de cursor que se utiliza en una **Recordset** objeto.|  
|[DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md)|Especifica el tipo de datos de un **campo**, **parámetro**, o **propiedad**.|  
|[EditModeEnum](../../../ado/reference/ado-api/editmodeenum.md)|Especifica el estado de edición de un registro.|  
|[ErrorValueEnum](../../../ado/reference/ado-api/errorvalueenum.md)|Especifica el tipo de error de tiempo de ejecución de ADO.|  
|[EventReasonEnum](../../../ado/reference/ado-api/eventreasonenum.md)|Especifica la razón por la que se produjo un evento que se produzca.|  
|[EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)|Especifica el estado actual de la ejecución de un evento.|  
|[ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md)|Especifica cómo un proveedor debe ejecutar un comando.|  
|[FieldEnum](../../../ado/reference/ado-api/fieldenum.md)|Especifica los campos especiales que se hace referencia en el **campos** colección de un **registro** objeto.|  
|[FieldAttributeEnum](../../../ado/reference/ado-api/fieldattributeenum.md)|Especifica uno o más atributos de un **campo** objeto.|  
|[FieldStatusEnum](../../../ado/reference/ado-api/fieldstatusenum.md)|Especifica el estado de un **campo** objeto.|  
|[FilterGroupEnum](../../../ado/reference/ado-api/filtergroupenum.md)|Especifica el grupo de registros que se deben filtrar en un **conjunto de registros**.|  
|[GetRowsOptionEnum](../../../ado/reference/ado-api/getrowsoptionenum.md)|Especifica cuántos registros se deben para recuperar de un **conjunto de registros**.|  
|[IsolationLevelEnum](../../../ado/reference/ado-api/isolationlevelenum.md)|Especifica el nivel de aislamiento de transacción para un **conexión** objeto.|  
|[LineSeparatorsEnum](../../../ado/reference/ado-api/lineseparatorsenum.md)|Especifica el carácter utilizado como separador de línea en texto **flujo** objetos.|  
|[LockTypeEnum](../../../ado/reference/ado-api/locktypeenum.md)|Especifica el tipo de bloqueo colocado en registros durante la edición.|  
|[MarshalOptionsEnum](../../../ado/reference/ado-api/marshaloptionsenum.md)|Especifica qué registros se deben devolver al servidor.|  
|[MoveRecordOptionsEnum](../../../ado/reference/ado-api/moverecordoptionsenum.md)|Especifica el comportamiento de la **registro** objeto **MoveRecord** método.|  
|[ObjectStateEnum](../../../ado/reference/ado-api/objectstateenum.md)|Especifica si un objeto está abierto o cerrado, conectando a un origen de datos, ejecutar un comando o capturar los datos.|  
|[ParameterAttributesEnum](../../../ado/reference/ado-api/parameterattributesenum.md)|Especifica los atributos de un **parámetro** objeto.|  
|[ParameterDirectionEnum](../../../ado/reference/ado-api/parameterdirectionenum.md)|Especifica si el **parámetro** representa un parámetro de entrada, un parámetro de salida o ambos, o si el parámetro es el valor devuelto de un procedimiento almacenado.|  
|[PersistFormatEnum](../../../ado/reference/ado-api/persistformatenum.md)|Especifica el formato en el que se va a guardar una **conjunto de registros**.|  
|[PositionEnum](../../../ado/reference/ado-api/positionenum.md)|Especifica la posición actual del puntero de registro dentro de un **conjunto de registros**.|  
|[PropertyAttributesEnum](../../../ado/reference/ado-api/propertyattributesenum.md)|Especifica los atributos de un **propiedad** objeto.|  
|[RecordCreateOptionsEnum](../../../ado/reference/ado-api/recordcreateoptionsenum.md)|Especifica para la **registro** objeto **abiertos** método si existente **registro** debe ser abierto, o un nuevo **registro** debe crearse.|  
|[RecordOpenOptionsEnum](../../../ado/reference/ado-api/recordopenoptionsenum.md)|Especifica opciones para abrir un **registro**. Estos valores se pueden combinar mediante un operador OR.|  
|[RecordStatusEnum](../../../ado/reference/ado-api/recordstatusenum.md)|Especifica el estado de un registro con respecto a las actualizaciones por lotes y otras operaciones masivas.|  
|[RecordTypeEnum](../../../ado/reference/ado-api/recordtypeenum.md)|Especifica el tipo de **registro** objeto.|  
|[ResyncEnum](../../../ado/reference/ado-api/resyncenum.md)|Especifica si se sobrescriben los valores subyacentes por una llamada a **Resync**.|  
|[SaveOptionsEnum](../../../ado/reference/ado-api/saveoptionsenum.md)|Especifica si se debe crear un archivo o sobrescribir al guardar desde un **flujo** objeto. Los valores se pueden combinar con un operador AND.|  
|[SchemaEnum](../../../ado/reference/ado-api/schemaenum.md)|Especifica el tipo de esquema **Recordset** que la **OpenSchema** método recupera. Especifica la dirección de una búsqueda de registros dentro de un **conjunto de registros**.|  
|[SearchDirectionEnum](../../../ado/reference/ado-api/searchdirectionenum.md)|Especifica la dirección de una búsqueda de registros dentro de un **conjunto de registros**. Especifica el tipo de **Seek** para ejecutar.|  
|[SeekEnum](../../../ado/reference/ado-api/seekenum.md)|Especifica el tipo de **Seek** para ejecutar. Especifica opciones para abrir un **flujo** objeto. Los valores se pueden combinar con un operador AND.|  
|[StreamOpenOptionsEnum](../../../ado/reference/ado-api/streamopenoptionsenum.md)|Especifica opciones para abrir un **flujo** objeto. Los valores se pueden combinar con un operador AND. Especifica si se debe leer toda la secuencia o la línea siguiente de un **flujo** objeto.|  
|[StreamReadEnum](../../../ado/reference/ado-api/streamreadenum.md)|Especifica si se debe leer toda la secuencia o la línea siguiente de un **flujo** objeto. Especifica el tipo de datos almacenados en una **flujo** objeto.|  
|[StreamTypeEnum](../../../ado/reference/ado-api/streamtypeenum.md)|Especifica el tipo de datos almacenados en una **flujo** objeto. Especifica si se agrega un separador de línea a la cadena escrita en un **flujo** objeto.|  
|[StreamWriteEnum](../../../ado/reference/ado-api/streamwriteenum.md)|Especifica si se agrega un separador de línea a la cadena escrita en un **flujo** objeto. Especifica el formato al recuperar un **Recordset** como una cadena.|  
|[StringFormatEnum](../../../ado/reference/ado-api/stringformatenum.md)|Especifica el formato al recuperar un **Recordset** como una cadena. Especifica los atributos de transacción de un **conexión** objeto.|  
|[XactAttributeEnum](../../../ado/reference/ado-api/xactattributeenum.md)|Especifica los atributos de transacción de un **conexión** objeto.|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de la API de ADO](../../../ado/reference/ado-api/ado-api-reference.md)   
 [Colecciones de ADO](../../../ado/reference/ado-api/ado-collections.md)   
 [Propiedades dinámicas de ADO](../../../ado/reference/ado-api/ado-dynamic-properties.md)   
 [Apéndice B: errores de ADO](../../../ado/guide/appendixes/appendix-b-ado-errors.md)   
 [Eventos de ADO](../../../ado/reference/ado-api/ado-events.md)   
 [Métodos de ADO](../../../ado/reference/ado-api/ado-methods.md)   
 [Modelo de objetos ADO](../../../ado/reference/ado-api/ado-object-model.md)   
 [Interfaces y los objetos ADO](../../../ado/reference/ado-api/ado-objects-and-interfaces.md)   
 [Propiedades de ADO](../../../ado/reference/ado-api/ado-properties.md)
