---
title: "Propiedades del servidor (página Seguridad) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.swb.serverproperties.security.f1
ms.assetid: b8a131c7-e7bd-4203-bf26-234f1ebfe622
caps.latest.revision: "31"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 908e7cd39bb8a415daef33e9e633dfbf0f6e3984
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="server-properties---security-page"></a>Propiedades del servidor (página Seguridad)
  Utilice esta página para ver o modificar las opciones de seguridad del servidor.  
  
## <a name="server-authentication"></a>Autenticación de servidor  
 **Modo de autenticación de Windows**  
 Utiliza la autenticación de Windows para validar las conexiones intentadas. Si la contraseña de **sa** está en blanco cuando se cambia el modo de seguridad, se solicita al usuario que escriba una contraseña de **sa** .  
  
> [!IMPORTANT]  
>  La Autenticación de Windows es mucho más segura que la Autenticación de SQL Server. Siempre que sea posible, utilice la autenticación de Windows.  
  
 **Modo de autenticación de Windows y SQL Server**  
 Utiliza autenticación de modo mixto para comprobar las conexiones intentadas, a efectos de compatibilidad con versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Si la contraseña de **sa** está en blanco cuando se cambia el modo de seguridad, se solicita al usuario que escriba una contraseña de **sa** .  
  
> [!NOTE]  
>  El cambio de la configuración de seguridad requiere reiniciar el servicio. Cuando se cambia la Autenticación de servidor al modo de autenticación de Windows y SQL Server, la cuenta SA no se habilita automáticamente. Para utilizar la cuenta SA, ejecute [ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md) con la opción ENABLE.  
  
## <a name="login-auditing"></a>Auditoría de inicio de sesión  
 **Ninguno**  
 Desactiva la auditoría de inicio de sesión.  
  
 **Solo inicios de sesión erróneos**  
 Solo realiza la auditoría de inicios de sesión incorrectos.  
  
 **Solo inicios de sesión correctos**  
 Solo realiza la auditoría de inicios de sesión correctos.  
  
 **Inicios de sesión correctos y erróneos**  
 Realiza la auditoría de todos los inicios de sesión.  
  
> [!NOTE]  
>  El cambio del nivel de auditoría requiere reiniciar el servicio.  
  
## <a name="server-proxy-account"></a>Cuenta de proxy del servidor  
 **Habilitar cuenta de proxy del servidor**  
 Permite que **xp_cmdshell**use una cuenta. Las cuentas de proxy permiten la suplantación de inicios de sesión, roles de servidor y roles de base de datos cuando se ejecuta un comando del sistema operativo.  
  
> [!CAUTION]  
>  El inicio de sesión que utiliza la cuenta de proxy del servidor debe tener asignados solo los privilegios mínimos necesarios para realizar el trabajo propuesto. Un usuario malicioso puede utilizar los privilegios excesivos en la cuenta de proxy para comprometer la seguridad del sistema.  
  
 **Cuenta de proxy**  
 Especifique la cuenta de proxy que se utiliza.  
  
 **Contraseña**  
 Especifique la contraseña de la cuenta de proxy.  
  
## <a name="options"></a>Opciones  
 **Habilitar C2 audit tracing**  
 Audita todos los intentos de obtener acceso a instrucciones y objetos, y registra dichos intentos en un archivo del directorio \MSSQL\Data para las instancias predeterminadas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o del directorio \MSSQL$*nombreDeInstancia*\Data para las instancias con nombre de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información, vea [c2 audit mode (opción de configuración del servidor)](../../database-engine/configure-windows/c2-audit-mode-server-configuration-option.md).  
  
 **Encadenamiento de propiedad entre bases de datos**  
 Seleccione esta opción para permitir que la base de datos pueda ser el origen o destino de una cadena de propiedad entre bases de datos. Para obtener más información, vea [cross db ownership chaining (opción de configuración del servidor)](../../database-engine/configure-windows/cross-db-ownership-chaining-server-configuration-option.md).  
  
## <a name="see-also"></a>Vea también  
 [Opciones de configuración de servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
  
