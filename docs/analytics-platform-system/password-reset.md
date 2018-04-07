---
title: Restablecimiento de contraseña (Analytics Platform System)
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
ms.assetid: a0f808fc-e120-430b-b6c9-11f2b1c90bf3
caps.latest.revision: 26
ms.openlocfilehash: 0574cf85dc4baaf6d92159aa423a0b1771042c59
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/06/2018
---
# <a name="password-reset"></a>Restablecimiento de contraseña
El **de restablecimiento de contraseña** página le permite cambiar la contraseña de las cuentas de administrador utilizada Analytics Platform System.  
  
> [!WARNING]  
> Utilice siempre la **Configuration Manager** para actualizar la contraseña de administrador de dominio de aplicación. Otros métodos no pueden actualizar todos los componentes de sistema de la plataforma de análisis y pudieron provocar problemas de acceso de dispositivo.  
  
Se dan las contraseñas de sistema de la plataforma de análisis cuando el dispositivo se entrega. Siempre debe cambiar las contraseñas a los nuevos valores al asumir la responsabilidad de su dispositivo. Hay tres contraseñas para actualizar. Las contraseñas no tiene que ser el mismo que entre sí.  
  
**F<*xxxx*>\Administrator**  
El **administrador** del dominio de aplicación.  
  
**.\Administrator**  
La variable local **administrador** cuenta en los equipos que hospedan las máquinas virtuales.  
  
> [!IMPORTANT]  
> Dispositivo de actualizaciones 1, **Configuration Manager** no da el cambio de la contraseña de las cuentas de administrador local en el PDW VM. Si es necesario, póngase en contacto con CSS para obtener instrucciones adicionales.  
  
**sa**  
El **sa** inicio de sesión en SQL Server. **SA** es un miembro de la **sysadmin** rol fijo de servidor y es un administrador de SQL Server. La contraseña de la **sa** también se puede cambiar el inicio de sesión mediante el uso de la **ALTER LOGIN** instrucción.  
  
## <a name="password-requirements"></a>Requisitos de contraseña  
Las credenciales de administrador de dominio y las credenciales de administrador de sistema cumplen las directivas de seguridad de contraseñas para cada tipo de credencial. Al cambiar las credenciales de administrador de dominio, la nueva contraseña se actualiza al dominio cuando sea necesario a lo largo de PDW de SQL Server.  
  
> [!IMPORTANT]  
> PDW de SQL Server no admite el carácter de signo de dólar (**$**) en el Administrador de dominio o las contraseñas de administrador local. Los caracteres **^ % &** se permiten en las contraseñas, sin embargo, PowerShell considera como caracteres especiales. Si ninguno de estos caracteres se usan en las contraseñas para el administrador del sistema o SQL Server**sa** cuentas (el **AdminPassword** y **PdwSAPassword** parámetros durante la el programa de instalación), a continuación, el programa de instalación, se producirá un error de instalación, actualización, REPLACENODE y aplicación de revisiones, incluido. Para garantizar una actualización correcta cuando las contraseñas actuales contienen caracteres no admitidos, cambiar estas contraseñas de manera que no contengan dichos caracteres antes de ejecutar la actualización. Una vez completada la actualización, puede establecer estas contraseñas a sus valores originales. Para obtener más información acerca de los requisitos de contraseña, vea [ALTER LOGIN](../t-sql/statements/alter-login-transact-sql.md).  
  
## <a name="to-reset-a-password"></a>Para restablecer una contraseña  
  
1.  Conectar con el nodo de Control e iniciar la **Configuration Manager** (**dwconfig.exe**). Para obtener más información, consulte [iniciar el Administrador de configuración &#40;Analytics Platform System&#41;](launch-the-configuration-manager.md).  
  
2.  En el panel izquierdo de la **Configuration Manager**, haga clic en **de restablecimiento de contraseña**.  
  
3.  Seleccione el tipo de administrador en el **cuenta** menú desplegable y, a continuación, escriba la nueva contraseña en el **contraseña** y **Confirmar contraseña** cuadros. Haga clic en **aplicar** para guardar los cambios.  
  
    Los cambios que realice para estas cuentas no afectan a las sesiones actualmente activas, pero se aplicarán en el próximo intento de inicio de sesión para cada usuario.  
  
    ![Contraseña de DWConfig SQL Server](./media/password-reset/SQL_Server_PDW_DWConfig_TopPW.png "SQL_Server_PDW_DWConfig_TopPW")  
  
## <a name="see-also"></a>Vea también  
[Establecer contraseña de administrador para iniciar sesión en los nodos de AD en modo de restauración de servicios de directorio &#40;DSRM&#41; &#40;sistema de la plataforma de análisis&#41;](set-admin-password-for-logging-on-to-ad-nodes-in-directory-services-restore-mode.md)  
[Inicie el Administrador de configuración &#40;sistema de la plataforma de análisis&#41;](launch-the-configuration-manager.md)  
  
