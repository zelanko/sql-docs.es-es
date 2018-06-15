---
title: Método Delete (colecciones de ADOX) | Documentos de Microsoft
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
- Views::Delete
- Groups::Delete
- Indexes::raw_Delete
- Columns::raw_Delete
- Tables::Delete
- Keys::Delete
- Users::Delete
- Users::raw_Delete
- Keys::raw_Delete
- Procedures::raw_Delete
- Views::raw_Delete
- Indexes::Delete
- Procedures::Delete
- Groups::raw_Delete
- Tables::raw_Delete
- Columns::Delete
helpviewer_keywords:
- delete method [ADOX]
ms.assetid: e6b6e3a4-8952-4d79-81f4-51019c338374
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8704e69c777c9426af158b9866ca89e70de054b5
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2018
ms.locfileid: "35285884"
---
# <a name="delete-method-adox-collections"></a>Método Delete (colecciones ADOX)
Quita un objeto de una colección.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Collection.Delete Name  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Nombre*  
 A **Variant** que especifica el nombre o la posición ordinal (índice) del objeto que se va a eliminar.  
  
## <a name="remarks"></a>Notas  
 Se producirá un error si la *nombre* no existe en la colección.  
  
 Para [tablas](../../../ado/reference/adox-api/tables-collection-adox.md) y [usuarios](../../../ado/reference/adox-api/users-collection-adox.md) colecciones, se producirá un error si el proveedor no admite la eliminación de tablas o de los usuarios, respectivamente. Para [procedimientos](../../../ado/reference/adox-api/procedures-collection-adox.md) y [vistas](../../../ado/reference/adox-api/views-collection-adox.md) colecciones, **eliminar** se producirá un error si el proveedor no admite comandos persistentes.  
  
## <a name="applies-to"></a>Se aplica a  
  
||||  
|-|-|-|  
|[Colección de columnas (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)|[Colección de grupos (ADOX)](../../../ado/reference/adox-api/groups-collection-adox.md)|[Colección de índices (ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md)|  
|[Colección de claves (ADOX)](../../../ado/reference/adox-api/keys-collection-adox.md)|[Colección de procedimientos (ADOX)](../../../ado/reference/adox-api/procedures-collection-adox.md)|[Colección de tablas (ADOX)](../../../ado/reference/adox-api/tables-collection-adox.md)|  
|[Colección de usuarios (ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)|[Colección de vistas (ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)||  
  
## <a name="see-also"></a>Vea también  
 [Eliminar de procedimientos de ejemplo del método (VB)](../../../ado/reference/adox-api/procedures-delete-method-example-vb.md)   
 [Ejemplo de método Delete de vistas (VB)](../../../ado/reference/adox-api/views-delete-method-example-vb.md)
