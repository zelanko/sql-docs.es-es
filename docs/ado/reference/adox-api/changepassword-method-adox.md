---
title: "ChangePassword (método, ADOX) | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
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
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 18dd53bc701cf6a4b77c8e77f5b1851aff57f2ba
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

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
  
 *NewPassword*  
 A **cadena** valor que especifica la nueva contraseña.  
  
## <a name="remarks"></a>Comentarios  
 Por motivos de seguridad, debe especificarse la contraseña anterior además de la nueva contraseña.  
  
 Se producirá un error si el proveedor no admite la administración de propiedades de usuario de confianza.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de usuario (ADOX)](../../../ado/reference/adox-api/user-object-adox.md)  
  
## <a name="see-also"></a>Vea también  
 [Los usuarios y grupos, ChangePassword ejemplo de métodos Append (VB)](../../../ado/reference/adox-api/groups-and-users-append-changepassword-methods-example-vb.md)

