---
title: DateModified (propiedad, ADOX) | Documentos de Microsoft
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
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
manager: craigg
ms.openlocfilehash: 755697fa07c0b1dd57c3fba658613e9c6cfe30a4
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2018
ms.locfileid: "35285624"
---
# <a name="datemodified-property-adox"></a>DateModified (propiedad, ADOX)
Indica la fecha en que se modificó por última vez el objeto.  
  
## <a name="return-values"></a>Valores devueltos  
 Devuelve un **Variant** valor que especifica la fecha de modificación. El valor es null si **DateModified** no es compatible con el proveedor.  
  
## <a name="remarks"></a>Notas  
 El **DateModified** propiedad es null para objetos recién anexados. Después de anexar una nueva [vista](../../../ado/reference/adox-api/view-object-adox.md) o [procedimiento](../../../ado/reference/adox-api/procedure-object-adox.md), debe llamar a la [actualizar](../../../ado/reference/ado-api/refresh-method-ado.md) método de la [vistas](../../../ado/reference/adox-api/views-collection-adox.md) o [procedimientos ](../../../ado/reference/adox-api/procedures-collection-adox.md) colección para obtener los valores de la **DateModified** propiedad.  
  
## <a name="applies-to"></a>Se aplica a  
  
||||  
|-|-|-|  
|[Objeto Procedure (ADOX)](../../../ado/reference/adox-api/procedure-object-adox.md)|[Objeto Table (ADOX)](../../../ado/reference/adox-api/table-object-adox.md)|[Objeto View (ADOX)](../../../ado/reference/adox-api/view-object-adox.md)|  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo DateCreated y DateModified propiedades (VB)](../../../ado/reference/adox-api/datecreated-and-datemodified-properties-example-vb.md)   
 [DateCreated (propiedad, ADOX)](../../../ado/reference/adox-api/datecreated-property-adox.md)
