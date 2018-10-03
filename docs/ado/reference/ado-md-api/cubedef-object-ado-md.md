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
manager: craigg
ms.openlocfilehash: d1027fc76cb09f7b846e1b8edad52a3cb5dbf2bc
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47694069"
---
# <a name="cubedef-object-ado-md"></a>Objeto CubeDef (ADO MD)
Representa un cubo de un esquema multidimensional, que contiene un conjunto de dimensiones relacionadas.  
  
## <a name="remarks"></a>Comentarios  
 Con las colecciones y propiedades de un **CubeDef** objeto, puede hacer lo siguiente:  
  
-   Identificar un **CubeDef** con el [nombre](../../../ado/reference/ado-md-api/name-property-ado-md.md) propiedad.  
  
-   Devolver una cadena que describe el cubo con la [descripción](../../../ado/reference/ado-md-api/description-property-ado-md.md) propiedad.  
  
-   Devolver las dimensiones que conforman el cubo con la [dimensiones](../../../ado/reference/ado-md-api/dimensions-collection-ado-md.md) colección.  
  
-   Obtener información adicional sobre el **CubeDef** con el estándar de ADO [propiedades](../../../ado/reference/ado-api/properties-collection-ado.md) colección.  
  
 El **propiedades** colección contiene las propiedades proporcionadas por el proveedor. En la tabla siguiente se enumera las propiedades que podrían estar disponibles. La lista de propiedades reales puede variar en función de la implementación del proveedor. Consulte la documentación del proveedor para obtener una lista completa de las propiedades disponibles.  
  
|Nombre|Descripción|  
|----------|-----------------|  
|CatalogName|El nombre del catálogo al que pertenece este cubo.|  
|CreatedOn|Fecha y hora de creación del cubo.|  
|CubeGUID|GUID del cubo.|  
|CubeName|Nombre del cubo.|  
|CubeType|El tipo de cubo.|  
|DataUpdatedBy|Id. de usuario de la persona que realiza la última actualización de datos.|  
|Descripción|Descripción del cubo.|  
|LastSchemaUpdate|Fecha y hora de última actualización del esquema.|  
|SchemaName|El nombre del esquema al que pertenece este cubo.|  
|SchemaUpdatedBy|Id. de usuario de la persona que realiza la última actualización del esquema.|  
  
 Esta sección contiene el siguiente tema.  
  
-   [Propiedades, métodos y eventos](../../../ado/reference/ado-md-api/cubedef-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de CubeDef (VBScript)](../../../ado/reference/ado-md-api/cubedef-example-vbscript.md)   
 [Objeto Catalog (ADO MD)](../../../ado/reference/ado-md-api/catalog-object-ado-md.md)   
 [Colección CubeDefs (ADO MD)](../../../ado/reference/ado-md-api/cubedefs-collection-ado-md.md)   
 [Colección Dimensions (ADO MD)](../../../ado/reference/ado-md-api/dimensions-collection-ado-md.md)   
 [Colección de propiedades (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
