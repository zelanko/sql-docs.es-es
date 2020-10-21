---
title: Características de Microsoft ODBC Driver
description: Obtenga información sobre las diferentes características admitidas por Microsoft ODBC Driver for SQL Server en Windows.
ms.custom: ''
ms.date: 05/06/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 76326eeb-1144-4b9f-85db-50524c655d30
author: v-makouz
ms.author: v-daenge
ms.openlocfilehash: 5fc07a171e42338ca76d51d66c04af187cb6beda
ms.sourcegitcommit: a5398f107599102af7c8cda815d8e5e9a367ce7e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/13/2020
ms.locfileid: "92005906"
---
# <a name="features-of-the-microsoft-odbc-driver-for-sql-server-on-windows"></a>Características de Microsoft ODBC Driver for SQL Server en Windows
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

    
## <a name="microsoft-odbc-driver-174-for-sql-server-on-windows"></a>Microsoft ODBC Driver 17.4 for SQL Server en Windows

El controlador ODBC 17.4 incluye la capacidad de ajustar la configuración de conexión persistente TCP. Puede modificarse agregando valores a las claves del Registro de DSN o el controlador. Las claves se encuentran en `HKEY_LOCAL_MACHINE\Software\ODBC\` para los orígenes de datos del sistema y en `HKEY_CURRENT_USER\Software\ODBC\` para los orígenes de datos de usuario. En el caso de DSN, los valores deben agregarse a `...\Software\ODBC\ODBC.INI\<DSN Name>` y, en el caso del controlador, a `...\Software\ODBC\ODBCINST.INI\ODBC Driver 17 for SQL Server`.

Consulte [Entradas del registro para los componentes de ODBC](../../../odbc/reference/install/registry-entries-for-odbc-components.md) para obtener más información.

Los valores son `REG_SZ` y son los siguientes:

- `KeepAlive` controla la frecuencia con la que TCP intenta comprobar que una conexión inactiva sigue intacta mediante el envío de un paquete de conexión persistente. El valor predeterminado es 30 segundos.

- `KeepAliveInterval` determina el intervalo que separa las retransmisiones de conexión persistente hasta que se recibe una respuesta. El valor predeterminado es 1 segundo.



## <a name="microsoft-odbc-driver-131-for-sql-server-on-windows"></a>Microsoft ODBC Driver 13.1 for SQL Server en Windows

El controlador ODBC 13.1 para SQL Server contiene todas las funciones de la versión anterior (11), además de compatibilidad con Always Encrypted y la autenticación de Azure Active Directory cuando se usa junto con Microsoft SQL Server 2016.  
  
Always Encrypted permite a los clientes cifrar datos confidenciales en aplicaciones de cliente y nunca revelar las claves de cifrado en SQL Server. Un controlador habilitado para Always Encrypted instalado en el equipo cliente consigue esto al cifrar y descifrar automáticamente los datos confidenciales en la aplicación cliente de SQL Server. El controlador cifra los datos en columnas confidenciales antes de pasar los datos a SQL Server y vuelve a escribir las consultas automáticamente para que se conserve la semántica de la aplicación. De forma similar, el controlador descifra de forma transparente los datos almacenados en columnas de base de datos cifradas que se incluyen en los resultados de la consulta. Para obtener más información, vea [Uso de Always Encrypted con ODBC Driver](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md).
 
Azure Active Directory permite a los usuarios, DBA y programadores de aplicaciones usar la autenticación de Azure Active Directory como un mecanismo de conexión a Microsoft Azure SQL Database y a Microsoft SQL Server 2016 mediante identidades en Azure Active Directory (Azure AD). Para más información, vea [Uso de Azure Active Directory con el controlador ODBC](../using-azure-active-directory.md) y [Conexión a SQL Database o a Azure Synapse Analytics mediante autenticación de Azure Active Directory](/azure/sql-database/sql-database-aad-authentication).   
  
## <a name="microsoft-odbc-driver-11-for-sql-server-on-windows"></a>Microsoft® ODBC Driver 11 for SQL Server® en Windows  

ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] contiene todas las funciones del controlador ODBC de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client incluido en [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]. Para obtener más información, consulte [Programación de SQL Server Native Client](../../../relational-databases/native-client/sql-server-native-client-programming.md). El controlador ODBC de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client se basa en el controlador ODBC que se incluye en el sistema operativo Windows. Para obtener más información, vea [Windows Data Access Components SDK (SDK de componentes de Windows Data Access)](/previous-versions/windows/desktop/legacy/aa968814(v=vs.85)).  
  
Esta versión de ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] contiene las siguientes características nuevas:  
  
### <a name="bcpexe--l-option-for-specifying-a-login-timeout"></a>Opción bcp.exe -l para especificar un tiempo de espera de inicio de sesión
 
La opción -l especifica el número de segundos que tienen que transcurrir antes de que un inicio de sesión de `bcp.exe` en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] agote el tiempo de espera cuando se trate de conectar a un servidor. El tiempo de espera de inicio de sesión predeterminado es de 15 segundos. El período de tiempo de espera de inicio de sesión debe ser un número comprendido entre 0 y 65534. Si el valor proporcionado no es numérico o no está dentro de este intervalo, `bcp.exe` genera un mensaje de error. Un valor de 0 especifica un tiempo de espera infinito. Un tiempo de espera de inicio de sesión de menos de 10 segundos (aproximadamente) no resulta confiable.  
  
### <a name="driver-aware-connection-pooling"></a>Agrupación de conexiones dependientes del controlador  
ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] es compatible con la [agrupación de conexiones dependientes del controlador](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md). Para obtener más información, consulte [Agrupación de conexiones dependientes del controlador en ODBC Driver for SQL Server | Microsoft Docs](driver-aware-connection-pooling-in-the-odbc-driver-for-sql-server.md).  
  
### <a name="asynchronous-execution-notification-method"></a>Ejecución asincrónica (método de notificación)  
ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] es compatible con la [ejecución asincrónica (método de notificación)](../../../odbc/reference/develop-app/asynchronous-execution-notification-method.md). Para obtener un ejemplo de uso, vea [Ejemplo de ejecución asincrónica &#40;método de notificación&#41;](asynchronous-execution-notification-method-sample.md).  
  
### <a name="connection-resiliency"></a>Resistencia de conexión
Para garantizar que las aplicaciones permanecen conectadas a una base de datos SQL de Microsoft Azure, el controlador ODBC de Windows puede restaurar conexiones inactivas. Para obtener más información, consulte [Resistencia de conexión en el controlador Windows ODBC](connection-resiliency-in-the-windows-odbc-driver.md).  
  
## <a name="behavior-changes"></a>Cambios de comportamiento

En [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, la opción `-y0` para `sqlcmd.exe` hizo que se truncara la salida en 1 MB si el ancho de pantalla era 0.
  
A partir de la versión ODBC Driver 11 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], no existe ningún límite en la cantidad de datos que se pueden recuperar en una sola columna al especificar `-y0`. `sqlcmd.exe` ahora transmite columnas de hasta 2 GB (tamaño máximo del tipo de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]).  
  
Otra diferencia radica en que especificar tanto `-h` como `-y0` genera ahora un error que informa de que las opciones son incompatibles. `-h`, que especifica el número de filas que se van a imprimir entre los encabezados de columna y que nunca ha sido compatible con `-y0`, se omitía, aunque no se imprimiera ningún encabezado.
  
Tenga en cuenta que `-y0` puede provocar problemas de rendimiento tanto en el servidor como en la red, en función del tamaño de los datos devueltos.

## <a name="see-also"></a>Consulte también  
[Microsoft ODBC Driver for SQL Server en Windows](microsoft-odbc-driver-for-sql-server-on-windows.md)  
