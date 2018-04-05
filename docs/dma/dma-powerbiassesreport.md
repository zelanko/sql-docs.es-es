---
title: Informes sobre sus evaluaciones consolidadas mediante Power BI (SQL Server datos Migration Assistant) | Documentos de Microsoft
ms.custom: ''
ms.date: 09/07/2017
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
- Data Migration Assistant, Assess
ms.assetid: ''
caps.latest.revision: ''
author: HJToland3
ms.author: jtoland
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 62f3ed0802a0a7570109bdae99151c8c6ce4fa01
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="report-on-your-consolidated-assessments-by-using-power-bi-data-migration-assistant"></a>Informes sobre sus evaluaciones consolidadas mediante Power BI (Asistente de migración de datos)

En este artículo se describe cómo crear un informe de Power BI para evaluaciones de migración consolidados.

Para obtener información sobre la consolidación de las evaluaciones de migración mediante el Asistente para la migración de datos, vea [consolidar los informes de evaluación de](../dma/dma-consolidatereports.md).

## <a name="sample-power-bi-reports"></a>Informes de ejemplo de Power BI

Puede descargar los ejemplos de informes de Power BI para evaluaciones de migración consolidados de esta [repositorio de Github](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/data-migration-assistant).

Los informes siguientes se incluyen: 

