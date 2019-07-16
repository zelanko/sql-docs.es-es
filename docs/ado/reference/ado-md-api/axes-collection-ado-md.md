---
title: Los ejes de colección (ADO MD) | Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67947405"
---
# <a name="axes-collection-ado-md"></a>Colección Axes (ADO MD)
Contiene el [eje](../../../ado/reference/ado-md-api/axis-object-ado-md.md) objetos que definen un conjunto de celdas.  
  
## <a name="remarks"></a>Comentarios  
 Un [Cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) objeto contiene un **ejes** colección. Una vez el **Cellset** está abierto, esta colección contendrá al menos una **eje**. Consulte la [eje](../../../ado/reference/ado-md-api/axis-object-ado-md.md) objeto para obtener una explicación más detallada de cómo usar **eje** objetos.  
  
> [!NOTE]
>  El eje del filtro de un **Cellset** no está contenida en el **ejes** colección. Consulte la [FilterAxis](../../../ado/reference/ado-md-api/filteraxis-property-ado-md.md) propiedad para obtener más información.  
  
 **Ejes** es una colección de ADO estándar. Con las propiedades y métodos de una colección, puede hacer lo siguiente:  
  
-   Obtener el número de objetos de la colección con el [recuento](../../../ado/reference/ado-api/count-property-ado.md) propiedad.  
  
-   Devolver un objeto de la colección con el valor predeterminado [elemento](../../../ado/reference/ado-api/item-property-ado.md) propiedad.  
  
-   Actualizar los objetos de la colección del proveedor con el [actualizar](../../../ado/reference/ado-api/refresh-method-ado.md) método.  
  
 Esta sección contiene el siguiente tema.  
  
-   [Propiedades, métodos y eventos](../../../ado/reference/ado-md-api/axes-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de conjunto de celdas (VB)](../../../ado/reference/ado-md-api/cellset-example-vb.md)   
 [Objeto Axis (ADO MD)](../../../ado/reference/ado-md-api/axis-object-ado-md.md)
