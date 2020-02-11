---
title: ChangePassword (método, ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _User25::raw_ChangePassword
- _User25::ChangePassword
helpviewer_keywords:
- ChangePassword method [ADOX]
ms.assetid: d187fbc6-5fac-4abb-803d-bf344dcf0302
author: MightyPen
ms.author: genemi
ms.openlocfilehash: de8baf504a76407037322fd6b799f6d63584eae7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67967038"
---
# <a name="changepassword-method-adox"></a>ChangePassword (método, ADOX)
Cambia la contraseña de una cuenta de [usuario](../../../ado/reference/adox-api/user-object-adox.md) .  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
User.ChangePassword OldPassword, NewPassword  
```  
  
#### <a name="parameters"></a>Parámetros  
 *OldPassword*  
 Valor de **cadena** que especifica la contraseña existente del usuario. Si el usuario no tiene actualmente una contraseña, use una cadena vacía ("") para *OldPassword*.  
  
 *NewPassword*  
 Valor de **cadena** que especifica la nueva contraseña.  
  
## <a name="remarks"></a>Observaciones  
 Por motivos de seguridad, se debe especificar la contraseña anterior además de la nueva contraseña.  
  
 Se producirá un error si el proveedor no admite la administración de las propiedades de confianza.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto User (ADOX)](../../../ado/reference/adox-api/user-object-adox.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de métodos Append y ChangePassword de grupos y usuarios (VB)](../../../ado/reference/adox-api/groups-and-users-append-changepassword-methods-example-vb.md)
