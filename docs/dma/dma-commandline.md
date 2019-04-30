---
title: Ejecutar Data Migration Assistant desde la línea de comandos (SQL Server) | Microsoft Docs
description: Obtenga información sobre cómo ejecutar Data Migration Assistant desde la línea de comandos para evaluar las bases de datos de SQL Server para la migración
ms.custom: ''
ms.date: 03/12/2019
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Command Line
ms.assetid: ''
author: HJToland3
ms.author: rajpo
manager: craigg
ms.openlocfilehash: ec274af1b3674cb821f0f5a477d1f798c404000e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63154676"
---
# <a name="run-data-migration-assistant-from-the-command-line"></a>Ejecutar Data Migration Assistant desde la línea de comandos
Con la versión 2.1 y anteriores, cuando instale Data Migration Assistant, también instalará dmacmd.exe en *% ProgramFiles %\\Microsoft Data Migration Assistant\\*. Usar dmacmd.exe para evaluar las bases de datos en modo desatendido y generar el resultado al archivo JSON o CSV. Este método es especialmente útil al evaluar varias bases de datos o bases de datos enormes. 

> [!NOTE]
> Dmacmd.exe admite solo las evaluaciones de ejecución. No se admiten las migraciones en este momento.


## <a name="assessments-using-the-command-line-interface-cli"></a>Evaluaciones mediante la interfaz de línea de comandos (CLI)

```
DmaCmd.exe /AssessmentName="string"
/AssessmentDatabases="connectionString1" \["connectionString2"\]
\[/AssessmentSourcePlatform="SourcePlatform"]
\[/AssessmentTargetPlatform="TargetPlatform"\]
/AssessmentEvaluateRecommendations|/AssessmentEvaluateCompatibilityIssues
\[/AssessmentOverwriteResult\]
/AssessmentResultJson="file"|/AssessmentResultCsv="file"
```

|Argumento  |Descripción  | Necesario (S/N)
|---------|---------|---------------|
| `/help or /?`     | Cómo usar el texto de ayuda dmacmd.exe        | N
|`/AssessmentName`     |   Nombre del proyecto de evaluación   | S
|`/AssessmentDatabases`     | Lista delimitada por espacios de las cadenas de conexión. Nombre de base de datos (catálogo inicial) distingue mayúsculas de minúsculas. | S
|`/AssessmentSourcePlatform`     | Plataforma de origen para la evaluación: <br>Valores admitidos para la evaluación: SqlOnPrem, RdsSqlServer (default) <br>Valores admitidos para la evaluación de disponibilidad de destino: SqlOnPrem, RdsSqlServer (valor predeterminado), Cassandra (versión preliminar)   | N
|`/AssessmentTargetPlatform`     | Plataforma de destino para la evaluación:  <br> Valores admitidos para la evaluación: AzureSqlDatabase, ManagedSqlServer, SqlServer2012, SqlServer2014, SqlServer2016, SqlServerLinux2017 y SqlServerWindows2017 (valor predeterminado)  <br> Valores admitidos para la evaluación de disponibilidad de destino: ManagedSqlServer (valor predeterminado), COSMOS DB (versión preliminar)   | N
|`/AssessmentEvaluateFeatureParity`  | Ejecutar reglas de paridad de características. Si la plataforma de origen es RdsSqlServer, no se admite la evaluación de paridad de característica para la plataforma de destino AzureSqlDatabase  | N
|`/AssessmentEvaluateCompatibilityIssues`     | Ejecutar las reglas de compatibilidad  | S <br> (AssessmentEvaluateCompatibilityIssues o AssessmentEvaluateRecommendations es necesario).
|`/AssessmentEvaluateRecommendations`     | Ejecute la recomendación de característica        | S <br> (AssessmentEvaluateCompatibilityIssues o AssessmentEvaluateRecommendationsis necesarios)
|`/AssessmentOverwriteResult`     | Sobrescribir el archivo de resultados    | N
|`/AssessmentResultJson`     | Ruta de acceso completa al archivo de resultados JSON     | S <br> (AssessmentResultJson o AssessmentResultCsv es necesario)
|`/AssessmentResultCsv`    | Ruta de acceso completa al archivo de resultado CSV   | S <br>(AssessmentResultJson o AssessmentResultCsv es necesario)
|`/Action`    | Use SkuRecommendation para obtener recomendaciones de SKU, use AssessTargetReadiness para realizar la evaluación de disponibilidad de destino.   | N
|`/SourceConnections`    | Lista delimitada por espacios de las cadenas de conexión. Nombre de base de datos (catálogo inicial) es opcional. Si se proporciona ningún nombre de base de datos, se evalúan todas las bases de datos en el origen.   | S <br>(Requerido si la acción es 'AssessTargetReadiness')
|`/TargetReadinessConfiguration`    | Ruta de acceso completa al archivo XML que describe los valores para nombre, las conexiones de origen y el archivo de resultados.   | S <br>(TargetReadinessConfiguration o SourceConnections es necesario)
|`/FeatureDiscoveryReportJson`    | Ruta de acceso a la detección de la característica informes JSON. Si se genera este archivo, se puede usar la evaluación de disponibilidad de destino para volver a ejecutar sin necesidad de conectarse al origen.   | N
|`/ImportFeatureDiscoveryReportJson`    | Ruta de acceso para el informe de JSON de detección de función creado anteriormente. En lugar de conexiones de origen, se usará este archivo.   | N

