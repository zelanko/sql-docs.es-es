---
title: Establecer Active Directory contraseña
description: Establezca Active Directory contraseña de inicio de sesión de administrador de nodos en Modo de restauración de servicios de directorio en Analytics Platform System (APS).
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 6bbbf42106602a25b03072a9c9abfb04f04d3c49
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/22/2019
ms.locfileid: "74400336"
---
# <a name="set-admin-password-for-logging-on-to-ad-nodes-in-directory-services-restore-mode-dsrm---analytics-platform-system"></a>Establecimiento de la contraseña de administrador para iniciar sesión en los nodos de AD en Modo de restauración de servicios de directorio (DSRM)-Analytics Platform System
Modo de restauración de servicios de directorio (DSRM) es un modo de arranque para reparar o recuperar Active Directory Domain Services (AD DS). Se usa para iniciar sesión en los nodos de AD del dispositivo después de que se haya producido un error en AD DS o cuando sea necesario restaurar AD DS. La contraseña de DSRM se inicializó durante la instalación del dispositivo en el sitio del proveedor de hardware y debe cambiarla el administrador del dispositivo. Analytics Platform System tiene dos AD DS (controladores de dominio). ** _appliance_domain_-AD01** y ** _appliance_domain_-AD02**. Para cada nodo AD de dispositivo, cambie la contraseña de DSRM siguiendo estos pasos.  
  
## <a name="HowToDSRM"></a>Para restablecer la contraseña de administrador  
  
1.  Abra una ventana del símbolo del sistema en un nodo AD de dispositivo <strong> _appliance_domain_AD_xx_</strong>máquina virtual.  
  
2.  En el símbolo del sistema, escriba `ntdsutil`.  
  
3.  En el **** símbolo del sistema de `set dsrm password`Ntdsutil, escriba.  
  
4.  En el símbolo del sistema de **Restablecer contraseña de administrador:** , escriba `reset password on server null`.  
  
5.  En el símbolo del sistema, escriba la nueva contraseña.  
  
6.  Repita los pasos 1-5 anteriores para cada máquina virtual de AD de la aplicación.  
  
    > [!WARNING]  
    > Analytics Platform System no admite el carácter de signo de dólar ($) en las contraseñas de administrador de dominio o de administrador local. Una contraseña que contenga un signo de dólar se validará y podrá usarse, pero puede bloquear las actividades de actualización y mantenimiento.  
  
> [!NOTE]  
> Si el Active Directory Domain Services o la máquina virtual se daña para una máquina virtual de AD específica, la ejecución de **ReplaceVM** para la máquina virtual de ad afectada es la acción correctiva recomendada. Póngase en contacto con CSS para obtener ayuda.  
  
## <a name="see-also"></a>Véase también  
[Restablecimiento de contraseña &#40;el sistema de plataforma de análisis&#41;](password-reset.md)  
  
