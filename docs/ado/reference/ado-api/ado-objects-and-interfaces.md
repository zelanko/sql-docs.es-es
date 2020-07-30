---
title: Objetos e interfaces de ADO | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO, objects and interfaces
- objects [ADO]
ms.assetid: d0b7e254-c89f-4406-b846-a060ef038c30
author: rothja
ms.author: jroth
ms.openlocfilehash: 6deb8166c775fcdcfe8fb0975662dda0be3b3581
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/28/2020
ms.locfileid: "87242855"
---
# <a name="ado-objects-and-interfaces"></a>Interfaces y objetos ADO
Las relaciones entre estos objetos se representan en el [modelo de objetos ADO](../../../ado/reference/ado-api/ado-object-model.md).  
  
 Cada objeto puede estar contenido en su colección correspondiente. Por ejemplo, un objeto de [error](../../../ado/reference/ado-api/error-object.md) puede estar contenido en una colección de [errores](../../../ado/reference/ado-api/errors-collection-ado.md) . Para obtener más información, vea [colecciones de ADO](../../../ado/reference/ado-api/ado-collections.md) o un tema específico de la colección.  
  
|Objeto o interfaz|Description|  
|-|-|  
|[IADOCommandConstruction](https://msdn.microsoft.com/library/windows/desktop/aa965677.aspx)|Se usa para recuperar el comando OLEDB subyacente de un objeto ADOCommand.|  
|[ADORecordConstruction](../../../ado/reference/ado-api/adorecordconstruction-interface.md)|Construye un objeto **Record** de ADO a partir de un objeto de **fila** OLE DB en una aplicación de C/C++.|  
|[ADORecordsetConstruction](../../../ado/reference/ado-api/adorecordsetconstruction-interface.md)|Construye un objeto de **conjunto de registros** ADO a partir de un objeto de **conjunto de filas** OLE DB en una aplicación de C/C++.|  
|[Interfaz ADOStreamConstruction](../../../ado/reference/ado-api/adostreamconstruction-interface.md)|Construye un objeto de **secuencia** de ADO a partir de un OLE DB objeto **IStream** en una aplicación de C/C++.|  
|[Comando](../../../ado/reference/ado-api/command-object-ado.md)|Define un comando específico que se va a ejecutar en un origen de datos.<br /><br /> El objeto **Command** no es seguro para el scripting.|  
|[Connection](../../../ado/reference/ado-api/connection-object-ado.md)|Representa una conexión abierta a un origen de datos.<br /><br /> El objeto de **conexión** es seguro para el scripting.|  
|[Interfaz IDSOShapeExtensions](../../../ado/reference/ado-api/idsoshapeextensions-interface.md)|Obtiene el objeto de origen de datos OLEDB subyacente para el proveedor de formas.|  
|[Error](../../../ado/reference/ado-api/error-object.md)|Contiene detalles sobre los errores de acceso a datos que pertenecen a una única operación que implica al proveedor.<br /><br /> El objeto de **error** no es seguro para el scripting.|  
|[Campo](../../../ado/reference/ado-api/field-object.md)|Representa una columna de datos con un tipo de datos común.|  
|[Parámetro](../../../ado/reference/ado-api/parameter-object.md)|Representa un parámetro o un argumento asociado a un objeto de **comando** basado en una consulta con parámetros o un procedimiento almacenado.<br /><br /> El objeto de **parámetro** no es seguro para el scripting.|  
|[Propiedad](../../../ado/reference/ado-api/property-object-ado.md)|Representa una característica dinámica de un objeto ADO definido por el proveedor.|  
|[Registro](../../../ado/reference/ado-api/record-object-ado.md)|Representa una fila de un **conjunto de registros**o un directorio o archivo en un sistema de archivos. El objeto de **registro** es seguro para el scripting.|  
|[DataRecordsets](../../../ado/reference/ado-api/recordset-object-ado.md)|Representa el conjunto de registros de una tabla base o los resultados de un comando ejecutado. En cualquier momento, el objeto de **conjunto de registros** hace referencia a un único registro del conjunto como el registro actual.<br /><br /> El objeto de **conjunto de registros** es seguro para el scripting.|  
|[Stream](../../../ado/reference/ado-api/stream-object-ado.md)|Representa un flujo binario de datos.<br /><br /> El objeto de **secuencia** es seguro para el scripting.|  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de la API de ADO](../../../ado/reference/ado-api/ado-api-reference.md)   
 [Colecciones de ADO](../../../ado/reference/ado-api/ado-collections.md)   
 [Propiedades dinámicas de ADO](../../../ado/reference/ado-api/ado-dynamic-properties.md)   
 [Constantes enumeradas de ADO](../../../ado/reference/ado-api/ado-enumerated-constants.md)   
 [Apéndice B: errores de ADO](../../../ado/guide/appendixes/appendix-b-ado-errors.md)   
 [Eventos de ADO](../../../ado/reference/ado-api/ado-events.md)   
 [Métodos de ADO](../../../ado/reference/ado-api/ado-methods.md)   
 [Modelo de objetos ADO](../../../ado/reference/ado-api/ado-object-model.md)   
 [Propiedades de ADO](../../../ado/reference/ado-api/ado-properties.md)