## <a name="examples-of-assessments-using-the-cli"></a>Ejemplos de las evaluaciones mediante la CLI

**Dmacmd.exe**

  `Dmacmd.exe /? or DmaCmd.exe /help`

**Evaluación de bases de datos única mediante reglas de compatibilidad de ejecución y autenticación de Windows**


```
DmaCmd.exe /AssessmentName="TestAssessment"
/AssessmentDatabases="Server=SQLServerInstanceName;Initial
Catalog=DatabaseName;Integrated Security=true"
/AssessmentEvaluateCompatibilityIssues /AssessmentOverwriteResult
/AssessmentResultJson="C:\\temp\\Results\\AssessmentReport.json"
```

**Evaluación de bases de datos única con la recomendación de característica de autenticación y la ejecución de SQL Server**

```
DmaCmd.exe /AssessmentName="TestAssessment"
/AssessmentDatabases="Server=SQLServerInstanceName;Initial
Catalog=DatabaseName;User Id=myUsername;Password=myPassword;"
/AssessmentEvaluateRecommendations /AssessmentOverwriteResult
/AssessmentResultCsv="C:\\temp\\Results\\AssessmentReport.csv"
```

**Evaluación de bases de datos único para la plataforma de destino de SQL Server 2012, guardar los resultados en el archivo .json y. csv**

```
DmaCmd.exe /AssessmentName="TestAssessment"
/AssessmentDatabases="Server=SQLServerInstanceName;Initial
Catalog=DatabaseName;Integrated Security=true"
/AssessmentTargetPlatform="SqlServer2012"
/AssessmentEvaluateRecommendations /AssessmentOverwriteResult
/AssessmentResultJson="C:\\temp\\Results\\AssessmentReport.json"
/AssessmentResultCsv="C:\\temp\\Results\\AssessmentReport.csv"
```

**Evaluación de bases de datos único para la plataforma de destino base de datos de SQL Azure, guardar los resultados en el archivo .json y. csv**

```
DmaCmd.exe /AssessmentName="TestAssessment" 
/AssessmentDatabases="Server=SQLServerInstanceName;Initial
Catalog=DatabaseName;Integrated Security=true"
/AssessmentTargetPlatform="AzureSqlDatabaseV12"
/AssessmentEvaluateCompatibilityIssues /AssessmentEvaluateFeatureParity
/AssessmentOverwriteResult 
/AssessmentResultCsv="C:\\temp\\AssessmentReport.csv" 
/AssessmentResultJson="C:\\temp\\AssessmentReport.json"
```

**Evaluación de varias bases de datos**

```
DmaCmd.exe /AssessmentName="TestAssessment"
/AssessmentDatabases="Server=SQLServerInstanceName1;Initial
Catalog=DatabaseName1;Integrated Security=true"
"Server=SQLServerInstanceName1;Initial Catalog=DatabaseName2;Integrated
Security=true" "Server=SQLServerInstanceName2;Initial
Catalog=DatabaseName3;Integrated Security=true"
/AssessmentTargetPlatform="SqlServer2016"
/AssessmentEvaluateCompatibilityIssues /AssessmentOverwriteResult
/AssessmentResultCsv="C:\\temp\\Results\\AssessmentReport.csv"
/AssessmentResultJson="C:\\Results\\test2016.json"
```

**Evaluación de preparación de destino de base de datos única mediante la autenticación de Windows**

