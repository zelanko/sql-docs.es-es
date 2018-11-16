---
title: Método SetServiceAccount (clase SqlService) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SetServiceAccount Method (SqlService Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetServiceAccount method
ms.assetid: d5782892-e9d8-4d48-92af-b3afe9610f84
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 43fb8aefcee5880cd941b8d88553c7ef6d266632
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/15/2018
ms.locfileid: "51675674"
---
# <a name="setserviceaccount-method-sqlservice-class"></a>Método SetServiceAccount (clase SqlService)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Intenta cambiar el nombre de usuario y la contraseña con los que se ejecuta la instancia del servicio.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
object.SetServiceAccount(ServiceStartName , ServiceStartPassword)  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 Objeto de la [clase SqlService](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) que representa el servicio.  
  
#### <a name="parameters"></a>Parámetros  
 *ServiceStartName*  
 Valor de cadena que especifica el nombre de la cuenta en la que se ejecuta el servicio. Según el tipo de servicio, el nombre de cuenta puede tener la forma NombreDominio\NombreUsuario. El proceso del servicio se registrará con uno de estos dos formatos cuando se ejecute:  
  
-   Si la cuenta pertenece al dominio integrado, puede especificarse \NombreUsuario.  
  
-   Si se especifica NULL, el servicio de haber iniciado sesión como el **LocalSystem** cuenta.  
  
 Para los controladores de kernel o nivel de sistema, *StartName* contiene el nombre de objeto de controlador, \FileSystem\Rdr o \Driver\Xns, que usa el sistema de E/S para cargar el controlador de dispositivo. Además, si se especifica NULL, el controlador se ejecutará con un nombre de objeto predeterminado creado por el sistema de E/S basado en el nombre del servicio. Ejemplo: DWDOM\Admin.  
  
 *ServiceStartPassword*  
 Un valor de cadena que especifica la contraseña para el nombre de cuenta en el *StartName* parámetro. Especifique NULL si no va a cambiar la contraseña. Especifique una cadena vacía si el servicio no tiene contraseña.  
  
## <a name="property-valuereturn-value"></a>Valor de propiedad y valor devuelto  
 Valor de **uint32** que es igual a 0 si se modificó el servicio correctamente o igual a 1 si no se admite la solicitud. Cualquier otro número indica que hubo un error.  
  
## <a name="remarks"></a>Comentarios  
  
## <a name="see-also"></a>Vea también  
 [Iniciar y detener servicios](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
