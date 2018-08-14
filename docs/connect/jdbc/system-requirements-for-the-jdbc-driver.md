---
title: Requisitos del sistema para el controlador JDBC
ms.custom: ''
ms.date: 07/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 447792bb-f39b-49b4-9fd0-1ef4154c74ab
caps.latest.revision: 73
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e5363b1135cb7e5d04201b2005bda9caf8ff8811
ms.sourcegitcommit: 2f9cafc1d7a3773a121bdb78a095018c8b7c149f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/08/2018
ms.locfileid: "39662287"
---
# <a name="system-requirements-for-the-jdbc-driver"></a>Requisitos del sistema para el controlador JDBC
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Para acceder a los datos de una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] mediante [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], debe tener los siguientes componentes instalados en el equipo:

- [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] ([descargar](download-microsoft-jdbc-driver-for-sql-server.md))
- Java Runtime Environment

## <a name="java-runtime-environment-requirements"></a>Requisitos de Java Runtime Environment  
 A partir de Microsoft JDBC Driver 7.0 para SQL Server, se admiten Sun Java SE Development Kit (JDK) 10.0 y Java Runtime Environment (JRE) 10.0.

 A partir de Microsoft JDBC Driver 6.4 para SQL Server, se admiten Sun Java SE Development Kit (JDK) 9.0 y Java Runtime Environment (JRE) 9.0.

 A partir de Microsoft JDBC Driver 4.2 para SQL Server, se admiten Sun Java SE Development Kit (JDK) 8.0 y Java Runtime Environment (JRE) 8.0. La compatibilidad con API de Java Database Connectivity (JDBC) Spec se ha ampliado para incluir la API de JDBC 4.1 y 4.2.  
  
 A partir de la versión 4.1 del controlador Microsoft JDBC para SQL Server, son compatibles el Kit de desarrollo Sun Java SE (JDK) 7.0 y Java Runtime Environment (JRE) 7.0.  
  
 A partir de [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)], la compatibilidad del controlador JDBC con la API de especificaciones de Java Database Connectivity (JDBC) se ha ampliado para incluir la API de JDBC 4.0. La API de JDBC 4.0 se presentó como parte de Sun Java SE Development Kit (JDK) 6.0 y de Java Runtime Environment (JRE) 6.0. JDBC 4.0 es un superconjunto de la API de JDBC 3.0.  
  
 Cuando se implementa [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] en sistemas operativos Windows y UNIX, se deben usar los paquetes de instalación, *sqljdbc_\<versión>_enu.exe* y *sqljdbc_\<versión>_enu.tar.gz*, respectivamente. Para obtener más información acerca de cómo implementar el controlador JDBC, vea el tema [Implementar el controlador JDBC](../../connect/jdbc/deploying-the-jdbc-driver.md).  
  
**Microsoft JDBC Driver 7.0 para SQL Server**  

  dos bibliotecas de clases JAR en cada paquete de instalación: mssql-jdbc-7.0.jre8.jar y mssql-jdbc-7.0.0.jre10.jar.

  JDBC Driver 7.0 está diseñado para funcionar con todas las máquinas virtuales de Java equivalentes de Sun y ser compatible con ellas, aunque solo se ha probado en Sun JRE 8.0 y 10.0.
  
  A continuación se resume la compatibilidad que ofrecen los dos archivos JAR incluidos en Microsoft JDBC Driver 7.0 para SQL Server:  
  
  |JAR|Cumplimiento con la versión JDBC|Versión de Java recomendada|Descripción|  
|---------|-----------------------------|----------------------|-----------------|   
|mssql-jdbc-7.0.0.jre8.jar|4.2|8|Requiere la versión 8.0 de Java Runtime Environment (JRE). El uso de JRE 7.0 o anterior lanzará una excepción.<br /><br /> Las nuevas características en 7.0 incluyen: compatibilidad con JDK 10, el nivel de compatibilidad predeterminado actualizado a las especificaciones de JDBC 4.2, compatibilidad con tipos de datos espaciales, cancelQueryTimeout propiedad de conexión, métodos de petición de límite, propiedad de conexión useBulkCopyForBatchInsert, datos Información de clasificación y detección, extensión de características de UTF-8 y soporte técnico de CityHash. |    
|mssql-jdbc-7.0.0.jre10.jar|4.3|10|Requiere Java Runtime Environment (JRE) 10.0. El uso de JRE 9.0 o anterior lanzará una excepción.<br /><br /> Las nuevas características en 7.0 incluyen: compatibilidad con JDK 10, el nivel de compatibilidad predeterminado actualizado a las especificaciones de JDBC 4.2, compatibilidad con tipos de datos espaciales, cancelQueryTimeout propiedad de conexión, métodos de petición de límite, propiedad de conexión useBulkCopyForBatchInsert, datos Información de clasificación y detección, extensión de características de UTF-8 y soporte técnico de CityHash. |    


  La 7.0 del controlador JDBC también está disponible en el repositorio Central de Maven y pueden agregarse a un proyecto de Maven agregando el código siguiente en el archivo POM. XML:  
  
 ```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>7.0.0.jre10</version>
</dependency>
```      
  
