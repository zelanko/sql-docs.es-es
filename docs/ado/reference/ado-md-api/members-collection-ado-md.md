---
title: Colección Members (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Level::Members
- Members
- Position::Members
helpviewer_keywords:
- Members collection [ADO MD]
ms.assetid: 3a647cde-efdc-4394-b1b9-8cbb1b9d689f
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: e7f2221f511d48acc68c379dce72e7708819b1aa
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2019
ms.locfileid: "66709039"
---
# <a name="members-collection-ado-md"></a>Colección Members (ADO MD)
Contiene el [miembro](../../../ado/reference/ado-md-api/member-object-ado-md.md) objetos de un nivel o una posición a lo largo de un eje.  
  
## <a name="remarks"></a>Comentarios  
 Un **miembros** colección se usa para contener los siguientes tipos de miembros:  
  
-   Los miembros que constituyen un nivel en un cubo. Se encuentran en el **miembros** colección de un [nivel](../../../ado/reference/ado-md-api/level-object-ado-md.md) objeto. Por ejemplo, utilizando el ejemplo de [información general de esquemas y datos multidimensionales](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md), los cuatro miembros del nivel de países son Estados Unidos, Canadá, Reino Unido y Alemania.  
  
-   Los miembros que son elementos secundarios de un miembro específico dentro de una jerarquía. Estos miembros devuelven el [hijos](../../../ado/reference/ado-md-api/children-property-ado-md.md) propiedad del elemento primario **miembro** objeto. Por ejemplo, nuevo con el mismo ejemplo, son los dos elementos secundarios del miembro Canada Canadá oriental y Canadá oeste.  
  
-   Los miembros que definen una posición específica en un eje de un [cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md). Mediante el objeto cellset de [trabajar con datos multidimensionales](../../../ado/guide/multidimensional/working-with-multidimensional-data.md) como por ejemplo, los dos miembros de la primera posición en el eje x son Valentine y Seattle. Estos miembros están incluidos en el **miembros** colección de un [posición](../../../ado/reference/ado-md-api/position-object-ado-md.md) objeto.  
  
 **Los miembros** es una colección de ADO estándar. Con las propiedades y métodos de una colección, puede hacer lo siguiente:  
  
-   Obtener el número de objetos de la colección con el [recuento](../../../ado/reference/ado-api/count-property-ado.md) propiedad.  
  
-   Devolver un objeto de la colección con el valor predeterminado [elemento](../../../ado/reference/ado-api/item-property-ado.md) propiedad.  
  
-   Actualizar los objetos de la colección del proveedor con el [actualizar](../../../ado/reference/ado-api/refresh-method-ado.md) método.  
  
 Esta sección contiene el siguiente tema.  
  
-   [Propiedades, métodos y eventos](../../../ado/reference/ado-md-api/members-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de Members (VBScript)](../../../ado/reference/ado-md-api/members-example-vbscript.md)   
 [Objeto de miembro (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)
