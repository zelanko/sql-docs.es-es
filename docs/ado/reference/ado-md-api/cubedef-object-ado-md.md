---
title: Objeto CubeDef (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- CubeDef
helpviewer_keywords:
- CubeDef object [ADO MD]
ms.assetid: feb2581c-fc41-471c-bb69-29f8a55fda70
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 61795a8cb10fb0b469f89012d52dfb4723aa0a89
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67949794"
---
# <a name="cubedef-object-ado-md"></a>Objeto CubeDef (ADO MD)
Representa un cubo de un esquema multidimensional que contiene un conjunto de dimensiones relacionadas.  
  
## <a name="remarks"></a>Observaciones  
 Con las colecciones y las propiedades de un objeto **CubeDef** , puede hacer lo siguiente:  
  
-   Identifique un **CubeDef** con la propiedad [Name](../../../ado/reference/ado-md-api/name-property-ado-md.md) .  
  
-   Devuelve una cadena que describe el cubo con la propiedad [Description](../../../ado/reference/ado-md-api/description-property-ado-md.md) .  
  
-   Devuelve las dimensiones que componen el cubo con la colección de [dimensiones](../../../ado/reference/ado-md-api/dimensions-collection-ado-md.md) .  
  
-   Obtenga información adicional sobre el **CubeDef** con la colección de [propiedades](../../../ado/reference/ado-api/properties-collection-ado.md) de ADO estándar.  
  
 La colección **Properties** contiene propiedades proporcionadas por el proveedor. En la tabla siguiente se enumeran las propiedades que pueden estar disponibles. La lista de propiedades real puede variar en función de la implementación del proveedor. Consulte la documentación del proveedor para obtener una lista más completa de las propiedades disponibles.  
  
|Nombre|Descripción|  
|----------|-----------------|  
|CatalogName|Nombre del catálogo al que pertenece este cubo.|  
|CreatedOn|Fecha y hora de creación del cubo.|  
|CubeGUID|GUID del cubo.|  
|CubeName|Nombre del cubo.|  
|CubeType|El tipo de cubo.|  
|DataUpdatedBy|IDENTIFICADOR de usuario de la persona que realiza la última actualización de datos.|  
|Descripción|Una descripción significativa del cubo.|  
|LastSchemaUpdate|Fecha y hora de la última actualización del esquema.|  
|SchemaName|Nombre del esquema al que pertenece este cubo.|  
|SchemaUpdatedBy|IDENTIFICADOR de usuario de la persona que realiza la última actualización del esquema.|  
  
 Esta sección contiene el siguiente tema.  
  
-   [Propiedades, métodos y eventos](../../../ado/reference/ado-md-api/cubedef-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de CubeDef (VBScript)](../../../ado/reference/ado-md-api/cubedef-example-vbscript.md)   
 [Objeto Catalog (ADO MD)](../../../ado/reference/ado-md-api/catalog-object-ado-md.md)   
 [Colección CubeDefs (ADO MD)](../../../ado/reference/ado-md-api/cubedefs-collection-ado-md.md)   
 [Colección de dimensiones (ADO MD)](../../../ado/reference/ado-md-api/dimensions-collection-ado-md.md)   
 [Colección de propiedades (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
