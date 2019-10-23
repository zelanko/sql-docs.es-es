---
title: Introducción al espacio de nombres Microsoft.Data.SqlClient
description: Página de introducción del espacio de nombres Microsoft. Data. SqlClient.
ms.date: 09/30/2019
ms.assetid: c18b1fb1-2af1-4de7-80a4-95e56fd976cb
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 4f4034c557c13054dcfb6ed425ca996b0c5363f6
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452383"
---
# <a name="introduction-to-microsoftdatasqlclient-namespace"></a>Introducción al espacio de nombres Microsoft.Data.SqlClient

![Download-DownArrow-Circled](../../ssdt/media/download.png)[Descargar ADO.NET](../sql-connection-libraries.md#anchor-20-drivers-relational-access)

En esta página se describe cómo el espacio de nombres Microsoft. Data. SqlClient ofrece funcionalidad adicional sobre el espacio de nombres System. Data. SqlClient existente.
  
## <a name="release-notes"></a>Notas de la versión
Todas las notas de la versión están disponibles en el [repositorio de github](https://github.com/dotnet/SqlClient/tree/master/release-notes).

## <a name="new-features"></a>Nuevas características

### <a name="new-features-over-net-framework-472-systemdatasqlclient"></a>Nuevas características sobre .NET Framework 4.7.2 System. Data. SqlClient

Clasificación de datos: disponible en Azure SQL Database y Microsoft SQL Server 2019 desde CTP 2,0.

Compatibilidad con UTF-8: disponible en Microsoft SQL Server SQL Server 2019 desde CTP 2,3.

### <a name="new-features-over-net-core-22-systemdatasqlclient"></a>Nuevas características de .NET Core 2,2 System. Data. SqlClient

Clasificación de datos: disponible en Azure SQL Database y Microsoft SQL Server 2019 desde CTP 2,0.

Compatibilidad con UTF-8: disponible en Microsoft SQL Server SQL Server 2019 desde CTP 2,3.

Always Encrypted con enclaves-Always Encrypted está disponible en Microsoft SQL Server 2016 y versiones posteriores. La compatibilidad con enclave se presentó en Microsoft SQL Server 2019 CTP 2,0.

Autenticación: Active Directory modo de autenticación de contraseña.

### <a name="data-classification"></a>Clasificación de datos

La clasificación de datos proporciona un nuevo conjunto de API que exponen información de clasificación y confidencialidad de datos de solo lectura sobre los objetos recuperados a través de SqlDataReader cuando el origen subyacente admite la característica y contiene metadatos sobre la [confidencialidad de los datos. clasificación](../../relational-databases/security/sql-data-discovery-and-classification.md).

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

La compatibilidad con UTF-8 no requiere ningún cambio en el código de la aplicación. Estos cambios de SqlClient simplemente optimizan la comunicación entre el cliente y el servidor cuando el servidor admite UTF-8 y la intercalación de columna subyacente es UTF-8. Vea la sección UTF-8 en [what's New in SQL Server 2019 Preview](../../sql-server/what-s-new-in-sql-server-ver15.md).

### <a name="always-encrypted-with-enclaves"></a>Always Encrypted con enclaves

En general, la documentación existente que usa System. Data. SqlClient en .NET Framework **y los proveedores de almacén de claves maestras de columna integradas** ahora deben funcionar también con .net Core.

 [Desarrollar con Always Encrypted con el proveedor de datos .NET Framework](../../relational-databases/security/encryption/develop-using-always-encrypted-with-net-framework-data-provider.md)

 [Always Encrypted: protección de datos confidenciales y almacenamiento de claves de cifrado en el almacén de certificados de Windows](https://docs.microsoft.com/azure/sql-database/sql-database-always-encrypted)

### <a name="authentication"></a>Autenticación

Se pueden especificar diferentes modos de autenticación mediante la opción de cadena de conexión _autenticación_ . Para obtener más información, consulte la [documentación de SqlAuthenticationMethod](https://docs.microsoft.com/dotnet/api/system.data.sqlclient.sqlauthenticationmethod?view=netframework-4.7.2).

> [!NOTE]
> Los proveedores de almacén de claves personalizados, como el proveedor de Azure Key Vault, deberán actualizarse para admitir Microsoft. Data. SqlClient. Del mismo modo, también será necesario actualizar los proveedores de enclave para que sean compatibles con Microsoft. Data. SqlClient.
> Always Encrypted solo se admite en los destinos de .NET Framework y .NET Core. No se admite con .NET Standard ya que en .NET Standard faltan algunas dependencias de cifrado.
