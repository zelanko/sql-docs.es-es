---
title: ChangePassword (método, ADOX) | Documentos de Microsoft
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
- _User25::raw_ChangePassword
- _User25::ChangePassword
helpviewer_keywords:
- ChangePassword method [ADOX]
ms.assetid: d187fbc6-5fac-4abb-803d-bf344dcf0302
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d88391c197a7d7fe0b112efa069d4f00c4f074bc
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2018
---
# <a name="changepassword-method-adox"></a>ChangePassword (método, ADOX)
Cambia la contraseña para un [usuario](../../../ado/reference/adox-api/user-object-adox.md) cuenta.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
User.ChangePassword OldPassword, NewPassword  
```  
  
#### <a name="parameters"></a>Parámetros  
 *OldPassword*  
 A **cadena** valor que especifica la contraseña del usuario existente. Si el usuario no tiene actualmente una contraseña, utilice una cadena vacía ("") para *OldPassword*.  
  
 *newPassword*  
 A **cadena** valor que especifica la nueva contraseña.  
  
## <a name="remarks"></a>Comentarios  
 Por motivos de seguridad, debe especificarse la contraseña anterior además de la nueva contraseña.  
  
 Se producirá un error si el proveedor no admite la administración de propiedades de usuario de confianza.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto User (ADOX)](../../../ado/reference/adox-api/user-object-adox.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de métodos Append y ChangePassword de grupos y usuarios (VB)](../../../ado/reference/adox-api/groups-and-users-append-changepassword-methods-example-vb.md)
