---
title: Colección views (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Catalog::Views
- Views
helpviewer_keywords:
- Views collection [ADOX]
ms.assetid: a55d380c-2b7b-4b57-af74-8ba0b3de0db9
author: rothja
ms.author: jroth
ms.openlocfilehash: 355a18d172939113eb71e58655811a44e89aa7c2
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2020
ms.locfileid: "82752990"
---
# <a name="views-collection-adox"></a>Colección de vistas (ADOX)
Contiene todos los objetos de [vista](../../../ado/reference/adox-api/view-object-adox.md) de un catálogo.  
  
## <a name="remarks"></a>Comentarios  
 El método [Append](../../../ado/reference/adox-api/append-method-adox-views.md) de una colección **views** es único para ADOX. Puede:  
  
-   Agregue una nueva vista a la colección con el método **Append** .  
  
 Las propiedades y los métodos restantes son estándar para las colecciones de ADO. Puede:  
  
-   Obtener acceso a una vista de la colección con la propiedad [Item](../../../ado/reference/ado-api/item-property-ado.md) .  
  
-   Devuelve el número de vistas contenidas en la colección con la propiedad [Count](../../../ado/reference/ado-api/count-property-ado.md) .  
  
-   Quitar una vista de la colección con el método [Delete](../../../ado/reference/adox-api/delete-method-adox-collections.md) .  
  
-   Actualice los objetos de la colección para que reflejen el esquema de la base de datos actual con el método [Refresh](../../../ado/reference/ado-api/refresh-method-ado.md) .  
  
 Esta sección contiene el siguiente tema.  
  
-   [Eventos, métodos y propiedades de la colección de vistas](../../../ado/reference/adox-api/views-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de colecciones y campos de vistas (VB)](../../../ado/reference/adox-api/views-and-fields-collections-example-vb.md)   
 [Ejemplo del método Append de vistas (VB)](../../../ado/reference/adox-api/views-append-method-example-vb.md)   
 [Colección views, ejemplo de propiedad CommandText (VB)](../../../ado/reference/adox-api/views-collection-commandtext-property-example-vb.md)   
 [Ejemplo de método Delete de vistas (VB)](../../../ado/reference/adox-api/views-delete-method-example-vb.md)   
 [Ejemplo del método de actualización de vistas (VB)](../../../ado/reference/adox-api/views-refresh-method-example-vb.md)   
 [Objeto Catalog (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [Objeto View (ADOX)](../../../ado/reference/adox-api/view-object-adox.md)
