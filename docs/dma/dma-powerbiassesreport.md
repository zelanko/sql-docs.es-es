---
title: Analizar informes de evaluación consolidados con Power BI
titleSuffix: Data Migration Assistant
description: Aprenda a usar Power BI para analizar los informes de evaluación de la migración de datos que ha importado y consolidado en SQL Server
ms.custom: seo-lt-2019
ms.date: 03/12/2019
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
ms.openlocfilehash: f2385914fc97fa8e118d871ddac6e0cdc9d49247
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056505"
---
# <a name="analyze-consolidated-assessment-reports-created-by-data-migration-assistant-with-power-bi"></a>Analizar informes consolidados de evaluación creados por Data Migration Assistant con Power BI

En este artículo se describe cómo crear un informe de Power BI para analizar las evaluaciones de migración consolidadas.

Para obtener información sobre la consolidación de las evaluaciones de migración creadas por el Data Migration Assistant, vea [consolidar informes de evaluación](../dma/dma-consolidatereports.md).

## <a name="sample-power-bi-reports"></a>Informes de Power BI de ejemplo

Puede descargar ejemplos de informes de Power BI para las evaluaciones de migración consolidadas en este [repositorio de github](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/data-migration-assistant).

Se incluyen los siguientes informes: 

- [Consola](#dashboard-report)

  Incluye estadísticas de instantáneas y un informe de obtención de detalles.

- [Preparación de la actualización local](#on-premises-upgrade-readiness-report)

  El origen de datos es la vista UpgradeSuccessRanking en la base de datos DMAReporting.  Este informe muestra el porcentaje de actualización correcta para las bases de datos evaluadas.

- [Paridad de características locales](#on-premises-feature-parity-report)

  Muestra las recomendaciones de características para la versión de SQL Server de destino.

- [Preparación de la actualización de Azure SQL Database](#azure-sql-db-upgrade-readiness-report)

  El origen de datos es la vista UpgradeSuccessRanking en la base de datos DMAReporting.  Este informe muestra el porcentaje de actualización correcta de las bases de datos evaluadas para las migraciones de Azure SQL Database.

- [Características no admitidas de Azure SQL Database](#azure-sql-db-unsupported-features-report)

  Muestra las características de las bases de datos existentes que no se admiten en Azure SQL DB (V12).

Puede modificar estos informes para que funcionen con su entorno cambiando el origen de datos en Power BI. 

1. Seleccione la flecha abajo situada junto a **Editar consultas**y seleccione **configuración de origen de datos**.

   ![Menú Editar consultas, configuración del origen de datos](../dma/media/DataSourceSettings.png)

1. Seleccione **cambiar origen...** y escriba los valores de servidor y base de datos.

   ![Cambiar el origen, el servidor y la base de datos](../dma/media/ChangeSource.png)

1. Seleccione **Aceptar**y, a continuación, seleccione **cerrar**.

1. Actualice los informes.

   ![Actualizar Power BI informe](../dma/media/RefreshReport.png)

### <a name="dashboard-report"></a>Informe del panel

![Informe del panel](../dma/media/DashboardReport.png)

En el panel se muestran los detalles de todas las evaluaciones. Puede usar las segmentaciones en el lado izquierdo para filtrar por instancia o base de datos. Puede usar el gráfico de barras para explorar en profundidad categorías específicas para ver dónde se encuentran los problemas.

Para explorar en profundidad, seleccione el círculo con la flecha hacia abajo que se encuentra en la esquina superior derecha del gráfico de barras.

![Obtención de detalles de categoría](../dma/media/CategoryDrillDown.png)

La secuencia de obtención de detalles se establece como se muestra en la siguiente imagen (en **eje**). Para cambiar la secuencia, arrastre las columnas hasta el orden deseado.

![Visualizaciones, eje del gráfico de barras](../dma/media/VisualizationsAxis.png)

Esta vista es aún más eficaz al filtrar por primera vez una base de datos concreta y, a continuación, profundizar en los problemas de categoría específicos. En el ejemplo siguiente, se selecciona la base de datos de recursos humanos para la instancia **SQL01** para ver todos los objetos que impiden Migraciones (cambios importantes).

![Principales cambios de la base de datos de recursos humanos](../dma/media/BreakingChanges.png)

### <a name="on-premises-upgrade-readiness-report"></a>Informe de preparación de la actualización local

![Informe de preparación de la actualización local](../dma/media/OnPremisesUpgradeReadinessReport.png)

Este informe muestra una instantánea de la preparación de la migración de las bases de datos a una versión posterior de SQL Server. Los datos de este informe proceden del DBO. UpgradeSuccessFactor\_vista local en la base de datos DMAReporting.

Filtrado por instancia y nombre de base de datos, y con las tarjetas de puntuación en la parte superior, puede ver qué versión de la base de datos también se puede migrar. Por ejemplo, si filtra por la base de datos AdventureWorks 2012, puede ver que la base de datos está lista para moverse a todas las versiones de SQL Server enumeradas en el informe. Esto se determina asegurándose de que no hay cambios importantes para la base de datos y el nivel de compatibilidad.

![Factor de actualización correcta para la base de datos AdventureWorks](../dma/media/UpgradeSuccessFactor.png)

### <a name="on-premises-feature-parity-report"></a>Informe de paridad de características locales

![Informe de paridad de características locales](../dma/media/OnPremisesFeatureParityReport.png)

Use este informe para resaltar las nuevas características que se pueden utilizar para la base de datos en la versión de SQL Server de destino.

Al seleccionar una característica en el gráfico de embudo, los datos de la parte inferior destacan qué objetos se ven afectados por la característica. En el ejemplo siguiente, se selecciona la característica **Stretch Database for Storage Savings** y se muestra una tabla que podría beneficiarse de esta característica.

![Recomendación de características para Stretch Database](../dma/media/FeatureRecommend_StretchDatabase.png)

### <a name="azure-sql-db-upgrade-readiness-report"></a>Informe preparación para la actualización de Azure SQL DB

![Informe preparación para la actualización de Azure SQL DB](../dma/media/AzureSQLDBUpgradeReadinessReport.png)

Este informe muestra la preparación de la base de datos para migrar a Azure SQL Database V12. Los datos de este informe proceden del DBO. Vista UpgradeSuccessRanking en la base de datos DMAReporting.

### <a name="azure-features-parity-report"></a>Informe de paridad de características de Azure

![Informe de paridad de características de Azure](../dma/media/AzureFeaturesParityReport.png)

Use este informe para resaltar las *características de nivel de instancia* que no son compatibles con Azure SQL Database V12.

Al seleccionar una característica en el gráfico de embudo, los datos de la parte inferior muestran las instancias y las características de base de datos que no se admiten. En el ejemplo siguiente, esta característica está seleccionada: **no se admite la configuración de grupos de disponibilidad AlwaysOn en Azure SQL Database**.  

![Característica de grupo de disponibilidad AlwaysOn](../dma/media/Feature_AlwaysOnAvailability.png)

 
### <a name="azure-sql-db-unsupported-features-report"></a>Informe de características no admitidas de Azure SQL Database

![Informe de características no admitidas de Azure SQL Database](../dma/media/AzureSQLDBUnsupportedFeaturesReport.png)

Este informe resalta las características que no son compatibles con una **base de datos** determinada cuando el destino es Azure SQL Database (V12).

Al filtrar por el nombre de la base de datos y el valor de la característica en el gráfico de embudo, puede ver los detalles de la característica no admitida. Los detalles incluyen el objeto afectado y las recomendaciones para solucionar el problema.

Por ejemplo, el filtrado por la base de datos de DTC y **las bases de datos de solo lectura no**se pueden actualizar, puede ver una lista de los objetos afectados.

![No se puede actualizar la base de datos de solo lectura](../dma/media/ReadOnlyDatabases.png)

## <a name="see-also"></a>Vea también

[Información general de Data Migration Assistant](../dma/dma-overview.md)

[Descargar Data Migration Assistant](https://www.microsoft.com/download/details.aspx?id=53595)

[Descargar Power BI](https://powerbi.microsoft.com/)
