---
title: Append (método) (grupos ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Groups::raw_Append
- Groups::Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: 56b94fc6-7ef0-4e4a-82a3-033b94c46036
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: b6b9740b58ef53fd4fcc2becda50f73609a1bf5c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66708353"
---
# <a name="append-method-adox-groups"></a>Append (método) (grupos ADOX)
Agrega un nuevo [grupo](../../../ado/reference/adox-api/group-object-adox.md) de objeto para el [grupos](../../../ado/reference/adox-api/groups-collection-adox.md) colección.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Groups.Append Group  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Grupo*  
 El **grupo** objeto anexar o el nombre del grupo para crear y anexar.  
  
## <a name="remarks"></a>Comentarios  
 El **grupos** colección de un [catálogo](../../../ado/reference/adox-api/catalog-object-adox.md) todas las cuentas de grupo del catálogo representa. El **grupos** colección para un [usuario](../../../ado/reference/adox-api/user-object-adox.md) representa sólo el grupo al que pertenece el usuario.  
  
 Si el proveedor no admite la creación de grupos, se producirá un error.  
  
> [!NOTE]
>  Antes de anexar una **grupo** de objeto para el **grupos** colección de un **usuario** objeto, un **grupo** objeto con el mismo [ Nombre](../../../ado/reference/adox-api/name-property-adox.md) ya debe existir en lo que se debe anexar el **grupos** colección de la **catálogo**.  
  
## <a name="applies-to"></a>Se aplica a  
 [Colección de grupos (ADOX)](../../../ado/reference/adox-api/groups-collection-adox.md)  
  
## <a name="see-also"></a>Vea también  
 [Usuarios y grupos, ChangePassword ejemplo de métodos Append (VB)](../../../ado/reference/adox-api/groups-and-users-append-changepassword-methods-example-vb.md)   
 [Append (método) (columnas ADOX)](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Append (método) (índices ADOX)](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Append (método) (claves ADOX)](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Append (método) (procedimientos ADOX)](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Append (método) (tablas ADOX)](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Append (método) (usuarios ADOX)](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Append (método) (vistas ADOX)](../../../ado/reference/adox-api/append-method-adox-views.md)
