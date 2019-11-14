---
title: Ejecutar Data Migration Assistant desde la línea de comandos
description: Obtenga información acerca de cómo ejecutar Data Migration Assistant desde la línea de comandos para evaluar las bases de datos de SQL Server para la migración.
ms.custom: seo-lt-2019
ms.date: 05/06/2019
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
ms.openlocfilehash: 3fbf2429a384ad64b1b416e3920a193d92a6c387
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056626"
---
# <a name="run-data-migration-assistant-from-the-command-line"></a>Ejecutar Data Migration Assistant desde la línea de comandos

Con la versión 2,1 y posteriores, al instalar Data Migration Assistant, también se instalará dmacmd. exe en *% ProgramFiles%\\Microsoft Data Migration Assistant\\* . Use dmacmd. exe para evaluar las bases de datos en modo desatendido y generar el resultado en un archivo JSON o CSV. Este método es especialmente útil al evaluar varias bases de datos o bases de datos de gran tamaño. 

> [!NOTE]
> Dmacmd. exe solo admite la ejecución de evaluaciones. En este momento no se admiten las migraciones.

## <a name="assessments-using-the-command-line-interface-cli"></a>Evaluaciones mediante la interfaz de la línea de comandos (CLI)

```
DmaCmd.exe /AssessmentName="string"
/AssessmentDatabases="connectionString1" \["connectionString2"\]
\[/AssessmentSourcePlatform="SourcePlatform"]
\[/AssessmentTargetPlatform="TargetPlatform"\]
/AssessmentEvaluateRecommendations|/AssessmentEvaluateCompatibilityIssues
\[/AssessmentOverwriteResult\]
/AssessmentResultJson="file"|/AssessmentResultCsv="file"
```

|Argumento  |Descripción  | Requerido (s/N)
|---------|---------|---------------|
| `/help or /?`     | Cómo usar el texto de ayuda de dmacmd. exe        | N
|`/AssessmentName`     |   Nombre del proyecto de evaluación   | S
|`/AssessmentDatabases`     | Lista delimitada por espacios de cadenas de conexión. El nombre de la base de datos (catálogo inicial) distingue mayúsculas de minúsculas. | S
|`/AssessmentSourcePlatform`     | Plataforma de origen para la evaluación: <br>Valores admitidos para la evaluación: SqlOnPrem, RdsSqlServer (valor predeterminado) <br>Valores admitidos para la evaluación de preparación de destino: SqlOnPrem, RdsSqlServer (valor predeterminado), Cassandra (versión preliminar)   | N
|`/AssessmentTargetPlatform`     | Plataforma de destino para la evaluación:  <br> Valores admitidos para la evaluación: AzureSqlDatabase, ManagedSqlServer, SqlServer2012, SqlServer2014, SqlServer2016, SqlServerLinux2017 y SqlServerWindows2017 (valor predeterminado)  <br> Valores admitidos para la evaluación de preparación de destino: ManagedSqlServer (valor predeterminado), CosmosDB (versión preliminar)   | N
|`/AssessmentEvaluateFeatureParity`  | Ejecutar reglas de paridad de características. Si la plataforma de origen es RdsSqlServer, la evaluación de la paridad de características no se admite para la plataforma de destino AzureSqlDatabase  | N
|`/AssessmentEvaluateCompatibilityIssues`     | Ejecutar reglas de compatibilidad  | S <br> (Se requiere AssessmentEvaluateCompatibilityIssues o AssessmentEvaluateRecommendations).
|`/AssessmentEvaluateRecommendations`     | Ejecutar recomendaciones de características        | S <br> (Se requiere AssessmentEvaluateCompatibilityIssues o AssessmentEvaluateRecommendations)
|`/AssessmentOverwriteResult`     | Sobrescribir el archivo de resultados    | N
|`/AssessmentResultJson`     | Ruta de acceso completa al archivo de resultados JSON     | S <br> (Se requiere AssessmentResultJson o AssessmentResultCsv)
|`/AssessmentResultCsv`    | Ruta de acceso completa al archivo de resultados CSV   | S <br> (Se requiere AssessmentResultJson o AssessmentResultCsv)
|`/Action`    | Use SkuRecommendation para obtener recomendaciones de SKU y use AssessTargetReadiness para realizar una evaluación de la preparación de destino.   | N
|`/SourceConnections`    | Lista delimitada por espacios de cadenas de conexión. El nombre de la base de datos (catálogo inicial) es opcional. Si no se proporciona ningún nombre de base de datos, se evalúan todas las bases de datos del origen.   | S <br> (Obligatorio si la acción es ' AssessTargetReadiness ')
|`/TargetReadinessConfiguration`    | Ruta de acceso completa al archivo XML que describe los valores para el nombre, las conexiones de origen y el archivo de resultados.   | S <br> (Se requiere TargetReadinessConfiguration o SourceConnections)
|`/FeatureDiscoveryReportJson`    | Ruta de acceso al informe JSON de detección de características. Si se genera este archivo, se puede usar para volver a ejecutar la evaluación de preparación de destino sin conectarse al origen. | N
|`/ImportFeatureDiscoveryReportJson`    | Ruta de acceso al informe JSON de detección de características creado anteriormente. En lugar de las conexiones de origen, se usará este archivo.   | N

