---
title: Dependencias de características de Microsoft JDBC Driver para SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 02/06/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 939a8773-2583-49a4-bf00-6b892fbe39dc
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 26402f5b15fa7dd8e24b13f3adc41836ff275228
ms.sourcegitcommit: c61c7b598aa61faa34cd802697adf3a224aa7dc4
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2019
ms.locfileid: "56154690"
---
# <a name="feature-dependencies-of-the-microsoft-jdbc-driver-for-sql-server"></a>Dependencias de características de Microsoft JDBC Driver para SQL Server

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

En este artículo se enumera las bibliotecas que depende de Microsoft JDBC Driver para SQL Server. El proyecto tiene las siguientes dependencias.

## <a name="compile-time"></a>Tiempo de compilación

 - `com.microsoft.azure:azure-keyvault` : Azure Key Vault Provider para la característica Always Encrypted Azure Key Vault (opcional)
 - `com.microsoft.azure:azure-keyvault-webkey` : Azure Key Vault Provider para la característica Always Encrypted Azure Key Vault (opcional)
 - `com.microsoft.azure:adal4j` : Biblioteca de Active Directory azure para Java para la característica de autenticación de Azure Active Directory y la característica de Azure Key Vault (opcional)
 - `com.microsoft.rest:client-runtime` : Biblioteca de Active Directory azure para Java para la característica de autenticación de Azure Active Directory y la característica de Azure Key Vault (opcional)
- `org.osgi:org.osgi.core`: Biblioteca de Core OSGi compatibilidad con el marco de trabajo OSGi.
- `org.osgi:org.osgi.compendium`: Biblioteca de Compendium OSGi para compatibilidad con el marco OSGi.

## <a name="test-time"></a>Tiempo de la prueba

Deben declarar explícitamente las dependencias correspondientes en su archivo POM proyectos específicos que requieran cualquiera de las características anteriores.

**Por ejemplo:** cuando usa la característica de autenticación de Azure Active Directory, deberá volver a declarar el `adal4j` dependencia en el archivo del proyecto POM. Vea el siguiente fragmento:

```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>7.2.1.jre11</version>
    <scope>compile</scope>
</dependency>

<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>adal4j</artifactId>
    <version>1.6.3</version>
</dependency>

<dependency>
    <groupId>com.microsoft.rest</groupId>
    <artifactId>client-runtime</artifactId>
    <version>1.6.5</version>
</dependency>
```

**Por ejemplo:** cuando usa la característica de Azure Key Vault, deberá volver a declarar el `azure-keyvault` dependencia y el `adal4j` dependencia en el archivo del proyecto POM. Vea el siguiente fragmento:

```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>7.2.1.jre11</version>
    <scope>compile</scope>
</dependency>

<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>adal4j</artifactId>
    <version>1.6.3</version>
</dependency>

<dependency>
    <groupId>com.microsoft.rest</groupId>
    <artifactId>client-runtime</artifactId>
    <version>1.6.5</version>
</dependency>

<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-keyvault</artifactId>
    <version>1.2.0</version>
</dependency>

<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-keyvault-webkey</artifactId>
    <version>1.2.0</version>
</dependency>
```

## <a name="dependency-requirements-for-the-jdbc-driver"></a>Requisitos de dependencias para JDBC Driver

### <a name="working-with-the-azure-key-vault-provider"></a>Trabajar con el proveedor de almacén de claves de Azure:

