---
title: Establecer contraseña de inicio de sesión de administrador de nodos de AD en modo de restauración de servicios de directorio (APS)
author: barbkess
ms.author: barbkess
manager: craigg
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: ''
ms.component: ''
ms.technology: mpp-data-warehouse
ms.custom: ''
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 97a9c715-2763-417d-b45c-bb0180759e47
caps.latest.revision: 20
ms.openlocfilehash: 3e09305152a2892ae4acaf7096921d2a73345b63
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/06/2018
---
# <a name="set-admin-password-for-logging-on-to-ad-nodes-in-directory-services-restore-mode-dsrm"></a>Establecer contraseña de administrador para iniciar sesión en los nodos de AD en modo de restauración de servicios de directorio (DSRM)
Modo de restauración de servicios de directorio (DSRM) es un modo de arranque para reparar o recuperar los servicios de dominio de Active Directory (AD DS). Se utiliza para iniciar sesión en los nodos de dispositivo AD cuando se produzca error AD DS o cuando AD DS debe restaurarse. La contraseña de DSRM se inicializó durante la instalación del dispositivo en el sitio del proveedor de hardware y debe ser cambiada por el administrador del equipo. Sistema de la plataforma de análisis tiene dos AD DS (controladores de dominio); ***appliance_domain *-AD01** y ***appliance_domain *-AD02**. Para cada nodo de dispositivo AD, cambie la contraseña DSRM con los siguientes pasos.  
  
## <a name="HowToDSRM"></a>Para restablecer la contraseña de administrador  
  
1.  Abra una ventana del símbolo del sistema en un nodo de dispositivo AD ***appliance_domain*AD*xx***máquina virtual.  
  
2.  En el símbolo del sistema, escriba `ntdsutil`.  
  
3.  En el **ntdsutil** , escriba `set dsrm password`.  
  
4.  En el **restablecer la contraseña de administrador:** , escriba `reset password on server null`.  
  
5.  En el símbolo del sistema, escriba la nueva contraseña.  
  
6.  Repita los pasos 1 a 5 anteriores para cada máquina virtual de AD del dispositivo.  
  
    > [!WARNING]  
    > Sistema de la plataforma de análisis no es compatible con el carácter de signo de dólar ($) en el Administrador de dominio o las contraseñas de administrador local. Una contraseña que contenga un signo de dólar podrá validar y utilizable pero puede bloquear las actividades de actualización y mantenimiento.  
  
> [!NOTE]  
> Si se daña los servicios de dominio de Active Directory o la máquina virtual para una máquina virtual específica de AD, ejecutando **ReplaceVM** para el anuncio afectado máquina virtual es la acción correctora recomendada. Póngase en contacto con CSS para obtener ayuda.  
  
## <a name="see-also"></a>Vea también  
[Restablecimiento de contraseña &#40;sistema de la plataforma de análisis&#41;](password-reset.md)  
  
