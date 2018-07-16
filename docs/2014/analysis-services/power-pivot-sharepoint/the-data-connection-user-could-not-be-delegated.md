---
title: 'La conexión de datos utiliza la autenticación de Windows y las credenciales del usuario no se pudieron delegar. No se pudieron actualizar las siguientes conexiones: datos PowerPivot | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: d2006df1-d244-4786-b272-49d8996cc88c
caps.latest.revision: 5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b9cdc773ef42536be619d8d8c0edac1d6d1dcb92
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37319385"
---
# <a name="the-data-connection-uses-windows-authentication-and-user-credentials-could-not-be-delegated-the-following-connections-failed-to-refresh-powerpivot-data"></a>La conexión de datos utiliza la autenticación de Windows y las credenciales del usuario no se pudieron delegar. No se pudieron actualizar las siguientes conexiones: datos PowerPivot
  En los libros de Excel que contienen datos PowerPivot, Excel Services devuelve este error si no puede conectarse a una instancia del servidor PowerPivot en SharePoint.  
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Se aplica a|PowerPivot para SharePoint|  
|Versión del producto|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|Causa|Error en la conexión al intentar utilizar un proveedor de datos PowerPivot.|  
|Texto del mensaje|La conexión de datos utiliza la autenticación de Windows y las credenciales del usuario no se pudieron delegar. No se pudieron actualizar las siguientes conexiones: datos PowerPivot|  
  
## <a name="explanation"></a>Explicación  
 Este mensaje de error tiene varias causas posibles. El factor común de todas ellas es que Servicios de Excel no puede recibir una identidad de usuario de Windows válida de un token de notificaciones en SharePoint. En el caso de los libros de Excel que contienen datos PowerPivot, este error se produce cuando se da alguna de las condiciones siguientes:  
  
-   Notificaciones del servicio de token de Windows no se está ejecutando. Puede confirmar la causa de este error en el archivo de registro de SharePoint. Si los registros de SharePoint incluyen el mensaje "El extremo de la canalización 'net.pipe://localhost/s 4u/022694f3-9fbd-422b-b4b2-312e25dae2a2' no se pudo encontrar en el equipo local", Notificaciones del servicio de token de Windows no se está ejecutando. Para iniciarlo, utilice Administración central y, a continuación, compruebe que el servicio se está ejecutando en la aplicación de consola de Servicios.  
  
-   Un controlador de dominio no está disponible para validar la identidad del usuario. Notificaciones del servicio de token de Windows no utiliza las credenciales almacenadas en memoria caché. Valida la identidad del usuario para cada conexión. Puede confirmar la causa de este error en el archivo de registro de SharePoint. Si los registros de SharePoint incluyen el mensaje "No se puede obtener WindowsIdentity de IClaimsIdentity", la identidad del usuario no se pudo autenticar.  
  
-   Los equipos deben ser miembros del mismo dominio o de dominios que tengan una relación de confianza bidireccional.  
  
-   Debe usar cuentas de usuario de dominio de Windows. Las cuentas deben tener un nombre de entidad de seguridad universal (UPN).  
  
-   La cuenta de servicio de Servicios de Excel debe tener los permisos de Active Directory para consultar el objeto.  
  
## <a name="user-action"></a>Acción del usuario  
 Utilice las siguientes instrucciones para comprobar el estado de Notificaciones del servicio de token de Windows.  
  
 Para todos los demás escenarios, consulte al administrador de red.  
  
#### <a name="enable-claims-to-windows-token-service"></a>Habilitar Notificaciones del servicio de token de Windows  
  
1.  En Administración central, en Configuración del sistema, haga clic en **Administrar servicios en el servidor**.  
  
2.  Seleccione **Notificaciones del servicio de token de Windows**y, a continuación, haga clic en **Inicio**.  
  
3.  Compruebe que el servicio esté ejecutándose también en la consola Servicios:  
  
    1.  En Herramientas administrativas, haga clic en Servicios.  
  
    2.  Inicie Notificaciones del servicio de token de Windows, si no se está ejecutando.  
  
## <a name="see-also"></a>Vea también  
 [Configurar las cuentas de servicio PowerPivot](configure-power-pivot-service-accounts.md)  
  
  
