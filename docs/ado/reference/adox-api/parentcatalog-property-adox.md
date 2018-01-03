---
title: ParentCatalog (propiedad, ADOX) | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
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
helpviewer_keywords: ParentCatalog property [ADOX]
ms.assetid: a0bb2ed8-d4cb-4f92-8de7-769bbe0e6273
caps.latest.revision: "15"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0d0cdd505a30252b603477499c44176957d1dc45
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
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
|[Objeto Column (ADOX)](../../../ado/reference/adox-api/column-object-adox.md)|[Objeto Table (ADOX)](../../../ado/reference/adox-api/table-object-adox.md)|  
|[Objeto User (ADOX)](../../../ado/reference/adox-api/user-object-adox.md)||  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de propiedad ParentCatalog (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)