**Microsoft JDBC Driver 6.4 para SQL Server:**  

  JDBC Driver 6.4 incluye tres bibliotecas de clases JAR en cada paquete de instalación: **mssql-jdbc-6.4.0.jre7.jar**, **mssql-jdbc-6.4.0.jre8.jar**, y **mssql-jdbc-6.4.0.jre9.jar** .

  JDBC Driver 6.4 está diseñado para funcionar con todas las máquinas virtuales de Java equivalentes de Sun y ser compatible con ellas, aunque solo se ha probado en Sun JRE 7.0, 8.0 y 9.0.
  
  A continuación se resume la compatibilidad que ofrecen los tres archivos JAR incluidos en Microsoft JDBC Driver 6.4 para SQL Server:  
  
  |JAR|Cumplimiento con la versión JDBC|Versión de Java recomendada|Descripción|  
|---------|-----------------------------|----------------------|-----------------|   
|mssql-jdbc-6.4.0.jre7.jar|4.1|7|Requiere la versión 7.0 de Java Runtime Environment (JRE). El uso de JRE 6.0 o anterior lanzará una excepción.<br /><br /> Las nuevas características en 6.4 incluyen: autenticación de Azure AD para Linux, el método de entidad de seguridad y la contraseña para la detección automática de REALM en SPN para la autenticación entre dominios, delegación restringida de Kerberos, el tiempo de espera de consulta, el tiempo de espera de Socket, Kerberos y preparadas identificador de instrucciones volver a usar. |  
|mssql-jdbc-6.4.0.jre8.jar|4.2|8|Requiere la versión 8.0 de Java Runtime Environment (JRE). El uso de JRE 7.0 o anterior lanzará una excepción.<br /><br /> Las nuevas características en 6.4 incluyen: autenticación de Azure AD para Linux, el método de entidad de seguridad y la contraseña para la detección automática de REALM en SPN para la autenticación entre dominios, delegación restringida de Kerberos, el tiempo de espera de consulta, el tiempo de espera de Socket, Kerberos y preparadas identificador de instrucciones volver a usar. |    
|mssql-jdbc-6.4.0.jre9.jar|4.3|9|Requiere Java Runtime Environment (JRE) 9.0. El uso de JRE 8.0 o anterior lanzará una excepción.<br /><br /> Las nuevas características en 6.4 incluyen: autenticación de Azure AD para Linux, el método de entidad de seguridad y la contraseña para la detección automática de REALM en SPN para la autenticación entre dominios, delegación restringida de Kerberos, el tiempo de espera de consulta, el tiempo de espera de Socket, Kerberos y preparadas identificador de instrucciones volver a usar. |

JDBC Driver 6.4 también está disponible en el repositorio Central de Maven y pueden agregarse a un proyecto de Maven agregando el código siguiente en el archivo POM. XML 

 ```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>6.4.0.jre9</version>
</dependency>
```

**Microsoft JDBC Driver 6.2 para SQL Server:**  
  
  JDBC Driver 6.2 incluye dos bibliotecas de clases JAR en cada paquete de instalación: **mssql-jdbc-6.2.2.jre7.jar** y **mssql-jdbc-6.2.2.jre8.jar**. 
  
 JDBC Driver 6.2 está diseñado para funcionar con todas las máquinas virtuales de Java equivalentes de Sun y ser compatible con ellas, aunque solo se ha probado en Sun JRE 5.0, 6.0, 7.0 y 8.0.
  
 A continuación se resume la compatibilidad que ofrecen los dos archivos JAR incluidos en Microsoft JDBC Driver 6.0 y 4.2 para SQL Server:  
  
|JAR|Cumplimiento con la versión JDBC|Versión de Java recomendada|Descripción|  
|---------|-----------------------------|----------------------|-----------------|
|MSSQL-jdbc-6.2.2.jre7.jar|4.1|7|Requiere la versión 7.0 de Java Runtime Environment (JRE). El uso de JRE 6.0 o anterior lanzará una excepción.<br /><br /> Nuevas características de 6.2 incluyen: autenticación de Azure AD para Linux, el método de entidad de seguridad y la contraseña para la detección automática de REALM en SPN para la autenticación entre dominios, delegación restringida de Kerberos, el tiempo de espera de consulta, el tiempo de espera de Socket, Kerberos y preparadas identificador de instrucciones volver a usar. |  
|MSSQL-jdbc-6.2.3.jre8.jar|4.2|8|Requiere la versión 8.0 de Java Runtime Environment (JRE). El uso de JRE 7.0 o anterior lanzará una excepción.<br /><br /> Nuevas características de 6.2 incluyen: autenticación de Azure AD para Linux, el método de entidad de seguridad y la contraseña para la detección automática de REALM en SPN para la autenticación entre dominios, delegación restringida de Kerberos, el tiempo de espera de consulta, el tiempo de espera de Socket, Kerberos y preparadas identificador de instrucción volver a usar|    

  JDBC Driver 6.2 también está disponible en el repositorio Central de Maven y pueden agregarse a un proyecto de Maven agregando el código siguiente en el archivo POM. XML 
  
 ```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>6.2.2.jre8</version>
</dependency>
```    

 **Microsoft JDBC Driver 6.0 y 4.2 para SQL Server:**  
  
  dos bibliotecas de clases JAR en cada paquete de instalación: sqljdbc41.jar y sqljdbc42.jar. 
  
 JDBC Driver 6.0 y 4.2 está diseñado para funcionar con todas las máquinas virtuales de Java equivalentes de Sun y ser compatible con ellas, aunque solo se ha probado en Sun JRE 5.0, 6.0, 7.0 y 8.0. 
  
 A continuación se resume la compatibilidad que ofrecen los dos archivos JAR incluidos en Microsoft JDBC Driver 6.0 y 4.2 para SQL Server:  
  
