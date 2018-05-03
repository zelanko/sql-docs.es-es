---
title: Propiedades de SQL Server Integration Services (pestaña Iniciar sesión) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: configuration-manager
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: c0eb1b87-6bb0-475e-8492-0fd3c3f910ea
caps.latest.revision: 14
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cd0f59372e51e597a09651fa817ac61d03c387c1
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MTE
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="sql-server-integration-services-properties-log-on-tab"></a>Propiedades de SQL Server Integration Services (pestaña Iniciar sesión)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  Use la pestaña **Iniciar sesión** del cuadro de diálogo [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] **Properties** dialog box to specify the account used by the [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] service, and to start and stop the service.  
  
## <a name="options"></a>Opciones  
 **Cuenta de sistema local**  
 Especifique una cuenta de sistema local, que no requiere una contraseña. No obstante, la cuenta del sistema local puede restringir la interacción del servicio con otros servidores, en función de los privilegios que se le hayan concedido.  
  
 **Esta cuenta**  
 Especifique una cuenta de usuario local o de dominio que utilice la autenticación de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows. [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomienda utilizar una cuenta de usuario de dominio que tenga derechos mínimos para los servicios. Para obtener información acerca de cómo seleccionar una cuenta, busque el tema sobre cómo configurar cuentas de servicios de Windows en los Libros en pantalla.  
  
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
  
  
