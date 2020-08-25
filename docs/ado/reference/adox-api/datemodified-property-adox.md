---
description: DateModified (propiedad, ADOX)
title: DateModified (propiedad, ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Table::get_DateModified
- _Table::DateModified
- _Table::GetDateModified
helpviewer_keywords:
- DateModified property [ADOX]
ms.assetid: fed09266-1547-4bda-9088-c254d81cc738
author: rothja
ms.author: jroth
ms.openlocfilehash: 02bb55cddb1e9496893ee30448a2b479d2311d01
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/24/2020
ms.locfileid: "88770714"
---
# <a name="datemodified-property-adox"></a>DateModified (propiedad, ADOX)
Indica la fecha en que se modificó el objeto por última vez.  
  
## <a name="return-values"></a>Valores devueltos  
 Devuelve un valor **Variant** que especifica la fecha de modificación. El valor es NULL si el proveedor no admite **DateModified** .  
  
## <a name="remarks"></a>Observaciones  
 La propiedad **DateModified** es null para los objetos recién anexados. Después de anexar una nueva [vista](./view-object-adox.md) o [procedimiento](./procedure-object-adox.md), debe llamar al método [Refresh](../ado-api/refresh-method-ado.md) de la colección [views](./views-collection-adox.md) o [Procedures](./procedures-collection-adox.md) para obtener los valores de la propiedad **DateModified** .  
  
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
 [DateCreated (propiedad, ADOX)](./datecreated-property-adox.md)