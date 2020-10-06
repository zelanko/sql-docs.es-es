---
title: Introducción al espacio de nombres Microsoft.Data.SqlClient
description: Infórmese sobre el espacio de nombres Microsoft.Data.SqlClient y por qué es la forma preferida de conectarse a SQL en el caso de las aplicaciones .NET.
ms.date: 09/29/2020
ms.assetid: c18b1fb1-2af1-4de7-80a4-95e56fd976cb
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-kaywon
ms.openlocfilehash: c3af23cb3816ad45fa75516633749d1f011c930d
ms.sourcegitcommit: d56a834269132a83e5fe0a05b033936776cda8bb
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/29/2020
ms.locfileid: "91529356"
---
# <a name="introduction-to-microsoftdatasqlclient-namespace"></a>Introducción al espacio de nombres Microsoft.Data.SqlClient

[!INCLUDE [Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

## <a name="release-notes-for-microsoftdatasqlclient-20"></a>Notas de la versión de Microsoft.Data.SqlClient 2.0

Las notas de la versión también están disponibles en el repositorio de GitHub: [Notas de la versión 2.0](https://github.com/dotnet/SqlClient/tree/master/release-notes/2.0).

### <a name="breaking-changes"></a>Últimos cambios

- El modificador de acceso de la interfaz del proveedor de enclave `SqlColumnEncryptionEnclaveProvider` ha cambiado de `public` a `internal`.

- Las constantes de la clase `SqlClientMetaDataCollectionNames` se han actualizado para reflejar los cambios en SQL Server.

- El controlador realizará ahora la validación del certificado de servidor cuando el servidor SQL Server de destino aplique el cifrado TLS, que es el valor predeterminado para las conexiones de Azure.

- `SqlDataReader.GetSchemaTable()` ahora devuelve un elemento `DataTable` vacío en lugar de `null`.

- El controlador ahora realiza el redondeo de la escala decimal para que coincida con el comportamiento de SQL Server. Para obtener compatibilidad con versiones anteriores, el comportamiento anterior del truncamiento se puede habilitar mediante un modificador AppContext.

- En el caso de las aplicaciones .NET Framework que consumen **Microsoft.Data.SqlClient**, los archivos SNI.dll descargados previamente en las carpetas `bin\x64` y `bin\x86` ahora se denominan `Microsoft.Data.SqlClient.SNI.x64.dll` y ` Microsoft.Data.SqlClient.SNI.x86.dll`, y se descargarán en el directorio `bin`.

- Por coherencia, los sinónimos nuevos de la propiedad cadena de conexión reemplazarán a las propiedades anteriores cuando se recupere la cadena de conexión de `SqlConnectionStringBuilder`. [Más información](#new-connection-string-property-synonyms)

### <a name="new-features"></a>Nuevas características

#### <a name="dns-failure-resiliency"></a>Resistencia ante errores de DNS

Ahora, el controlador copiará en caché las direcciones IP de todas las conexiones correctas a un punto de conexión de SQL Server que admita la característica. Si se produce un error de resolución de DNS durante un intento de conexión, el controlador intentará establecer una conexión mediante una dirección IP copiada en caché para ese servidor, si existe. 

#### <a name="eventsource-tracing"></a>Seguimiento de EventSource

Esta versión permite la captura de registros de seguimiento de eventos para la depuración de aplicaciones. Para capturar estos eventos, las aplicaciones cliente deben escuchar eventos de la implementación de EventSource de SqlClient:

```
Microsoft.Data.SqlClient.EventSource
```

Para obtener más información, vea cómo [habilitar el seguimiento de eventos en SqlClient](enable-eventsource-tracing.md).

#### <a name="enabling-managed-networking-on-windows"></a>Habilitación de redes administradas en Windows

Un nuevo modificador de AppContext **"Switch.Microsoft.Data.SqlClient.UseManagedNetworkingOnWindows"** permite el uso de una implementación de SNI administrada en Windows con fines de prueba y depuración. Este modificador alternará el comportamiento del controlador a fin de usar un SNI administrado en los proyectos de .NET Core 2.1+ y .NET Standard 2.0+ en Windows, eliminando todas las dependencias de las bibliotecas nativas para la biblioteca Microsoft.Data.SqlClient.

```csharp
AppContext.SetSwitch("Switch.Microsoft.Data.SqlClient.UseManagedNetworkingOnWindows", true);
```

Vea [Modificadores de AppContext en SqlClient](appcontext-switches.md) para obtener una lista completa de los modificadores disponibles en el controlador.

#### <a name="enabling-decimal-truncation-behavior"></a>Habilitación del comportamiento de truncamiento decimal 

El controlador redondeará la escala de datos decimal de forma predeterminada, tal y como lo hace SQL Server. Para obtener la compatibilidad con versiones anteriores, puede establecer el modificador de AppContext **"Switch.Microsoft.Data.SqlClient.TruncateScaledDecimal"** en **true**.

```csharp
AppContext.SetSwitch("Switch.Microsoft.Data.SqlClient.TruncateScaledDecimal", true);
```

#### <a name="new-connection-string-property-synonyms"></a>Sinónimos nuevos de la propiedad de cadena de conexión

Se han agregado sinónimos nuevos para las siguientes propiedades de cadena de conexión existentes a fin de evitar la confusión de espaciado en torno a las propiedades con más de una palabra. Los nombres de propiedades anteriores seguirán siendo compatibles con versiones anteriores, pero las propiedades nuevas de cadena de conexión ahora se incluirán cuando se recupere la cadena de conexión de [SqlConnectionStringBuilder](https://docs.microsoft.com/dotnet/api/microsoft.data.sqlclient.sqlconnectionstringbuilder).

|Propiedad existente de cadena de conexión|Nuevo sinónimo|
|-----------------------------------|-----------|
| Intención de aplicaciones | Intención de aplicaciones |
| ConnectRetryCount | Recuento de reintentos de conexión |
| ConnectRetryInterval | Intervalo de reintentos de conexión |
| PoolBlockingPeriod | Período de bloqueo del grupo |
| MultipleActiveResultSets | Conjunto de resultados activo múltiple (MARS) |
| MultiSubnetFailover | Conmutación por error de varias subredes |
| TransparentNetworkIPResolution | Resolución de IP de red transparente |
| TrustServerCertificate | TrustServerCertificate |

#### <a name="sqlbulkcopy-rowscopied-property"></a>Propiedad RowsCopied de SqlBulkCopy

La propiedad RowsCopied proporciona acceso de solo lectura al número de filas que se han procesado en la operación de copia masiva en curso. Este valor no necesariamente tiene que ser igual al número final de filas agregadas a la tabla de destino. 

#### <a name="connection-open-overrides"></a>Invalidaciones de apertura de la conexión

El comportamiento predeterminado de SqlConnection.Open() se puede invalidar para deshabilitar el retraso de diez segundos y los reintentos de conexión automática que desencadenan los errores transitorios.

```csharp
using SqlConnection sqlConnection = new SqlConnection("Data Source=(local);Integrated Security=true;Initial Catalog=AdventureWorks;");
sqlConnection.Open(SqlConnectionOverrides.OpenWithoutRetry);
```

> [!NOTE]
> Tenga en cuenta que esta invalidación solo se puede aplicar a SqlConnection.Open() y no a SqlConnection.OpenAsync().

#### <a name="username-support-for-active-directory-interactive-mode"></a>Compatibilidad con el nombre de usuario para el modo interactivo de Active Directory

Se puede especificar un nombre de usuario en la cadena de conexión cuando se usa el modo interactivo de autenticación de Azure Active Directory para .NET Framework y .NET Core.

Establezca un nombre de usuario mediante la propiedad de cadena de conexión **User ID** o **UID**:

```
"Server=<server name>; Database=<db name>; Authentication=Active Directory Interactive; User Id=<username>;"
```

#### <a name="order-hints-for-sqlbulkcopy"></a>Sugerencias de orden para SqlBulkCopy

Se pueden proporcionar sugerencias de orden para mejorar el rendimiento de las operaciones de copia masiva en tablas con índices agrupados. Para obtener más información, vea la sección [Operaciones de copia masiva](sql/bulk-copy-order-hints.md).

#### <a name="sni-dependency-changes"></a>Cambios de dependencia de SNI

Microsoft.Data.SqlClient (.NET Core y .NET Standard) en Windows ahora depende de **Microsoft.Data.SqlClient.SNI.runtime**, reemplazando la dependencia anterior en **runtime.native.System.Data.SqlClient.SNI**. La dependencia nueva agrega compatibilidad con la plataforma ARM junto con las plataformas ya admitidas ARM64, x64 y x86 en Windows.

## <a name="release-notes-for-microsoftdatasqlclient-110"></a>Notas de la versión de Microsoft.Data.SqlClient 1.1.0

Las notas de la versión también están disponibles en el repositorio de GitHub: [Notas de la versión 1.1](https://github.com/dotnet/SqlClient/tree/master/release-notes/1.1).

### <a name="new-features"></a>Nuevas características

#### <a name="always-encrypted-with-secure-enclaves"></a>Always Encrypted con enclaves seguros

Always Encrypted está disponible a partir de Microsoft SQL Server 2016. Los enclaves seguros están disponibles a partir de Microsoft SQL Server 2019. Para usar la característica de enclaves, las cadenas de conexión deben incluir el protocolo de atestación y la dirección URL de atestación necesarios. Por ejemplo:

```
Attestation Protocol=HGS;Enclave Attestation Url=<attestation_url_for_HGS>
```

Para más información, consulte:

- [Compatibilidad de SqlClient para Always Encrypted](sql/sqlclient-support-always-encrypted.md)
- [Tutorial: Desarrollo de una aplicación de .NET mediante Always Encrypted con enclaves seguros](sql/tutorial-always-encrypted-enclaves-develop-net-apps.md)

## <a name="release-notes-for-microsoftdatasqlclient-10"></a>Notas de la versión de Microsoft.Data.SqlClient 1.0

La versión inicial del espacio de nombres Microsoft.Data.SqlClient ofrece funcionalidades adicionales del espacio de nombres System.Data.SqlClient existente.
Las notas de la versión también están disponibles en el repositorio de GitHub: [Notas de la versión 1.0](https://github.com/dotnet/SqlClient/tree/master/release-notes/1.0).

### <a name="new-features"></a>Nuevas características

#### <a name="new-features-over-net-framework-472-systemdatasqlclient"></a>Nuevas características de System.Data.SqlClient en .NET Framework 4.7.2

- **Clasificación de datos**: disponible en Azure SQL Database y Microsoft SQL Server 2019.

- **Compatibilidad con UTF-8**: disponible en Microsoft SQL Server 2019.

#### <a name="new-features-over-net-core-22-systemdatasqlclient"></a>Nuevas características de System.Data.SqlClient en .NET Core 2.2

- **Clasificación de datos**: disponible en Azure SQL Database y Microsoft SQL Server 2019.

- **Compatibilidad con UTF-8**: disponible en Microsoft SQL Server 2019.

- **Autenticación**: modo de autenticación de contraseña de Active Directory.

### <a name="data-classification"></a>Clasificación de datos

La clasificación de datos proporciona un nuevo conjunto de API que exponen información de clasificación y confidencialidad de los datos de solo lectura de los objetos recuperados a través de SqlDataReader cuando el origen subyacente admite la característica y contiene metadatos de [confidencialidad y clasificación de datos](../../relational-databases/security/sql-data-discovery-and-classification.md). Vea la aplicación de ejemplo en [Detección y clasificación de datos en SqlClient](https://github.com/dotnet/SqlClient/tree/master/release-notes/1.1).

```csharp
public class SqlDataReader
{
    public Microsoft.Data.SqlClient.DataClassification.SensitivityClassification SensitivityClassification
}

namespace Microsoft.Data.SqlClient.DataClassification
{
    public class ColumnSensitivity
    {
        public System.Collections.ObjectModel.ReadOnlyCollection<Microsoft.Data.SqlClient.DataClassification.SensitivityProperty> SensitivityProperties
    }
    public class InformationType
    {
        public string Id
        public string Name
    }
    public class Label
    {
        public string Id
        public string Name
    }
    public class SensitivityClassification
    {
        public System.Collections.ObjectModel.ReadOnlyCollection<Microsoft.Data.SqlClient.DataClassification.ColumnSensitivity> ColumnSensitivities
        public System.Collections.ObjectModel.ReadOnlyCollection<Microsoft.Data.SqlClient.DataClassification.InformationType> InformationTypes
        public System.Collections.ObjectModel.ReadOnlyCollection<Microsoft.Data.SqlClient.DataClassification.Label> Labels
    }
    public class SensitivityProperty
    {
        public Microsoft.Data.SqlClient.DataClassification.InformationType InformationType
        public Microsoft.Data.SqlClient.DataClassification.Label Label
    }
}
```

### <a name="utf-8-support"></a>Compatibilidad con UTF-8

La compatibilidad con UTF-8 no requiere hacer ningún cambio en el código de la aplicación. Estos cambios de SqlClient optimizan la comunicación entre el cliente y el servidor cuando el servidor admite UTF-8 y la intercalación de columna subyacente es UTF-8. Consulte la sección UTF-8 en [Novedades de SQL Server 2019](../../sql-server/what-s-new-in-sql-server-ver15.md).

### <a name="always-encrypted-with-enclaves"></a>Always Encrypted con enclaves seguros

En general, la documentación existente que usa System.Data.SqlClient en .NET Framework **y los proveedores de almacenamiento de claves maestras de columna integradas** ahora deben trabajar también con .NET Core.

 [Desarrollar con Always Encrypted con el proveedor de datos .NET Framework](../../relational-databases/security/encryption/develop-using-always-encrypted-with-net-framework-data-provider.md)

 [Always Encrypted: Protección de datos confidenciales y almacenamiento de claves de cifrado en el almacén de certificados de Windows](https://docs.microsoft.com/azure/sql-database/sql-database-always-encrypted)

### <a name="authentication"></a>Authentication

Se pueden especificar diferentes modos de autenticación mediante la opción de cadena de conexión _Autenticación_. Para obtener más información, consulte la [documentación de SqlAuthenticationMethod](https://docs.microsoft.com/dotnet/api/system.data.sqlclient.sqlauthenticationmethod?view=netframework-4.7.2).

> [!NOTE]
> Los proveedores de almacén de claves personalizados, como el proveedor de Azure Key Vault, deberán actualizarse para admitir Microsoft.Data.SqlClient. Del mismo modo, también será necesario actualizar los proveedores de enclaves para que sean compatibles con Microsoft.Data.SqlClient.
> Always Encrypted solo se admite en los destinos de .NET Framework y .NET Core. No se admite con .NET Standard ya que en .NET Standard faltan algunas dependencias de cifrado.