- Versión del controlador JDBC 7.2.1 - las versiones de dependencias: Azure-Keyvault (versión 1.2.0), Azure-Keyvault-Webkey (versión 1.2.0), Adal4j (versión 1.6.3), cliente en tiempo de ejecución de AutoRest (1.6.5) y sus dependencias ([delaaplicacióndeejemplo](../../connect/jdbc/azure-key-vault-sample.md))
- Versión del controlador JDBC 7.0.0 - las versiones de dependencias: Azure-Keyvault (versión 1.0.0), Adal4j (versión 1.6.0) y sus dependencias ([aplicación de ejemplo](../../connect/jdbc/azure-key-vault-sample.md))
- Versión del controlador JDBC 6.4.0 - las versiones de dependencias: Azure-Keyvault (versión 1.0.0), Adal4j (versión 1.4.0) y sus dependencias ([aplicación de ejemplo](../../connect/jdbc/azure-key-vault-sample-version-6.2.2.md))
- Versión del controlador JDBC 6.2.2 - las versiones de dependencias: Azure-Keyvault (versión 1.0.0), Adal4j (versión 1.4.0) y sus dependencias ([aplicación de ejemplo](../../connect/jdbc/azure-key-vault-sample-version-6.2.2.md))
- Versión del controlador JDBC 6.0.0 - las versiones de dependencias: Azure-Keyvault (versión 0.9.7), Adal4j (versión 1.3.0) y sus dependencias ( [aplicación de ejemplo](../../connect/jdbc/azure-key-vault-sample-version-6.0.0.md))

> [!NOTE]
> Con las versiones de controlador 6.2.2 y 6.4.0, la dependencia de azure-keyvault-java había actualizada a la versión 1.0.0. Sin embargo, la nueva versión no era compatible con la versión anterior (0.9.7) e interrumpe la implementación existente en el controlador. La nueva implementación en el controlador requiere cambios en la API, que a su vez interrumpe programas cliente que usan el proveedor de almacén de claves de Azure.
>
> Este problema se resuelve con la versión más reciente del controlador (7.0.0). El constructor quitado que utiliza el mecanismo de devolución de llamada de autenticación se agrega al proveedor de almacén de claves de Azure para la compatibilidad con versiones anteriores.

### <a name="working-with-azure-active-directory-authentication"></a>Uso de la autenticación de Azure Active Directory:

- Versión del controlador JDBC 7.2.1 - las versiones de dependencias: Adal4j (versión 1.6.3), cliente en tiempo de ejecución de AutoRest (1.6.5) y sus dependencias
- Versión del controlador JDBC 7.0.0 - las versiones de dependencias: Adal4j (versión 1.6.0) y sus dependencias
- Versión del controlador JDBC 6.4.0 - las versiones de dependencias: Adal4j (versión 1.4.0) y sus dependencias
- Versión del controlador JDBC 6.2.2 - las versiones de dependencias: Adal4j (versión 1.4.0) y sus dependencias
- Versión del controlador JDBC 6.0.0 - las versiones de dependencias: Adal4j (versión 1.3.0) y sus dependencias. En esta versión del controlador, puede conectarse mediante _ActiveDirectoryIntegrated_ modo de autenticación solo en un sistema operativo de Windows y mediante sqljdbc_auth.dll y Active Directory Authentication Library para SQL Server () ADALSQL. (DLL).

Desde la versión del controlador 6.4.0 en adelante, las aplicaciones no requieren necesariamente utilizando ADALSQL. Archivo DLL en sistemas operativos de Windows. Para *sistemas de operativos que no sean Windows*, el controlador requiere un vale Kerberos para trabajar con la autenticación de ActiveDirectoryIntegrated. Para obtener más información sobre cómo conectarse a Active Directory mediante el uso de Kerberos, vea [vale de Kerberos establecido en Windows, Linux y Mac](https://docs.microsoft.com/sql/connect/jdbc/connecting-using-azure-active-directory-authentication#set-kerberos-ticket-on-windows-linux-and-mac).

Para *los sistemas operativos de Windows*, el controlador busca sqljdbc_auth.dll de forma predeterminada y no requiere instalación de vale de Kerberos ni dependencias de biblioteca de Azure. Si sqljdbc_auth.dll no está disponible, el controlador busca el vale de Kerberos para autenticarse en Active Directory como en otros sistemas operativos.

Puede obtener un [aplicación de ejemplo](../../connect/jdbc/connecting-using-azure-active-directory-authentication.md) que usa esta característica.

## <a name="see-also"></a>Vea también

[Repositorio de GitHub del controlador JDBC](https://github.com/microsoft/mssql-jdbc)  
 [Referencia de API de JDBC Driver](../../connect/jdbc/reference/jdbc-driver-api-reference.md)
