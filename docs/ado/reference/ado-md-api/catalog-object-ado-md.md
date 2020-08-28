---
description: Objeto Catalog (ADO MD)
title: Objeto Catalog (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: 0e62b4eedd835cff2d5bd99e054648339ffd9bc0
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2020
ms.locfileid: "88987306"
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