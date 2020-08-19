---
description: Objeto Cell (ADO MD)
title: Objeto Cell (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Cell
helpviewer_keywords:
- Cell object [ADO MD]
ms.assetid: dcc2f044-b785-4a29-9bc5-b673f66eedf9
author: rothja
ms.author: jroth
ms.openlocfilehash: a6cb4d32a4a527cce7bc69eb39f8829bbf5cf58a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88441247"
---
# <a name="cell-object-ado-md"></a>Objeto Cell (ADO MD)
Representa los datos en la intersección de las coordenadas del eje contenidas en un Cellset.  
  
## <a name="remarks"></a>Observaciones  
 La propiedad [Item](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md) de un objeto [Cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) devuelve un objeto **Cell** .  
  
 Con las colecciones y las propiedades de un objeto **Cell** , puede hacer lo siguiente:  
  
-   Devuelve los datos de la **celda** con la propiedad [Value](../../../ado/reference/ado-md-api/value-property-ado-md.md) .  
  
-   Devuelve la cadena que representa la presentación con formato de la propiedad **Value** con la propiedad [FormattedValue](../../../ado/reference/ado-md-api/formattedvalue-property-ado-md.md) .  
  
-   Devuelve el valor ordinal de la **celda** dentro del **Cellset** con la propiedad [ordinal](../../../ado/reference/ado-md-api/ordinal-property-ado-md-cell.md) .  
  
-   Determinar la posición de la **celda** dentro del [CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md) con la colección [positions](../../../ado/reference/ado-md-api/positions-collection-ado-md.md) .  
  
-   Recupere otra información sobre la **celda** con la colección de [propiedades](../../../ado/reference/ado-api/properties-collection-ado.md) de ADO estándar.  
  
 La colección **Properties** contiene propiedades proporcionadas por el proveedor. En la tabla siguiente se enumeran las propiedades que pueden estar disponibles. La lista de propiedades real puede variar en función de la implementación del proveedor. Consulte la documentación del proveedor para obtener una lista más completa de las propiedades disponibles.  
  
|Nombre|Descripción|  
|----------|-----------------|  
|BackColor|Color de fondo que se usa al mostrar la celda.|  
|FontFlags|Máscara de máscara que detalla los efectos de la fuente.|  
|FontName|Fuente utilizada para mostrar el valor de la celda.|  
|FontSize|Tamaño de fuente utilizado para mostrar el valor de la celda.|  
|ForeColor|Color de primer plano que se usa al mostrar la celda.|  
|FormatString|Valor en una cadena con formato.|  
  
 Esta sección contiene el siguiente tema.  
  
-   [Propiedades, métodos y eventos](../../../ado/reference/ado-md-api/cell-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de eje (VBScript)](../../../ado/reference/ado-md-api/axis-example-vbscript.md)   
 [Objeto Cellset (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)   
 [Colección positions (ADO MD)](../../../ado/reference/ado-md-api/positions-collection-ado-md.md)   
 [Colección de propiedades (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
