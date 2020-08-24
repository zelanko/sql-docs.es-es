---
description: Objeto Catalog (ADO MD)
title: Objeto Catalog (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Catalog
helpviewer_keywords:
- Catalog object [ADO MD]
ms.assetid: 11f6f896-d69c-44a4-94cd-d54c93140e4a
author: rothja
ms.author: jroth
ms.openlocfilehash: b198e9765a8d0e68e61ecd3f9ed334e34c714ea8
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/24/2020
ms.locfileid: "88778344"
---
# <a name="catalog-object-ado-md"></a>Objeto Catalog (ADO MD)
Contiene información de esquema multidimensional (es decir, cubos y dimensiones subyacentes, jerarquías, niveles y miembros) específicas de un proveedor de datos multidimensionales (MDP).  
  
## <a name="remarks"></a>Observaciones  
 Con las colecciones y las propiedades de un objeto de **Catálogo** , puede hacer lo siguiente:  
  
-   Abra el catálogo estableciendo la propiedad [ActiveConnection](./activeconnection-property-ado-md.md) en un objeto de [conexión](../ado-api/connection-object-ado.md) ADO estándar o en una cadena de conexión válida.  
  
-   Identifique el **Catálogo** con la propiedad [Name](./name-property-ado-md.md) .  
  
-   Recorrer en iteración los cubos de un catálogo mediante la colección [CubeDefs](./cubedefs-collection-ado-md.md) .  
  
 Esta sección contiene el siguiente tema.  
  
-   [Propiedades, métodos y eventos](./catalog-object-properties-methods-and-events-ado-md.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de catálogo (VB)](./catalog-example-vb.md)   
 [Connection (objeto) (ADO)](../ado-api/connection-object-ado.md)   
 [Colección CubeDefs (ADO MD)](./cubedefs-collection-ado-md.md)