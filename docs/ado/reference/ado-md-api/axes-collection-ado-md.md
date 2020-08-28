---
description: Colección Axes (ADO MD)
title: Colección axes (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 78113cb7854ec3f56ffe6f7322a6bb732939f27f
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2020
ms.locfileid: "88987416"
---
# <a name="axes-collection-ado-md"></a>Colección Axes (ADO MD)
Contiene los objetos de [eje](./axis-object-ado-md.md) que definen un objeto Cellset.  
  
## <a name="remarks"></a>Observaciones  
 Un objeto [Cellset](./cellset-object-ado-md.md) contiene una colección **Axes** . Una vez que se abre el conjunto de **celdas** , esta colección contendrá al menos un **eje**. Vea el objeto [AXIS](./axis-object-ado-md.md) para obtener una explicación más detallada de cómo usar los objetos de **eje** .  
  
> [!NOTE]
>  El eje de filtro de un conjunto de **celdas** no está contenido en la colección de **ejes** . Vea la propiedad [FilterAxis](./filteraxis-property-ado-md.md) para obtener más información.  
  
 **Axes** es una colección estándar de ADO. Con las propiedades y los métodos de una colección, puede hacer lo siguiente:  
  
-   Obtiene el número de objetos de la colección con la propiedad [Count](../ado-api/count-property-ado.md) .  
  
-   Devuelve un objeto de la colección con la propiedad de [elemento](../ado-api/item-property-ado.md) predeterminada.  
  
-   Actualice los objetos de la colección desde el proveedor con el método [Refresh](../ado-api/refresh-method-ado.md) .  
  
 Esta sección contiene el siguiente tema.  
  
-   [Propiedades, métodos y eventos](./axes-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de Cellset (VB)](./cellset-example-vb.md)   
 [Objeto Axis (ADO MD)](./axis-object-ado-md.md)