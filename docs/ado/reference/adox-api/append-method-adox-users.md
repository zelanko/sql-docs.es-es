---
title: Append (método) (usuarios ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Users::raw_Append
- Users::Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: b80bc5d5-78ca-4f75-956b-2ac658029cc7
author: rothja
ms.author: jroth
ms.openlocfilehash: c010b291468432544a037d15fbaa790fc3ee789d
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2020
ms.locfileid: "82764026"
---
# <a name="append-method-adox-users"></a>Append (método) (usuarios ADOX)
Agrega un nuevo objeto de [usuario](../../../ado/reference/adox-api/user-object-adox.md) a la colección de [usuarios](../../../ado/reference/adox-api/users-collection-adox.md) .  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Users.Append User[,Password]  
```  
  
#### <a name="parameters"></a>Parámetros  
 *User*  
 Valor de **tipo Variant** que contiene el objeto de **usuario** que se va a anexar o el nombre del usuario que se va a crear y anexar.  
  
 *Contraseña*  
 Opcional. Valor de **cadena** que contiene la contraseña del usuario. El parámetro *password* corresponde al valor especificado por el método [ChangePassword](../../../ado/reference/adox-api/changepassword-method-adox.md) de un objeto **User** .  
  
## <a name="remarks"></a>Comentarios  
 La colección de **usuarios** de un [Catálogo](../../../ado/reference/adox-api/catalog-object-adox.md) representa todos los usuarios del catálogo. La colección de **usuarios** de un [Grupo](../../../ado/reference/adox-api/group-object-adox.md) representa solo los usuarios que tienen una pertenencia al grupo específico.  
  
 Se producirá un error si el proveedor no admite la creación de usuarios.  
  
> [!NOTE]
>  Antes de anexar un objeto de **usuario** a la colección de **usuarios** de un objeto de **Grupo** , ya debe existir un objeto de **usuario** con el mismo [nombre](../../../ado/reference/adox-api/name-property-adox.md) que el que se va a anexar en la colección de **usuarios** del **Catálogo**.  
  
## <a name="applies-to"></a>Se aplica a  
 [Colección de usuarios (ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de métodos Append y ChangePassword de grupos y usuarios (VB)](../../../ado/reference/adox-api/groups-and-users-append-changepassword-methods-example-vb.md)   
 [Append (método) (columnas ADOX)](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Append (método) (grupos ADOX)](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Append (método) (índices ADOX)](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Append (método) (claves ADOX)](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Append (método) (procedimientos ADOX)](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Append (método) (tablas ADOX)](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Append (método) (vistas ADOX)](../../../ado/reference/adox-api/append-method-adox-views.md)
