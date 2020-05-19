---
title: Constantes enumeradas de ADO | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- enumerated constants [ADO]
ms.assetid: c97ed131-1a93-463c-9e61-22f029b0c474
author: rothja
ms.author: jroth
ms.openlocfilehash: 00b33a9fa92dd6ec86cbac5a939fe593725bc091
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2020
ms.locfileid: "82749215"
---
# <a name="ado-enumerated-constants"></a>Constantes enumeradas de ADO
Para ayudar en la depuración, las enumeraciones de ADO muestran un valor para cada constante. Sin embargo, este valor es meramente consultivo y puede cambiar de una versión de ADO a otra. El código solo debe depender del nombre, no del valor real, de cada constante enumerada.  
  
|||  
|-|-|  
|[ADCPROP_ASYNCTHREADPRIORITY_ENUM](../../../ado/reference/ado-api/adcprop-asyncthreadpriority-enum.md)|Para un objeto de **conjunto de registros** RDS, especifica la prioridad de ejecución del subproceso asincrónico que recupera los datos.|  
|[ADCPROP_AUTORECALC_ENUM](../../../ado/reference/ado-api/adcprop-autorecalc-enum.md)|Especifica cuándo el proveedor **MSDataShape** vuelve a calcular las columnas agregadas y calculadas en un **conjunto de registros**jerárquico.|  
|[ADCPROP_UPDATECRITERIA_ENUM](../../../ado/reference/ado-api/adcprop-updatecriteria-enum.md)|Especifica los campos que se pueden utilizar para detectar conflictos durante una actualización optimista de una fila del origen de datos con un objeto de **conjunto de registros** .|  
|[ADCPROP_UPDATERESYNC_ENUM](../../../ado/reference/ado-api/adcprop-updateresync-enum.md)|Especifica si el método **UpdateBatch** va seguido de una operación de método **Resync** implícita y, en caso afirmativo, el ámbito de esa operación.|  
|[AffectEnum](../../../ado/reference/ado-api/affectenum.md)|Especifica qué registros se ven afectados por una operación.|  
|[BookmarkEnum](../../../ado/reference/ado-api/bookmarkenum.md)|Especifica un marcador que indica dónde debe comenzar la operación.|  
|[CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)|Especifica cómo debe interpretarse un argumento de comando.|  
|[CompareEnum](../../../ado/reference/ado-api/compareenum.md)|Especifica la posición relativa de dos registros representados por sus marcadores.|  
|[ConnectModeEnum](../../../ado/reference/ado-api/connectmodeenum.md)|Especifica los permisos disponibles para modificar los datos de una **conexión**, abrir un **registro**o especificar valores para la propiedad **mode** de los objetos **Record** y **Stream** .|  
|[ConnectOptionEnum](../../../ado/reference/ado-api/connectoptionenum.md)|Especifica si el método **Open** de un objeto **Connection** debe devolver después de (de forma sincrónica) o antes de que se establezca la conexión.|  
|[ConnectPromptEnum](../../../ado/reference/ado-api/connectpromptenum.md)|Especifica si se debe mostrar un cuadro de diálogo en el que se le pidan los parámetros que faltan al abrir una conexión a un origen de datos ODBC.|  
|[CopyRecordOptionsEnum](../../../ado/reference/ado-api/copyrecordoptionsenum.md)|Especifica el comportamiento del método **CopyRecord** .|  
|[CursorLocationEnum](../../../ado/reference/ado-api/cursorlocationenum.md)|Especifica la ubicación del motor de cursor.|  
|[CursorOptionEnum](../../../ado/reference/ado-api/cursoroptionenum.md)|Especifica qué funcionalidad debe probar el método **Supports** .|  
|[CursorTypeEnum](../../../ado/reference/ado-api/cursortypeenum.md)|Especifica el tipo de cursor utilizado en un objeto de **conjunto de registros** .|  
|[DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md)|Especifica el tipo de datos de un **campo**, un **parámetro**o una **propiedad**.|  
|[EditModeEnum](../../../ado/reference/ado-api/editmodeenum.md)|Especifica el estado de edición de un registro.|  
|[ErrorValueEnum](../../../ado/reference/ado-api/errorvalueenum.md)|Especifica el tipo de error en tiempo de ejecución de ADO.|  
|[EventReasonEnum](../../../ado/reference/ado-api/eventreasonenum.md)|Especifica la razón por la que se produjo un evento.|  
|[EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)|Especifica el estado actual de la ejecución de un evento.|  
|[ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md)|Especifica cómo un proveedor debe ejecutar un comando.|  
|[FieldEnum](../../../ado/reference/ado-api/fieldenum.md)|Especifica los campos especiales a los que se hace referencia en la colección de **campos** de un objeto de **registro** .|  
|[FieldAttributeEnum](../../../ado/reference/ado-api/fieldattributeenum.md)|Especifica uno o más atributos de un objeto de **campo** .|  
|[FieldStatusEnum](../../../ado/reference/ado-api/fieldstatusenum.md)|Especifica el estado de un objeto de **campo** .|  
|[FilterGroupEnum](../../../ado/reference/ado-api/filtergroupenum.md)|Especifica el grupo de registros que se van a filtrar de un **conjunto de registros**.|  
|[GetRowsOptionEnum](../../../ado/reference/ado-api/getrowsoptionenum.md)|Especifica el número de registros que se van a recuperar de un **conjunto de registros**.|  
|[IsolationLevelEnum](../../../ado/reference/ado-api/isolationlevelenum.md)|Especifica el nivel de aislamiento de transacción para un objeto de **conexión** .|  
|[LineSeparatorsEnum](../../../ado/reference/ado-api/lineseparatorsenum.md)|Especifica el carácter que se usa como separador de línea en los objetos de **flujo** de texto.|  
|[LockTypeEnum](../../../ado/reference/ado-api/locktypeenum.md)|Especifica el tipo de bloqueo colocado en los registros durante la edición.|  
|[MarshalOptionsEnum](../../../ado/reference/ado-api/marshaloptionsenum.md)|Especifica los registros que se deben devolver al servidor.|  
|[MoveRecordOptionsEnum](../../../ado/reference/ado-api/moverecordoptionsenum.md)|Especifica el comportamiento del método **MoveRecord** del objeto de **registro** .|  
|[ObjectStateEnum](../../../ado/reference/ado-api/objectstateenum.md)|Especifica si un objeto está abierto o cerrado, se está conectando a un origen de datos, ejecutando un comando o capturando datos.|  
|[ParameterAttributesEnum](../../../ado/reference/ado-api/parameterattributesenum.md)|Especifica los atributos de un objeto de **parámetro** .|  
|[ParameterDirectionEnum](../../../ado/reference/ado-api/parameterdirectionenum.md)|Especifica si el **parámetro** representa un parámetro de entrada, un parámetro de salida o ambos, o si el parámetro es el valor devuelto de un procedimiento almacenado.|  
|[PersistFormatEnum](../../../ado/reference/ado-api/persistformatenum.md)|Especifica el formato en el que se va a guardar un **conjunto de registros**.|  
|[PositionEnum](../../../ado/reference/ado-api/positionenum.md)|Especifica la posición actual del puntero de registro dentro de un **conjunto de registros**.|  
|[PropertyAttributesEnum](../../../ado/reference/ado-api/propertyattributesenum.md)|Especifica los atributos de un objeto de **propiedad** .|  
|[RecordCreateOptionsEnum](../../../ado/reference/ado-api/recordcreateoptionsenum.md)|Especifica para el método **Open** del objeto de **registro** si se debe abrir un **registro** existente o se debe crear un nuevo **registro** .|  
|[RecordOpenOptionsEnum](../../../ado/reference/ado-api/recordopenoptionsenum.md)|Especifica las opciones para abrir un **registro**. Estos valores se pueden combinar mediante el uso de un operador OR.|  
|[RecordStatusEnum](../../../ado/reference/ado-api/recordstatusenum.md)|Especifica el estado de un registro con respecto a las actualizaciones por lotes y otras operaciones masivas.|  
|[RecordTypeEnum](../../../ado/reference/ado-api/recordtypeenum.md)|Especifica el tipo de objeto de **registro** .|  
|[ResyncEnum](../../../ado/reference/ado-api/resyncenum.md)|Especifica si se sobrescriben los valores subyacentes mediante una llamada a **Resync**.|  
|[SaveOptionsEnum](../../../ado/reference/ado-api/saveoptionsenum.md)|Especifica si se debe crear o sobrescribir un archivo al guardar desde un objeto de **flujo** . Los valores se pueden combinar con un operador AND.|  
|[SchemaEnum](../../../ado/reference/ado-api/schemaenum.md)|Especifica el tipo de **conjunto de registros** de esquema que recupera el método **OpenSchema** . Especifica la dirección de una búsqueda de registros dentro de un **conjunto de registros**.|  
|[SearchDirectionEnum](../../../ado/reference/ado-api/searchdirectionenum.md)|Especifica la dirección de una búsqueda de registros dentro de un **conjunto de registros**. Especifica el tipo de **búsqueda** que se va a ejecutar.|  
|[SeekEnum](../../../ado/reference/ado-api/seekenum.md)|Especifica el tipo de **búsqueda** que se va a ejecutar. Especifica las opciones para abrir un objeto de **flujo** . Los valores se pueden combinar con un operador AND.|  
|[StreamOpenOptionsEnum](../../../ado/reference/ado-api/streamopenoptionsenum.md)|Especifica las opciones para abrir un objeto de **flujo** . Los valores se pueden combinar con un operador AND. Especifica si se debe leer toda la secuencia o la línea siguiente de un objeto de **secuencia** .|  
|[StreamReadEnum](../../../ado/reference/ado-api/streamreadenum.md)|Especifica si se debe leer toda la secuencia o la línea siguiente de un objeto de **secuencia** . Especifica el tipo de datos almacenado en un objeto de **secuencia** .|  
|[StreamTypeEnum](../../../ado/reference/ado-api/streamtypeenum.md)|Especifica el tipo de datos almacenado en un objeto de **secuencia** . Especifica si un separador de línea se anexa a la cadena escrita en un objeto de **secuencia** .|  
|[StreamWriteEnum](../../../ado/reference/ado-api/streamwriteenum.md)|Especifica si un separador de línea se anexa a la cadena escrita en un objeto de **secuencia** . Especifica el formato al recuperar un **conjunto de registros** como una cadena.|  
|[StringFormatEnum](../../../ado/reference/ado-api/stringformatenum.md)|Especifica el formato al recuperar un **conjunto de registros** como una cadena. Especifica los atributos de transacción de un objeto de **conexión** .|  
|[XactAttributeEnum](../../../ado/reference/ado-api/xactattributeenum.md)|Especifica los atributos de transacción de un objeto de **conexión** .|  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de la API de ADO](../../../ado/reference/ado-api/ado-api-reference.md)   
 [Colecciones de ADO](../../../ado/reference/ado-api/ado-collections.md)   
 [Propiedades dinámicas de ADO](../../../ado/reference/ado-api/ado-dynamic-properties.md)   
 [Apéndice B: errores de ADO](../../../ado/guide/appendixes/appendix-b-ado-errors.md)   
 [Eventos de ADO](../../../ado/reference/ado-api/ado-events.md)   
 [Métodos de ADO](../../../ado/reference/ado-api/ado-methods.md)   
 [Modelo de objetos ADO](../../../ado/reference/ado-api/ado-object-model.md)   
 [Objetos e interfaces de ADO](../../../ado/reference/ado-api/ado-objects-and-interfaces.md)   
 [Propiedades de ADO](../../../ado/reference/ado-api/ado-properties.md)
