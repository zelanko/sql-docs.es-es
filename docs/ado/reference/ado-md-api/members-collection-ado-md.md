---
title: Colección Members (ADO MD) | Documentos de Microsoft
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Level::Members
- Members
- Position::Members
helpviewer_keywords:
- Members collection [ADO MD]
ms.assetid: 3a647cde-efdc-4394-b1b9-8cbb1b9d689f
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d6b4a6902ebf9efae5b02eccb14f1d06e9279cc6
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2018
ms.locfileid: "35284659"
---
# <a name="members-collection-ado-md"></a>Colección Members (ADO MD)
Contiene el [miembro](../../../ado/reference/ado-md-api/member-object-ado-md.md) objetos de un nivel o una posición a lo largo de un eje.  
  
## <a name="remarks"></a>Notas  
 A **miembros** colección se utiliza para contener los siguientes tipos de miembros:  
  
-   Los miembros que componen un nivel en un cubo. Estos miembros se incluyen en el **miembros** colección de un [nivel](../../../ado/reference/ado-md-api/level-object-ado-md.md) objeto. Por ejemplo, mediante el ejemplo de [información general de esquemas y datos multidimensionales](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md), los cuatro miembros del nivel Countries son Canadá, Estados Unidos, Reino Unido y Alemania.  
  
-   Los miembros que son los elementos secundarios de un miembro específico dentro de una jerarquía. Estos miembros devueltos por la [elementos secundarios](../../../ado/reference/ado-md-api/children-property-ado-md.md) propiedad del elemento primario **miembro** objeto. Por ejemplo, utilizando de nuevo el mismo ejemplo, los dos miembros secundarios del miembro Canada son Canada-East y Canada-West.  
  
-   Los miembros que definen una posición específica a lo largo de un eje de un [cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md). Con el conjunto de celdas de [trabajar con datos multidimensionales](../../../ado/guide/multidimensional/working-with-multidimensional-data.md) como ejemplo, los dos miembros de la primera posición en el eje x son Valentine y Seattle. Estos miembros están incluidos en el **miembros** colección de un [posición](../../../ado/reference/ado-md-api/position-object-ado-md.md) objeto.  
  
 **Los miembros** es una colección de ADO estándar. Con las propiedades y métodos de una colección, puede hacer lo siguiente:  
  
-   Obtener el número de objetos de la colección con el [recuento](../../../ado/reference/ado-api/count-property-ado.md) propiedad.  
  
-   Devolver un objeto de la colección con el valor predeterminado [elemento](../../../ado/reference/ado-api/item-property-ado.md) propiedad.  
  
-   Actualizar los objetos de la colección del proveedor con el [actualizar](../../../ado/reference/ado-api/refresh-method-ado.md) método.  
  
 Esta sección contiene el siguiente tema.  
  
-   [Propiedades, métodos y eventos](../../../ado/reference/ado-md-api/members-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de Members (VBScript)](../../../ado/reference/ado-md-api/members-example-vbscript.md)   
 [Objeto de miembro (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)
