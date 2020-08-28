---
description: Colección Members (ADO MD)
title: Colección de miembros (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: e0f12771ebb759a658d5e3c99244755c4daa99b0
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2020
ms.locfileid: "88986386"
---
# <a name="members-collection-ado-md"></a>Colección Members (ADO MD)
Contiene los objetos [miembro](./member-object-ado-md.md) de un nivel o una posición a lo largo de un eje.  
  
## <a name="remarks"></a>Observaciones  
 Una colección de **miembros** se usa para contener los siguientes tipos de miembros:  
  
-   Los miembros que componen un nivel en un cubo. Están contenidos en la colección **Members** de un objeto [LEVEL](./level-object-ado-md.md) . Por ejemplo, mediante el ejemplo de [información general de esquemas y datos multidimensionales](../../guide/multidimensional/overview-of-multidimensional-schemas-and-data.md), los cuatro miembros del nivel países son Canadá, EE. UU., Reino Unido y Alemania.  
  
-   Los miembros que son elementos secundarios de un miembro específico dentro de una jerarquía. Estos miembros son devueltos por la propiedad [Children](./children-property-ado-md.md) del objeto **miembro** primario. Por ejemplo, de nuevo con el mismo ejemplo, los dos elementos secundarios del miembro Canada son Canada-East y Canada-West.  
  
-   Los miembros que definen una posición específica a lo largo de un eje de un [Cellset](./cellset-object-ado-md.md). Al usar el Cellset para [trabajar con datos multidimensionales](../../guide/multidimensional/working-with-multidimensional-data.md) como ejemplo, los dos miembros de la primera posición en el eje x son San Valentín y Seattle. Estos miembros están incluidos en la colección **Members** de un objeto [Position](./position-object-ado-md.md) .  
  
 **Members** es una colección estándar de ADO. Con las propiedades y los métodos de una colección, puede hacer lo siguiente:  
  
-   Obtiene el número de objetos de la colección con la propiedad [Count](../ado-api/count-property-ado.md) .  
  
-   Devuelve un objeto de la colección con la propiedad de [elemento](../ado-api/item-property-ado.md) predeterminada.  
  
-   Actualice los objetos de la colección desde el proveedor con el método [Refresh](../ado-api/refresh-method-ado.md) .  
  
 Esta sección contiene el siguiente tema.  
  
-   [Propiedades, métodos y eventos](./members-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de miembros (VBScript)](./members-example-vbscript.md)   
 [Objeto de miembro (ADO MD)](./member-object-ado-md.md)