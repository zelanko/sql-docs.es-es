---
title: Conectarse a SQL Server con el controlador JDBC | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 94bcfbe3-f00e-4774-bda8-bb7577518fec
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 526b0cbcd0a27adb7f2e8e848bf64a4f39198b54
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="connecting-to-sql-server-with-the-jdbc-driver"></a>Conectar SQL Server con el controlador JDBC
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Una de las operaciones más importantes que realizará con el [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] consiste en establecer una conexión con un [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] base de datos. Todas las interacciones con la base de datos se produce a través de la [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) objeto, y debido a que el controlador JDBC posee una arquitectura tan plana, casi todos los comportamientos interesantes afectan el objeto SQLServerConnection.  
  
 Si un [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] es solo escucha en un puerto IPv6, establezca la propiedad del sistema java.net.preferIPv6Addresses para asegurarse de que se utiliza IPv6 en lugar de IPv4 para conectarse a la [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]:  
  
```  
System.setProperty("java.net.preferIPv6Addresses", "true");  
```  
  
 Los temas de esta sección describen cómo establecer y trabajar con una conexión a un [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] base de datos.  
  
## <a name="in-this-section"></a>En esta sección  
  
|Tema|Description|  
|-----------|-----------------|  
|[Generar URL de conexión](../../connect/jdbc/building-the-connection-url.md)|Describe cómo formar una URL de conexión para conectarse a un [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] base de datos. También describe cómo conectarse a instancias con nombre de un [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] base de datos.|  
|[Establecer las propiedades de conexión](../../connect/jdbc/setting-the-connection-properties.md)|Describe las distintas propiedades de conexión y cómo se puede usar cuando se conecta a un [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] base de datos.|  
|[Establecer las propiedades de los orígenes de datos](../../connect/jdbc/setting-the-data-source-properties.md)|Describe cómo usar los orígenes de datos en un entorno de Java Platform, Enterprise Edition (Java EE).|  
|[Trabajar con una conexión](../../connect/jdbc/working-with-a-connection.md)|Describe las distintas formas en que se va a crear una instancia de una conexión a un [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] base de datos.|  
|[Usar agrupación de conexiones](../../connect/jdbc/using-connection-pooling.md)|Describe la compatibilidad del controlador JDBC con el uso de agrupaciones de conexiones.|  
|[Mediante la creación de reflejo de base de datos &#40;JDBC&#41;](../../connect/jdbc/using-database-mirroring-jdbc.md)|Describe la compatibilidad del controlador JDBC con el uso de la creación de reflejo de la base de datos.|  
|[Compatibilidad del controlador JDBC con la alta disponibilidad y la recuperación ante desastres](../../connect/jdbc/jdbc-driver-support-for-high-availability-disaster-recovery.md)|Describe cómo desarrollar una aplicación que se conectará a un grupo de disponibilidad AlwaysOn.|  
|[Usar la autenticación integrada de Kerberos para conectar con SQL Server](../../connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server.md)|Describe una implementación de Java para las aplicaciones se conecten a un [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] base de datos mediante la autenticación integrada de Kerberos.|  
|[Conectarse a una instancia de Azure SQL Database](../../connect/jdbc/connecting-to-an-azure-sql-database.md)|Explica los problemas de conectividad con bases de datos en SQL Azure.|  
  
## <a name="see-also"></a>Vea también  
 [Introducción al controlador JDBC](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
