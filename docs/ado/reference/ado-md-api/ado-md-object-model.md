---
description: Modelo de objetos ADO MD
title: Modelo de objetos de ADO MD | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO MD, object model
ms.assetid: 6242b374-091b-406f-827a-c0dcd3e1967a
author: rothja
ms.author: jroth
ms.openlocfilehash: ed7b8c7dec95183dc66204ca63cc3bf6951d4bf3
ms.sourcegitcommit: 370cab80fba17c15fb0bceed9f80cb099017e000
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/17/2020
ms.locfileid: "97639748"
---
# <a name="ado-md-object-model"></a>Modelo de objetos ADO MD
En este tema se describe cómo se representan los objetos y cómo se relacionan en ADO MD.  
  
 ![Modelo de objetos ADO MD](../../../ado/reference/ado-md-api/media/ado_md_object_model.gif "ADO_MD_object_model")  
  
 Cada uno de los objetos [AXIS](./axis-object-ado-md.md) y [Cell](./cell-object-ado-md.md) tiene una colección [positions](./positions-collection-ado-md.md) .  
  
 Cada uno de los objetos de [nivel](./level-object-ado-md.md) y [posición](./position-object-ado-md.md) tienen una colección de [miembros](./members-collection-ado-md.md) .  
  
 Los objetos [AXIS](./axis-object-ado-md.md), [Cell](./cell-object-ado-md.md), [Cellset](./cellset-object-ado-md.md), [CubeDef](./cubedef-object-ado-md.md), [Dimension](./dimension-object-ado-md.md), [HIERARCHY](./hierarchy-object-ado-md.md), [LEVEL](./level-object-ado-md.md)y [member](./member-object-ado-md.md) tienen una colección de [propiedades](../ado-api/properties-collection-ado.md) de ADO estándar.  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplos de código ADO MD](./ado-md-code-examples.md)   
 [Colecciones de ADO MD](./ado-md-collections.md)   
 [ADO MD constantes enumeradas](./ado-md-enumerated-constants.md)   
 [Métodos ADO MD](./ado-md-methods.md)   
 [Objetos ADO MD](./ado-md-objects.md)   
 [Propiedades de ADO MD](./ado-md-properties.md)   
 [ADO (multidimensional) (ADO MD)](../../guide/multidimensional/ado-multidimensional-ado-md.md)   
 [Información general de los esquemas y datos multidimensionales](../../guide/multidimensional/overview-of-multidimensional-schemas-and-data.md)   
 [Trabajo con datos multidimensionales](../../guide/multidimensional/working-with-multidimensional-data.md)
