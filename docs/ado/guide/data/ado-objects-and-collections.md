---
title: Colecciones y los objetos ADO | Documentos de Microsoft
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO, objects and collections
ms.assetid: 7a745aae-9372-49b6-8dae-b9c93e5f3216
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 03671824ef02a7316398f1d9b8d51d57845be736
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="ado-objects-and-collections"></a>Colecciones y los objetos ADO
ADO consta de los siguientes objetos de nueve y cuatro colecciones.  
  
|Objeto o colección|Description|  
|--------------------------|-----------------|  
|**Conexión** objeto|Representa una sesión única con un origen de datos. En el caso de un sistema de base de datos cliente/servidor, puede ser equivalente a una conexión de red real con el servidor. Dependiendo de la funcionalidad admitida por el proveedor, algunas colecciones, métodos o propiedades de un **conexión** objeto no estén disponible.|  
|Objeto**Command** |Se utiliza para definir un comando específico, como una consulta SQL, que se van a ejecutar en un origen de datos.|  
|**Conjunto de registros** objeto|Representa todo el conjunto de registros de una tabla base o los resultados de un comando ejecutado. Todos los **Recordset** objetos constan de registros (filas) y campos (columnas).|  
|**Registro** objeto|Representa una única fila de datos, ya sea desde un **Recordset** o desde el proveedor. Este registro puede representar un registro de base de datos o algún otro tipo de objeto como un archivo o directorio, dependiendo del proveedor.|  
|**Secuencia** objeto|Representa un flujo de datos binarios o de texto. Por ejemplo, un documento XML se puede cargar en una secuencia de comandos de entrada o devuelto de ciertos proveedores como los resultados de una consulta. A **flujo** objeto puede utilizarse para manipular campos o registros que contengan estas secuencias de datos.|  
|**Parámetro** objeto|Representa un parámetro o un argumento asociado con un **comando** objeto se basa en una consulta con parámetros o un procedimiento almacenado.|  
|**Campo** objeto|Representa una columna de datos con un tipo de datos común. Cada **campo** objeto corresponde a una columna de la **conjunto de registros**.|  
|**Propiedad** objeto|Representa una característica de un objeto ADO definido por el proveedor. Objetos ADO tienen dos tipos de propiedades: integradas y dinámicas. Las propiedades integradas son esas propiedades implementadas en ADO y disponibles inmediatamente para cualquier objeto nuevo. El **propiedad** objeto es un contenedor para las propiedades dinámicas, definido por el proveedor subyacente.|  
|Objeto**Error** |Contiene detalles sobre los errores de acceso de datos que pertenecen a una única operación que implique al proveedor.|  
|**Campos** colección|Contiene todos los **campo** objetos de un **Recordset** o **registro** objeto.|  
|**Propiedades** colección|Contiene todos los **propiedad** objetos de una instancia concreta de un objeto.|  
|**Parámetros de** colección|Contiene todos los **parámetro** objetos de un **comando** objeto.|  
|**Errores** colección|Contiene todos los **Error** objetos creados en respuesta a un error relacionado con el proveedor.|  
  
## <a name="see-also"></a>Vea también  
 [Modelo de objetos ADO](../../../ado/reference/ado-api/ado-object-model.md)
