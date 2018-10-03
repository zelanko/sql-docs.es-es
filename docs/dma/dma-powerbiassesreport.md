---
title: Analizar los informes de evaluación de Data Migration Assistant consolidados con Power BI (SQL Server) | Microsoft Docs
description: Aprenda a usar Power BI para analizar los informes de evaluación de migración de datos que ha importado y consolidado en SQL Server
ms.custom: ''
ms.date: 08/29/2018
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Assess
ms.assetid: ''
author: HJToland3
ms.author: rajpo
manager: craigg
ms.openlocfilehash: 35cd161d29977d97ab3da650de5afdb46ab748a8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47832243"
---
# <a name="analyze-consolidated-assessment-reports-created-by-data-migration-assistant-with-power-bi"></a>Analizar los informes de evaluación consolidada creados por Data Migration Assistant con Power BI

En este artículo se describe cómo crear un informe de Power BI para analizar las evaluaciones de migración consolidada.

Para obtener información acerca de la consolidación de las evaluaciones de migración creadas por el Asistente para migración de datos, vea [consolidar los informes de evaluación](../dma/dma-consolidatereports.md).

## <a name="sample-power-bi-reports"></a>Ejemplos de informes de Power BI

Puede descargar ejemplos de informes de Power BI para valoraciones consolidadas migración desde esta [repositorio de Github](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/data-migration-assistant).

Los siguientes informes se incluyen: 

