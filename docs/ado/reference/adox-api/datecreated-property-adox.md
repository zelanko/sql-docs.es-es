---
description: DateCreated (propiedad, ADOX)
title: DateCreated (propiedad, ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Table::get_DateCreated
- _Table::DateCreated
- _Table::GetDateCreated
helpviewer_keywords:
- DateCreated property [ADOX]
ms.assetid: 2bf4b00d-045c-444e-8af7-8af6297ed418
author: rothja
ms.author: jroth
ms.openlocfilehash: 7ae2c0fcfdc164906f0216abb45f98f705de9cd4
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/24/2020
ms.locfileid: "88770744"
---
# <a name="datecreated-property-adox"></a>DateCreated (propiedad, ADOX)
Indica la fecha de creación del objeto.  
  
## <a name="return-values"></a>Valores devueltos  
 Devuelve un valor **Variant** que especifica la fecha de creación. El valor es NULL si el proveedor no admite **DateCreated** .  
  
## <a name="remarks"></a>Observaciones  
 La propiedad **DateCreated** es null para los objetos recién anexados. Después de anexar una nueva [vista](./view-object-adox.md) o [procedimiento](./procedure-object-adox.md), debe llamar al método [Refresh](../ado-api/refresh-method-ado.md) de la colección [views](./views-collection-adox.md) o [Procedures](./procedures-collection-adox.md) para obtener los valores de la propiedad **DateCreated** .  
  
## <a name="applies-to"></a>Se aplica a  

:::row:::
    :::column:::
        [Objeto Procedure (ADOX)](./procedure-object-adox.md)  
    :::column-end:::
    :::column:::
        [Objeto Table (ADOX)](./table-object-adox.md)  
    :::column-end:::
    :::column:::
        [Objeto View (ADOX)](./view-object-adox.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>Consulte también  
 [Ejemplo de propiedades DateCreated y DateModified (VB)](./datecreated-and-datemodified-properties-example-vb.md)   
 [DateModified (propiedad, ADOX)](./datemodified-property-adox.md)