## <a name="examples-of-assessments-using-the-cli"></a>Ejemplos de evaluaciones mediante la CLI

**Dmacmd.exe**

  `Dmacmd.exe /? or DmaCmd.exe /help`

**Evaluación de una sola base de datos mediante la autenticación de Windows y reglas de compatibilidad en ejecución**

```
DmaCmd.exe /AssessmentName="TestAssessment"
/AssessmentDatabases="Server=SQLServerInstanceName;Initial
Catalog=DatabaseName;Integrated Security=true"
/AssessmentEvaluateCompatibilityIssues /AssessmentOverwriteResult
/AssessmentResultJson="C:\\temp\\Results\\AssessmentReport.json"
```

**Evaluación de una sola base de datos mediante la autenticación de SQL Server y la recomendación de características en ejecución**

```
DmaCmd.exe /AssessmentName="TestAssessment"
/AssessmentDatabases="Server=SQLServerInstanceName;Initial
Catalog=DatabaseName;User Id=myUsername;Password=myPassword;"
/AssessmentEvaluateRecommendations /AssessmentOverwriteResult
/AssessmentResultCsv="C:\\temp\\Results\\AssessmentReport.csv"
```

**Evaluación de una sola base de datos para la plataforma de destino SQL Server 2012, guardar los resultados en un archivo. JSON y. csv**

```
DmaCmd.exe /AssessmentName="TestAssessment"
/AssessmentDatabases="Server=SQLServerInstanceName;Initial
Catalog=DatabaseName;Integrated Security=true"
/AssessmentTargetPlatform="SqlServer2012"
/AssessmentEvaluateRecommendations /AssessmentOverwriteResult
/AssessmentResultJson="C:\\temp\\Results\\AssessmentReport.json"
/AssessmentResultCsv="C:\\temp\\Results\\AssessmentReport.csv"
```

**Evaluación de base de datos única para la plataforma de destino SQL Azure base de datos, guardar los resultados en un archivo. JSON y. csv**

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

**Evaluación de preparación de destino de una sola base de datos mediante la autenticación de Windows**

```
DmaCmd.exe /Action=AssessTargetReadiness 
/AssessmentName="TestAssessment" 
/SourceConnections="Server=SQLServerInstanceName;Initial Catalog=DatabaseName;Integrated Security=true" 
/AssessmentOverwriteResult 
/AssessmentResultJson="C:\temp\Results\AssessmentReport.json"
```

**Evaluación de preparación de destino de una sola base de datos mediante la autenticación de SQL Server**

```
DmaCmd.exe /Action=AssessTargetReadiness 
/AssessmentName="TestAssessment" 
/SourceConnections="Server=SQLServerInstanceName;Initial Catalog=DatabaseName;User Id=myUsername;Password=myPassword;" /AssessmentEvaluateRecommendations 
/AssessmentOverwriteResult 
/AssessmentResultJson="C:\temp\Results\AssessmentReport.json" 

```

