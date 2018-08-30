---
title: Conexión a SQL Server con el controlador JDBC
ms.custom: ''
ms.date: 07/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 94bcfbe3-f00e-4774-bda8-bb7577518fec
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7a5d7e44945fdb435b7dcadbdd7c67033f8d4f8c
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 08/14/2018
ms.locfileid: "42786348"
---
# <a name="connecting-to-sql-server-with-the-jdbc-driver"></a>Conectar SQL Server con el controlador JDBC
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Una de las operaciones más importantes que realizará con el [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] es establecer una conexión con una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Todas las interacciones con la base de datos tienen lugar a través del objeto SQLServerConnection[ y, debido a que el controlador JDBC posee una arquitectura tan plana, casi todos los comportamientos interesantes afectan al objeto ](../../connect/jdbc/reference/sqlserverconnection-class.md).  
  
 Si [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] solo está realizando escuchas en un puerto IPv6, establezca la propiedad del sistema java.net.preferIPv6Addresses para asegurarse de que se utiliza IPv6 en lugar de IPv4 para conectar a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
```java
System.setProperty("java.net.preferIPv6Addresses", "true");  
```  
  
 En los temas de esta sección se describe cómo establecer y trabajar con una conexión a una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="in-this-section"></a>En esta sección  
  
|Tema|Descripción|  
|-----------|-----------------|  
|[Generar URL de conexión](../../connect/jdbc/building-the-connection-url.md)|Describe cómo formar una URL de conexión a una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. También describe cómo conectarse a instancias con nombre de una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[Establecer las propiedades de conexión](../../connect/jdbc/setting-the-connection-properties.md)|Describe las diferentes propiedades de conexión y cómo usarlas cuando se establece una conexión a una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[Establecer las propiedades de los orígenes de datos](../../connect/jdbc/setting-the-data-source-properties.md)|Describe cómo usar los orígenes de datos en un entorno de Java Platform, Enterprise Edition (Java EE).|  
|[Trabajar con una conexión](../../connect/jdbc/working-with-a-connection.md)|Describe las diferentes formas de crear una instancia de conexión a una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[Usar agrupación de conexiones](../../connect/jdbc/using-connection-pooling.md)|Describe la compatibilidad del controlador JDBC con el uso de agrupaciones de conexiones.|  
|[Usar la creación de reflejo de bases de datos](../../connect/jdbc/using-database-mirroring-jdbc.md)|Describe la compatibilidad del controlador JDBC con el uso de la creación de reflejo de la base de datos.|  
|[Compatibilidad del controlador JDBC con la alta disponibilidad y la recuperación ante desastres](../../connect/jdbc/jdbc-driver-support-for-high-availability-disaster-recovery.md)|Describe cómo desarrollar una aplicación que se conectará a un grupo de disponibilidad AlwaysOn.|  
|[Usar la autenticación integrada de Kerberos para conectar con SQL Server](../../connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server.md)|Describe una implementación Java para que las aplicaciones se conecten con una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante la autenticación integrada de Kerberos.|  
|[Conectarse a una instancia de Azure SQL Database](../../connect/jdbc/connecting-to-an-azure-sql-database.md)|Explica los problemas de conectividad con bases de datos en SQL Azure.|  
  
## <a name="see-also"></a>Ver también  
 [Introducción al controlador JDBC](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
