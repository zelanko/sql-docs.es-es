---
title: Append (método) (grupos ADOX) | Documentos de Microsoft
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Groups::raw_Append
- Groups::Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: 56b94fc6-7ef0-4e4a-82a3-033b94c46036
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 70fad30091c3f17162998ead00ce8b5de24ad680
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2018
---
# <a name="append-method-adox-groups"></a>Append (método) (grupos ADOX)
Agrega un nuevo [grupo](../../../ado/reference/adox-api/group-object-adox.md) el objeto a la [grupos](../../../ado/reference/adox-api/groups-collection-adox.md) colección.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Groups.Append Group  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Grupo*  
 El **grupo** objeto que se anexará o el nombre del grupo para crear y anexar.  
  
## <a name="remarks"></a>Comentarios  
 El **grupos** colección de un [catálogo](../../../ado/reference/adox-api/catalog-object-adox.md) todas las cuentas de grupo del catálogo representa. El **grupos** colección para un [usuario](../../../ado/reference/adox-api/user-object-adox.md) representa sólo el grupo al que pertenece el usuario.  
  
 Si el proveedor no admite la creación de grupos, se producirá un error.  
  
> [!NOTE]
>  Antes de anexar una **grupo** el objeto a la **grupos** colección de un **usuario** objeto, un **grupo** objeto con el mismo [ Nombre](../../../ado/reference/adox-api/name-property-adox.md) tal y como lo que se debe anexar ya debe existir en el **grupos** colección de la **catálogo**.  
  
## <a name="applies-to"></a>Se aplica a  
 [Colección de grupos (ADOX)](../../../ado/reference/adox-api/groups-collection-adox.md)  
  
## <a name="see-also"></a>Vea también  
 [Los usuarios y grupos, ChangePassword ejemplo de métodos Append (VB)](../../../ado/reference/adox-api/groups-and-users-append-changepassword-methods-example-vb.md)   
 [Append (método) (columnas ADOX)](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Append (método) (índices ADOX)](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Append (método) (claves ADOX)](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Append (método) (ADOX procedimientos)](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Append (método) (tablas ADOX)](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Append (método) (usuarios ADOX)](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Append (método) (vistas ADOX)](../../../ado/reference/adox-api/append-method-adox-views.md)
