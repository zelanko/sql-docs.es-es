---
title: Microsoft ODBC Driver for SQL Server en Windows | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b10cfc22-6a2c-4707-a456-0dcec317982b
caps.latest.revision: 37
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: be37bf73c0fe662b15c8ad26210ed243b5ca317c
ms.contentlocale: es-es
ms.lasthandoff: 09/27/2017

---
# <a name="microsoft-odbc-driver-for-sql-server-on-windows"></a>Microsoft ODBC Driver for SQL Server en Windows
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Microsoft ODBC Driver 13.1, 13 y 11 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] son controladores ODBC independientes que proporcionan una interfaz de programación de aplicaciones (API) que implementa las interfaces ODBC estándares en Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)].

Microsoft ODBC Driver for SQL Server puede utilizarse para crear nuevas aplicaciones. También puede actualizar sus aplicaciones más antiguas que usen actualmente un controlador ODBC anterior. El controlador ODBC para SQL Server admite conexiones a la base de datos de SQL Azure, almacenamiento de datos de SQL Azure, SQL Server 2016, SQL Server 2014, SQL Server 2012, SQL Server 2008 R2, SQL Server 2008 y SQL Server 2005.  

## <a name="summary"></a>Resumen

| Versión       | Características admitidas      |
| ------------- |---------------| 
| Microsoft ODBC Driver 13.1 for SQL Server     | <ul><li>Always Encrypted</li><li>Autenticación de Azure AD</li><li>Grupos de disponibilidad (AG) AlwaysOn</li></ul>   | 
| Microsoft ODBC Driver 13 for SQL Server      | <ul><li>Nombre de dominio internacionalizado (IDN)</li></ul> |
| Controlador ODBC 11 de Microsoft para SQL Server | <ul><li>Agrupación de conexiones dependientes del controlador</li><li>Resistencia de conexión</li><li>Ejecución asincrónica (método de sondeo)</li></ul> |    

## <a name="documentation"></a>Documentación  
Estos son los temas que trata esta documentación sobre Microsoft ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] :  
  
-   [Notas de la versión](../../../connect/odbc/windows/release-notes.md)  
-   [Características de Microsoft ODBC Driver for SQL Server en Windows](../../../connect/odbc/windows/features-of-the-microsoft-odbc-driver-for-sql-server-on-windows.md)  
-   [Requisitos del sistema, instalación y archivos del controlador](../../../connect/odbc/windows/system-requirements-installation-and-driver-files.md)  
-   [Agrupación de conexiones dependientes del controlador ODBC para SQL Server](../../../connect/odbc/windows/driver-aware-connection-pooling-in-the-odbc-driver-for-sql-server.md)  
-   [Ejemplo de ejecución asincrónica &#40;método de notificación&#41;](../../../connect/odbc/windows/asynchronous-execution-notification-method-sample.md)  
-   [Resistencia de conexión en el controlador Windows ODBC](../../../connect/odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md)  
-   [Uso de Always Encrypted con el controlador ODBC](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md)
-   [Con Azure Active Directory con el controlador ODBC](../../../connect/odbc/using-azure-active-directory.md) 
-   [Utilizando la resolución de IP de red transparente](../../../connect/odbc/using-transparent-network-ip-resolution.md)   

## <a name="community"></a>Comunidad  
- [Blog del equipo de Microsoft ODBC Driver for SQL Server](http://blogs.msdn.com/sqlnativeclient/default.aspx)  
- [Foro para el acceso a los datos de SQL Server](http://social.technet.microsoft.com/Forums/en/sqldataaccess/threads)  
  
## <a name="see-also"></a>Vea también  
- [Sobre SQL Server Native Client](https://msdn.microsoft.com/sqlserver/ff658532.aspx)   
- [Creación de aplicaciones con SQL Server Native Client](../../../relational-databases/native-client/applications/building-applications-with-sql-server-native-client.md)   
- [Preguntas más frecuentes de SQL Server Native Client](https://msdn.microsoft.com/sqlserver/aa937707.aspx)   
- [Referencia del programador de ODBC](../../../odbc/reference/odbc-programmer-s-reference.md)   
- [SQL Server Native Client (ODBC)](../../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  

