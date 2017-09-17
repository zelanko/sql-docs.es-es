---
title: DateCreated (propiedad, ADOX) | Documentos de Microsoft
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
- _Table::get_DateCreated
- _Table::DateCreated
- _Table::GetDateCreated
helpviewer_keywords:
- DateCreated property [ADOX]
ms.assetid: 2bf4b00d-045c-444e-8af7-8af6297ed418
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0403fbd8d7136f008a2ec3bd2ee3071f40ce2cf2
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="datecreated-property-adox"></a>DateCreated (propiedad, ADOX)
Indica la fecha en que se creó el objeto.  
  
## <a name="return-values"></a>Valores devueltos  
 Devuelve un **Variant** valor que especifica la fecha de creación. El valor es null si **DateCreated** no es compatible con el proveedor.  
  
## <a name="remarks"></a>Comentarios  
 El **DateCreated** propiedad es null para objetos recién anexados. Después de anexar una nueva [vista](../../../ado/reference/adox-api/view-object-adox.md) o [procedimiento](../../../ado/reference/adox-api/procedure-object-adox.md), debe llamar a la [actualizar](../../../ado/reference/ado-api/refresh-method-ado.md) método de la [vistas](../../../ado/reference/adox-api/views-collection-adox.md) o [procedimientos ](../../../ado/reference/adox-api/procedures-collection-adox.md) colección para obtener los valores de la **DateCreated** propiedad.  
  
## <a name="applies-to"></a>Se aplica a  
  
||||  
|-|-|-|  
|[Objeto de procedimiento (ADOX)](../../../ado/reference/adox-api/procedure-object-adox.md)|[Objeto de tabla (ADOX)](../../../ado/reference/adox-api/table-object-adox.md)|[Objeto de vista (ADOX)](../../../ado/reference/adox-api/view-object-adox.md)|  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo DateCreated y DateModified propiedades (VB)](../../../ado/reference/adox-api/datecreated-and-datemodified-properties-example-vb.md)   
 [DateModified (propiedad, ADOX)](../../../ado/reference/adox-api/datemodified-property-adox.md)
