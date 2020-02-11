---
title: Delete (método) (colecciones ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: be2aa91cf27d7dc12d3cd0c1e0bf719bd43797ab
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67966434"
---
# <a name="delete-method-adox-collections"></a>Delete (método) (colecciones ADOX)
Quita un objeto de una colección.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Collection.Delete Name  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Nombre*  
 **Variante** que especifica el nombre o la posición ordinal (índice) del objeto que se va a eliminar.  
  
## <a name="remarks"></a>Observaciones  
 Se producirá un error si el *nombre* no existe en la colección.  
  
 En el caso de las colecciones de [tablas](../../../ado/reference/adox-api/tables-collection-adox.md) y [usuarios](../../../ado/reference/adox-api/users-collection-adox.md) , se producirá un error si el proveedor no admite la eliminación de tablas o usuarios, respectivamente. En el caso de [los procedimientos](../../../ado/reference/adox-api/procedures-collection-adox.md) y las colecciones de [vistas](../../../ado/reference/adox-api/views-collection-adox.md) , **Delete** producirá un error si el proveedor no admite comandos persistentes.  
  
## <a name="applies-to"></a>Se aplica a  
  
||||  
|-|-|-|  
|[Colección de columnas (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)|[Colección de grupos (ADOX)](../../../ado/reference/adox-api/groups-collection-adox.md)|[Colección de índices (ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md)|  
|[Colección de claves (ADOX)](../../../ado/reference/adox-api/keys-collection-adox.md)|[Colección de procedimientos (ADOX)](../../../ado/reference/adox-api/procedures-collection-adox.md)|[Colección de tablas (ADOX)](../../../ado/reference/adox-api/tables-collection-adox.md)|  
|[Colección de usuarios (ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)|[Colección de vistas (ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)||  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de método Delete de procedimientos (VB)](../../../ado/reference/adox-api/procedures-delete-method-example-vb.md)   
 [Ejemplo de método Delete de vistas (VB)](../../../ado/reference/adox-api/views-delete-method-example-vb.md)
