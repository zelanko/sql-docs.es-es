---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cc41c630b8201651e933f5d6538e6887e7933c95
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "67966503"
---
# <a name="datemodified-property-adox"></a>DateModified (propiedad, ADOX)
Indica la fecha en que se modificó el objeto por última vez.  
  
## <a name="return-values"></a>Valores devueltos  
 Devuelve un valor **Variant** que especifica la fecha de modificación. El valor es NULL si el proveedor no admite **DateModified** .  
  
## <a name="remarks"></a>Observaciones  
 La propiedad **DateModified** es null para los objetos recién anexados. Después de anexar una nueva [vista](../../../ado/reference/adox-api/view-object-adox.md) o [procedimiento](../../../ado/reference/adox-api/procedure-object-adox.md), debe llamar al método [Refresh](../../../ado/reference/ado-api/refresh-method-ado.md) de la colección [views](../../../ado/reference/adox-api/views-collection-adox.md) o [Procedures](../../../ado/reference/adox-api/procedures-collection-adox.md) para obtener los valores de la propiedad **DateModified** .  
  
## <a name="applies-to"></a>Se aplica a  
  
||||  
|-|-|-|  
|[Objeto Procedure (ADOX)](../../../ado/reference/adox-api/procedure-object-adox.md)|[Objeto Table (ADOX)](../../../ado/reference/adox-api/table-object-adox.md)|[Objeto View (ADOX)](../../../ado/reference/adox-api/view-object-adox.md)|  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de propiedades DateCreated y DateModified (VB)](../../../ado/reference/adox-api/datecreated-and-datemodified-properties-example-vb.md)   
 [DateCreated (propiedad, ADOX)](../../../ado/reference/adox-api/datecreated-property-adox.md)
