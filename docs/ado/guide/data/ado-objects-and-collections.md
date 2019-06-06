---
title: Colecciones y los objetos ADO | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO, objects and collections
ms.assetid: 7a745aae-9372-49b6-8dae-b9c93e5f3216
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 62616ecebb8fa7795462c7e22437aabebb56bcaa
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2019
ms.locfileid: "66700957"
---
# <a name="ado-objects-and-collections"></a>Colecciones y los objetos ADO
ADO consta de los siguientes nueve objetos y cuatro colecciones.  
  
|Objeto o colección|Descripción|  
|--------------------------|-----------------|  
|**Conexión** objeto|Representa una sesión única con un origen de datos. En el caso de un sistema de base de datos cliente/servidor, puede ser equivalente a una conexión de red real con el servidor. Dependiendo de la funcionalidad admitida por el proveedor, algunas colecciones, métodos o propiedades de un **conexión** objeto no esté disponible.|  
|Objeto**Command**|Se utiliza para definir un comando específico, por ejemplo, una consulta SQL, diseñada para ejecutarse en un origen de datos.|  
|**Conjunto de registros** objeto|Representa todo el conjunto de registros de una tabla base o los resultados de un comando ejecutado. Todos los **Recordset** objetos constan de registros (filas) y campos (columnas).|  
|**Registro** objeto|Representa una sola fila de datos, ya sea desde un **Recordset** o desde el proveedor. Este registro podría representar un registro de base de datos o algún otro tipo de objeto como un archivo o directorio, dependiendo del proveedor.|  
|**Stream** objeto|Representa un flujo de datos binarios o texto. Por ejemplo, un documento XML se puede cargar en una secuencia de comandos de entrada o devueltos desde ciertos proveedores, como los resultados de una consulta. Un **Stream** objeto puede utilizarse para manipular campos o registros que contienen estas secuencias de datos.|  
|**Parámetro** objeto|Representa un parámetro o un argumento asociado a un **comando** objeto se basa en un procedimiento almacenado o una consulta parametrizada.|  
|**Campo** objeto|Representa una columna de datos con un tipo de datos común. Cada **campo** objeto corresponde a una columna de la **Recordset**.|  
|**Propiedad** objeto|Representa una característica de un objeto ADO que está definida por el proveedor. Los objetos ADO tienen dos tipos de propiedades: integradas y dinámicas. Las propiedades integradas son esas propiedades implementadas en ADO y disponibles inmediatamente para cualquier objeto nuevo. El **propiedad** objeto es un contenedor para las propiedades dinámicas, definido por el proveedor subyacente.|  
|Objeto**Error**|Contiene detalles sobre los errores de acceso de datos que pertenecen a una única operación que implica al proveedor.|  
|**Campos** colección|Contiene todos los **campo** objetos de un **Recordset** o **registro** objeto.|  
|**Propiedades** colección|Contiene todos los **propiedad** objetos para una instancia específica de un objeto.|  
|**Parámetros** colección|Contiene todos los **parámetro** objetos de un **comando** objeto.|  
|**Errores** colección|Contiene todos los **Error** objetos creados en respuesta a un error relacionado con el proveedor.|  
  
## <a name="see-also"></a>Vea también  
 [Modelo de objetos ADO](../../../ado/reference/ado-api/ado-object-model.md)
