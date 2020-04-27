---
title: Cuentas de servicio (Asistente para la configuración de seguridad de la creación de reflejo de bases de datos) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.configdbmsecurwiz.serviceaccounts.f1
ms.assetid: d58d8f93-7888-4d66-af4d-969ef6a2dbee
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 69877c6a20e37e012925185d0b807e9579066e35
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "62754396"
---
# <a name="service-accounts-configure-database-mirroring-security-wizard"></a>Cuentas de servicio (Asistente para la configuración de seguridad de la creación de reflejo de bases de datos)
  Al utilizar la autenticación de Windows, si las instancias del servidor usan cuentas diferentes, especifique las cuentas de servicio para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Estas cuentas de servicio deben ser cuentas de dominio (en el mismo dominio o en dominios de confianza).  
  
 Si todas las instancias del servidor utilizan la misma cuenta de dominio o la autenticación basada en certificados, deje los campos en blanco. Basta con hacer clic en **Finalizar**y el asistente configura automáticamente las cuentas en función de la cuenta del asistente actual.  
  
> [!IMPORTANT]  
>  Si los extremos de creación de reflejo de la base de datos de las instancias de servidor están configurados para usar certificados, debe dejar vacíos los campos de cuenta de servicio.  
  
 **Para configurar la creación de reflejo de la base de datos mediante SQL Server Management Studio**  
  
-   [Establecer una sesión de creación de reflejo de la base de datos mediante la autenticación de Windows &#40;SQL Server Management Studio&#41;](establish-database-mirroring-session-windows-authentication.md)  
  
-   [Iniciar el Asistente para la configuración de seguridad de la creación de reflejo de la base de datos &#40;SQL Server Management Studio&#41;](start-the-configuring-database-mirroring-security-wizard.md)  
  
## <a name="options"></a>Opciones  
 **Entidad**  
 Especifique la cuenta de servicio de la instancia de servidor principal. Escriba el nombre del dominio en mayúsculas:  
  
 *NombreDeDominio*\\*nombreDeUsuario*  
  
 **Reflejo**  
 Especifique la cuenta de servicio de la instancia del servidor reflejado. Escriba el nombre del dominio en mayúsculas:  
  
 *NombreDeDominio*\\*nombreDeUsuario*  
  
 **Testigo**  
 Especifique la cuenta de servicio de la instancia de servidor testigo. Escriba el nombre del dominio en mayúsculas:  
  
 *NombreDeDominio*\\*nombreDeUsuario*  
  
## <a name="see-also"></a>Consulte también  
 [Propiedades de la base de datos &#40;página creación de reflejo&#41;](../../relational-databases/databases/database-properties-mirroring-page.md)   
 [Iniciar Monitor de creación de reflejo de la base de datos &#40;SQL Server Management Studio&#41;](../database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)   
 [SQL Server de &#40;de creación de reflejo de la base de datos&#41;](database-mirroring-sql-server.md)   
 [Configurar cuentas de inicio de sesión para la creación de reflejo de la base de datos o Grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](set-up-login-accounts-database-mirroring-always-on-availability.md)  
  
  
