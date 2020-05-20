---
title: Colección de miembros (ADO MD) | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: e8337bfd2e7fb8ece226709f86c3b57ef746baca
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2020
ms.locfileid: "82765135"
---
# <a name="members-collection-ado-md"></a>Colección Members (ADO MD)
Contiene los objetos [miembro](../../../ado/reference/ado-md-api/member-object-ado-md.md) de un nivel o una posición a lo largo de un eje.  
  
## <a name="remarks"></a>Comentarios  
 Una colección de **miembros** se usa para contener los siguientes tipos de miembros:  
  
-   Los miembros que componen un nivel en un cubo. Están contenidos en la colección **Members** de un objeto [LEVEL](../../../ado/reference/ado-md-api/level-object-ado-md.md) . Por ejemplo, mediante el ejemplo de [información general de esquemas y datos multidimensionales](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md), los cuatro miembros del nivel países son Canadá, EE. UU., Reino Unido y Alemania.  
  
-   Los miembros que son elementos secundarios de un miembro específico dentro de una jerarquía. Estos miembros son devueltos por la propiedad [Children](../../../ado/reference/ado-md-api/children-property-ado-md.md) del objeto **miembro** primario. Por ejemplo, de nuevo con el mismo ejemplo, los dos elementos secundarios del miembro Canada son Canada-East y Canada-West.  
  
-   Los miembros que definen una posición específica a lo largo de un eje de un [Cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md). Al usar el Cellset para [trabajar con datos multidimensionales](../../../ado/guide/multidimensional/working-with-multidimensional-data.md) como ejemplo, los dos miembros de la primera posición en el eje x son San Valentín y Seattle. Estos miembros están incluidos en la colección **Members** de un objeto [Position](../../../ado/reference/ado-md-api/position-object-ado-md.md) .  
  
 **Members** es una colección estándar de ADO. Con las propiedades y los métodos de una colección, puede hacer lo siguiente:  
  
-   Obtiene el número de objetos de la colección con la propiedad [Count](../../../ado/reference/ado-api/count-property-ado.md) .  
  
-   Devuelve un objeto de la colección con la propiedad de [elemento](../../../ado/reference/ado-api/item-property-ado.md) predeterminada.  
  
-   Actualice los objetos de la colección desde el proveedor con el método [Refresh](../../../ado/reference/ado-api/refresh-method-ado.md) .  
  
 Esta sección contiene el siguiente tema.  
  
-   [Propiedades, métodos y eventos](../../../ado/reference/ado-md-api/members-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de miembros (VBScript)](../../../ado/reference/ado-md-api/members-example-vbscript.md)   
 [Objeto de miembro (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)
