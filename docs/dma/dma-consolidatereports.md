---
title: Consolidar los informes de evaluación (SQL Server datos Migration Assistant) | Documentos de Microsoft
ms.custom: ''
ms.date: 04/16/2018
ms.prod: sql
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
- Data Migration Assistant, Assess
ms.assetid: ''
caps.latest.revision: ''
author: HJToland3
ms.author: jtoland
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 30399ddacff6c84ea1f5d914f87b11dac02167b4
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="consolidate-assessment-reports-data-migration-assistant"></a>Consolidar los informes de evaluación (Asistente de migración de datos)

Puede usar la línea de comandos para realizar evaluaciones de la migración en modo desatendido, empezando por el Asistente de migración de datos v2.1. Esta característica puede ayudarle a ejecutar las evaluaciones a escala. Los resultados de evaluación en el formulario de un archivo JSON o CSV.

Puede evaluar varias bases de datos en una única instancia de la utilidad de línea de comandos el Asistente de migración de datos y exportar todos los resultados de las evaluaciones en un único archivo JSON. O bien, puede evaluar una base de datos en tiempo y más adelante consolidar los resultados de estas varios archivos JSON en una base de datos SQL.

Para obtener información sobre cómo ejecutar el Asistente de migración de datos desde la línea de comandos, consulte [ejecutar datos Migration Assistant desde línea de comandos](../dma/dma-commandline.md). 


## <a name="import-assessment-results-into-a-sql-server-database"></a>Importar resultados de la evaluación en una base de datos de SQL Server

Usar el script de PowerShell disponible en este [repositorio de Github](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/data-migration-assistant) para importar los resultados de la evaluación de los archivos JSON en una base de datos de SQL Server.

> [!NOTE]
> PowerShell v5 o posterior es necesario.

Cuando se ejecuta la secuencia de comandos, debe proporcionar la siguiente información: 

- **serverName**: nombre de la instancia de SQL Server que van a importar la evaluación resultante de archivos JSON.

- **databaseName**: el nombre de base de datos que se importarán los resultados a.

- **jsonDirectory**: la carpeta que guardan los resultados de la evaluación, en uno o más archivos JSON.

- **encarguen**: SQL Server

Agregue los valores anteriores en la sección "Ejecutar funciones", como se indica a continuación.

```
dmaProcessor -serverName localhost \`\
-databaseName DMAReporting \`\
-jsonDirectory "C:\\temp\\DMACmd\\output\\" \`\
-processTo SQLServer
```

El script de PowerShell crea los siguientes objetos en la instancia SQL que se ha especificado, si los objetos aún no existen:

- **Base de datos** : el nombre proporcionado en los parámetros de PowerShell

  - Repositorio principal

- **Tabla** : DatosSoftware

  - Datos de informes

- **Tabla** -BreakingChangeWeighting

  - Tabla de referencia para todos los cambios. Aquí puede definir sus propios valores de ponderación para influir en una clasificación de actualización correcta de porcentaje (%) más precisa.

- **Vista** : UpgradeSuccessRanking\_local

  - Vista que muestra un factor de éxito para cada base de datos ser migrados local.

- **Vista** : UpgradeSuccessRanking\_Azure

  - Vista que muestra un factor de éxito para cada base de datos ser migrados local.

- **Procedimiento almacenado** : JSONResults\_insertar

  - Se usa para importar datos desde un archivo JSON en SQL Server.

- **Procedimiento almacenado** : AzureFeatureParityResults\_insertar

  - Se usa para importar resultados de la paridad de características de Azure desde un archivo JSON en SQL Server.

- **Tipo de tabla** – JSONResults

  - Utiliza para almacenar los resultados de JSON para evaluaciones locales y pasar a la JSONResults\_procedimiento almacenado para Insert

- **Tipo de tabla** – AzureFeatureParityResults

  - Utiliza para almacenar los resultados de la paridad de las evaluaciones de azure de la característica de Azure y pasar a la AzureFeatureParityResults\_procedimiento almacenado para Insert

