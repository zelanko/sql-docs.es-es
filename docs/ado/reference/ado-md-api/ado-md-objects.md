---
title: Objetos ADO MD | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO MD, objects
- objects [ADO MD]
ms.assetid: 2a32e873-3282-4520-a7ed-89493f1da80e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d568ca20cca6c12a04c0f3d54a2c134d59a0d7fc
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "67930572"
---
# <a name="ado-md-objects"></a>Objetos de ADO MD

|||  
|-|-|  
|[Eje](../../../ado/reference/ado-md-api/axis-object-ado-md.md)|Representa un eje posicional o de filtro de un objeto Cellset, que contiene los miembros seleccionados de una o más dimensiones.|  
|[Catálogo](../../../ado/reference/ado-md-api/catalog-object-ado-md.md)|Contiene información de esquema multidimensional (es decir, cubos y dimensiones subyacentes, jerarquías, niveles y miembros) específicas de un proveedor de datos multidimensionales (MDP).|  
|[Móvil](../../../ado/reference/ado-md-api/cell-object-ado-md.md)|Representa los datos en la intersección de las coordenadas del eje, contenidas en un Cellset.|  
|[Celdas](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)|Representa los resultados de una consulta multidimensional. Es una colección de celdas seleccionadas de cubos u otros celdas.|  
|[CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)|Representa un cubo de un esquema multidimensional que contiene un conjunto de dimensiones relacionadas.|  
|[Dimensión](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)|Representa una de las dimensiones de un cubo multidimensional que contiene una o más jerarquías de miembros.|  
|[Hierarchy](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md)|Representa una manera en la que los miembros de una dimensión se pueden agregar o "acumular". Una dimensión se puede Agregar A una o más jerarquías.|  
|[Level](../../../ado/reference/ado-md-api/level-object-ado-md.md)|Contiene un conjunto de miembros, cada uno de los cuales tiene el mismo rango dentro de una jerarquía.|  
|[Member](../../../ado/reference/ado-md-api/member-object-ado-md.md)|Representa un miembro de un nivel de un cubo, los elementos secundarios de un miembro de un nivel o un miembro de una posición a lo largo de un eje de un Cellset.|  
|[Localización](../../../ado/reference/ado-md-api/position-object-ado-md.md)|Representa un conjunto de uno o más miembros de distintas dimensiones que define un punto a lo largo de un eje.|  
  
 Además, el objeto de **Catálogo** se conecta a un objeto de **conexión** ADO, que se incluye con la biblioteca estándar de ADO:  
  
|Object|Descripción|  
|------------|-----------------|  
|[Connection](../../../ado/reference/ado-api/connection-object-ado.md)|Representa una conexión abierta a un origen de datos.|  
  
 Las relaciones entre estos objetos se ilustran en el [modelo de objetos de ADO MD](../../../ado/reference/ado-md-api/ado-md-object-model.md).  
  
 Muchos objetos ADO MD pueden estar contenidos en una colección correspondiente. Por ejemplo, un objeto [CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md) puede estar contenido en una colección [CubeDefs](../../../ado/reference/ado-md-api/cubedefs-collection-ado-md.md) de un **Catálogo**. Para obtener más información, vea [colecciones de ADO MD](../../../ado/reference/ado-md-api/ado-md-collections.md).  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de API de ADO MD](../../../ado/reference/ado-md-api/ado-md-api-reference.md)   
 [Ejemplos de código ADO MD](../../../ado/reference/ado-md-api/ado-md-code-examples.md)   
 [Colecciones de ADO MD](../../../ado/reference/ado-md-api/ado-md-collections.md)   
 [ADO MD constantes enumeradas](../../../ado/reference/ado-md-api/ado-md-enumerated-constants.md)   
 [Métodos ADO MD](../../../ado/reference/ado-md-api/ado-md-methods.md)   
 [Modelo de objetos de ADO MD](../../../ado/reference/ado-md-api/ado-md-object-model.md)   
 [Propiedades de ADO MD](../../../ado/reference/ado-md-api/ado-md-properties.md)
