---
title: ParentCatalog (propiedad, ADOX) | Documentos de Microsoft
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
- _User::get_ParentCatalog
- _Column::ParentCatalog
- _Table::put_ParentCatalog
- _Group::put_ParentCatalog
- _Column::get_ParentCatalog
- _Table::PutParentCatalog
- _Group::putref_ParentCatalog
- _Group::ParentCatalog
- _Column::PutParentCatalog
- _Column::put_ParentCatalog
- _Group::get_ParentCatalog
- _User::put_ParentCatalog
- _User::putref_ParentCatalog
- _Table::get_ParentCatalog
- _Group::PutParentCatalog
- _Table::ParentCatalog
- _Column::GetParentCatalog
- _Table::PutRefParentCatalog
- _User::GetParentCatalog
- _Table::GetParentCatalog
- _Table::putref_ParentCatalog
- _User::PutParentCatalog
- _User::ParentCatalog
- _User::PutRefParentCatalog
- _Group::GetParentCatalog
- _Group::PutRefParentCatalog
helpviewer_keywords:
- ParentCatalog property [ADOX]
ms.assetid: a0bb2ed8-d4cb-4f92-8de7-769bbe0e6273
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f5229c37299494ca2b3b31e3ca3e0d091c93d96a
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="parentcatalog-property-adox"></a>ParentCatalog (propiedad, ADOX)
Especifica el catálogo del elemento primario de un objeto de tabla, el usuario o la columna para proporcionar acceso a propiedades específicas del proveedor.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece y devuelve un [catálogo](../../../ado/reference/adox-api/catalog-object-adox.md) objeto. Establecer **ParentCatalog** a un formato de archivo **catálogo** permite el acceso a propiedades específicas del proveedor antes de anexar una tabla o columna a una **catálogo** colección.  
  
## <a name="remarks"></a>Comentarios  
 Algunos proveedores de datos que permiten valores de propiedades específicas del proveedor se escriban sólo durante la creación: es decir, cuando una tabla o columna se anexa a su **catálogo** colección. Para tener acceso a estas propiedades antes de anexar estos objetos a un **catálogo**, especifique el **catálogo** en el **ParentCatalog** propiedad primero.  
  
 Se produce un error cuando la tabla o columna se anexa a otra **catálogo** que la **ParentCatalog**.  
  
## <a name="applies-to"></a>Se aplica a  
  
|||  
|-|-|  
|[Objeto Column (ADOX)](../../../ado/reference/adox-api/column-object-adox.md)|[Objeto de tabla (ADOX)](../../../ado/reference/adox-api/table-object-adox.md)|  
|[Objeto de usuario (ADOX)](../../../ado/reference/adox-api/user-object-adox.md)||  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de propiedad ParentCatalog (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)
