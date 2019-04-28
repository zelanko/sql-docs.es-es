---
title: Establecer contraseña de Active Directory - Analytics Platform System | Microsoft Docs
description: Establecer contraseña de inicio de sesión de administrador de Active Directory nodos en modo de restauración de servicios de directorio en Analytics Platform System (APS).
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 3df6203a4d98bace5d23a92e70a596a34dedb60e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62678343"
---
# <a name="set-admin-password-for-logging-on-to-ad-nodes-in-directory-services-restore-mode-dsrm---analytics-platform-system"></a>Establecer contraseña de administrador para iniciar sesión en los nodos de AD en Directory Services Restore modo (DSRM) - Analytics Platform System
Modo de restauración de servicios de directorio (DSRM) es un modo de arranque para reparar o recuperar los servicios de dominio de Active Directory (AD DS). Se utiliza para iniciar sesión en los nodos de AD del dispositivo después de que ha producido un error en AD DS o cuando AD DS debe restaurarse. La contraseña de DSRM se inicializó durante la configuración del dispositivo en el sitio del proveedor de hardware y debe ser cambiada por el administrador del dispositivo. Analytics Platform System tiene dos AD DS (controladores de dominio);  **_appliance_domain_-AD01** y  **_appliance_domain_-AD02**. Para cada nodo de dispositivo AD, cambie la contraseña DSRM siguiendo estos pasos.  
  
## <a name="HowToDSRM"></a>Para restablecer la contraseña de administrador  
  
1.  Abra una ventana del símbolo del sistema en un nodo de dispositivo AD  <strong>_appliance_domain_-AD_xx_</strong>máquina virtual.  
  
2.  En el símbolo del sistema, escriba `ntdsutil`.  
  
3.  En el **ntdsutil** , escriba `set dsrm password`.  
  
4.  En el **restablecer la contraseña de administrador:** , escriba `reset password on server null`.  
  
5.  En el símbolo del sistema, escriba la nueva contraseña.  
  
6.  Repita los pasos 1-5 anteriores para cada máquina virtual de AD del dispositivo.  
  
    > [!WARNING]  
    > Analytics Platform System no es compatible con el carácter de signo de dólar ($) en el Administrador de dominio o las contraseñas de administrador local. Una contraseña que contenga un signo de dólar validará y ser utilizable pero puede bloquear las actividades de actualización y mantenimiento.  
  
> [!NOTE]  
> Si se daña el Active Directory Domain Services o la máquina virtual para una máquina virtual específica de AD, ejecute **ReplaceVM** para el anuncio afectado la máquina virtual es la acción correctora recomendada. Póngase en contacto con CSS para obtener ayuda.  
  
## <a name="see-also"></a>Vea también  
[Restablecimiento de contraseña &#40;Analytics Platform System&#41;](password-reset.md)  
  
