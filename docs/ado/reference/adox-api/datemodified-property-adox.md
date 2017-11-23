---
title: DateModified (propiedad, ADOX) | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- _Table::get_DateModified
- _Table::DateModified
- _Table::GetDateModified
helpviewer_keywords: DateModified property [ADOX]
ms.assetid: fed09266-1547-4bda-9088-c254d81cc738
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7d4c35300d67bb689ce2479bbcb8c61c40ac9731
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="datemodified-property-adox"></a>DateModified (propiedad, ADOX)
Indica la fecha en que se modificó por última vez el objeto.  
  
## <a name="return-values"></a>Valores devueltos  
 Devuelve un **Variant** valor que especifica la fecha de modificación. El valor es null si **DateModified** no es compatible con el proveedor.  
  
## <a name="remarks"></a>Comentarios  
 El **DateModified** propiedad es null para objetos recién anexados. Después de anexar una nueva [vista](../../../ado/reference/adox-api/view-object-adox.md) o [procedimiento](../../../ado/reference/adox-api/procedure-object-adox.md), debe llamar a la [actualizar](../../../ado/reference/ado-api/refresh-method-ado.md) método de la [vistas](../../../ado/reference/adox-api/views-collection-adox.md) o [procedimientos ](../../../ado/reference/adox-api/procedures-collection-adox.md) colección para obtener los valores de la **DateModified** propiedad.  
  
## <a name="applies-to"></a>Se aplica a  
  
||||  
|-|-|-|  
|[Objeto Procedure (ADOX)](../../../ado/reference/adox-api/procedure-object-adox.md)|[Objeto Table (ADOX)](../../../ado/reference/adox-api/table-object-adox.md)|[Objeto View (ADOX)](../../../ado/reference/adox-api/view-object-adox.md)|  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo DateCreated y DateModified propiedades (VB)](../../../ado/reference/adox-api/datecreated-and-datemodified-properties-example-vb.md)   
 [DateCreated (propiedad, ADOX)](../../../ado/reference/adox-api/datecreated-property-adox.md)