El script de PowerShell crea un **procesados** directorio en el directorio proporcionado que contiene los archivos JSON que se procesan.

Una vez completada la secuencia de comandos, los resultados se importan en la tabla, DatosSoftware.

### <a name="viewing-the-results-in-sql-server"></a>Ver los resultados en SQL Server

Una vez se han cargado los datos, conectarse a la instancia de SQL Server. La pantalla debe aparecer como se muestra en el siguiente gráfico:

![Informes consolidados en la base de datos de SQL Server](../dma/media/DMAReportingDatabase.png)

La tabla dbo. Tabla de datosSoftware incluye el contenido del archivo en formato JSON.

## <a name="on-premises-upgrade-success-ranking"></a>Local actualiza clasificación correcto

Para ver una lista de las bases de datos y su rango de éxito de porcentaje (%), seleccione el dbo. Vista de UpgradeSuccessRanking_OnPrem:

![Ver datos en UpgradeSuccessRaning_OnPrem](../dma/media/UpgradeSuccessRankingView.png)

Aquí puede ver una base de datos dada ¿cuál es la posibilidad de actualización correcto para los niveles de compatibilidad diferentes. Por lo tanto, por ejemplo, la base de datos de recursos humanos se evalúa con respecto a los niveles de compatibilidad 100, 110, 120 y 130. Esta evaluación ayuda a ver visualmente la cantidad de trabajo está implicada en la migración a una versión posterior de SQL Server desde la versión actual que se encuentra la base de datos.

Normalmente la métrica que le interesa es están cuántos cambios existe para una base de datos. En el ejemplo anterior, puede ver que la base de datos de recursos humanos tiene un factor de éxito de actualización de un 50% para los niveles de compatibilidad 100, 110, 120 y 130.

Esta métrica se puede influir modificando los valores de ponderación de dbo. Tabla BreakingChangeWeighting.

En el ejemplo siguiente, el esfuerzo implicado en corregir el problema de sintaxis en la base de datos de recursos humanos se considera alto por lo que se asigna un valor de 3 **esfuerzo**. Dado que no sería tardan tiempo para solucionar el problema de sintaxis, se asigna un valor de 1 a **FixTime**. Dado que podría haber algún coste implicados en la realización del cambio, se asigna un valor de 2 a **costo**. Este valor cambia el Changerank combinada a 2.

> [!NOTE]
> La puntuación es en una escala del 1 al 5.  1 es baja y 5 es alta. Además, el ChangeRank es una columna calculada.

![Costo, esfuerzo y FixTime los valores para el problema de sintaxis](../dma/media/SyntaxIssueEffort.png)

Ahora, en este ejemplo, al consultar el dbo. Vista de UpgradeSuccessRanking_OnPrem, quitó el factor de éxito de actualización para la base de datos de recursos humanos para cambios importantes.

![Factor de éxito de la actualización de base de datos de recursos humanos](../dma/media/UpgradeSuccessFactor_HR.png)

## <a name="azure-upgrade-success-ranking"></a>Clasificación de actualización Azure correcta

Para ver una lista de bases de datos para migrar a base de datos de SQL Azure y su rango de éxito de porcentaje, seleccione la tabla dbo. Vista de UpgradeSuccessRanking_Azure.

![Ver datos en UpgradeSuccessRanking_Azure](../dma/media/UpgradeSuccessRankingView_Azure.png)

Aquí está interesado en el valor de MigrationBlocker. 100,00 significa que hay un rango de éxito del 100% para mover una base de datos a base de datos de SQL Azure v12.

La diferencia con esta vista es que actualmente no hay ningún reemplazo para cambiar la ponderación de reglas de bloqueo de migración.

Para obtener información sobre cómo informar de estos datos con Power BI, consulte [informar sobre sus evaluaciones consolidadas con Power BI](../dma/dma-powerbiassesreport.md).
