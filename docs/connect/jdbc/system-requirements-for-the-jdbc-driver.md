---
title: Requisitos del sistema para el controlador JDBC | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 447792bb-f39b-49b4-9fd0-1ef4154c74ab
caps.latest.revision: 73
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: eed93fab6f0ceec655b7b9f6b392abc390b5f0ff
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="system-requirements-for-the-jdbc-driver"></a>Requisitos del sistema para el controlador JDBC
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Para obtener acceso a datos desde una [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] utilizando el [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], debe tener los siguientes componentes instalados en el equipo:  
  
-   [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]  
  
     Puede descargar el controlador JDBC de Microsoft desde los vínculos de Microsoft Download Center siguientes: 
     * [Microsoft JDBC Driver 6.2 para SQL Server](http://go.microsoft.com/fwlink/?linkid=852460)
     * [Microsoft JDBC Driver 6.0 para SQL Server](http://go.microsoft.com/fwlink/?linkid=841535)
     * [Microsoft JDBC Driver 4.2 para SQL Server](http://go.microsoft.com/fwlink/?linkid=841534) 
     * [Microsoft JDBC Driver 4.1 para SQL Server](http://go.microsoft.com/fwlink/?linkid=841533) 
     * [Controlador JDBC 4.0 de Microsoft para SQL Server](http://go.microsoft.com/fwlink/?linkid=841532)
  
-   Java Runtime Environment  
  
## <a name="java-runtime-environment-requirements"></a>Requisitos de Java Runtime Environment  
 A partir de Microsoft JDBC Driver 4.2 para SQL Server, se admiten Sun Java SE Development Kit (JDK) 8.0 y Java Runtime Environment (JRE) 8.0. La compatibilidad con API de Java Database Connectivity (JDBC) Spec se ha ampliado para incluir la API de JDBC 4.1 y 4.2.  
  
 A partir de la versión 4.1 del controlador Microsoft JDBC para SQL Server, son compatibles el Kit de desarrollo Sun Java SE (JDK) 7.0 y Java Runtime Environment (JRE) 7.0.  
  
 A partir de la [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)], el controlador JDBC proporciona compatibilidad para la API de Java Database Connectivity (JDBC) Spec se ha ampliado para incluir la API de JDBC 4.0. La API de JDBC 4.0 se presentó como parte de Sun Java SE Development Kit (JDK) 6.0 y de Java Runtime Environment (JRE) 6.0. JDBC 4.0 es un superconjunto de la API de JDBC 3.0.  
  
 Cuando se implementa el [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] en los sistemas operativos Windows y UNIX, debe usar los paquetes de instalación, *sqljdbc_\<versión > _enu.exe* y *sqljdbc_\<versión > _ ENU.tar.gz*, respectivamente. Para obtener más información sobre cómo implementar el controlador JDBC, consulte [implementar el controlador JDBC](../../connect/jdbc/deploying-the-jdbc-driver.md) tema.  
  
**Microsoft JDBC Driver 6.2 para SQL Server:**  
  
  El 6.2 del controlador JDBC incluye dos bibliotecas de clases JAR en cada paquete de instalación: **mssql-jdbc-6.2.1.jre7.jar**, y **mssql-jdbc-6.2.1.jre8.jar**. 
  
 El 6.2 del controlador JDBC está diseñado para trabajar con y ser compatibles con todas las principales Sun máquinas virtuales Java equivalentes, pero se ha probado sólo en Sun JRE 5.0, 6.0, 7.0 y 8.0. 
  
 A continuación resume la compatibilidad proporcionada por los dos archivos JAR incluidos con Microsoft JDBC Drivers 6.0 y 4.2 para SQL Server:  
  
|JAR|Cumplimiento con la versión JDBC|Versión de Java recomendada|Description|  
|---------|-----------------------------|----------------------|-----------------|   
|MSSQL-jdbc-6.2.1.jre7.jar|4.1|7|Requiere la versión 7.0 de Java Runtime Environment (JRE). El uso de JRE 6.0 o anterior lanzará una excepción.<br /><br /> Nuevas características de 6.2 incluyen: autenticación de Azure AD para Linux, método de entidad de seguridad y la contraseña para la detección automática de dominio KERBEROS de SPN para la autenticación entre dominios, delegación limitada de Kerberos, el tiempo de espera de consulta, el tiempo de espera de Socket, Kerberos y preparada identificador de instrucciones volver a usar. |  
|MSSQL-jdbc-6.2.1.jre8.jar|4.2|8|Requiere la versión 8.0 de Java Runtime Environment (JRE). El uso de JRE 7.0 o anterior lanzará una excepción.<br /><br /> Nuevas características de 6.2 incluyen: autenticación de Azure AD para Linux, método de entidad de seguridad y la contraseña para la detección automática de dominio KERBEROS de SPN para la autenticación entre dominios, delegación limitada de Kerberos, el tiempo de espera de consulta, el tiempo de espera de Socket, Kerberos y preparada identificador de instrucción volver a usar|    

  El 6.2 del controlador JDBC también está disponible en el repositorio Central de Maven y puede agregado a un proyecto de Maven agregando el código siguiente en el POM. XML 
  
 ```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>6.2.1.jre8</version>
</dependency>
```    

 **Microsoft JDBC Driver 6.0 y 4.2 para SQL Server:**  
  
  JDBC Drivers 6.0 y 4.2 incluyen dos bibliotecas de clases JAR en cada paquete de instalación: **sqljdbc41.jar**, y **sqljdbc42.jar**. 
  
 JDBC Drivers 6.0 y 4.2 están diseñados para trabajar con y ser compatibles con todas las principales Sun máquinas virtuales Java equivalentes, pero se ha probado sólo en Sun JRE 5.0, 6.0, 7.0 y 8.0. 
  
 A continuación resume la compatibilidad proporcionada por los dos archivos JAR incluidos con Microsoft JDBC Drivers 6.0 y 4.2 para SQL Server:  
  
|JAR|Cumplimiento con la versión JDBC|Versión de Java recomendada|Description|  
|---------|-----------------------------|----------------------|-----------------|   
|sqljdbc41.jar|4.1|7|Requiere la versión 7.0 de Java Runtime Environment (JRE). El uso de JRE 6.0 o anterior lanzará una excepción.<br /><br /> Las nuevas características de los paquetes 6.0 y 4.2 incluyen: JBC 4.1 Compliance y Bulk Copy<br /><br /> Además, nuevas características de únicamente el paquete 6.0 incluyen: Always Encrypted, parámetros con valores de tabla, Azure autenticación de Active Directory, conexiones transparentes a grupos de disponibilidad AlwaysOn, para la mejora de la recuperación de metadatos de parámetro para preparar las consultas y el nombre de dominio internacionalizado (IDN)|  
|sqljdbc42.jar|4.2|8|Requiere la versión 8.0 de Java Runtime Environment (JRE). El uso de JRE 7.0 o anterior lanzará una excepción.<br /><br /> Las nuevas características de los paquetes 6.0 y 4.2 incluyen: JDBC 4.1 Compliance, JDBC 4.2 Compliance y Bulk Copy<br /><br /> Además, nuevas características de únicamente el paquete 6.0 incluyen: Always Encrypted, parámetros con valores de tabla, Azure autenticación de Active Directory, conexiones transparentes a grupos de disponibilidad AlwaysOn, para la mejora de la recuperación de metadatos de parámetro para preparar las consultas y el nombre de dominio internacionalizado (IDN)|  
  
 **Microsoft JDBC Driver 4.1 para SQL Server:**  
  
 JDBC Driver 4.1 incluye una biblioteca de clases JAR en cada paquete de instalación: **sqljdbc41.jar**.  
    
|JAR|Description|  
|---------|-----------------|  
|sqljdbc41.jar|**sqljdbc41.jar** biblioteca de clases proporciona compatibilidad con API de JDBC 4.0. Incluye todas las características del controlador JDBC 4.0, así como los métodos de la API de JDBC 4.0. JDBC 4.1 no es compatible (se producirá una excepción "SQLFeatureNotSupportedException").<br /><br /> **sqljdbc41.jar** biblioteca de clases requiere un 7.0 de Java Runtime Environment (JRE). Usar **sqljdbc41.jar** en JRE 6.0 y 5.0 se iniciará una excepción.<br /><br /> 
  
 Tenga en cuenta que el controlador JDBC se ha diseñado para funcionar con todas las principales máquinas virtuales Java equivalentes de Sun y ser compatibles con las mismas, pero se prueba en Sun JRE 5.0, 6.0 y 7.0.  
  
 A continuación resume la compatibilidad proporcionada por el archivo JAR incluido con Microsoft JDBC Driver 4.1 para SQL Server.  
  
|JAR|Versión de JDBC|JRE (puede ejecutarse)|JDK (puede compilar)|  
|---------|------------------|---------------------|-------------------------|   
|sqljdbc41.jar|4|7|7 6 5|  
  
 **Microsoft JDBC Driver 4.0 para SQL Server:**  
  
 Para ofrecer compatibilidad con versiones anteriores y posibles escenarios de actualización, el controlador JDBC incluye dos bibliotecas de clases JAR en cada paquete de instalación: **sqljdbc.jar** y **sqljdbc4.jar**.  
  
|JAR|Description|  
|---------|-----------------|  
|sqljdbc.jar|**sqljdbc.jar** biblioteca de clases proporciona compatibilidad con JDBC 3.0.<br /><br /> **sqljdbc.jar** biblioteca de clases requiere un servicio de Java Runtime Environment (JRE) versión 5.0. Usar **sqljdbc.jar** en JRE 6.0 o JRE 7.0 se iniciará una excepción cuando se conecta a una base de datos.<br /><br /> **Nota:** el controlador JDBC no es compatible con JRE 1.4. Debe actualizar JRE 1.4 a JRE 5.0, JRE 6.0 o JRE 7.0 al usar el Controlador JDBC. En algunos casos, es posible que necesite volver a compilar la aplicación porque puede ser no compatible con la API de JDK 5.0 o de JDK 6.0. Para obtener más información, consulte la documentación disponible en el sitio web de Sun Microsystems.<br /><br /> [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)]no admite JDK 7.|  
|sqljdbc4.jar|**sqljdbc4.jar** biblioteca de clases proporciona compatibilidad con API de JDBC 4.0. Incluye todas las características de la **sqljdbc.jar** , así como los nuevos métodos de API de JDBC 4.0.<br /><br /> **sqljdbc4.jar** biblioteca de clases requiere un servicio de Java Runtime Environment (JRE) versión 6.0 o 7.0. Usar **sqljdbc4.jar** en JRE 5.0 se iniciará una excepción.<br /><br /> **Nota:** usar **sqljdbc4.jar** cuando la aplicación debe ejecutarse en JRE 6.0 o 7.0, incluso si la aplicación no usa características de la API de JDBC 4.0.|  
  
 Tenga en cuenta que el controlador JDBC se ha diseñado para funcionar con todas las principales máquinas virtuales Java equivalentes de Sun y ser compatibles con las mismas, pero se prueba en Sun JRE 5.0, 6.0 y 7.0.  
  
## <a name="sql-server-requirements"></a>Requisitos de SQL Server  
 El controlador JDBC admite conexiones a la base de datos SQL de Azure y SQL Server. Para Microsoft JDBC Driver 4.2 y 4.1 para SQL Server, la compatibilidad comienza a partir de SQL Server 2008. Para Microsoft JDBC Driver 4.0 para SQL Server, la compatibilidad comienza a partir de SQL Server 2005.  
  
## <a name="operating-system-requirements"></a>Requisitos de sistema operativo  
 El controlador JDBC se ha diseñado para funcionar en cualquier sistema operativo que admita el uso de una máquina virtual Java (JVM). No obstante, solo se han probado oficialmente los sistemas operativos Sun Solaris, SUSE Linux y Windows.  
  
## <a name="supported-languages"></a>Idiomas admitidos  
 El controlador JDBC admite todos los [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] intercalaciones de columna. Para obtener más información acerca de las intercalaciones admitidas por el controlador JDBC, consulte [características internacionales del controlador JDBC](../../connect/jdbc/international-features-of-the-jdbc-driver.md).  
  
 Para obtener más información acerca de las intercalaciones, vea "Trabajar con intercalaciones" en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] libros en pantalla.  
  
## <a name="see-also"></a>Vea también  
 [Información general sobre el controlador JDBC](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  

