---
title: Servicio desconocido (pestaña iniciar sesión) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- configmgr-client
ms.topic: conceptual
ms.assetid: e9b35cb5-d8ae-42ea-b59e-deedc99c4823
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8d72dbd993c3944131e80ad4ba6215cee3d3cf2e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48147485"
---
# <a name="unknown-service-log-on-tab"></a>Servicio desconocido (pestaña Iniciar sesión)
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no puede identificar este servicio.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] recibe información de los servicios del proveedor WMI del equipo que ejecuta el servicio. Se ha producido un error al leer las propiedades del servicio o éstas no están completas. Para solucionar el problema, intente cerrar y volver a abrir el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o compruebe el proveedor WMI del equipo en el que se ejecuta el servicio.  
  
 El proveedor WMI es un componente de Windows. Para obtener información sobre cómo comprobar los permisos en el proveedor de WMI, vea "Cómo: Configure WMI para mostrar Estado del Servidor en herramientas SQL Server" en los Libros en pantalla de SQL Server.  
  
 Si cree que está viendo el servicio correcto, utilice la pestaña **Iniciar sesión** del cuadro de diálogo **Propiedades de Servicio desconocido** para especificar la cuenta utilizada por este servicio, así como para iniciar y detener el servicio.  
  
## <a name="options"></a>Opciones  
 **Cuenta de sistema local**  
 Especifique una cuenta de sistema local, que no requiere una contraseña. No obstante, la cuenta del sistema local puede impedir la interacción del servicio con otros servidores, en función de los privilegios que se hayan concedido a la cuenta.  
  
 **Esta cuenta**  
 Especifique una cuenta de usuario local o de dominio que utilice la autenticación de Windows. Se recomienda utilizar una cuenta de usuario de dominio que tenga derechos mínimos para los servicios. Para obtener información acerca de cómo seleccionar una cuenta, vea el tema sobre la configuración de cuentas de servicios de Windows en los Libros en pantalla de SQL Server.  
  
 **Nombre de cuenta**  
 Escriba el nombre de la cuenta de usuario local o de dominio.  
  
 **Contraseña**  
 Escriba la contraseña de la cuenta.  
  
 **Confirmar contraseña**  
 Escriba de nuevo la contraseña de la cuenta.  
  
 **Iniciar**  
 Inicie el servicio.  
  
 **Detener**  
 Detenga el servicio.  
  
 **Pausar**  
 Pause el servicio.  
  
 **Reanudar**  
 Reanude un servicio en pausa.  
  
  
