---
title: Características de las dependencias del controlador JDBC de Microsoft para SQL Server | Documentos de Microsoft
ms.custom: ''
ms.date: 02/28/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 939a8773-2583-49a4-bf00-6b892fbe39dc
caps.latest.revision: 57
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 052628258ae1d8c1f31430ea132ed594a976be98
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="feature-dependencies-of-microsoft-jdbc-driver-for-sql-server"></a>Dependencias de características del controlador JDBC de Microsoft para SQL Server
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

 Esta página contiene la lista de bibliotecas que depende el controlador JDBC de Microsoft para SQL Server. El proyecto tiene las siguientes dependencias.
 
 ## <a name="compile-time"></a>Tiempo de compilación
 - `azure-keyvault` : Proveedor de almacén de claves azure para la característica de siempre cifrado Azure Key Vault (opcional)
 - `adal4j` : Biblioteca de Active Directory azure para Java para la característica de autenticación de Azure Active Directory y la característica de almacén de claves de Azure (opcional)

 ##  <a name="test-time"></a>Tiempo de la prueba
Proyectos específicos que requieran cualquiera de las dos funciones anteriores deben declarar explícitamente las dependencias correspondientes en su archivo pom:

***Por ejemplo:*** si utilizas *característica de autenticación de Azure Active Directory*, deberá volver a declarar *adal4j* dependencia en el archivo del proyecto pom. Ver el fragmento de código siguiente: 
```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>6.4.0.jre8</version>
    <scope>compile</scope>
</dependency>

<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>adal4j</artifactId>
    <version>1.4.0</version>
</dependency>
```

***Por ejemplo:*** si utilizas *característica almacén de claves de Azure* , a continuación, debe volver a declarar *azure keyvault* dependencia y *adal4j* dependencia en el archivo de pom del proyecto. Ver el fragmento de código siguiente: 
```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>6.4.0.jre8</version>
    <scope>compile</scope>
</dependency>

<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>adal4j</artifactId>
    <version>1.4.0</version>
</dependency>

<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-keyvault</artifactId>
    <version>1.0.0</version>
</dependency>
```
 
 ## <a name="dependency-requirements-for-the-jdbc-driver"></a>Requisitos de dependencia para el controlador JDBC

 ### <a name="azure-keyvault-feature"></a>Característica Keyvault Azure:
- Versión 6.0.0 del controlador JDBC 
    - Versiones de dependencia: Keyvault de Azure (versión 0.9.7), Adal4j (versión 1.3.0) y sus dependencias ( [aplicación de ejemplo](../../connect/jdbc/azure-key-vault-sample-version-6.0.0.md))
- Versión 6.2.2 del controlador JDBC y versiones posteriores (incluido el 6.4.0 más reciente)
    - Versiones de dependencia: Keyvault de Azure (versión 1.0.0), Adal4j (versión 1.4.0) y sus dependencias ([aplicación de ejemplo](../../connect/jdbc/azure-key-vault-sample-version-6.2.2.md))

> [!NOTE]
>   A partir de v6.2.2, la dependencia de java de keyvault de azure se actualiza a la versión 1.0.0. Sin embargo, la nueva versión no es compatible con la versión anterior (versión 0.9.7) y, por tanto, interrumpe la implementación existente en el controlador. La nueva implementación en el controlador requiere cambios en la API, que a su vez interrumpir los programas de clientes que utilizan la característica de almacén de claves de Azure.

  
 ### <a name="azure-active-directory-authentication"></a>Autenticación de Azure Active Directory:
- Versión 6.0.0 del controlador JDBC 
    - Versiones de dependencia: Adal4j (versión 1.3.0) y sus dependencias
        - En esta versión del controlador, se puede conectar con *ActiveDirectoryIntegrated* modo de autenticación solo en una ventana de sistema operativo y el uso de sqljdbc_auth.dll y biblioteca de autenticación de Active Directory para SQL Server () ADALSQL. (DLL). 
- Versión 6.4.0 del controlador JDBC
    - Versiones de dependencia: Adal4j (versión 1.4.0) y sus dependencias
        - En esta versión del controlador, la aplicación no requieren el uso de ADALSQL. DLL. Dependiendo de los sistemas operativos. Para **sistemas operativos que no sean Windows**, el controlador requiere el vale de Kerberos para trabajar con la autenticación de ActiveDirectoryIntegrated. Vea [vale de Kerberos establecido en Windows, Linux y Mac](https://docs.microsoft.com/sql/connect/jdbc/connecting-using-azure-active-directory-authentication#set-kerberos-ticket-on-windows-linux-and-mac) para obtener más detalles. Para **sistemas operativos Windows**, controlador de forma predeterminada comprueba si sqljdbc_auth.dll se carga y no requiere la dependencia de instalación o adal4j del vale de Kerberos. Sin embargo, si no se carga sqljdbc_auth.dll, controlador se comporta del mismo modo que los sistemas operativos que no son Windows y requeriría el programa de instalación, que se describe en el ejemplo siguiente: una aplicación de ejemplo con esta característica puede encontrarse [aquí](../../connect/jdbc/connecting-using-azure-active-directory-authentication.md) .

 ## <a name="see-also"></a>Vea también  
 [Repositorio de GitHub del controlador JDBC](https://github.com/microsoft/mssql-jdbc)  
 [Referencia de API del controlador JDBC](../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  