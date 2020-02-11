---
title: Colección axes (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Axes
- Cellset::Axes
helpviewer_keywords:
- Axes collection [ADO MD]
ms.assetid: 072fb21a-ec0f-4b02-9022-1cef3ad4bfff
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6c06faf6327d60be823ce9d99215655b5badf5e3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67947405"
---
# <a name="axes-collection-ado-md"></a>Colección Axes (ADO MD)
Contiene los objetos de [eje](../../../ado/reference/ado-md-api/axis-object-ado-md.md) que definen un objeto Cellset.  
  
## <a name="remarks"></a>Observaciones  
 Un objeto [Cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) contiene una colección **Axes** . Una vez que se abre el conjunto de **celdas** , esta colección contendrá al menos un **eje**. Vea el objeto [AXIS](../../../ado/reference/ado-md-api/axis-object-ado-md.md) para obtener una explicación más detallada de cómo usar los objetos de **eje** .  
  
> [!NOTE]
>  El eje de filtro de un conjunto de **celdas** no está contenido en la colección de **ejes** . Vea la propiedad [FilterAxis](../../../ado/reference/ado-md-api/filteraxis-property-ado-md.md) para obtener más información.  
  
 **Axes** es una colección estándar de ADO. Con las propiedades y los métodos de una colección, puede hacer lo siguiente:  
  
-   Obtiene el número de objetos de la colección con la propiedad [Count](../../../ado/reference/ado-api/count-property-ado.md) .  
  
-   Devuelve un objeto de la colección con la propiedad de [elemento](../../../ado/reference/ado-api/item-property-ado.md) predeterminada.  
  
-   Actualice los objetos de la colección desde el proveedor con el método [Refresh](../../../ado/reference/ado-api/refresh-method-ado.md) .  
  
 Esta sección contiene el siguiente tema.  
  
-   [Propiedades, métodos y eventos](../../../ado/reference/ado-md-api/axes-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de Cellset (VB)](../../../ado/reference/ado-md-api/cellset-example-vb.md)   
 [Objeto Axis (ADO MD)](../../../ado/reference/ado-md-api/axis-object-ado-md.md)
