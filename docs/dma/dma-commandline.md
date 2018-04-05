---
title: Ejecutar desde la línea de comandos (SQL Server datos Migration Assistant) | Documentos de Microsoft
ms.custom: ''
ms.date: 09/01/2017
ms.prod: sql-non-specified
ms.prod_service: dma
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-dma
ms.tgt_pltfrm: ''
ms.topic: article
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Command Line
ms.assetid: ''
caps.latest.revision: ''
author: HJToland3
ms.author: jtoland
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6147d01802a363082baf27d6b909e2c98f9afef2
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="run-data-migration-assistant-from-the-command-line"></a>Ejecutar el Asistente de migración de datos desde la línea de comandos
Con la versión 2.1 y versiones posteriores, cuando instale el Asistente de migración de datos, también se instalará dmacmd.exe en *% ProgramFiles %\\el Asistente para la migración de datos de Microsoft\\*. Use dmacmd.exe para evaluar las bases de datos en modo desatendido y generar el resultado al archivo JSON o CSV. Esto es especialmente útil al evaluar varias bases de datos o bases de datos muy grandes. 

> [!NOTE]
> Dmacmd.exe admite solo las evaluaciones de ejecución. No se admiten migraciones en este momento.


## <a name="command-line-arguments"></a>Argumentos de línea de comandos

```
DmaCmd.exe /AssessmentName="string"
/AssessmentDatabases="connectionString1" \["connectionString2"\]
\[/AssessmentTargetPlatform="TargetPlatform"\]
/AssessmentEvaluateRecommendations|/AssessmentEvaluateCompatibilityIssues
\[/AssessmentOverwriteResult\]
/AssessmentResultJson="file"|/AssessmentResultCsv="file"
```


|Argumento  |Description  | Necesaria (Y/N)
|---------|---------|---------------|
| `/help or /?`     | Cómo usar el texto de ayuda dmacmd.exe        | N
|`/AssessmentName`     |   Nombre del proyecto de evaluación   | S
|`/AssessmentDatabases`     | Lista delimitada por espacios de cadenas de conexión. Nombre de base de datos (catálogo inicial) distingue mayúsculas de minúsculas. | S
|`/AssessmentTargetPlatform`     | Plataforma de destino para la evaluación, con los valores admitidos: SqlServer2012, SqlServer2014, SqlServer2016 y AzureSqlDatabaseV12. Valor predeterminado es SqlServer2016   | N
|`/AssessmentEvaluateFeatureParity`  | Ejecutar reglas de paridad de características  | N
|`/AssessmentEvaluateCompatibilityIssues`     | Ejecutar las reglas de compatibilidad  | S <br> (AssessmentEvaluateCompatibilityIssues o AssessmentEvaluateRecommendations es necesario).
|`/AssessmentEvaluateRecommendations`     | Ejecutar las recomendaciones de característica        | S <br> (AssessmentEvaluateCompatibilityIssues o AssessmentEvaluateRecommendationsis necesario)
|`/AssessmentOverwriteResult`     | Sobrescribir el archivo de resultados    | N
|`/AssessmentResultJson`     | Ruta de acceso completa al archivo de resultados JSON     | S <br> (AssessmentResultJson o AssessmentResultCsv es necesario)
|`/AssessmentResultCsv`    | Ruta de acceso completa al archivo de resultados CSV   | S <br>(AssessmentResultJson o AssessmentResultCsv es necesario)




## <a name="examples"></a>Ejemplos

**Dmacmd.exe**

  `Dmacmd.exe /? or DmaCmd.exe /help`

**Evaluación de base de datos único mediante reglas de compatibilidad de ejecución y autenticación de Windows**

```
DmaCmd.exe /AssessmentName="TestAssessment"
/AssessmentDatabases="Server=SQLServerInstanceName;Initial
Catalog=DatabaseName;***Integrated Security=true*"**
***/AssessmentEvaluateCompatibilityIssues*** /AssessmentOverwriteResult
/AssessmentResultJson="C:\\temp\\Results\\AssessmentReport.json"
```



**Evaluación de base de datos único mediante la recomendación de característica de autenticación y la ejecución de SQL Server**

```
DmaCmd.exe /AssessmentName="TestAssessment"
/AssessmentDatabases="Server=SQLServerInstanceName;Initial
Catalog=DatabaseName;***User Id=myUsername;Password=myPassword;***"
***/AssessmentEvaluateRecommendations*** /AssessmentOverwriteResult
/AssessmentResultCsv="C:\\temp\\Results\\AssessmentReport.csv"
```


**Evaluación de base de datos único para la plataforma de destino SQL Server 2012 y guardar los resultados en el archivo .json y .csv**

```
DmaCmd.exe /AssessmentName="TestAssessment"
/AssessmentDatabases="Server=SQLServerInstanceName;Initial
Catalog=DatabaseName;Integrated Security=true"
***/AssessmentTargetPlatform="SqlServer2012"***
/AssessmentEvaluateRecommendations /AssessmentOverwriteResult
***/AssessmentResultJson***="C:\\temp\\Results\\AssessmentReport.json"
***/AssessmentResultCsv***="C:\\temp\\Results\\AssessmentReport.csv"
```


**Evaluación de base de datos único para la plataforma de destino base de datos de SQL Azure guardar los resultados en el archivo .json y .csv**

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
***/AssessmentDatabases="Server=SQLServerInstanceName1;Initial
Catalog=DatabaseName1;Integrated Security=true"
"Server=SQLServerInstanceName1;Initial Catalog=DatabaseName2;Integrated
Security=true" "Server=SQLServerInstanceName2;Initial
Catalog=DatabaseName3;Integrated Security=true"***
/AssessmentTargetPlatform="SqlServer2016"
/AssessmentEvaluateCompatibilityIssues /AssessmentOverwriteResult
/AssessmentResultCsv="C:\\temp\\Results\\AssessmentReport.csv"
/AssessmentResultJson="C:\\Results\\test2016.json"
```



## <a name="see-also"></a>Vea también

[Descarga de Asistente de migración de datos](https://www.microsoft.com/download/details.aspx?id=53595)
