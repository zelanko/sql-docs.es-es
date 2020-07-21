---
title: ParentCatalog (propiedad, ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 6c3557af934ab7029822b5f9d3657828ee5d2a75
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2020
ms.locfileid: "82763766"
---
# <a name="parentcatalog-property-adox"></a>ParentCatalog (propiedad, ADOX)
Especifica el catálogo primario de un objeto de tabla, usuario o columna para proporcionar acceso a las propiedades específicas del proveedor.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece y devuelve un objeto de [Catálogo](../../../ado/reference/adox-api/catalog-object-adox.md) . Establecer **ParentCatalog** en un **Catálogo** abierto permite el acceso a las propiedades específicas del proveedor antes de anexar una tabla o una columna a una colección de **catálogos** .  
  
## <a name="remarks"></a>Observaciones  
 Algunos proveedores de datos permiten escribir valores de propiedad específicos del proveedor solo en la creación: es decir, cuando se anexa una tabla o columna a su colección de **catálogos** . Para tener acceso a estas propiedades antes de anexar estos objetos a un **Catálogo**, especifique primero el **Catálogo** en la propiedad **ParentCatalog** .  
  
 Se produce un error cuando la tabla o la columna se anexan a un **Catálogo** diferente del **ParentCatalog**.  
  
## <a name="applies-to"></a>Se aplica a  
  
|||  
|-|-|  
|[Objeto Column (ADOX)](../../../ado/reference/adox-api/column-object-adox.md)|[Objeto Table (ADOX)](../../../ado/reference/adox-api/table-object-adox.md)|  
|[Objeto User (ADOX)](../../../ado/reference/adox-api/user-object-adox.md)||  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de propiedad ParentCatalog (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)
