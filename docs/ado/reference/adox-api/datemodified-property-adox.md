---
title: DateModified (propiedad, ADOX) | Documentos de Microsoft
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- _Table::get_DateModified
- _Table::DateModified
- _Table::GetDateModified
helpviewer_keywords:
- DateModified property [ADOX]
ms.assetid: fed09266-1547-4bda-9088-c254d81cc738
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f76f2f250ae7a40cdb2184ce29c5e20772f7ccaf
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

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
|[Objeto de procedimiento (ADOX)](../../../ado/reference/adox-api/procedure-object-adox.md)|[Objeto de tabla (ADOX)](../../../ado/reference/adox-api/table-object-adox.md)|[Objeto de vista (ADOX)](../../../ado/reference/adox-api/view-object-adox.md)|  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo DateCreated y DateModified propiedades (VB)](../../../ado/reference/adox-api/datecreated-and-datemodified-properties-example-vb.md)   
 [DateCreated (propiedad, ADOX)](../../../ado/reference/adox-api/datecreated-property-adox.md)
