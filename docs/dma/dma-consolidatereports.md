---
title: Importar y consolidar los informes de evaluación de Data Migration Assistant (SQL Server) | Microsoft Docs
description: Información sobre cómo importar informes de evaluación de Data Migration Assistant en una base de datos de SQL Server y consolidar varios informes
ms.custom: ''
ms.date: 04/16/2018
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.suite: sql
ms.technology: dma
ms.tgt_pltfrm: ''
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Assess
ms.assetid: ''
caps.latest.revision: ''
author: HJToland3
ms.author: jtoland
manager: craigg
ms.openlocfilehash: be9fc224093f0d5ae14372d4674a52589a2d4801
ms.sourcegitcommit: 05e18a1e80e61d9ffe28b14fb070728b67b98c7d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/04/2018
ms.locfileid: "37781776"
---
# <a name="import-and-consolidate-data-migration-assistant-assessment-reports"></a>Importar y consolidar los informes de evaluación de Data Migration Assistant

Puede usar la línea de comandos para realizar evaluaciones de la migración en modo desatendido, empezando por v2.1 Data Migration Assistant. Esta característica le ayuda a ejecutar las evaluaciones a escala. Los resultados de evaluación en forma de un archivo JSON o CSV.

Puede evaluar varias bases de datos en una única instancia de la utilidad de línea de comandos de Data Migration Assistant y exportar todos los resultados de las evaluaciones en un único archivo JSON. O bien, puede evaluar una base de datos en tiempo y consolidar más adelante los resultados de estas varios archivos JSON en una base de datos SQL.

Para obtener información sobre cómo ejecutar Data Migration Assistant desde la línea de comandos, consulte [ejecutar Data Migration Assistant desde la línea de comandos](../dma/dma-commandline.md). 

## <a name="import-assessment-results-into-a-sql-server-database"></a>Importar los resultados de evaluación a una base de datos de SQL Server

Use el script de PowerShell disponible en este [repositorio de Github](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/data-migration-assistant) para importar los resultados de evaluación desde archivos JSON en una base de datos de SQL Server.

> [!NOTE]
> PowerShell v5 se requiere o superior.

Cuando se ejecuta la secuencia de comandos, deberá proporcionar la siguiente información: 

- **serverName**: da como resultado un nombre de instancia de SQL Server que van a importar la evaluación desde archivos JSON.

- **databaseName**: el nombre de base de datos que importarán a los resultados.

- **jsonDirectory**: la carpeta que guardan los resultados de evaluación, en uno o más archivos JSON.

- **encarguen**: SQLServer

Agregue los valores anteriores en la sección "Ejecutar funciones", como sigue.

```
dmaProcessor -serverName localhost \`\
-databaseName DMAReporting \`\
-jsonDirectory "C:\\temp\\DMACmd\\output\\" \`\
-processTo SQLServer
```

El script de PowerShell crea los siguientes objetos en la instancia SQL que se ha especificado, si los objetos aún no existen:

- **Base de datos** : el nombre proporcionado en los parámetros de PowerShell

  - Repositorio principal

- **Tabla** – DatosSoftware

  - Datos de informes

- **Tabla** -BreakingChangeWeighting

  - Tabla de referencia para todos los cambios importantes. Aquí puede definir sus propios valores de ponderación para influir en una clasificación más precisa de actualización correcta de porcentaje (%).

- **Vista** – UpgradeSuccessRanking\_OnPrem

  - Vista que muestra un factor de éxito para cada base de datos migrados en el entorno local.

- **Vista** – UpgradeSuccessRanking\_Azure

  - Vista que muestra un factor de éxito para cada base de datos migrados en el entorno local.

- **Procedimiento almacenado** – JSONResults\_insertar

  - Se usa para importar datos desde un archivo JSON en SQL Server.

- **Procedimiento almacenado** – AzureFeatureParityResults\_insertar

  - Se usa para importar los resultados de la paridad de características de Azure desde un archivo JSON en SQL Server.

- **Tipo de tabla** – JSONResults

  - Utilizado para almacenar los resultados JSON para las evaluaciones de forma local y pasar a la JSONResults\_procedimiento almacenado para Insert

