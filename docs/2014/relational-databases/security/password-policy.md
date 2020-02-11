---
title: Directiva de contraseñas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- ALTER LOGIN statement
- passwords [SQL Server], policy enforcement
- logins [SQL Server], passwords
- CHECK_EXPIRATION option
- complex passwords [SQL Server]
- passwords [SQL Server], expiration
- manual bad password count resets
- MUST_CHANGE option
- expiration [SQL Server]
- expired password [SQL Server]
- symbols [SQL Server]
- NetValidatePasswordPolicy() API
- passwords [SQL Server]
- password policy [SQL Server]
- resetting bad password counts
- security [SQL Server], passwords
- CHECK_POLICY option
- passwords [SQL Server], symbols
- bad password counts
- passwords [SQL Server], complexity
- characters [SQL Server], password policies
ms.assetid: c0040c0a-a18f-45b9-9c40-0625685649b1
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 7b28043d797585496686dea6fd0c5fad276f16b9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "63187969"
---
# <a name="password-policy"></a>Directiva de contraseñas
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede usar los mecanismos de directiva de contraseñas de Windows. La directiva de contraseñas se aplica a un inicio de sesión que usa la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y a un usuario con contraseña de una base de datos independiente.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede aplicar las mismas directivas de complejidad y expiración que se usan en Windows a las contraseñas que se usan en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esta funcionalidad depende de la API `NetValidatePasswordPolicy` .  
  
## <a name="password-complexity"></a>Complejidad de las contraseñas  
 Las directivas de complejidad de contraseñas están diseñadas para impedir ataques por fuerza bruta mediante el aumento del número de contraseñas posibles. Cuando se aplica la directiva de complejidad de contraseñas, se exige que las nuevas contraseñas cumplan las siguientes directrices:  
  
-   La contraseña no debe contener el nombre de la cuenta del usuario.  
  
-   La contraseña debe tener una longitud de ocho caracteres como mínimo.  
  
-   La contraseña debe contener caracteres de tres de las siguientes categorías:  
  
    -   Letras en mayúsculas del alfabeto Latín (de la A a la Z)  
  
    -   Letras en minúsculas del alfabeto Latín (de la "a" a la "z")  
  
    -   Dígitos en base 10 (del 0 al 9)  
  
    -   Caracteres que no sean alfanuméricos, como signo de admiración (!), signo de moneda ($), signo de almohadilla (#) o porcentaje (%).  
  
 Las contraseñas pueden tener hasta 128 caracteres. Se recomienda utilizar contraseñas lo más largas y complejas posible.  
  
## <a name="password-expiration"></a>Expiración de las contraseñas  
 Las directivas de expiración de contraseñas se utilizan para administrar la duración de una contraseña. Cuando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aplica la directiva de expiración de contraseñas, se recuerda a los usuarios que cambien las contraseñas antiguas, y las cuentas con contraseñas que han expirado se deshabilitan.  
  
## <a name="policy-enforcement"></a>Aplicación de las directivas  
 La aplicación de la directiva de contraseñas se puede configurar independientemente para cada inicio de sesión de SQL Server. Use [ALTER LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-login-transact-sql) para configurar las opciones de la directiva de contraseñas de un inicio de sesión de SQL Server. Se aplican las siguientes reglas a la configuración de la aplicación de directivas de contraseñas:  
  
-   Cuando el valor de CHECK_POLICY se cambia a ON, ocurre lo siguiente:  
  
    -   CHECK_EXPIRATION también se establece en ON, salvo que se haya establecido de forma explícita en OFF.  
  
    -   El historial de contraseñas se inicializa con el valor del hash de contraseña actual.  
  
    -   **Duración del bloqueo de cuenta**, **umbral de bloqueo de cuenta**y **restablecer contador de bloqueo de cuenta después** de también están habilitados.  
  
-   Cuando el valor de CHECK_POLICY se cambia a OFF, ocurre lo siguiente:  
  
    -   La opción CHECK_EXPIRATION también se cambia a OFF.  
  
    -   Se borra el historial de contraseñas.  
  
    -   Se restablece el valor de `lockout_time` .  
  
 Algunas combinaciones de opciones de directiva no se admiten.  
  
-   Si se especifica MUST_CHANGE, CHECK_EXPIRATION y CHECK_POLICY, deben establecerse en ON. Si no es así, la instrucción producirá un error.  
  
-   Si CHECK_POLICY se establece en OFF, CHECK_EXPIRATION no puede establecerse en ON. Una instrucción ALTER LOGIN con esta combinación de opciones dará error.  
  
 Establecer CHECK_POLICY = ON impide la creación de las contraseñas que sean:  
  
-   NULL o vacías  
  
-   Iguales al nombre del equipo o el inicio de sesión  
  
-   Una de las siguientes: "password", "admin", "administrator", "sa", "sysadmin"  
  
 La directiva de seguridad se podría establecer en Windows o se podría recibir del dominio. Para ver la directiva de contraseñas en el equipo, use el complemento de MMC Directiva de seguridad local (**secpol.msc**).  
  
## <a name="related-tasks"></a>Related Tasks  
 [CREATE LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-login-transact-sql)  
  
 [ALTER LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-login-transact-sql)  
  
 [CREATE USER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-user-transact-sql)  
  
 [ALTER USER &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-user-transact-sql)  
  
 [Crear un inicio de sesión](authentication-access/create-a-login.md)  
  
 [Creación de un usuario de base de datos](authentication-access/create-a-database-user.md)  
  
## <a name="related-content"></a>Contenido relacionado  
 [Contraseñas seguras](strong-passwords.md)  
  
  
