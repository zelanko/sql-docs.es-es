---
title: Dependencias de características de Microsoft JDBC Driver para SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 07/31/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 939a8773-2583-49a4-bf00-6b892fbe39dc
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 61c66d192a158fb754563e2d103eba946dee47c6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47830363"
---
# <a name="feature-dependencies-of-microsoft-jdbc-driver-for-sql-server"></a>Dependencias de características de Microsoft JDBC Driver para SQL Server

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Esta página se enumera las bibliotecas que depende de Microsoft JDBC Driver para SQL Server. El proyecto tiene las siguientes dependencias.

## <a name="compile-time"></a>Tiempo de compilación

- `azure-keyvault`: Azure Key Vault Provider para la característica Always Encrypted Azure Key Vault (opcional)
- `adal4j`: Biblioteca de Active Directory azure para Java para la característica de autenticación de Azure Active Directory y la característica de Azure Key Vault (opcional)

## <a name="test-time"></a>Tiempo de la prueba

Deben declarar explícitamente las dependencias correspondientes en su archivo pom proyectos específicos que requieran cualquiera de las dos características anteriores:

**_Por ejemplo:_**  al usar _característica de autenticación de Azure Active Directory_, deberá volver a declarar _adal4j_ dependencia en el archivo del proyecto pom. Vea el siguiente fragmento:

```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>7.0.0.jre10</version>
    <scope>compile</scope>
</dependency>

<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>adal4j</artifactId>
    <version>1.6.0</version>
</dependency>
```

**_Por ejemplo:_**  al usar _la característica Azure Key Vault_, deberá volver a declarar _azure-keyvault_ dependencia y _adal4j_ dependencia en el archivo del proyecto pom. Vea el siguiente fragmento:

```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>7.0.0.jre10</version>
    <scope>compile</scope>
</dependency>

<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>adal4j</artifactId>
    <version>1.6.0</version>
</dependency>

<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-keyvault</artifactId>
    <version>1.0.0</version>
</dependency>
```

## <a name="dependency-requirements-for-the-jdbc-driver"></a>Requisitos de dependencias para el controlador JDBC

### <a name="working-with-azure-key-vault-provider"></a>Trabajar con Azure Key Vault Provider:

- Versión del controlador JDBC 7.0.0 - las versiones de dependencias: Azure-Keyvault (versión 1.0.0), Adal4j (versión 1.6.0) y sus dependencias ([aplicación de ejemplo](../../connect/jdbc/azure-key-vault-sample-version-7-0-0.md))
- Versión del controlador JDBC 6.4.0 - las versiones de dependencias: Azure-Keyvault (versión 1.0.0), Adal4j (versión 1.4.0) y sus dependencias ([aplicación de ejemplo](../../connect/jdbc/azure-key-vault-sample-version-6.2.2.md))
- Versión del controlador JDBC 6.2.2 - las versiones de dependencias: Azure-Keyvault (versión 1.0.0), Adal4j (versión 1.4.0) y sus dependencias ([aplicación de ejemplo](../../connect/jdbc/azure-key-vault-sample-version-6.2.2.md))
- Versión del controlador JDBC 6.0.0 - las versiones de dependencias: Azure-Keyvault (versión 0.9.7), Adal4j (versión 1.3.0) y sus dependencias ( [aplicación de ejemplo](../../connect/jdbc/azure-key-vault-sample-version-6.0.0.md))

> [!NOTE]
> Con las versiones de controlador v6.2.2 y v6.4.0, la dependencia de azure-keyvault-java había actualizada a la versión 1.0.0. Sin embargo, la nueva versión no era compatible con la versión anterior (versión 0.9.7) y, por tanto, interrumpe la implementación existente en el controlador. La nueva implementación en el controlador requiere cambios en la API, que a su vez interrumpe programas cliente que usan el proveedor de almacén de claves de Azure.

> Este problema se ha resuelto con v7.0.0 de versión más reciente de controlador como el constructor quitado mediante el mecanismo de devolución de llamada de autenticación se agrega al proveedor de Azure Key Vault para hacia atrás compatibilidad.

### <a name="working-with-azure-active-directory-authentication"></a>Uso de la autenticación de Azure Active Directory:

- Versión del controlador JDBC 7.0.0 - las versiones de dependencias: Ada4j (versión 1.6.0) y sus dependencias
- Versión del controlador JDBC 6.4.0 - las versiones de dependencias: Adal4j (versión 1.4.0) y sus dependencias
- Versión del controlador JDBC 6.2.2 - las versiones de dependencias: Adal4j (versión 1.4.0) y sus dependencias
- Versión del controlador JDBC 6.0.0 - las versiones de dependencias: Adal4j (versión 1.3.0), y sus dependencias: en esta versión del controlador, se puede conectar con _ActiveDirectoryIntegrated_ modo de autenticación solo en un sistema operativo de Windows y mediante sqljdbc_auth.dll y Active Directory Authentication Library para SQL Server (ADALSQL. (DLL).

Desde la versión del controlador 6.4.0 y versiones posteriores, las aplicaciones no requieren necesariamente utilizando ADALSQL. Archivo DLL en sistemas operativos de Windows. Para **sistemas que no son Windows**, el controlador requiere el vale de Kerberos para trabajar con la autenticación de ActiveDirectoryIntegrated. Para obtener más información sobre cómo conectarse a Active Directory con Kerberos, vea [vale de Kerberos establecido en Windows, Linux y Mac](https://docs.microsoft.com/sql/connect/jdbc/connecting-using-azure-active-directory-authentication#set-kerberos-ticket-on-windows-linux-and-mac).

Para **los sistemas operativos de Windows**, controlador busca sqljdbc_auth.dll de forma predeterminada y no requiere instalación de vale de Kerberos o las dependencias de biblioteca de Azure. Sin embargo, si sqljdbc_auth.dll no está disponible, controlador busca el vale de Kerberos para autenticarse en Active Directory como en otros sistemas operativos.

Puede encontrar una aplicación de ejemplo utilizando esta característica [aquí](../../connect/jdbc/connecting-using-azure-active-directory-authentication.md).

## <a name="see-also"></a>Ver también

[Repositorio de GitHub del controlador JDBC](https://github.com/microsoft/mssql-jdbc)  
 [Referencia de API del controlador JDBC](../../connect/jdbc/reference/jdbc-driver-api-reference.md)