```
DmaCmd.exe /Action=AssessTargetReadiness 
/AssessmentName="TestAssessment" 
/SourceConnections="Server=SQLServerInstanceName;Initial Catalog=DatabaseName;Integrated Security=true" 
/AssessmentOverwriteResult 
/AssessmentResultJson="C:\temp\Results\AssessmentReport.json"
```

**Evaluación de preparación de destino de base de datos única mediante la autenticación de SQL Server**

```
DmaCmd.exe /Action=AssessTargetReadiness 
/AssessmentName="TestAssessment" 
/SourceConnections="Server=SQLServerInstanceName;Initial Catalog=DatabaseName;User Id=myUsername;Password=myPassword;" /AssessmentEvaluateRecommendations 
/AssessmentOverwriteResult 
/AssessmentResultJson="C:\temp\Results\AssessmentReport.json" 

```

**Evaluación de bases de datos único para la plataforma de destino base de datos de SQL Azure, guardar los resultados en el archivo .json y. csv**

```
DmaCmd.exe /AssessmentName="TestAssessment" 
/AssessmentDatabases="Server=SQLServerInstanceName;Initial
Catalog=DatabaseName;Integrated Security=true"
/AssessmentSourcePlatform="SqlOnPrem"
/AssessmentTargetPlatform="AzureSqlDatabase"
/AssessmentEvaluateCompatibilityIssues /AssessmentEvaluateFeatureParity
/AssessmentOverwriteResult 
/AssessmentResultCsv="C:\\temp\\AssessmentReport.csv" 
/AssessmentResultJson="C:\\temp\\AssessmentReport.json"

```

**Evaluación de disponibilidad de destino de varias bases de datos**

```
DmaCmd.exe /Action=AssessTargetReadiness 
/AssessmentName="TestAssessment" 
/AssessmentSourcePlatform=SourcePlatform
/AssessmentTargetPlatform=TargetPlatform
/SourceConnections="Server=SQLServerInstanceName1;Initial Catalog=DatabaseName1;Integrated Security=true" "Server=SQLServerInstanceName1;Initial Catalog=DatabaseName2;Integrated Security=true" "Server=SQLServerInstanceName2;Initial Catalog=DatabaseName3;Integrated Security=true" 
/AssessmentOverwriteResult  
/AssessmentResultJson="C:\Results\test2016.json"

(/AssessmentSourcePlatform and /AssessmentTargetPlatform are optional.)
```

**Evaluación de disponibilidad de destino para todas las bases de datos en un servidor mediante la autenticación de Windows**

```
DmaCmd.exe /Action=AssessTargetReadiness 
/AssessmentName="TestAssessment" 
/SourceConnections="Server=SQLServerInstanceName;Integrated Security=true" 
/AssessmentOverwriteResult 
/AssessmentResultJson="C:\temp\Results\AssessmentReport.json"

```

**Evaluación de disponibilidad de destino mediante la importación de informe de detección de función que creó anteriormente**

```
DmaCmd.exe /Action=AssessTargetReadiness 
/AssessmentName="TestAssessment" 
/ImportFeatureDiscoveryReportJson="c:\temp\feature_report.json" 
/AssessmentOverwriteResult 
/AssessmentResultJson="C:\temp\Results\AssessmentReport.json"

```

**Evaluación de preparación del destino proporcionando el archivo de configuración**

```
DmaCmd.exe /Action=AssessTargetReadiness 
/TargetReadinessConfiguration=.\Config.xml

```
Contenido del archivo de configuración cuando se usan conexiones de origen:
```
<?xml version="1.0" encoding="utf-8" ?>
<TargetReadinessConfiguration xmlns="http://microsoft.com/schemas/SqlServer/Advisor/TargetReadinessConfiguration">
  <AssessmentName>name</AssessmentName>
  <SourcePlatform>Source Platform</SourcePlatform> <!-- Optional. The default is SqlOnPrem -->
  <TargetPlatform>TargetPlatform</TargetPlatform> <!-- Optional. The default is ManagedSqlServer -->
  <SourceConnections>
    <SourceConnection>connection string 1</SourceConnection>
    <SourceConnection>connection string 2</SourceConnection>
    <!-- ... -->
    <SourceConnection>connection string n</SourceConnection>
  </SourceConnections>
  <AssessmentResultJson>path\to\file.json</AssessmentResultJson>
  <FeatureDiscoveryReportJson>path\to\featurediscoveryreport.json</FeatureDiscoveryReportJson>
  <OverwriteResult>true</OverwriteResult> <!-- or false -->
</TargetReadinessConfiguration>
```

