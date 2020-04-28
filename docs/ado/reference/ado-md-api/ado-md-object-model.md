---
title: Modelo de objetos de ADO MD | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO MD, object model
ms.assetid: 6242b374-091b-406f-827a-c0dcd3e1967a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 68a4b4a11c8662cfdd3df19aa99cdc2e749f1de9
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "67930590"
---
# <a name="ado-md-object-model"></a>Modelo de objetos ADO MD
En este tema se describe cómo se representan los objetos y cómo se relacionan en ADO MD.  
  
 ![Modelo de objetos ADO MD](../../../ado/reference/ado-md-api/media/ado_md_object_model.gif "ADO_MD_object_model")  
  
 Cada uno de los objetos [AXIS](../../../ado/reference/ado-md-api/axis-object-ado-md.md) y [Cell](../../../ado/reference/ado-md-api/cell-object-ado-md.md) tiene una colección [positions](../../../ado/reference/ado-md-api/positions-collection-ado-md.md) .  
  
 Cada uno de los objetos de [nivel](../../../ado/reference/ado-md-api/level-object-ado-md.md) y [posición](../../../ado/reference/ado-md-api/position-object-ado-md.md) tienen una colección de [miembros](../../../ado/reference/ado-md-api/members-collection-ado-md.md) .  
  
 Los objetos [AXIS](../../../ado/reference/ado-md-api/axis-object-ado-md.md), [Cell](../../../ado/reference/ado-md-api/cell-object-ado-md.md), [Cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md), [CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md), [Dimension](../../../ado/reference/ado-md-api/dimension-object-ado-md.md), [HIERARCHY](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md), [LEVEL](../../../ado/reference/ado-md-api/level-object-ado-md.md)y [member](../../../ado/reference/ado-md-api/member-object-ado-md.md) tienen una colección de [propiedades](../../../ado/reference/ado-api/properties-collection-ado.md) de ADO estándar.  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de API de ADO MD](../../../ado/reference/ado-md-api/ado-md-api-reference.md)   
 [Ejemplos de código ADO MD](../../../ado/reference/ado-md-api/ado-md-code-examples.md)   
 [Colecciones de ADO MD](../../../ado/reference/ado-md-api/ado-md-collections.md)   
 [ADO MD constantes enumeradas](../../../ado/reference/ado-md-api/ado-md-enumerated-constants.md)   
 [Métodos ADO MD](../../../ado/reference/ado-md-api/ado-md-methods.md)   
 [Objetos ADO MD](../../../ado/reference/ado-md-api/ado-md-objects.md)   
 [Propiedades de ADO MD](../../../ado/reference/ado-md-api/ado-md-properties.md)   
 [ADO (multidimensional) (ADO MD)](../../../ado/guide/multidimensional/ado-multidimensional-ado-md.md)   
 [Información general de los esquemas y datos multidimensionales](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md)   
 [Trabajo con datos multidimensionales](../../../ado/guide/multidimensional/working-with-multidimensional-data.md)
