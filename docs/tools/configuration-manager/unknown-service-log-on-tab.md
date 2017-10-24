---
title: "Servicio desconocido (pestaña iniciar sesión) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e9b35cb5-d8ae-42ea-b59e-deedc99c4823
caps.latest.revision: 16
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 8951624c19b03c7630698fe08aa7987e780dc35d
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="unknown-service-log-on-tab"></a>Servicio desconocido (pestaña Iniciar sesión)
  [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] No puede identificar este servicio.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Administrador de configuración recibe información del servicio del proveedor WMI en el equipo que ejecuta el servicio. Se ha producido un error al leer las propiedades del servicio o éstas no están completas. Para solucionar el problema, intente cerrar y volver a abrir el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o compruebe el proveedor WMI del equipo en el que se ejecuta el servicio.  
  
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
  
  

