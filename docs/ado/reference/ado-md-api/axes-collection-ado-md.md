---
title: Ejes (colección) (ADO MD) | Documentos de Microsoft
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Axes
- Cellset::Axes
helpviewer_keywords:
- Axes collection [ADO MD]
ms.assetid: 072fb21a-ec0f-4b02-9022-1cef3ad4bfff
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4503d2e5c202e2178bd897ce412b64a10f11378d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="axes-collection-ado-md"></a>Colección Axes (ADO MD)
Contiene el [eje](../../../ado/reference/ado-md-api/axis-object-ado-md.md) objetos que definen un conjunto de celdas.  
  
## <a name="remarks"></a>Comentarios  
 A [Cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) objeto contiene un **ejes** colección. Una vez el **Cellset** está abierto, esta colección contendrá al menos una **eje**. Consulte la [eje](../../../ado/reference/ado-md-api/axis-object-ado-md.md) objeto para obtener una explicación más detallada de cómo usar **eje** objetos.  
  
> [!NOTE]
>  El eje del filtro de un **Cellset** no se encuentra en la **ejes** colección. Consulte la [PivotView](../../../ado/reference/ado-md-api/filteraxis-property-ado-md.md) propiedad para obtener más información.  
  
 **Ejes** es una colección de ADO estándar. Con las propiedades y métodos de una colección, puede hacer lo siguiente:  
  
-   Obtener el número de objetos de la colección con el [recuento](../../../ado/reference/ado-api/count-property-ado.md) propiedad.  
  
-   Devolver un objeto de la colección con el valor predeterminado [elemento](../../../ado/reference/ado-api/item-property-ado.md) propiedad.  
  
-   Actualizar los objetos de la colección del proveedor con el [actualizar](../../../ado/reference/ado-api/refresh-method-ado.md) método.  
  
 Esta sección contiene el siguiente tema.  
  
-   [Propiedades, métodos y eventos](../../../ado/reference/ado-md-api/axes-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de conjunto de celdas (VB)](../../../ado/reference/ado-md-api/cellset-example-vb.md)   
 [Objeto Axis (ADO MD)](../../../ado/reference/ado-md-api/axis-object-ado-md.md)