- **Tipo de tabla** – AzureFeatureParityResults

  - Utilizado para almacenar la característica de Azure los resultados de paridad de las evaluaciones de azure y pasar a la AzureFeatureParityResults\_procedimiento almacenado para Insert

El script de PowerShell crea un **procesados** directorio dentro del directorio proporcionado que contiene los archivos JSON que se procesan.

Una vez finalizada la secuencia de comandos, los resultados se importan en la tabla, DatosSoftware.

### <a name="viewing-the-results-in-sql-server"></a>Ver los resultados en SQL Server

Después de que se han cargado los datos, conectarse a la instancia de SQL Server. La pantalla debe aparecer como se muestra en el gráfico siguiente:

![Informes consolidados en la base de datos de SQL Server](../dma/media/DMAReportingDatabase.png)

El dbo. Tabla DatosSoftware incluye el contenido del archivo JSON en formato sin procesar.

## <a name="on-premises-upgrade-success-ranking"></a>En el entorno local actualiza clasificación de éxito

Para ver una lista de bases de datos y su rango de éxito de porcentaje (%), seleccione el dbo. Vista UpgradeSuccessRanking_OnPrem:

![Datos en la vista UpgradeSuccessRaning_OnPrem](../dma/media/UpgradeSuccessRankingView.png)

Aquí puede ver una base de datos dada ¿qué es la posibilidad de actualización correcta de los niveles de compatibilidad diferentes. Por lo tanto, por ejemplo, la base de datos de recursos humanos se evalúa en relación con los niveles de compatibilidad 100, 110, 120 y 130. Esta evaluación le ayuda a ver cuánto esfuerzo está implicado en la migración a una versión posterior de SQL Server desde la versión actual que se encuentra la base de datos.

Normalmente, la métrica que le interesa es cuántos cambios importantes son para una base de datos. En el ejemplo anterior, puede ver que la base de datos de recursos humanos tiene un factor de éxito de actualización de un 50% para los niveles de compatibilidad 100, 110, 120 y 130.

Esta métrica puede influir modificando los valores de ponderación de dbo. Tabla BreakingChangeWeighting.

En el ejemplo siguiente, el esfuerzo para corregir el problema de sintaxis en la base de datos de recursos humanos se considera alto por lo que se asigna un valor de 3 a **esfuerzo**. Dado que no tienen mucho para corregir el problema de sintaxis, se asigna un valor de 1 a **FixTime**. Porque habrá algún costo implicado en realizar el cambio, se asigna un valor de 2 a **costo**. Uso de este valor cambia el Changerank combinada a 2.

> [!NOTE]
> La puntuación es en una escala del 1 al 5.  1 es baja y 5 como alto. Además, el ChangeRank es una columna calculada.

![Costo, esfuerzo y FixTime valores para el problema de sintaxis](../dma/media/SyntaxIssueEffort.png)

Ahora en este ejemplo, al consultar el dbo. Vista UpgradeSuccessRanking_OnPrem, quitó el factor de éxito de actualización para la base de datos HR cambios importantes.

![Factor de éxito de la actualización de base de datos de recursos humanos](../dma/media/UpgradeSuccessFactor_HR.png)

## <a name="azure-upgrade-success-ranking"></a>Clasificación de actualización de Azure correcta

Para ver una lista de bases de datos para migrar a Azure SQL Database y su rango de éxito de porcentaje, seleccione el dbo. Vista UpgradeSuccessRanking_Azure.

![Datos en la vista UpgradeSuccessRanking_Azure](../dma/media/UpgradeSuccessRankingView_Azure.png)

Aquí está interesado en el valor MigrationBlocker. 100,00 significa que hay un rango de éxito del 100% para mover una base de datos a Azure SQL Database v12.

La diferencia con esta vista es que no hay actualmente ninguna invalidación para cambiar la ponderación de las reglas de bloqueo de migración.

Para obtener información sobre la creación de informes sobre estos datos mediante Power BI, consulte [informar sobre sus valoraciones consolidadas con Power BI](../dma/dma-powerbiassesreport.md).
