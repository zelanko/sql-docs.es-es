---
title: Introducción al espacio de nombres Microsoft.Data.SqlClient
description: Página de introducción al espacio de nombres Microsoft.Data.SqlClient.
ms.date: 09/30/2019
ms.assetid: c18b1fb1-2af1-4de7-80a4-95e56fd976cb
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: e64a4b04e5059ebc4acbd8e673746fc3953fbb03
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "75251002"
---
# <a name="introduction-to-microsoftdatasqlclient-namespace"></a>Introducción al espacio de nombres Microsoft.Data.SqlClient

![Download-DownArrow-Circled](../../ssdt/media/download.png)[Descargar ADO.NET](../sql-connection-libraries.md#anchor-20-drivers-relational-access)

## <a name="release-notes-for-microsoftdatasqlclient-110"></a>Notas de la versión de Microsoft.Data.SqlClient 1.1.0

Las notas de la versión también están disponibles en el repositorio de GitHub: [Notas de la versión 1.1](https://github.com/dotnet/SqlClient/tree/master/release-notes/1.1).

### <a name="new-features"></a>Nuevas características

#### <a name="always-encrypted-with-secure-enclaves"></a>Always Encrypted con enclaves seguros

Always Encrypted está disponible a partir de Microsoft SQL Server 2016. Los enclaves seguros están disponibles a partir de Microsoft SQL Server 2019. Para usar la característica de enclaves, las cadenas de conexión deben incluir el protocolo de atestación y la dirección URL de atestación necesarios. Ejemplos:

```
Attestation Protocol=HGS;Enclave Attestation Url=<attestation_url_for_HGS>
```

Para obtener información, consulte:

- [Compatibilidad de SqlClient con Always Encrypted](sql/sqlclient-support-always-encrypted.md)
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

La clasificación de datos proporciona un nuevo conjunto de API que exponen información de clasificación y confidencialidad de los datos de solo lectura de los objetos recuperados a través de SqlDataReader cuando el origen subyacente admite la característica y contiene metadatos de [confidencialidad y clasificación de datos](../../relational-databases/security/sql-data-discovery-and-classification.md).

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

La compatibilidad con UTF-8 no requiere hacer ningún cambio en el código de la aplicación. Estos cambios de SqlClient simplemente optimizan la comunicación entre el cliente y el servidor cuando el servidor admite UTF-8 y la intercalación de columna subyacente es UTF-8. Vea la sección UTF-8 en [Novedades de SQL Server 2019 (15.x)](../../sql-server/what-s-new-in-sql-server-ver15.md).

### <a name="always-encrypted-with-enclaves"></a>Always Encrypted con enclaves seguros

En general, la documentación que usa System.Data.SqlClient en .NET Framework **y los proveedores de almacenamiento de claves maestras de columna integradas** ahora deben funcionar también con .NET Core.

 [Desarrollar con Always Encrypted con el proveedor de datos .NET Framework](../../relational-databases/security/encryption/develop-using-always-encrypted-with-net-framework-data-provider.md)

 [Always Encrypted: Protección de datos confidenciales y almacenamiento de claves de cifrado en el almacén de certificados de Windows](https://docs.microsoft.com/azure/sql-database/sql-database-always-encrypted)

### <a name="authentication"></a>Authentication

Se pueden especificar diferentes modos de autenticación mediante la opción de cadena de conexión _Autenticación_. Para obtener más información, consulte la [documentación de SqlAuthenticationMethod](https://docs.microsoft.com/dotnet/api/system.data.sqlclient.sqlauthenticationmethod?view=netframework-4.7.2).

> [!NOTE]
> Los proveedores de almacén de claves personalizados, como el proveedor de Azure Key Vault, deberán actualizarse para admitir Microsoft.Data.SqlClient. Del mismo modo, también será necesario actualizar los proveedores de enclaves para que sean compatibles con Microsoft.Data.SqlClient.
> Always Encrypted solo se admite en los destinos de .NET Framework y .NET Core. No se admite con .NET Standard ya que en .NET Standard faltan algunas dependencias de cifrado.