**Evaluación de base de datos única para la plataforma de destino SQL Azure base de datos, guardar los resultados en un archivo. JSON y. csv**

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

**Evaluación de preparación de destino de varias bases de datos**

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

**Evaluación de la preparación para todas las bases de datos de un servidor mediante la autenticación de Windows**

```
DmaCmd.exe /Action=AssessTargetReadiness
/AssessmentName="TestAssessment"
/SourceConnections="Server=SQLServerInstanceName;Integrated Security=true"
/AssessmentOverwriteResult
/AssessmentResultJson="C:\temp\Results\AssessmentReport.json"

```

**Evaluación de la preparación de destino mediante la importación del informe de detección de características creado anteriormente**

```
DmaCmd.exe /Action=AssessTargetReadiness
/AssessmentName="TestAssessment"
/ImportFeatureDiscoveryReportJson="c:\temp\feature_report.json" 
/AssessmentOverwriteResult
/AssessmentResultJson="C:\temp\Results\AssessmentReport.json"

```

**Evaluación de la preparación de destino mediante el archivo de configuración**

```
DmaCmd.exe /Action=AssessTargetReadiness 
/TargetReadinessConfiguration=.\Config.xml
```

Contenido del archivo de configuración cuando se usan conexiones de origen:

```
<?xml version="1.0" encoding="utf-8" ?>
<TargetReadinessConfiguration xmlns="https://microsoft.com/schemas/SqlServer/Advisor/TargetReadinessConfiguration">
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
<TargetReadinessConfiguration xmlns="https://microsoft.com/schemas/SqlServer/Advisor/TargetReadinessConfiguration">
  <AssessmentName>name</AssessmentName>
  <ImportFeatureDiscoveryReportJson>path\to\featurediscoveryfile.json</ImportFeatureDiscoveryReportJson>
  <AssessmentResultJson>path\to\resultfile.json</AssessmentResultJson>
  <OverwriteResult>true</OverwriteResult><!-- or false -->
</TargetReadinessConfiguration>
```

## <a name="azure-sql-databasemanaged-instance-sku-recommendations-using-the-cli"></a>Recomendaciones de SKU de instancia administrada y Azure SQL Database mediante la CLI

Estos comandos admiten recomendaciones para Azure SQL Database opciones de implementación de base de datos única y de instancia administrada.

```
.\DmaCmd.exe /Action=SkuRecommendation
/SkuRecommendationInputDataFilePath="C:\TestOut\out.csv"
/SkuRecommendationTsvOutputResultsFilePath="C:\TestOut\prices.tsv"
/SkuRecommendationJsonOutputResultsFilePath="C:\TestOut\prices.json"
/SkuRecommendationOutputResultsFilePath="C:\TestOut\prices.html"
/SkuRecommendationPreventPriceRefresh=true 
```