|JAR|Cumplimiento con la versión JDBC|Versión de Java recomendada|Descripción|  
|---------|-----------------------------|----------------------|-----------------|   
|sqljdbc41.jar|4.1|7|Requiere la versión 7.0 de Java Runtime Environment (JRE). El uso de JRE 6.0 o anterior lanzará una excepción.<br /><br /> Las nuevas características de los paquetes 6.0 y 4.2 incluyen: JBC 4.1 Compliance y Bulk Copy<br /><br /> Además, las nuevas características solo del paquete 6.0 incluyen: Always Encrypted, los parámetros con valores de tabla, Azure autenticación de Active Directory, conexiones transparentes a grupos de disponibilidad AlwaysOn, mejora en la recuperación de metadatos de parámetro para preparado las consultas y el nombre de dominio internacionalizado (IDN)|  
|sqljdbc42.jar|4.2|8|Requiere la versión 8.0 de Java Runtime Environment (JRE). El uso de JRE 7.0 o anterior lanzará una excepción.<br /><br /> Las nuevas características de los paquetes 6.0 y 4.2 incluyen: JDBC 4.1 Compliance, JDBC 4.2 Compliance y Bulk Copy<br /><br /> Además, las nuevas características solo del paquete 6.0 incluyen: Always Encrypted, los parámetros con valores de tabla, Azure autenticación de Active Directory, conexiones transparentes a grupos de disponibilidad AlwaysOn, mejora en la recuperación de metadatos de parámetro para preparado las consultas y el nombre de dominio internacionalizado (IDN)|  
  
 **Microsoft JDBC Driver 4.1 para SQL Server:**  
  
 dos bibliotecas de clases JAR en cada paquete de instalación: sqljdbc41.jar y sqljdbc42.jar.  
    
|JAR|Descripción|  
|---------|-----------------|  
|sqljdbc41.jar|La biblioteca de clases **sqljdbc41.jar** proporciona compatibilidad con la API de JDBC 4.0. Incluye todas las características de JDBC 4.0 y los métodos de la API de JDBC 4.0. JDBC 4.1 no es compatible (se produce una excepción "SQLFeatureNotSupportedException").<br /><br /> La biblioteca de clases **sqljdbc41.jar** requiere Java Runtime Environment (JRE) 7.0. Uso de **sqljdbc41.jar** en JRE 6.0 y 5.0 produce una excepción.<br /><br /> 
  
 El controlador JDBC se ha diseñado para funcionar con las principales máquinas virtuales Java equivalentes de Sun y ser compatible con ellas, pero se ha probado en Sun JRE 5.0, 6.0 y 7.0.  
  
 A continuación se resume la compatibilidad que ofrece el archivo JAR incluido en Microsoft JDBC Driver 4.1 para SQL Server.  
  
|JAR|Versión de JDBC|JRE (puede ejecutarse)|JDK (puede compilar)|  
|---------|------------------|---------------------|-------------------------|   
|sqljdbc41.jar|4|7|7 6 5|  
  
## <a name="sql-server-requirements"></a>Requisitos de SQL Server  
 El controlador JDBC admite conexiones a Azure SQL Database y SQL Server. Para Microsoft JDBC Driver 4.2 y 4.1 para SQL Server, la compatibilidad comienza a partir de SQL Server 2008.
  
## <a name="operating-system-requirements"></a>Requisitos de sistema operativo  
 El controlador JDBC se ha diseñado para funcionar en cualquier sistema operativo que admita el uso de una máquina virtual Java (JVM). No obstante, solo se han probado oficialmente los sistemas operativos Sun Solaris, SUSE Linux y Windows.  
  
## <a name="supported-languages"></a>Idiomas admitidos  
 El controlador JDBC es compatible con todas las intercalaciones de columnas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Para obtener más información acerca de las intercalaciones compatibles con el controlador JDBC, consulte [Características internacionales del controlador JDBC](../../connect/jdbc/international-features-of-the-jdbc-driver.md).  
  
 Para obtener más información sobre las intercalaciones, vea "Trabajar con intercalaciones" en Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
## <a name="see-also"></a>Ver también  
 [Introducción al controlador JDBC](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
