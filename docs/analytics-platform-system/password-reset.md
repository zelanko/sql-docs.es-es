---
title: 'Restablecimiento de contraseña: Analytics Platform System | Microsoft Docs'
description: La página de restablecimiento de contraseña permite cambiar la contraseña de Analytics Platform System utilizada las cuentas de administrador.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 5fb3bbb5adba5754c220c34503a22656f6da39c5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67960466"
---
# <a name="password-reset---analytics-platform-system"></a>Restablecimiento de contraseñas: Analytics Platform System
El **de restablecimiento de contraseña** página le permite cambiar la contraseña de Analytics Platform System utilizada las cuentas de administrador.  
  
> [!WARNING]  
> Use siempre la **Configuration Manager** para actualizar la contraseña de administrador de dominio de aplicación. Otros métodos no pueden actualizar todos los componentes de Analytics Platform System y podrían provocar problemas de acceso de dispositivo.  
  
Las contraseñas de Analytics Platform System, se proporciona cuando se entrega el dispositivo. Siempre debe cambiar las contraseñas con los nuevos valores cuando asume la responsabilidad de su dispositivo. Hay tres contraseñas para la actualización. Las contraseñas no debe ser igual entre sí.  
  
**F <*xxxx*> \Administrator**  
El **administrador** del dominio de aplicación.  
  
**. \Administrator**  
Local **administrador** cuenta en los equipos que hospedan las máquinas virtuales.  
  
> [!IMPORTANT]  
> Para el dispositivo de actualización 1, **Configuration Manager** ¿correctamente no cambiará la contraseña de las cuentas de administrador local en todo el PDW VM. Si es necesario, póngase en contacto con CSS para obtener instrucciones adicionales.  
  
**sa**  
El **sa** inicio de sesión en SQL Server. **SA** es un miembro de la **sysadmin** rol fijo de servidor y es un administrador de SQL Server. La contraseña de la **sa** también se puede cambiar el inicio de sesión mediante el uso de la **ALTER LOGIN** instrucción.  
  
## <a name="password-requirements"></a>Requisitos de contraseña  
Las credenciales de administrador de dominio y las credenciales de administrador del sistema cumplan las directivas de seguridad de contraseñas para cada tipo de credencial. Al cambiar las credenciales de administrador de dominio, la nueva contraseña se actualiza en el dominio donde sea necesario a lo largo de PDW de SQL Server.  
  
> [!IMPORTANT]  
> PDW de SQL Server no admite el carácter de signo de dólar ( **$** ) en el Administrador de dominio o las contraseñas de administrador local. Los caracteres **^ % &** se permiten en las contraseñas, sin embargo, PowerShell lo que respecta a estos elementos como caracteres especiales. Si alguno de estos caracteres se usan en las contraseñas para el administrador del sistema o SQL Server**sa** cuentas (el **AdminPassword** y **PdwSAPassword** parámetros durante programa de instalación), a continuación, instalación, se producirá un error de instalación, actualización, REPLACENODE y aplicación de revisiones, incluidos. Para garantizar una actualización correcta cuando contraseñas actuales contienen caracteres no admitidos, cambiar estas contraseñas para que no contienen dichos caracteres antes de ejecutar la actualización. Una vez completada la actualización, puede establecer estas contraseñas a sus valores originales. Para obtener más información acerca de los requisitos de contraseña, consulte [ALTER LOGIN](../t-sql/statements/alter-login-transact-sql.md).  
  
## <a name="to-reset-a-password"></a>Para restablecer una contraseña  
  
1.  Conectar con el nodo de Control e iniciar el **Configuration Manager** (**dwconfig.exe**). Para obtener más información, consulte [iniciar el Administrador de configuración &#40;Analytics Platform System&#41;](launch-the-configuration-manager.md).  
  
2.  En el panel izquierdo de la **Configuration Manager**, haga clic en **de restablecimiento de contraseña**.  
  
3.  Seleccione el tipo de administrador en el **cuenta** menú desplegable y, a continuación, escriba la nueva contraseña en el **contraseña** y **Confirmar contraseña** cuadros. Haga clic en **aplicar** para guardar los cambios.  
  
    Cambios en estas cuentas no afectan a las sesiones activas actualmente, pero se aplicará en el próximo intento de inicio de sesión para cada usuario.  
  
    ![Contraseña de DWConfig SQL Server](./media/password-reset/SQL_Server_PDW_DWConfig_TopPW.png "SQL_Server_PDW_DWConfig_TopPW")  
  
## <a name="see-also"></a>Vea también  
[Establecer contraseña de administrador para iniciar sesión en los nodos de AD en el modo de restauración de servicios de directorio &#40;DSRM&#41; &#40;Analytics Platform System&#41;](set-admin-password-for-logging-on-to-ad-nodes-in-directory-services-restore-mode.md)  
[Inicie el Administrador de configuración &#40;Analytics Platform System&#41;](launch-the-configuration-manager.md)  
  
