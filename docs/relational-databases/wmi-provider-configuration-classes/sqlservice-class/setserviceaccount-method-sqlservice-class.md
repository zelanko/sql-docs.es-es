---
title: "Método SetServiceAccount (clase SqlService) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: wmi
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- SetServiceAccount Method (SqlService Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetServiceAccount method
ms.assetid: d5782892-e9d8-4d48-92af-b3afe9610f84
caps.latest.revision: 
author: JennieHubbard
ms.author: jhubbard
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1bdcb3f6789baf009165a74bcf3d82630fa868fd
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2018
---
# <a name="setserviceaccount-method-sqlservice-class"></a>Método SetServiceAccount (clase SqlService)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
Intenta cambiar el nombre de usuario y la contraseña con los que se ejecuta la instancia del servicio.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
object.SetServiceAccount(ServiceStartName , ServiceStartPassword)  
```  
  
## <a name="parts"></a>Partes  
 *objeto*  
 Objeto de la [clase SqlService](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) que representa el servicio.  
  
#### <a name="parameters"></a>Parámetros  
 *ServiceStartName*  
 Valor de cadena que especifica el nombre de la cuenta en la que se ejecuta el servicio. Según el tipo de servicio, el nombre de cuenta puede tener la forma NombreDominio\NombreUsuario. El proceso del servicio se registrará con uno de estos dos formatos cuando se ejecute:  
  
-   Si la cuenta pertenece al dominio integrado, puede especificarse \NombreUsuario.  
  
-   Si se especifica NULL, el servicio se registrará como el **LocalSystem** cuenta.  
  
 Para el kernel o los controladores de nivel de sistema, *StartName* contiene el nombre del objeto controlador, \FileSystem\Rdr o \Driver\Xns, que el sistema de E/S que se utiliza para cargar el controlador de dispositivo. Además, si se especifica NULL, el controlador se ejecutará con un nombre de objeto predeterminado creado por el sistema de E/S basado en el nombre del servicio. Ejemplo: DWDOM\Admin.  
  
 *ServiceStartPassword*  
 Un valor de cadena que especifica la contraseña para el nombre de cuenta en el *StartName* parámetro. Especifique NULL si no va a cambiar la contraseña. Especifique una cadena vacía si el servicio no tiene contraseña.  
  
## <a name="property-valuereturn-value"></a>Valor de propiedad y valor devuelto  
 Valor de **uint32** que es igual a 0 si se modificó el servicio correctamente o igual a 1 si no se admite la solicitud. Cualquier otro número indica que hubo un error.  
  
## <a name="remarks"></a>Comentarios  
  
## <a name="see-also"></a>Vea también  
 [Iniciar y detener servicios](http://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