Contenido del archivo de configuración al importar el informe de detección de características:
```
<TargetReadinessConfiguration xmlns="http://microsoft.com/schemas/SqlServer/Advisor/TargetReadinessConfiguration">
  <AssessmentName>name</AssessmentName>
  <ImportFeatureDiscoveryReportJson>path\to\featurediscoveryfile.json</ImportFeatureDiscoveryReportJson>
  <AssessmentResultJson>path\to\resultfile.json</AssessmentResultJson>
  <OverwriteResult>true</OverwriteResult><!-- or false -->
</TargetReadinessConfiguration>
```

## <a name="azure-sql-database-sku-recommendations-using-the-cli"></a>Recomendaciones de SKU de la base de datos de SQL Azure mediante la CLI

```
.\DmaCmd.exe /Action=SkuRecommendation
/SkuRecommendationInputDataFilePath="C:\TestOut\out.csv"
/SkuRecommendationTsvOutputResultsFilePath="C:\TestOut\prices.tsv"
/SkuRecommendationJsonOutputResultsFilePath="C:\TestOut\prices.json"
/SkuRecommendationOutputResultsFilePath="C:\TestOut\prices.html"
/SkuRecommendationPreventPriceRefresh=true 
```

|Argumento  |Descripción  | Necesario (S/N)
|---------|---------|---------------|
|`/Action=SkuRecommendation` | Ejecutar la evaluación de SKU con línea de comandos DMA | S
|`/SkuRecommendationInputDataFilePath`  | Ruta de acceso completa al archivo de contador de rendimiento recopilados desde el equipo que hospeda las bases de datos |    S
|`/SkuRecommendationTsvOutputResultsFilePath`   | Ruta de acceso completa al archivo de resultados TSV |    S <br>(La ruta de acceso de archivo TSV o JSON o HTML se requiere)
|`/SkuRecommendationJsonOutputResultsFilePath`  | Ruta de acceso completa al archivo de resultados JSON |   S <br>(La ruta de acceso de archivo TSV o JSON o HTML se requiere)
|`/SkuRecommendationHtmlResultsFilePath` |  Ruta de acceso completa al archivo de resultados HTML | S <br>(La ruta de acceso de archivo TSV o JSON o HTML se requiere)
|`/SkuRecommendationPreventPriceRefresh` |  Impide que la actualización de precios que se producen. Utilizar si está ejecutando en modo sin conexión. |    S <br>(Este argumento está seleccionada para los precios estáticos o todos los argumentos siguientes deben seleccionarse para obtener los precios más recientes)
|`/SkuRecommendationCurrencyCode` | La moneda en que se va a mostrar los precios (p. ej. "USD") | S <br>(Si desea obtener los precios más recientes)
|`/SkuRecommendationOfferName` |    Nombre de la oferta (p. ej. "MS-AZR-0003P"). Para obtener más información, consulte el [detalles de la oferta de Microsoft Azure](https://azure.microsoft.com/support/legal/offer-details/) página. |   S <br>(Si desea obtener los precios más recientes)
|`/SkuRecommendationRegionName` |   Nombre de la región (por ejemplo "WestUS") |   S <br>(Si desea obtener los precios más recientes)
|`/SkuRecommendationSubscriptionId` | Identificador de la suscripción. |    S <br>(Si desea obtener los precios más recientes)
|`/AzureAuthenticationTenantId` | El inquilino de autenticación. |  S <br>(Si desea obtener los precios más recientes)
|`/AzureAuthenticationClientId` | El identificador de cliente de la aplicación AAD que se usa para la autenticación. | S <br>(Si desea obtener los precios más recientes)
|`/AzureAuthenticationInteractiveAuthentication`    | Establézcalo en true para la ventana emergente. |   S <br>(Si desea obtener los precios más recientes) <br>(Elija una de las opciones de 3 autenticación - opción 1)
|`/AzureAuthenticationCertificateStoreLocation` | Establecido en la ubicación del almacén de certificados (p. ej. "CurrentUser"). | S <br>(Si desea obtener los precios más recientes) <br>(Elija una de las opciones de 3 autenticación - opción 2)
|`/AzureAuthenticationCertificateThumbprint`    | Se establece en la huella digital del certificado. | S <br>(Si desea obtener los precios más recientes) <br>(Elija una de las opciones de 3 autenticación - opción 2)
|`/AzureAuthenticationToken` |  Establecer en el token de certificado. | S <br>(Si desea obtener los precios más recientes) <br>(Elija una de las opciones de 3 autenticación - opción 3)

## <a name="examples-of-sku-assessments-using-the-cli"></a>Ejemplos de las evaluaciones de SKU mediante la CLI

**Dmacmd.exe**

  `Dmacmd.exe /? or DmaCmd.exe /help`

**Recomendación de SKU de la base de datos de SQL Azure con la actualización de precio (precios más recientes de get) - autenticación interactiva** 
```
.\DmaCmd.exe /Action=SkuRecommendation
/SkuRecommendationInputDataFilePath="C:\TestOut\out.csv"
/SkuRecommendationTsvOutputResultsFilePath="C:\TestOut\prices.tsv"
/SkuRecommendationJsonOutputResultsFilePath="C:\TestOut\prices.json"
/SkuRecommendationOutputResultsFilePath="C:\TestOut\prices.html"
/SkuRecommendationCurrencyCode=USD
/SkuRecommendationOfferName=MS-AZR-0044p
/SkuRecommendationRegionName=UKWest
/SkuRecommendationSubscriptionId=<Your Subscription Id>
/AzureAuthenticationClientId=<Your AzureAuthenticationClientId>
/AzureAuthenticationTenantId=<Your AzureAuthenticationTenantId>
/AzureAuthenticationInteractiveAuthentication=true 
```

**Recomendación de SKU de la base de datos de SQL Azure con la actualización de precio (precios más recientes de get) - autenticación de certificados**
```
.\DmaCmd.exe /Action=SkuRecommendation
/SkuRecommendationInputDataFilePath="C:\TestOut\out.csv"
/SkuRecommendationTsvOutputResultsFilePath="C:\TestOut\prices.tsv"
/SkuRecommendationJsonOutputResultsFilePath="C:\TestOut\prices.json"
/SkuRecommendationOutputResultsFilePath="C:\TestOut\prices.html"
/SkuRecommendationCurrencyCode=USD
/SkuRecommendationOfferName=MS-AZR-0044p
/SkuRecommendationRegionName=UKWest
/SkuRecommendationSubscriptionId=<Your Subscription Id>
/AzureAuthenticationClientId=<Your AzureAuthenticationClientId>
/AzureAuthenticationTenantId=<Your AzureAuthenticationTenantId>
/AzureAuthenticationCertificateStoreLocation=<Your Certificate Store Location>
/AzureAuthenticationCertificateThumbprint=<Your Certificate Thumbprint>  
```

**Símbolo (token) de la recomendación de SKU de la base de datos de SQL Azure con la actualización de precio (precios más recientes de get) - autenticación**  
```
.\DmaCmd.exe /Action=SkuRecommendation
/SkuRecommendationInputDataFilePath="C:\TestOut\out.csv"
/SkuRecommendationTsvOutputResultsFilePath="C:\TestOut\prices.tsv"
/SkuRecommendationJsonOutputResultsFilePath="C:\TestOut\prices.json"
/SkuRecommendationOutputResultsFilePath="C:\TestOut\prices.html"
/SkuRecommendationCurrencyCode=USD
/SkuRecommendationOfferName=MS-AZR-0044p
/SkuRecommendationRegionName=UKWest
/SkuRecommendationSubscriptionId=<Your Subscription Id>
/AzureAuthenticationClientId=<Your AzureAuthenticationClientId>
/AzureAuthenticationTenantId=<Your AzureAuthenticationTenantId>
/AzureAuthenticationToken=<Your Authentication Token> 
```

**Recomendación de SKU de la base de datos de SQL Azure sin realizar ninguna actualización de precio (precios de uso estático)** 
```
.\DmaCmd.exe /Action=SkuRecommendation
/SkuRecommendationInputDataFilePath="C:\TestOut\out.csv"
/SkuRecommendationTsvOutputResultsFilePath="C:\TestOut\prices.tsv"
/SkuRecommendationJsonOutputResultsFilePath="C:\TestOut\prices.json"
/SkuRecommendationOutputResultsFilePath="C:\TestOut\prices.html"
/SkuRecommendationPreventPriceRefresh=true  
```

## <a name="see-also"></a>Vea también
- [Data Migration Assistant](https://aka.ms/get-dma) descargar.
- El artículo [identificar la SKU de base de datos SQL de Azure adecuada para la base de datos local](https://aka.ms/dma-sku-recommend-sqldb).
