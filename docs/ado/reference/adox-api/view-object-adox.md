---
description: Objeto View (ADOX)
title: Objeto de vista (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- View
helpviewer_keywords:
- View object [ADOX]
ms.assetid: 653421ce-7b94-43d0-9bc6-4900f8f2af45
author: rothja
ms.author: jroth
ms.openlocfilehash: eefc7c259d12f20ada1676a6518fa357719abe63
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2020
ms.locfileid: "88982996"
---
# <a name="view-object-adox"></a>Objeto View (ADOX)
Representa un conjunto filtrado de registros o una tabla virtual. Cuando se usa junto con el objeto de [comando](../ado-api/command-object-ado.md) de ADO, el objeto de **vista** se puede usar para agregar, eliminar o modificar vistas.  
  
## <a name="remarks"></a>Observaciones  
 Una vista es una tabla virtual creada a partir de otras tablas o vistas de base de datos. El objeto de **vista** le permite crear una vista sin necesidad de conocer o utilizar la sintaxis de "crear vista" del proveedor.  
  
 Con las propiedades de un objeto de **vista** , puede:  
  
-   Identifique la vista con la propiedad [Name](./name-property-adox.md) .  
  
-   Especifique el objeto **Command** de ADO que se puede utilizar para agregar, eliminar o modificar vistas con la propiedad [Command](./command-property-adox.md) .  
  
-   Devuelve información de fecha con las propiedades [DateCreated](./datecreated-property-adox.md) y [DateModified](./datemodified-property-adox.md) .  
  
 Esta sección contiene el siguiente tema.  
  
-   [Propiedades, métodos y eventos del objeto View](./view-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de colecciones y campos de vistas (VB)](./views-and-fields-collections-example-vb.md)   
 [Ejemplo del método Append de vistas (VB)](./views-append-method-example-vb.md)   
 [Colección views, ejemplo de propiedad CommandText (VB)](./views-collection-commandtext-property-example-vb.md)   
 [Ejemplo de método Delete de vistas (VB)](./views-delete-method-example-vb.md)   
 [Colección de vistas (ADOX)](./views-collection-adox.md)