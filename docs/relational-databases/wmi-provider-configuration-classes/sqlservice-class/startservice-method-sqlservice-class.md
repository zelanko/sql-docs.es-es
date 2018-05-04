---
title: Método StartService (clase SqlService) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: wmi
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- StartService Method (SqlService Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- StartService method
ms.assetid: 83dfb6bd-dbd5-45d8-aad2-a11926317f91
caps.latest.revision: 34
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 356a81746d12b3564ff5c7af1c7984100bb7f71d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="startservice-method-sqlservice-class"></a>Método StartService (clase SqlService)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Intenta poner el servicio en estado iniciado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
object.StartService()  
```  
  
## <a name="parts"></a>Partes  
 *objeto*  
 Objeto de la [clase SqlService](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) que representa el servicio.  
  
## <a name="property-valuereturn-value"></a>Valor de propiedad y valor devuelto  
 Valor uint32 que especifica uno de los estados de inicio siguientes.  
  
 0  
 Correcto. Se aceptó la solicitud.  
  
 1  
 No compatible. No se admite la solicitud.  
  
 2  
 Acceso denegado. El usuario no tenía el permiso de acceso adecuado.  
  
 3  
 Servicios dependientes en ejecución. No se puede detener el servicio porque otros servicios que se están ejecutando dependen de él.  
  
 4  
 Control de servicio no válido. El código de control solicitado no es válido o no es aceptable para el servicio.  
  
 5  
 El servicio no puede aceptar el control. El código de control solicitado no se puede enviar al servicio porque el estado del servicio (Win32_BaseService:State) es igual a 0, 1 ó 2.  
  
 6  
 Servicio no activo. El servicio no se ha iniciado.  
  
 7  
 Tiempo de espera de solicitud de servicio. El servicio no respondió a tiempo a la solicitud de inicio.  
  
 8  
 Error desconocido. Se produjo un error desconocido al iniciar el servicio.  
  
 9  
 No se ha encontrado la ruta de acceso. No se encontró la ruta de acceso al directorio del ejecutable del servicio.  
  
 10  
 Servicio ya en ejecución. El servicio ya se está ejecutando.  
  
 11  
 Base de datos de servicio bloqueada. La base de datos para agregar un nuevo servicio está bloqueada.  
  
 12  
 Dependencia de servicio eliminada. Una dependencia en la que se basaba este servicio se ha quitado del sistema.  
  
 13  
 Error de dependencia de servicio. El servicio no pudo encontrar el servicio necesario de un servicio dependiente.  
  
 14  
 Servicio deshabilitado. El servicio se ha deshabilitado del sistema.  
  
 15  
 Error de inicio de sesión del servicio. El servicio no tiene la autenticación correcta para ejecutarse en el sistema.  
  
 16  
 Servicio marcado para eliminación. El servicio se va a quitar del sistema.  
  
 17  
 Servicio sin subproceso. No hay ningún subproceso de ejecución para el servicio.  
  
 18  
 Estado Dependencia circular. Hay dependencias circulares al iniciarse el servicio.  
  
 19  
 Estado Nombre replicado. Hay un servicio que se ejecuta con el mismo nombre.  
  
 20  
 Estado Nombre no válido. Hay caracteres no válidos en el nombre del servicio.  
  
 21  
 Estado Parámetro no válido. Se han pasado parámetros no válidos al servicio.  
  
 22  
 Estado Cuenta de servicio no válida. La cuenta bajo la que se ejecuta este servicio no es válida o carece de permisos para ejecutar el servicio.  
  
 23  
 Estado El servicio existe. El servicio existe en la base de datos de servicios disponibles del sistema.  
  
 24  
 Servicio ya pausado. El servicio se encuentra en pausa actualmente en el sistema.  
  
## <a name="remarks"></a>Comentarios  
  
## <a name="see-also"></a>Vea también  
 [Iniciar y detener servicios](http://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