- [Panel](#dashboard--details)

  Incluye estadísticas de instantáneas y un informe de obtención de detalles.

- [Preparación de actualización local](#on-premises-upgrade-readiness--details)

  El origen de datos es la vista de UpgradeSuccessRanking en la base de datos de DMAReporting.  Este informe muestra el porcentaje de actualización correcta para las bases de datos calculados.

- [Paridad de características locales](#on-premise-feature-parity--details)

  Muestra las recomendaciones de característica para la versión de SQL Server de destino.

- [Preparación de actualización de base de datos de SQL Azure](#azure-sql-db-upgrade-readiness--details)

  El origen de datos es la vista de UpgradeSuccessRanking en la base de datos de DMAReporting.  Este informe muestra el porcentaje de actualización correcta para las bases de datos que se evalúa para migraciones de base de datos de SQL Azure.

- [Características de base de datos de SQL no admitida de Azure](#azure-sql-db-unsupported-features--details)

  Muestra características de bases de datos existentes que no se admiten en la base de datos de SQL de Azure (V12).

Puede modificar estos informes para que funcione con su entorno, cambie el origen de datos en Power BI. 

1. Seleccione la flecha hacia abajo junto a **editar consultas**y seleccione **configuración del origen de datos**.

   ![Editar menú consultas, configuración del origen de datos](../dma/media/DataSourceSettings.png)

1. Seleccione **cambiar origen...** y escriba los valores de servidor y base de datos.

   ![Cambiar el origen, el servidor y base de datos](../dma/media/ChangeSource.png)

1. Seleccione **Aceptar**y, a continuación, seleccione **cerrar**.

1. Actualizar los informes.

   ![Actualizar el informe de Power BI](../dma/media/RefreshReport.png)

### <a name="dashboard-report"></a>Informes de panel

![Informes de panel](../dma/media/DashboardReport.png)

El panel muestra detalles de todas las de sus evaluaciones. Puede utilizar las segmentaciones de datos en el lado izquierdo para filtrar por instancia o base de datos. Puede usar el gráfico de barras para profundizar en categorías específicas para ver dónde se encuentran los problemas.

Para explorar en profundidad, seleccione el círculo con la flecha hacia abajo en la esquina superior derecha del gráfico de barras.

![Obtención de detalles de categoría](../dma/media/CategoryDrillDown.png)

La secuencia de obtención de detalles se define como se muestra en la siguiente imagen (en **eje**). Para cambiar la secuencia, arrastre las columnas en el orden deseado.

![Visualizaciones, el eje del gráfico de barras](../dma/media/VisualizationsAxis.png)

Esta vista se vuelve más eficaz cuando en primer lugar, filtre por una base de datos y, a continuación, examinar con detalle los problemas de categoría específica. En el ejemplo siguiente, la base de datos de recursos humanos está seleccionado para la instancia **SQL01** para ver todos los objetos que impidan que las migraciones (cambios importantes).

![Principales cambios de base de datos de recursos humanos](../dma/media/BreakingChanges.png)

### <a name="on-premises-upgrade-readiness-report"></a>Informe de preparación de actualización de locales

![Informe de preparación de actualización de locales](../dma/media/OnPremisesUpgradeReadinessReport.png)

Este informe muestra una instantánea de la lista son las bases de datos migrar a una versión posterior de SQL Server. Los datos de este informe proceden de la tabla dbo. UpgradeSuccessFactor\_vista de instancia en la base de datos de DMAReporting.

El filtrado por instancia y el nombre de la base de datos y uso de las tarjetas de puntuación en la parte superior, puede ver qué versión de la base de datos pudo migrarse demasiado. Por ejemplo, si se filtra por la base de datos de AdventureWorks 2012, puede ver que la base de datos está listo para mover a todas las versiones de SQL Server enumeradas en el informe. Esto se determina al garantizar que no hay cambios importantes para esa base de datos y nivel de compatibilidad.

![Factor de éxito de actualización de base de datos de AdventureWorks](../dma/media/UpgradeSuccessFactor.png)

### <a name="on-premises-feature-parity-report"></a>Informe de paridad de características locales

![Informe de paridad de características locales](../dma/media/OnPremisesFeatureParityReport.png)

Use este informe para resaltar las nuevas características que pueden usarse para la base de datos en la versión de SQL Server de destino.

Cuando se selecciona una característica en el gráfico de embudo, los datos en la parte inferior resaltan los objetos que se ven afectados por la característica. En el ejemplo siguiente, la **Stretch database para ahorro de almacenamiento** característica está seleccionada y se muestra una tabla que podrían beneficiarse de esta característica.

![Recomendación de característica para Stretch Database](../dma/media/FeatureRecommend_StretchDatabase.png)

### <a name="azure-sql-db-upgrade-readiness-report"></a>Informe de preparación de actualización de base de datos de SQL Azure

![Informe de preparación de actualización de base de datos de SQL Azure](../dma/media/AzureSQLDBUpgradeReadinessReport.png)

Este informe muestra la preparación para la base de datos para migrar a V12 de base de datos de SQL Azure. Los datos de este informe proceden de la tabla dbo. Vista de UpgradeSuccessRanking en la base de datos de DMAReporting.

### <a name="azure-features-parity-report"></a>Informe de paridad de características de Azure

![Informe de paridad de características de Azure](../dma/media/AzureFeaturesParityReport.png)

Use este informe para resaltar la *características de nivel de instancia* que no son compatibles con V12 de base de datos de SQL Azure.

Cuando se elige una característica en el gráfico de embudo, los datos en la parte inferior muestran las instancias y características de base de datos que no son compatibles. En el ejemplo siguiente, se selecciona esta característica: **siempre en configuración del grupo de disponibilidad no se admite en la base de datos de SQL Azure**.  

![Siempre en la característica grupo de disponibilidad](../dma/media/Feature_AlwaysOnAvailability.png)

 
### <a name="azure-sql-db-unsupported-features-report"></a>Informe de características no admitidas de base de datos de SQL Azure

![Informe de características no admitidas de base de datos de SQL Azure](../dma/media/AzureSQLDBUnsupportedFeaturesReport.png)

Este informe resalta las características que no se admiten para un determinado **base de datos** cuando el destino es la base de datos de SQL de Azure (V12).

Mediante el filtrado por el valor de nombre y la característica de base de datos en el gráfico de embudo, puede ver detalles de la función no admitida. Los detalles incluyen qué objeto se ve afectado y recomendaciones para resolver el problema.

Por ejemplo, el filtrado por la base de datos DTC y **no se puede actualizar las bases de datos de solo lectura**, puede ver una lista de objetos que se ven afectados.

![Las bases de datos de solo lectura no se pueden actualizar el problema](../dma/media/ReadOnlyDatabases.png)

## <a name="see-also"></a>Vea también

[Información general del Asistente de migración de datos](../dma/dma-overview.md)

[Descarga de Asistente de migración de datos](https://www.microsoft.com/download/details.aspx?id=53595)

[Descarga de Power BI](https://powerbi.microsoft.com/)
