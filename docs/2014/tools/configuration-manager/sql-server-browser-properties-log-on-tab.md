---
title: Propiedades de SQL Server Browser (pestaña Iniciar sesión) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- configmgr-client
ms.topic: conceptual
ms.assetid: c77871ec-c2f4-4e4a-9a10-5aeb4ae70507
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 685911d9efb0b43b9b0d111e5d45a341c5436a13
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48210515"
---
# <a name="sql-server-browser-properties-log-on-tab"></a>Propiedades de SQL Server Browser (pestaña Iniciar sesión)
  El programa Explorador de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se ejecuta como un servicio en el servidor. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser escucha las solicitudes entrantes de recursos de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y proporciona información acerca de las instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instaladas en el equipo.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] El Explorador escucha en un puerto UDP y acepta solicitudes no autenticadas que usan el protocolo de resolución de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SSRP).  
  
 Cambiar la contraseña de una cuenta surte efecto inmediato, sin necesidad de reiniciar el servicio.  
  
## <a name="options"></a>Opciones  
 **Cuenta de sistema local**  
 Ejecute el servicio Explorador de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el contexto de seguridad de la cuenta Sistema local. Si es posible, utilice en su lugar una cuenta con permisos limitados.  
  
 **Esta cuenta**  
 Especifique una cuenta de usuario local o de dominio que utilice la autenticación de Windows. Se recomienda utilizar una cuenta de usuario de dominio que tenga derechos mínimos para los servicios. Para obtener información acerca de cómo seleccionar una cuenta, vea el tema sobre la configuración de cuentas de servicios de Windows en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **Examinar**  
 Busque un usuario o una entidad de seguridad integrada.  
  
> [!IMPORTANT]  
>  Utilice una cuenta con permisos limitados. Para obtener información sobre los permisos necesarios para el servicio Explorador de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , vea la sección sobre seguridad del [Servicio SQL Server Browser](../../../2014/tools/configuration-manager/sql-server-browser-service.md).  
  
 **Contraseña**  
 Escriba la contraseña de la entidad de seguridad.  
  
 **Confirmar contraseña**  
 Confirme la contraseña de la entidad de seguridad.  
  
 **Estado del servicio**  
 Indica si el servicio está en ejecución, detenido o deshabilitado. "**…**" indica que hay un cambio de estado pendiente.  
  
 **Iniciar**  
 Inicie el servicio Explorador de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **Detener**  
 Detenga el servicio Explorador de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **Pausar**  
 Pause el servicio Explorador de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **Reanudar**  
 Reanude un servicio Explorador de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pausado.  
  
## <a name="see-also"></a>Vea también  
 [Servicio SQL Server Browser](../../../2014/tools/configuration-manager/sql-server-browser-service.md)  
  
  
