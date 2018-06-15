---
title: Características de Microsoft ODBC Driver for SQL Server en Windows | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 76326eeb-1144-4b9f-85db-50524c655d30
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9e2b7c107a40a60a1da5ed891d7a26a7c85011db
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32856340"
---
# <a name="features-of-the-microsoft-odbc-driver-for-sql-server-on-windows"></a>Características de Microsoft ODBC Driver for SQL Server en Windows
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

    
## <a name="microsoft-odbc-driver-131-for-sql-server-on-windows"></a>Microsoft ODBC Driver 13.1 for SQL Server en Windows

ODBC Driver 13.1 para SQL Server contiene todas las funciones de la versión anterior (11) y agrega compatibilidad para la autenticación de Always Encrypted y Azure Active Directory cuando se utiliza junto con Microsoft SQL Server 2016.  
  
Always Encrypted permite a los clientes cifrar datos confidenciales en aplicaciones de cliente y nunca revelar las claves de cifrado en SQL Server. Un controlador habilitado para Always Encrypted instalado en el equipo cliente consigue esto al cifrar y descifrar automáticamente los datos confidenciales en la aplicación cliente de SQL Server. El controlador cifra los datos en columnas confidenciales antes de pasar los datos a SQL Server y vuelve a escribir las consultas automáticamente para que se conserve la semántica de la aplicación. De forma similar, el controlador descifra de forma transparente los datos almacenados en columnas de base de datos cifradas que se incluyen en los resultados de la consulta. Para obtener más información, consulte [usar Always Encrypted con el controlador ODBC](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md).
 
Azure Active Directory permite a los usuarios, el DBA y los programadores de aplicaciones utilizar la autenticación de Azure Active Directory como un mecanismo de conectarse a la base de datos de SQL de Microsoft Azure y Microsoft SQL Server 2016 mediante el uso de identidades en Azure Active Directory (Azure AD ). Para obtener más información, consulte [mediante Azure Active Directory con el controlador ODBC](../../../connect/odbc/using-azure-active-directory.md), y [conectarse a la base de datos SQL o SQL datos almacenamiento mediante Azure Active Directory autenticación](https://azure.microsoft.com/en-us/documentation/articles/sql-database-aad-authentication/).   
  
## <a name="microsoft-odbc-driver-11-for-sql-server-on-windows"></a>Microsoft® ODBC Driver 11 for SQL Server® en Windows  

ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] contiene todas las funciones del controlador ODBC de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Native Client incluido en [!INCLUDE[ssSQL11](../../../includes/sssql11_md.md)]. Para obtener más información, consulte [Programación de SQL Server Native Client](http://msdn.microsoft.com/library/ms130892.aspx). El controlador ODBC de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Native Client se basa en el controlador ODBC que se incluye en el sistema operativo Windows. Para obtener más información, vea [Windows Data Access Components SDK (SDK de componentes de Windows Data Access)](http://msdn.microsoft.com/library/aa968814(VS.85).aspx).  
  
Esta versión de ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] contiene las siguientes características nuevas:  
  
### <a name="bcpexe-l-option-for-specifying-a-login-timeout"></a>opción de bcp.exe – l para especificar un tiempo de espera de inicio de sesión
 
La opción – l Especifica el número de segundos antes de que un `bcp.exe` inicio de sesión a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] tiempos de espera al intentar conectarse a un servidor. El tiempo de espera de inicio de sesión predeterminado es 15 segundos. El tiempo de espera de inicio de sesión debe ser un número comprendido entre 0 y 65534. Si el valor proporcionado no es numérico o no está dentro de este intervalo, `bcp.exe` genera un mensaje de error. Un valor de 0 especifica un tiempo de espera infinito. Un tiempo de espera de inicio de sesión de menos de 10 segundos (aproximadamente) no es confiable.  
  
### <a name="driver-aware-connection-pooling"></a>Agrupación de conexiones dependientes del controlador  
ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] admite [agrupación de conexiones dependientes del controlador](http://msdn.microsoft.com/library/hh405031(VS.85).aspx). Para obtener más información, consulte [Driver-Aware Connection Pooling in the ODBC Driver for SQL Server](../../../connect/odbc/windows/driver-aware-connection-pooling-in-the-odbc-driver-for-sql-server.md).  
  
### <a name="asynchronous-execution-notification-method"></a>Ejecución asincrónica (método de notificación)  
ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] admite [ejecución asincrónica (método de notificación)](http://msdn.microsoft.com/library/hh405038(VS.85).aspx). Para obtener un ejemplo de uso, consulte [ejecución asincrónica &#40;método de notificación&#41; ejemplo](../../../connect/odbc/windows/asynchronous-execution-notification-method-sample.md).  
  
### <a name="connection-resiliency"></a>Resistencia de conexión
Para garantizar que las aplicaciones permanecen conectadas a una base de datos SQL de Microsoft Azure, el controlador ODBC de Windows puede restaurar conexiones inactivas. Para obtener más información, consulte [Connection Resiliency in the Windows ODBC Driver](../../../connect/odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md).  
  
## <a name="behavior-changes"></a>Cambios de comportamiento

En [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Native Client, el `-y0` opción `sqlcmd.exe` hace que la salida se trunque en 1 MB si el ancho de pantalla es 0.
  
A partir de la versión ODBC Driver 11 para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)], no hay ningún límite en la cantidad de datos que se pueden recuperar en una sola columna cuando `–y0` se especifica. `sqlcmd.exe` Ahora transmite columnas tan grandes como 2 GB ([!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] máximo del tipo de datos).  
  
Otra diferencia es que si se especifica tanto `-h` y `-y0` ahora produce un error notificando que las opciones son incompatibles. `-h`, que especifica el número de filas que se va a imprimir entre los encabezados de columna y nunca ha sido compatible con `-y0`, se omitió aunque se imprimiera ningún encabezado.
  
Tenga en cuenta que `-y0` puede causar problemas de rendimiento en el servidor y la red, según el tamaño de los datos devueltos.

## <a name="see-also"></a>Vea también  
[Microsoft ODBC Driver for SQL Server en Windows](../../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)  
