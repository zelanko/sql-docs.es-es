---
title: Método SetServiceAccount (clase SqlService) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
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
caps.latest.revision: 36
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 74f296fd52640c950d7d2c4b227a1c3aedb17df7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36103492"
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
  
-   Si se especifica NULL, el servicio se registrará como el **LocalSystem** cuenta.  
  
 Para el kernel o los controladores de nivel de sistema, *StartName* contiene el nombre del objeto controlador, \FileSystem\Rdr o \Driver\Xns, que el sistema de E/S que se utiliza para cargar el controlador de dispositivo. Además, si se especifica NULL, el controlador se ejecutará con un nombre de objeto predeterminado creado por el sistema de E/S basado en el nombre del servicio. Ejemplo: DWDOM\Admin.  
  
 *ServiceStartPassword*  
 Un valor de cadena que especifica la contraseña para el nombre de cuenta en el *StartName* parámetro. Especifique NULL si no va a cambiar la contraseña. Especifique una cadena vacía si el servicio no tiene contraseña.  
  
## <a name="property-valuereturn-value"></a>Valor de propiedad y valor devuelto  
 Valor de `uint32` que es igual a 0 si se modificó el servicio correctamente o igual a 1 si no se admite la solicitud. Cualquier otro número indica que hubo un error.  
  
## <a name="remarks"></a>Notas  
  
## <a name="see-also"></a>Vea también  
 [Iniciar y detener servicios](http://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  