- [Panel](#dashboard--details)

  Incluye estadísticas de la instantánea y un informe de exploración en profundidad.

- [Preparación de actualización local](#on-premises-upgrade-readiness--details)

  El origen de datos es la vista de UpgradeSuccessRanking en la base de datos DMAReporting.  Este informe muestra el porcentaje de actualización correcta para las bases de datos evaluados.

- [Paridad de características en el entorno local](#on-premise-feature-parity--details)

  Se muestran las recomendaciones de característica para la versión de SQL Server de destino.

- [Preparación de actualización de base de datos SQL Azure](#azure-sql-db-upgrade-readiness--details)

  El origen de datos es la vista de UpgradeSuccessRanking en la base de datos DMAReporting.  Este informe muestra el porcentaje de actualización correcta para bases de datos que se evalúa para las migraciones de base de datos de SQL Azure.

- [Características de Azure SQL DB no compatibles](#azure-sql-db-unsupported-features--details)

  Muestra características de las bases de datos existentes que no se admiten en Azure SQL Database (V12).

Puede modificar estos informes para que funcione con su entorno al cambiar el origen de datos en Power BI. 

1. Seleccione la flecha abajo junto a **editar consultas**y seleccione **configuración del origen de datos**.

   ![Editar menú consultas, configuración de origen de datos](../dma/media/DataSourceSettings.png)

1. Seleccione **cambiar origen...** y escriba los valores de servidor y base de datos.

   ![Cambiar origen, el servidor y la base de datos](../dma/media/ChangeSource.png)

1. Seleccione **Aceptar**y, a continuación, seleccione **cerrar**.

1. Actualizar los informes.

   ![Actualizar informe de Power BI](../dma/media/RefreshReport.png)

### <a name="dashboard-report"></a>Informe del panel

![Informe del panel](../dma/media/DashboardReport.png)

El panel muestra detalles acerca de todas sus evaluaciones. Puede usar las segmentaciones de datos en el lado izquierdo para filtrar por instancia o base de datos. Puede usar el gráfico de barras para profundizar en las categorías específicas para ver dónde se encuentran los problemas.

Para explorar en profundidad, seleccione el círculo con la flecha hacia abajo en la esquina superior derecha del gráfico de barras.

![Obtención de detalles de categoría](../dma/media/CategoryDrillDown.png)

La secuencia de obtención de detalles se define como se muestra en la siguiente imagen (bajo **eje**). Para cambiar la secuencia, arrastre las columnas en el orden deseado.

![Visualizaciones, el eje del gráfico de barras](../dma/media/VisualizationsAxis.png)

Esta vista es aún más eficaces cuando primero filtrar por una base de datos específica y, a continuación, explorar en profundidad los problemas de la categoría específica. En el ejemplo siguiente, la base de datos de recursos humanos se selecciona, por ejemplo **SQL01** para ver todos los objetos que impiden las migraciones (cambios importantes).

![Importantes cambios para la base de datos de recursos humanos](../dma/media/BreakingChanges.png)

### <a name="on-premises-upgrade-readiness-report"></a>Informe de preparación de actualización de local

![Informe de preparación de actualización de local](../dma/media/OnPremisesUpgradeReadinessReport.png)

Este informe muestra una instantánea del nivel de preparación de las bases de datos son migrar a una versión posterior de SQL Server. Los datos de este informe proceden de dbo. UpgradeSuccessFactor\_vista local en la base de datos DMAReporting.

Filtrado por instancia y el nombre de la base de datos y el uso de las tarjetas de puntuación en la parte superior, puede ver qué versión de la base de datos podría migrarse demasiado. Por ejemplo, si se filtra por la base de datos AdventureWorks 2012, puede ver que la base de datos está listo para mover a todas las versiones de SQL Server que aparecen en el informe. Esto se determina asegurándose de que no hay ningún cambio importante para ese nivel de compatibilidad y la base de datos.

![Factor de éxito de actualización para la base de datos AdventureWorks](../dma/media/UpgradeSuccessFactor.png)

### <a name="on-premises-feature-parity-report"></a>Informe de paridad de características en el entorno local

![Informe de paridad de características en el entorno local](../dma/media/OnPremisesFeatureParityReport.png)

Use este informe para resaltar las nuevas características que se pueden usar para la base de datos en la versión de SQL Server de destino.

Cuando se selecciona una característica en el gráfico de embudo, los datos en la parte inferior resaltan los objetos que se ven afectados por la característica. En el ejemplo siguiente, la **Stretch database para ahorro de almacenamiento** característica está seleccionada y aparece una tabla que podrían beneficiarse de esta característica.

![Recomendación de característica para Stretch Database](../dma/media/FeatureRecommend_StretchDatabase.png)

### <a name="azure-sql-db-upgrade-readiness-report"></a>Informe de preparación de actualización de base de datos SQL Azure

![Informe de preparación de actualización de base de datos SQL Azure](../dma/media/AzureSQLDBUpgradeReadinessReport.png)

Este informe muestra la preparación para la base de datos para migrar a Azure SQL Database V12. Los datos de este informe proceden de dbo. Vista UpgradeSuccessRanking en la base de datos DMAReporting.

### <a name="azure-features-parity-report"></a>Informe de paridad de características de Azure

![Informe de paridad de características de Azure](../dma/media/AzureFeaturesParityReport.png)

Use este informe para resaltar el *características de nivel de instancia* que no son compatibles con Azure SQL Database V12.

Cuando se elige una característica en el gráfico de embudo, los datos en la parte inferior muestran las instancias y las características de base de datos que no son compatibles. En el ejemplo siguiente, se selecciona esta característica: **siempre en configuración del grupo de disponibilidad no se admite en Azure SQL Database**.  

![Característica de grupo de disponibilidad de AlwaysOn](../dma/media/Feature_AlwaysOnAvailability.png)

 
### <a name="azure-sql-db-unsupported-features-report"></a>Informe de características no admitidas de base de datos de SQL Azure

![Informe de características no admitidas de base de datos de SQL Azure](../dma/media/AzureSQLDBUnsupportedFeaturesReport.png)

Este informe resalta las características que no se admiten para un determinado **base de datos** cuando el destino es Azure SQL Database (V12).

Mediante el filtrado por el valor de nombre y la característica de base de datos en el gráfico de embudo, puede ver detalles sobre la característica no admitida. Los detalles incluyen recomendaciones para resolver el problema y qué objeto se ve afectado.

Por ejemplo, el filtrado por la base de datos DTC y **no se puede actualizar las bases de datos de solo lectura**, puede ver una lista de objetos que se ven afectados.

![Las bases de datos de solo lectura no pueden ser actualizado problema](../dma/media/ReadOnlyDatabases.png)

## <a name="see-also"></a>Vea también

[Información general de Data Migration Assistant](../dma/dma-overview.md)

[Descarga de Data Migration Assistant](https://www.microsoft.com/download/details.aspx?id=53595)

[Descarga de Power BI](https://powerbi.microsoft.com/)
