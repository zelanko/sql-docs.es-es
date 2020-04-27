---
title: Método SetServiceAccount (clase SqlService) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- SetServiceAccount Method (SqlService Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- SetServiceAccount method
ms.assetid: d5782892-e9d8-4d48-92af-b3afe9610f84
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 65f9c926a75ae4d64e54d6f600aba2a70f0482cf
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "63218106"
---
# <a name="setserviceaccount-method-sqlservice-class"></a>Método SetServiceAccount (clase SqlService)
  Intenta cambiar el nombre de usuario y la contraseña con los que se ejecuta la instancia del servicio.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
object  
.SetServiceAccount(  
ServiceStartName , ServiceStartPassword  
)  
  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 Objeto de la [clase SqlService](sqlservice-class.md) que representa el servicio.  
  
#### <a name="parameters"></a>Parámetros  
 *ServiceStartName*  
 Valor de cadena que especifica el nombre de la cuenta en la que se ejecuta el servicio. Según el tipo de servicio, el nombre de cuenta puede tener la forma NombreDominio\NombreUsuario. El proceso del servicio se registrará con uno de estos dos formatos cuando se ejecute:  
  
-   Si la cuenta pertenece al dominio integrado, puede especificarse \NombreUsuario.  
  
-   Si se especifica NULL, el servicio se iniciará sesión como la cuenta **LocalSystem** .  
  
 En el caso de los controladores de kernel o de nivel de sistema, *StartName* contiene el nombre de objeto del controlador, ya sea \FileSystem\Rdr o \Driver\Xns, que el sistema de e/s utiliza para cargar el controlador de dispositivo. Además, si se especifica NULL, el controlador se ejecutará con un nombre de objeto predeterminado creado por el sistema de E/S basado en el nombre del servicio. Ejemplo: DWDOM\Admin.  
  
 *ServiceStartPassword*  
 Valor de cadena que especifica la contraseña para el nombre de cuenta en el parámetro *StartName* . Especifique NULL si no va a cambiar la contraseña. Especifique una cadena vacía si el servicio no tiene contraseña.  
  
## <a name="property-valuereturn-value"></a>Valor de propiedad y valor devuelto  
 Valor de `uint32` que es igual a 0 si se modificó el servicio correctamente o igual a 1 si no se admite la solicitud. Cualquier otro número indica que hubo un error.  
  
## <a name="remarks"></a>Observaciones  
  
## <a name="see-also"></a>Consulte también  
 [Iniciar y detener servicios](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
