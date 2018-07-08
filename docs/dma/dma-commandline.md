---
title: Ejecutar Data Migration Assistant desde la línea de comandos (SQL Server) | Microsoft Docs
description: Obtenga información sobre cómo ejecutar Data Migration Assistant desde la línea de comandos para evaluar las bases de datos de SQL Server para la migración
ms.custom: ''
ms.date: 09/01/2017
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.suite: sql
ms.technology: dma
ms.tgt_pltfrm: ''
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Command Line
ms.assetid: ''
caps.latest.revision: ''
author: HJToland3
ms.author: jtoland
manager: craigg
ms.openlocfilehash: 6b364dc03d48cbc1c0487362712e10f7ab0b782e
ms.sourcegitcommit: 05e18a1e80e61d9ffe28b14fb070728b67b98c7d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/04/2018
ms.locfileid: "37785466"
---
# <a name="run-data-migration-assistant-from-the-command-line"></a>Ejecutar Data Migration Assistant desde la línea de comandos
Con la versión 2.1 y anteriores, cuando instale Data Migration Assistant, también instalará dmacmd.exe en *% ProgramFiles %\\Microsoft Data Migration Assistant\\*. Usar dmacmd.exe para evaluar las bases de datos en modo desatendido y generar el resultado al archivo JSON o CSV. Este método es especialmente útil al evaluar varias bases de datos o bases de datos enormes. 

> [!NOTE]
> Dmacmd.exe admite solo las evaluaciones de ejecución. No se admiten las migraciones en este momento.


## <a name="command-line-arguments"></a>Argumentos de línea de comandos

```
DmaCmd.exe /AssessmentName="string"
/AssessmentDatabases="connectionString1" \["connectionString2"\]
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
|`/AssessmentTargetPlatform`     | Plataforma de destino para la evaluación, los valores admitidos: SqlServer2012, SqlServer2014, SqlServer2016 y AzureSqlDatabaseV12. El valor predeterminado es SqlServer2016   | N
|`/AssessmentEvaluateFeatureParity`  | Ejecutar reglas de paridad de características  | N
|`/AssessmentEvaluateCompatibilityIssues`     | Ejecutar las reglas de compatibilidad  | S <br> (AssessmentEvaluateCompatibilityIssues o AssessmentEvaluateRecommendations es necesario).
|`/AssessmentEvaluateRecommendations`     | Ejecute la recomendación de característica        | S <br> (AssessmentEvaluateCompatibilityIssues o AssessmentEvaluateRecommendationsis necesarios)
|`/AssessmentOverwriteResult`     | Sobrescribir el archivo de resultados    | N
|`/AssessmentResultJson`     | Ruta de acceso completa al archivo de resultados JSON     | S <br> (AssessmentResultJson o AssessmentResultCsv es necesario)
|`/AssessmentResultCsv`    | Ruta de acceso completa al archivo de resultado CSV   | S <br>(AssessmentResultJson o AssessmentResultCsv es necesario)




## <a name="examples"></a>Ejemplos

**Dmacmd.exe**

  `Dmacmd.exe /? or DmaCmd.exe /help`

**Evaluación de bases de datos única mediante reglas de compatibilidad de ejecución y autenticación de Windows**

```
DmaCmd.exe /AssessmentName="TestAssessment"
/AssessmentDatabases="Server=SQLServerInstanceName;Initial
Catalog=DatabaseName;***Integrated Security=true*"**
***/AssessmentEvaluateCompatibilityIssues*** /AssessmentOverwriteResult
/AssessmentResultJson="C:\\temp\\Results\\AssessmentReport.json"
```



**Evaluación de bases de datos única con la recomendación de característica de autenticación y la ejecución de SQL Server**

```
DmaCmd.exe /AssessmentName="TestAssessment"
/AssessmentDatabases="Server=SQLServerInstanceName;Initial
Catalog=DatabaseName;***User Id=myUsername;Password=myPassword;***"
***/AssessmentEvaluateRecommendations*** /AssessmentOverwriteResult
/AssessmentResultCsv="C:\\temp\\Results\\AssessmentReport.csv"
```


**Evaluación de bases de datos único para la plataforma de destino de SQL Server 2012, guardar los resultados en el archivo .json y. csv**

```
DmaCmd.exe /AssessmentName="TestAssessment"
/AssessmentDatabases="Server=SQLServerInstanceName;Initial
Catalog=DatabaseName;Integrated Security=true"
***/AssessmentTargetPlatform="SqlServer2012"***
/AssessmentEvaluateRecommendations /AssessmentOverwriteResult
***/AssessmentResultJson***="C:\\temp\\Results\\AssessmentReport.json"
***/AssessmentResultCsv***="C:\\temp\\Results\\AssessmentReport.csv"
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

[Descarga de Ayudante de migración de datos](https://www.microsoft.com/download/details.aspx?id=53595)