|Argumento  |Descripción  | Requerido (s/N)
|---------|---------|---------------|
|`/Action=SkuRecommendation` | Ejecutar evaluación de SKU mediante la línea de comandos DMA | S
|`/SkuRecommendationInputDataFilePath` | Ruta de acceso completa al archivo de contador de rendimiento recopilado del equipo que hospeda las bases de datos | S
|`/SkuRecommendationTsvOutputResultsFilePath` | Ruta de acceso completa al archivo de resultados TSV | S <br> (Requiere TSV o JSON o la ruta de acceso del archivo HTML)
|`/SkuRecommendationJsonOutputResultsFilePath` | Ruta de acceso completa al archivo de resultados JSON | S <br> (Requiere TSV o JSON o la ruta de acceso del archivo HTML)
|`/SkuRecommendationHtmlResultsFilePath` | Ruta de acceso completa al archivo de resultados HTML | S <br> (Requiere TSV o JSON o la ruta de acceso del archivo HTML)
|`/SkuRecommendationPreventPriceRefresh` | Impide que se produzca la actualización del precio. Use si se ejecuta en modo sin conexión (por ejemplo, true). | S <br> (Seleccione este argumento para precios estáticos o se deben seleccionar todos los argumentos siguientes para obtener los precios más recientes).
|`/SkuRecommendationCurrencyCode` | Moneda en la que se van a mostrar los precios (por ejemplo, "USD") | S <br> (Para los precios más recientes)
|`/SkuRecommendationOfferName` | El nombre de la oferta (por ejemplo, "MS-AZR-0003P"). Para obtener más información, consulte la página Detalles de la [oferta de Microsoft Azure](https://azure.microsoft.com/support/legal/offer-details/) . | S <br> (Para los precios más recientes)
|`/SkuRecommendationRegionName` | El nombre de la región (por ejemplo, "Westus") | S <br> (Para los precios más recientes)
|`/SkuRecommendationSubscriptionId` | Identificador de la suscripción. | S <br> (Para los precios más recientes)
|`/SkuRecommendationDatabasesToRecommend` | Lista separada por espacios de las bases de datos que se van a recomendar para (por ejemplo, "Database1" "Database2" "Database3"). Los nombres distinguen mayúsculas de minúsculas y deben ir entre comillas dobles. Si se omite, se proporcionan recomendaciones para todas las bases de datos. | N
|`/AzureAuthenticationTenantId` | El inquilino de autenticación. | S <br> (Para los precios más recientes)
|`/AzureAuthenticationClientId` | IDENTIFICADOR de cliente de la aplicación de AAD que se usa para la autenticación. | S <br> (Para los precios más recientes)
|`/AzureAuthenticationInteractiveAuthentication` | Establézcalo en true para mostrar la ventana. | S <br> (Para los precios más recientes) <br>(Seleccione una de las tres opciones de autenticación: opción 1)
|`/AzureAuthenticationCertificateStoreLocation` | Establezca en la ubicación del almacén de certificados (por ejemplo, "CurrentUser"). | S <br>(Para los precios más recientes) <br> (Seleccione una de las tres opciones de autenticación: opción 2)
|`/AzureAuthenticationCertificateThumbprint` | Establezca en la huella digital del certificado. | S <br> (Para los precios más recientes) <br>(Seleccione una de las tres opciones de autenticación: opción 2)
|`/AzureAuthenticationToken` | Establezca en el token de certificado. | S <br> (Para los precios más recientes) <br>(Seleccione una de las tres opciones de autenticación: opción 3)

## <a name="examples-of-sku-assessments-using-the-cli"></a>Ejemplos de evaluaciones de SKU mediante la CLI

**Dmacmd.exe**

`Dmacmd.exe /? or DmaCmd.exe /help`

**Azure SQL DB/recomendación de SKU de MI con actualización de precios (obtener los precios más recientes)-autenticación interactiva** 

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

**Azure SQL DB/recomendación de SKU de MI con actualización de precios (obtener los precios más recientes)-autenticación de certificados**

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

**Recomendación de Azure SQL DB SKU/MI con actualización de precios (obtener los precios más recientes)-autenticación de tokens y especificar las bases de datos que se recomiendan**
  
```
.\DmaCmd.exe /Action=SkuRecommendation
/SkuRecommendationInputDataFilePath="C:\TestOut\out.csv"
/SkuRecommendationTsvOutputResultsFilePath="C:\TestOut\prices.tsv"
/SkuRecommendationJsonOutputResultsFilePath="C:\TestOut\prices.json"
/SkuRecommendationOutputResultsFilePath="C:\TestOut\prices.html"
/SkuRecommendationCurrencyCode=USD
/SkuRecommendationOfferName=MS-AZR-0044p
/SkuRecommendationRegionName=UKWest
/SkuRecommendationDatabasesToRecommend=“TPCDS1G,EDW_3G,TPCDS10G”
/SkuRecommendationSubscriptionId=<Your Subscription Id>
/AzureAuthenticationClientId=<Your AzureAuthenticationClientId>
/AzureAuthenticationTenantId=<Your AzureAuthenticationTenantId>
/AzureAuthenticationToken=<Your Authentication Token> 
```

**Azure SQL DB/recomendación de SKU de MI sin actualización de precios (usar precios estáticos)** 
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
- En el artículo se [identifican los Azure SQL Database SKU correctos para la base de datos local](https://aka.ms/dma-sku-recommend-sqldb).
