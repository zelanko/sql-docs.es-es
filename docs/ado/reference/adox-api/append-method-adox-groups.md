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
ms.openlocfilehash: 8281b8b480289dca2b4976cea61a6d6838fa2779
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67967315"
---
# <a name="append-method-adox-groups"></a>Append (método) (grupos ADOX)
Agrega un nuevo objeto de [Grupo](../../../ado/reference/adox-api/group-object-adox.md) a la colección de [grupos](../../../ado/reference/adox-api/groups-collection-adox.md) .  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Groups.Append Group  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Grupo*  
 Objeto de **Grupo** que se va a anexar o nombre del grupo que se va a crear y anexar.  
  
## <a name="remarks"></a>Observaciones  
 La colección de **grupos** de un [Catálogo](../../../ado/reference/adox-api/catalog-object-adox.md) representa todas las cuentas de grupo del catálogo. La colección de **grupos** para un [usuario](../../../ado/reference/adox-api/user-object-adox.md) representa solo el grupo al que pertenece el usuario.  
  
 Se producirá un error si el proveedor no admite la creación de grupos.  
  
> [!NOTE]
>  Antes de anexar un objeto de **Grupo** a la colección **Groups** de un objeto **User** , el objeto **Group** con el mismo [nombre](../../../ado/reference/adox-api/name-property-adox.md) que el que se va a anexar ya debe existir en la colección **Groups** del **Catálogo**.  
  
## <a name="applies-to"></a>Se aplica a  
 [Colección de grupos (ADOX)](../../../ado/reference/adox-api/groups-collection-adox.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de métodos Append y ChangePassword de grupos y usuarios (VB)](../../../ado/reference/adox-api/groups-and-users-append-changepassword-methods-example-vb.md)   
 [Append (método) (columnas ADOX)](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Append (método) (índices ADOX)](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Append (método) (claves ADOX)](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Append (método) (procedimientos ADOX)](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Append (método) (tablas ADOX)](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Append (método) (usuarios ADOX)](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Append (método) (vistas ADOX)](../../../ado/reference/adox-api/append-method-adox-views.md)
