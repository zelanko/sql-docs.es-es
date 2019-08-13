---
title: Usar la autenticación NTLM para conectarse a SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 07/31/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: lilgreenbird
ms.author: v-susanh
manager: kenvh
ms.openlocfilehash: 11fe35e1dc90e32cac460b61fe8a6078c817b0ca
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 08/09/2019
ms.locfileid: "68894107"
---
# <a name="using-ntlm-authentication-to-connect-to-sql-server"></a>Usar la autenticación NTLM para conectarse a SQL Server

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Permite que una aplicación use la propiedad de conexión **authenticationScheme** para indicar que desea conectarse a una base de datos mediante la autenticación NTLM v2. [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 

Las siguientes propiedades también se usan para la autenticación NTLM:

- **dominio = nombreDeDominio** opta
- **usuario = nombre de usuario**
- **password = contraseña**
- **integratedSecurity = true**

Aparte de **dominio**, las demás propiedades son obligatorias, el controlador producirá un error si faltan cuando se utiliza la propiedad AuthenticationScheme de **NTLM** . 

Para obtener más información sobre las propiedades de conexión, vea [establecer las propiedades de conexión](../../connect/jdbc/setting-the-connection-properties.md). Para obtener más información sobre el protocolo de autenticación NTLM de Microsoft, consulte [Microsoft NTLM](https://docs.microsoft.com/windows/desktop/SecAuthN/microsoft-ntlm).

## <a name="remarks"></a>Notas

Consulte [seguridad de red: nivel de autenticación de LAN Manager](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/network-security-lan-manager-authentication-level) para obtener una descripción de la configuración de SQL Server, que controla el comportamiento de la autenticación NTLM. 

## <a name="logging"></a>Registro

Se ha agregado un nuevo registrador para admitir la autenticación NTLM: com.microsoft.sqlserver.jdbc.internals.NTLMAuthentication. Para obtener más información, vea [Hacer un seguimiento del funcionamiento del controlador](../../connect/jdbc/tracing-driver-operation.md).

## <a name="datasource"></a>DataSource

Cuando se usa un origen de orígenes para crear conexiones, las propiedades de NTLM se pueden establecer mediante programación con **setAuthenticationScheme**, **setDomain**y, opcionalmente, **setServerSpn**.

```java
SQLServerDataSource ds = new SQLServerDataSource();
ds.setServerName("<server>");
ds.setPortNumber(1433); // change if necessary
ds.setIntegratedSecurity(true);
ds.setAuthenticationScheme("NTLM");
ds.setDomain("<domainName>");
ds.setUser("<userName>");
ds.setPassword("<password>");
ds.setDatabaseName("<database>");
ds.setServerSpn("<serverSpn");

try (Connection c = ds.getConnection(); Statement s = c.createStatement();
        ResultSet rs = s.executeQuery("select auth_scheme from sys.dm_exec_connections where session_id=@@spid")) {
    while (rs.next()) {
        System.out.println("Authentication Scheme: " + rs.getString(1));
    }
}
```

## <a name="service-principal-names"></a>Nombres de entidad de seguridad de servicio

Un nombre principal de servicio (SPN) es el nombre por el que un cliente identifica de forma unívoca una instancia de un servicio.

Puede especificar el SPN con la propiedad de conexión **serverSpn** o dejar que el controlador lo genere automáticamente (el valor predeterminado). Esta propiedad tiene el formato "MSSQLSvc/fqdn:port\@REALM", donde fqdn es el nombre de dominio completo, port es el número de puerto y REALM es el dominio de SQL Server en letras mayúsculas. La parte del dominio Kerberos de esta propiedad es opcional, ya que el dominio Kerberos predeterminado es el mismo que el del servidor.

Por ejemplo, el SPN podría tener el siguiente aspecto: "MSSQLSvc/some-Server. zzz. Corp. contoso. com: 1433"

Para obtener más información sobre los nombres de entidad de seguridad de servicio (SPN), vea:

- [Compatibilidad con Nombre de la entidad de seguridad de servicio (SPN) en conexiones cliente](https://docs.microsoft.com/sql/relational-databases/native-client/features/service-principal-name-spn-support-in-client-connections?view=sql-server-2017)

> [!NOTE]  
> El atributo de conexión serverSpn solo es compatible con Microsoft JDBC Driver 4.2 y superior.

> Antes de la versión 6,2 del controlador JDBC, tendría que establecer explícitamente el valor de **serverSpn**. A partir de la versión 6,2, el controlador podrá compilar el **serverSpn** de forma predeterminada, aunque también puede usar **serverSpn** explícitamente.

## <a name="security-risks"></a>Riesgos de seguridad

El protocolo NTLM es un protocolo de autenticación antiguo con diversas vulnerabilidades, que suponen un riesgo para la seguridad. Se basa en un esquema criptográfico relativamente débil y es vulnerable a varios ataques. Se reemplaza con Kerberos, que es mucho más seguro y recomendado. La autenticación NTLM solo debe usarse en un entorno de confianza seguro o cuando no se puede usar Kerberos.

El [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] solo admite NTLM v2, que tiene algunas mejoras de seguridad sobre el protocolo v1 original. It'ss también se recomienda para habilitar la protección ampliada o usar el cifrado SSL para mejorar la seguridad. 

Para obtener más información sobre cómo habilitar la protección ampliada y, consulte:

- [Conectar al motor de base de datos con protección ampliada](../../database-engine/configure-windows/connect-to-the-database-engine-using-extended-protection.md)

Para obtener más información sobre cómo conectarse con el cifrado SSL, vea:

- [Conectar con el cifrado SSL](../../connect/jdbc/connecting-with-ssl-encryption.md)

> [!NOTE]
> En la versión 7,4, no **** se admite la habilitación de la protección ampliada y el cifrado.

## <a name="see-also"></a>Consulte también

[Conexión a SQL Server con el controlador JDBC](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)
