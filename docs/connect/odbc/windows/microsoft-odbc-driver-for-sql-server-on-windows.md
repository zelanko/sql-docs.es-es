---
title: Microsoft ODBC Driver for SQL Server en Windows | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b10cfc22-6a2c-4707-a456-0dcec317982b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bb53e8e44d0f6b9e9f293f6afa5a470e91103a0c
ms.sourcegitcommit: 02b22274da4a103760a376c4ddf26c4829018454
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2020
ms.locfileid: "84681194"
---
# <a name="microsoft-odbc-driver-for-sql-server-on-windows"></a>Microsoft ODBC Driver for SQL Server en Windows
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Los controladores ODBC de Microsoft para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] son controladores ODBC independientes que proporcionan una interfaz de programación de aplicaciones (API) que implementa las interfaces ODBC estándar en Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].

Microsoft ODBC Driver for SQL Server puede usarse para crear nuevas aplicaciones. También se pueden actualizar las aplicaciones más antiguas que usen actualmente un controlador ODBC anterior. El Controlador ODBC de SQL Server admite conexiones a Azure SQL Database, Azure SQL Data Warehouse y [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  

## <a name="summary"></a>Resumen

| Versión       | Características admitidas      |
| ------------- |---------------| 
| Microsoft ODBC Driver 17 for SQL Server | <ul><li>Compatibilidad con Always Encrypted para la API de BCP</li><li>El nuevo atributo de cadena de conexión UseFMTONLY hace que el controlador use metadatos heredados en casos especiales que requieren tablas temporales</li>
| Microsoft ODBC Driver 13.1 for SQL Server     | <ul><li>Always Encrypted</li><li>Autenticación de Azure AD</li><li>Grupos de disponibilidad (AG) AlwaysOn</li></ul>   | 
| Microsoft ODBC Driver 13 for SQL Server      | <ul><li>Nombre de dominio internacionalizado (IDN)</li></ul> |
| Controlador ODBC 11 de Microsoft para SQL Server | <ul><li>Agrupación de conexiones dependientes del controlador</li><li>Resistencia de conexión</li><li>Ejecución asincrónica (método de sondeo)</li></ul> |    

## <a name="documentation"></a>Documentación  
Estos son los temas que trata esta documentación sobre Microsoft ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]:  
  
-   [Notas de la versión de ODBC para SQL Server en Windows](../../../connect/odbc/windows/release-notes-odbc-sql-server-windows.md)  
-   [Características de Microsoft ODBC Driver for SQL Server en Windows](../../../connect/odbc/windows/features-of-the-microsoft-odbc-driver-for-sql-server-on-windows.md)  
-   [Requisitos del sistema, instalación y archivos del controlador](../../../connect/odbc/windows/system-requirements-installation-and-driver-files.md)  
-   [Agrupación de conexiones dependientes del controlador ODBC para SQL Server](../../../connect/odbc/windows/driver-aware-connection-pooling-in-the-odbc-driver-for-sql-server.md)  
-   [Ejemplo de ejecución asincrónica &#40;método de notificación&#41;](../../../connect/odbc/windows/asynchronous-execution-notification-method-sample.md)  
-   [Resistencia de conexión en el controlador Windows ODBC](../../../connect/odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md)  
-   [Uso de Always Encrypted con el controlador ODBC](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md)
-   [Uso de Azure Active Directory con el controlador ODBC](../../../connect/odbc/using-azure-active-directory.md) 
-   [Uso de resolución de IP de red transparente](../../../connect/odbc/using-transparent-network-ip-resolution.md)   

## <a name="community"></a>Comunidad  
- [Blog de controladores de SQL Server](https://techcommunity.microsoft.com/t5/sql-server/bg-p/SQLServer/label-name/SQLServerDrivers)  
- [Foro para el acceso a los datos de SQL Server](https://social.technet.microsoft.com/Forums/en/sqldataaccess/threads)  
  
## <a name="see-also"></a>Consulte también  
- [Generar aplicaciones con SQL Server Native Client](../../../relational-databases/native-client/applications/building-applications-with-sql-server-native-client.md)   
- [Preguntas más frecuentes de SQL Server Native Client](https://msdn.microsoft.com/sqlserver/aa937707.aspx)   
- [Referencia del programador de ODBC](../../../odbc/reference/odbc-programmer-s-reference.md)   
- [SQL Server Native Client (ODBC)](../../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
