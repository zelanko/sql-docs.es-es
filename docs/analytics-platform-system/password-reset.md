---
title: Restablecimiento de contraseña
description: La página de restablecimiento de contraseña le permite cambiar la contraseña de las cuentas de administrador que usa Analytics Platform System.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 952dbda04b4f7132406e3a6de4479afea1be92e7
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/25/2020
ms.locfileid: "74400906"
---
# <a name="password-reset---analytics-platform-system"></a>Restablecimiento de contraseña: Analytics Platform System
La página de **restablecimiento de contraseña** le permite cambiar la contraseña de las cuentas de administrador que usa Analytics Platform System.  
  
> [!WARNING]  
> Use siempre el **Configuration Manager** para actualizar la contraseña de administrador de dominio de la aplicación. Otros métodos podrían no actualizar todos los componentes de Analytics Platform System y podrían causar problemas de acceso a la aplicación.  
  
Cuando se entregue el dispositivo, se le proporcionarán las contraseñas del sistema de la plataforma de análisis. Cambie siempre las contraseñas a nuevos valores cuando asuma la responsabilidad de su dispositivo. Hay tres contraseñas para actualizar. No es necesario que las contraseñas sean las mismas.  
  
**F<*xxxx*> \Administrador**  
El **Administrador** del dominio de la aplicación.  
  
**.\Administrator**  
La cuenta de **Administrador** local en los equipos que hospedan las máquinas virtuales.  
  
> [!IMPORTANT]  
> En el caso de la actualización 1 del dispositivo, **Configuration Manager** no cambia correctamente la contraseña de las cuentas de administrador local en las máquinas virtuales de PDW. Si es necesario, póngase en contacto con CSS para obtener instrucciones adicionales.  
  
**valida**  
Inicio de sesión **SA** en SQL Server. **SA** es miembro del rol fijo de servidor **sysadmin** y es un administrador de SQL Server. La contraseña del inicio de sesión **SA** también se puede cambiar mediante la instrucción **ALTER login** .  
  
## <a name="password-requirements"></a>Requisitos de contraseñas  
Las credenciales de administrador de dominio y las credenciales de administrador del sistema se adhieren a las directivas de seguridad de contraseña para cada tipo de credencial. Al cambiar las credenciales de administrador de dominio, la nueva contraseña se actualiza en el dominio donde sea necesario en PDW de SQL Server.  
  
> [!IMPORTANT]  
> PDW de SQL Server no admite el carácter de signo de dólar ( **$** ) en las contraseñas de administrador de dominio o de administrador local. Los caracteres **^% &** se permiten en las contraseñas; sin embargo, PowerShell los considera como caracteres especiales. Si se usa cualquiera de estos caracteres en contraseñas para el administrador del sistema o SQL Server cuentas**SA** (los parámetros **AdminPassword** y **PdwSAPassword** durante la instalación), se producirá un error en la instalación, incluida la instalación, la actualización, la REPLACENODE y la revisión. Para garantizar una actualización correcta cuando las contraseñas actuales contienen caracteres no admitidos, cambie estas contraseñas para que no contengan dichos caracteres antes de ejecutar la actualización. Una vez finalizada la actualización, puede volver a establecer estas contraseñas en sus valores originales. Para obtener más información sobre los requisitos de contraseña, consulte [ALTER login](../t-sql/statements/alter-login-transact-sql.md).  
  
## <a name="to-reset-a-password"></a>Para restablecer una contraseña  
  
1.  Conéctese al nodo de control e inicie el **Configuration Manager** (**dwconfig.exe**). Para obtener más información, consulte [Inicio del&#41;de &#40;de Configuration Manager de la plataforma de análisis ](launch-the-configuration-manager.md).  
  
2.  En el panel izquierdo del **Configuration Manager**, haga clic en **restablecimiento de contraseña**.  
  
3.  Seleccione el tipo de administrador en el menú desplegable **cuenta** y, a continuación, escriba la nueva contraseña en los cuadros **contraseña** y **Confirmar contraseña** . Haga clic en **aplicar** para guardar los cambios.  
  
    Los cambios que realice en estas cuentas no afectarán a las sesiones activas, pero se aplicarán en el siguiente intento de inicio de sesión de cada usuario.  
  
    ![Contraseña SQL Server DWConfig](./media/password-reset/SQL_Server_PDW_DWConfig_TopPW.png "SQL_Server_PDW_DWConfig_TopPW")  
  
## <a name="see-also"></a>Consulte también  
[Establezca la contraseña de administrador para iniciar sesión en los nodos de AD en Modo de restauración de servicios de directorio &#40;DSRM&#41; &#40;Analytics Platform System&#41;](set-admin-password-for-logging-on-to-ad-nodes-in-directory-services-restore-mode.md)  
[Inicie el sistema de Configuration Manager &#40;Analytics Platform&#41;](launch-the-configuration-manager.md)  
  
