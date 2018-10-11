---
title: Características de Microsoft ODBC Driver for SQL Server en Windows | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 76326eeb-1144-4b9f-85db-50524c655d30
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7e56d57cb3df19df1cbf09811ebfebca66efe51b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47677583"
---
# <a name="features-of-the-microsoft-odbc-driver-for-sql-server-on-windows"></a>Características de Microsoft ODBC Driver for SQL Server en Windows
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

    
## <a name="microsoft-odbc-driver-131-for-sql-server-on-windows"></a>Microsoft ODBC Driver 13.1 for SQL Server en Windows

El controlador ODBC 13.1 para SQL Server contiene toda la funcionalidad de la versión anterior (11) y agrega compatibilidad para la autenticación de Always Encrypted y Azure Active Directory cuando se usa junto con Microsoft SQL Server 2016.  
  
Always Encrypted permite a los clientes cifrar datos confidenciales en aplicaciones de cliente y nunca revelar las claves de cifrado en SQL Server. Un controlador habilitado para Always Encrypted instalado en el equipo cliente consigue esto al cifrar y descifrar automáticamente los datos confidenciales en la aplicación cliente de SQL Server. El controlador cifra los datos en columnas confidenciales antes de pasar los datos a SQL Server y vuelve a escribir las consultas automáticamente para que se conserve la semántica de la aplicación. De forma similar, el controlador descifra de forma transparente los datos almacenados en columnas de base de datos cifradas que se incluyen en los resultados de la consulta. Para obtener más información, vea [Uso de Always Encrypted con ODBC Driver](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md).
 
Azure Active Directory permite a los usuarios, DBA y los programadores de aplicaciones usar la autenticación de Azure Active Directory como un mecanismo de conexión a Microsoft Azure SQL Database y Microsoft SQL Server 2016 mediante identidades de Azure Active Directory (Azure AD ). Para obtener más información, consulte [mediante Azure Active Directory con el controlador ODBC](../../../connect/odbc/using-azure-active-directory.md), y [conectarse a SQL Database o SQL Data Warehouse por usar Azure Active Directory autenticación](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/).   
  
## <a name="microsoft-odbc-driver-11-for-sql-server-on-windows"></a>Microsoft® ODBC Driver 11 for SQL Server® en Windows  

ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] contiene todas las funciones del controlador ODBC de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client incluido en [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]. Para obtener más información, vea [Programación de SQL Server Native Client](../../../relational-databases/native-client/sql-server-native-client-programming.md). El controlador ODBC de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client se basa en el controlador ODBC que se incluye en el sistema operativo Windows. Para obtener más información, vea [Windows Data Access Components SDK (SDK de componentes de Windows Data Access)](http://msdn.microsoft.com/library/aa968814(VS.85).aspx).  
  
Esta versión de ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] contiene las siguientes características nuevas:  
  
### <a name="bcpexe-l-option-for-specifying-a-login-timeout"></a>opción – l de bcp.exe para especificar un tiempo de espera de inicio de sesión
 
La opción –l especifica el número de segundos que tienen que transcurrir antes de que un inicio de sesión de `bcp.exe` en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] agote el tiempo de espera cuando se trate de conectar a un servidor. El tiempo de espera de inicio de sesión predeterminado es 15 segundos. El período de tiempo de espera de inicio de sesión debe ser un número comprendido entre 0 y 65534. Si el valor proporcionado no es numérico o no está dentro de este intervalo, `bcp.exe` genera un mensaje de error. Un valor de 0 especifica un tiempo de espera infinito. Un tiempo de espera de inicio de sesión de menos de 10 segundos (aproximadamente) no resulta confiable.  
  
### <a name="driver-aware-connection-pooling"></a>Agrupación de conexiones dependientes del controlador  
ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] es compatible con la [agrupación de conexiones dependientes del controlador](http://msdn.microsoft.com/library/hh405031(VS.85).aspx). Para obtener más información, consulte [Driver-Aware Connection Pooling in the ODBC Driver for SQL Server](../../../connect/odbc/windows/driver-aware-connection-pooling-in-the-odbc-driver-for-sql-server.md).  
  
### <a name="asynchronous-execution-notification-method"></a>Ejecución asincrónica (método de notificación)  
ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] es compatible con la [ejecución asincrónica (método de notificación)](http://msdn.microsoft.com/library/hh405038(VS.85).aspx). Para obtener un ejemplo de uso, vea [Ejemplo de ejecución asincrónica &#40;método de notificación&#41;](../../../connect/odbc/windows/asynchronous-execution-notification-method-sample.md).  
  
### <a name="connection-resiliency"></a>Resistencia de conexión
Para garantizar que las aplicaciones permanecen conectadas a una base de datos SQL de Microsoft Azure, el controlador ODBC de Windows puede restaurar conexiones inactivas. Para obtener más información, consulte [Connection Resiliency in the Windows ODBC Driver](../../../connect/odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md).  
  
## <a name="behavior-changes"></a>Cambios de comportamiento

En [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, el `-y0` opción `sqlcmd.exe` hace que la salida se trunque en 1 MB si el ancho de pantalla era 0.
  
A partir de la versión ODBC Driver 11 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], no existe ningún límite en la cantidad de datos que se pueden recuperar en una sola columna al especificar `–y0`. `sqlcmd.exe` ahora transmite columnas de hasta 2 GB (tamaño máximo del tipo de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]).  
  
Otra diferencia es que si se especifica tanto `-h` y `-y0` ahora produce un error que informa de que las opciones son incompatibles. `-h`, que especifica el número de filas que se van a imprimir entre los encabezados de columna y que nunca ha sido compatible con `-y0`, se omitía, aunque no se imprimiera ningún encabezado.
  
Tenga en cuenta que `-y0` puede provocar problemas de rendimiento tanto en el servidor como en la red, en función del tamaño de los datos devueltos.

## <a name="see-also"></a>Ver también  
[Microsoft ODBC Driver for SQL Server en Windows](../../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)  
