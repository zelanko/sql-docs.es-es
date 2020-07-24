---
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
ms.openlocfilehash: 2a94ea4d86d727bc2258b853285eaa7ebc1e48bc
ms.sourcegitcommit: 591bbf4c7e4e2092f8abda6a2ffed263cb61c585
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/22/2020
ms.locfileid: "86942438"
---
# <a name="datecreated-property-adox"></a>DateCreated (propiedad, ADOX)
Indica la fecha de creación del objeto.  
  
## <a name="return-values"></a>Valores devueltos  
 Devuelve un valor **Variant** que especifica la fecha de creación. El valor es NULL si el proveedor no admite **DateCreated** .  
  
## <a name="remarks"></a>Observaciones  
 La propiedad **DateCreated** es null para los objetos recién anexados. Después de anexar una nueva [vista](../../../ado/reference/adox-api/view-object-adox.md) o [procedimiento](../../../ado/reference/adox-api/procedure-object-adox.md), debe llamar al método [Refresh](../../../ado/reference/ado-api/refresh-method-ado.md) de la colección [views](../../../ado/reference/adox-api/views-collection-adox.md) o [Procedures](../../../ado/reference/adox-api/procedures-collection-adox.md) para obtener los valores de la propiedad **DateCreated** .  
  
## <a name="applies-to"></a>Se aplica a  

:::row:::
    :::column:::
        [Objeto Procedure (ADOX)](../../../ado/reference/adox-api/procedure-object-adox.md)  
    :::column-end:::
    :::column:::
        [Objeto Table (ADOX)](../../../ado/reference/adox-api/table-object-adox.md)  
    :::column-end:::
    :::column:::
        [Objeto View (ADOX)](../../../ado/reference/adox-api/view-object-adox.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>Consulte también  
 [Ejemplo de propiedades DateCreated y DateModified (VB)](../../../ado/reference/adox-api/datecreated-and-datemodified-properties-example-vb.md)   
 [DateModified (propiedad, ADOX)](../../../ado/reference/adox-api/datemodified-property-adox.md)
