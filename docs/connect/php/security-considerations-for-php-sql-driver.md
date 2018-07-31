---
title: Consideraciones de seguridad para los controladores de Microsoft para PHP para SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- security considerations
ms.assetid: a8c1a570-9204-454f-b94c-ba34f54d487c
caps.latest.revision: 37
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 453207bf1a9e8a843cbaf5f19d77180453b6c43e
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "37983090"
---
# <a name="security-considerations-for-the-microsoft-drivers-for-php-for-sql-server"></a>Consideraciones de seguridad para los controladores de Microsoft para PHP para SQL Server
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

En este tema se describen consideraciones de seguridad específicas para el desarrollo, la implementación y la ejecución de aplicaciones que utilizan los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]. Para obtener más información sobre la seguridad de SQL Server, consulte [información general de seguridad de SQL Server](https://docs.microsoft.com/dotnet/framework/data/adonet/sql/overview-of-sql-server-security).  
  
## <a name="connect-using-windows-authentication"></a>Conexión con la autenticación de Windows  
Debe utilizarse la autenticación de Windows para conectarse a SQL Server siempre que sea posible por los siguientes motivos:  
  
-   **No se transmiten credenciales por la red durante la autenticación.** Los nombres de usuario y las contraseñas no se incrustan en la cadena de conexión de la base de datos. Por tanto, los atacantes o usuarios malintencionados no pueden obtener las credenciales supervisando la red o consultando las cadenas de conexión de los archivos de configuración.  
  
-   **Los usuarios tienen que pasar por un proceso de administración de cuentas centralizada.** Se aplican directivas de seguridad (por ejemplo, periodos de expiración de contraseñas, longitudes mínimas de contraseñas y bloqueo de cuentas) después de varias solicitudes de inicio de sesión no válidas.  
  
Para obtener información sobre cómo conectarse a un servidor con la autenticación de Windows, consulte [Cómo conectarse mediante la autenticación de Windows](../../connect/php/how-to-connect-using-windows-authentication.md).  
  
Cuando se conecte mediante la autenticación de Windows, se recomienda que configure el entorno para que SQL Server puede utilizar el protocolo de autenticación Kerberos. Para obtener más información, vea [Cómo asegurarse de que está utilizando la autenticación Kerberos cuando crea una conexión remota a una instancia de SQL Server 2005](https://support.microsoft.com/en-ca/help/909801/how-to-make-sure-that-you-are-using-kerberos-authentication-when-you-c) o [Autenticación Kerberos y SQL Server](https://msdn.microsoft.com/library/cc280744.aspx).  
  
## <a name="use-encrypted-connections-when-transferring-sensitive-data"></a>Uso de conexiones cifradas cuando se transfiere información confidencial  
Se deben usar conexiones cifradas siempre que se envíe información confidencial o se recupere de SQL Server. Para obtener información sobre cómo habilitar conexiones cifradas, vea el artículo [Habilitar conexiones cifradas en el motor de base de datos (Administrador de configuración de SQL Server)](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md). Para establecer una conexión segura con los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], utilice el atributo de conexión Encrypt cuando se conecte al servidor. Para obtener más información sobre los atributos de conexión, consulte [Connection Options](../../connect/php/connection-options.md).  
  
## <a name="use-parameterized-queries"></a>Uso de consultas con parámetros  
Utilice consultas con parámetros para reducir el riesgo de ataques por inyección de SQL. Para obtener ejemplos de la ejecución de consultas con parámetros, consulte [How to: Perform Parameterized Queries](../../connect/php/how-to-perform-parameterized-queries.md).  
  
Para obtener más información sobre los ataques por inyección de SQL y las consideraciones de seguridad relacionadas, vea [Inyección de código SQL](https://msdn.microsoft.com/library/ms161953.aspx).  
  
## <a name="do-not-accept-server-or-connection-string-information-from-end-users"></a>No aceptación de información de la cadena de conexión o del servidor procedente de usuarios finales  
Escriba aplicaciones para que los usuarios finales no puedan enviar información de la cadena de conexión o del servidor a la aplicación. Al mantener un control estricto sobre la información de la cadena de conexión y del servidor, se reduce el área expuesta a actividades malintencionadas.  
  
## <a name="turn-warningsaserrors-on-during-application-development"></a>Activación de WarningsAsErrors durante el desarrollo de las aplicaciones  
Desarrolle aplicaciones con la configuración **WarningsAsErrors** definida como **True** para que las advertencias emitidas por el controlador se traten como errores. Esto le permitirá abordar las advertencias antes de implementar su aplicación. Para obtener más información, consulte [Handling Errors and Warnings](../../connect/php/handling-errors-and-warnings.md).  
  
## <a name="secure-logs-for-deployed-application"></a>Registros seguros para la aplicación implementada  
Para las aplicaciones implementadas, asegúrese de que los registros se agregan a una ubicación segura o de que el registro esté desactivado. Esto ayuda a proteger contra la posibilidad de que los usuarios finales accedan a información escrita en los archivos de registro. Para obtener más información, consulte [Logging Activity](../../connect/php/logging-activity.md).  
  
## <a name="see-also"></a>Ver también  
[Programación de guía para los controladores de Microsoft para PHP para SQL Server](../../connect/php/programming-guide-for-php-sql-driver.md)
  
