---
title: Ver informes de análisis para actualizaciones de SQL Server
description: Ver informes de análisis en Asistente para experimentación con bases de datos
ms.custom: seo-lt-2019
ms.date: 10/22/2018
ms.prod: sql
ms.prod_service: dea
ms.suite: sql
ms.technology: dea
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: HJToland3
ms.author: ajaykar
ms.reviewer: mathoma
ms.openlocfilehash: fddc71bf7cdf7686154b4f9b5612cf671ca64fce
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056661"
---
# <a name="view-analysis-reports-in-database-experimentation-assistant"></a>Ver informes de análisis en Asistente para experimentación con bases de datos

Después de [crear el informe de análisis](database-experimentation-assistant-create-report.md) en Asistente para experimentación con bases de datos (DEA), complete los pasos descritos en este artículo para ver el informe y obtener información de rendimiento proporcionada por la prueba A/B.

## <a name="select-a-server"></a>Seleccionar un servidor

En DEA, seleccione el icono de menú. En el menú expandido, seleccione **informes de análisis** junto al icono de lista de comprobación para abrir la ventana informes de análisis.

En **informes de análisis**, escriba el nombre de un equipo que ejecute SQL Server que tenga una base de datos de análisis. Seleccione **Conectar**. 

![Conectarse a un informe existente](./media/database-experimentation-assistant-view-report/dea-view-report-connect.png)

Si faltan dependencias, la página **requisitos previos** le pedirá vínculos para instalarlas. Instale los requisitos previos y, a continuación, seleccione Volver **a intentarlo**.

![Página requisitos previos](./media/database-experimentation-assistant-view-report/dea-view-report-prereq.png)

## <a name="select-an-analysis-report-to-view"></a>Seleccionar un informe de análisis para verlo

En la lista de informes de análisis, haga doble clic en un informe para abrirlo.

![Ver informe existente](./media/database-experimentation-assistant-view-report/dea-view-report-view-existing.png)

Puede obtener información sobre el grado de representación de la carga de trabajo, como se muestra en este gráfico de ejemplo:

![Gráficos de representación de carga de trabajo](./media/database-experimentation-assistant-view-report/dea-view-report-workload-compare.png)

## <a name="view-and-understand-the-analysis-report"></a>Ver y entender el informe de análisis

Esta sección le guía a través del informe de análisis.

### <a name="query-categories"></a>Categorías de consulta

Seleccione distintos sectores del gráfico circular izquierdo para mostrar solo las consultas que se encuentran bajo esa categoría.

![Segmentos del gráfico circular](./media/database-experimentation-assistant-view-report/dea-view-report-pie-slices.png)

- **Consultas degradadas**: consultas que se realizaron mejor en un que en B.  
- **Errores**: consultas que muestran errores en la instancia B pero no en la instancia A.  
- **Consultas mejoradas**: consultas que se ejecutaron mejor en la instancia B que en la instancia a.  
- **Consultas indeterminadas**: consultas con un cambio de rendimiento indeterminado.  
- Lo **mismo**: consultas en las que el rendimiento ha permanecido igual en las instancias a y B.

### <a name="individual-query-drill-down"></a>Obtención de detalles de consulta individual

Puede seleccionar los vínculos de la plantilla de consulta para ver información más detallada sobre consultas específicas.

![Obtención de detalles de consultas](./media/database-experimentation-assistant-view-report/dea-view-report-drilldown.png)

Seleccione una consulta específica para abrir un resumen de comparación de la consulta.

![Resumen de comparación](./media/database-experimentation-assistant-view-report/dea-view-report-comparison-summary.png)

Puede ver las instancias A y B en las que se ejecutó la consulta. También puede ver una plantilla del aspecto que podría tener la consulta. Una tabla muestra información de consulta específica de las instancias a y B.

### <a name="error-queries"></a>Consultas de error

El informe de Resumen de comparación tiene secciones de información de **error** y de **plan de consulta** expansibles. En las secciones se muestran los errores y la información del plan para ambas instancias.

Seleccione el gráfico de error (rojo) para mostrar estos tipos de errores:
- **Errores existentes**: errores que estaban en un.
- **Nuevos errores**: errores que se encontraban en B.
- **Errores resueltos**: errores que estaban en, pero no en B.

![Gráficos de error](./media/database-experimentation-assistant-view-report/dea-view-report-error-charts.png)

## <a name="next-steps"></a>Pasos siguientes

- Para obtener información sobre cómo generar un informe de análisis en un símbolo del sistema, vea [ejecutar en el símbolo del sistema](database-experimentation-assistant-run-command-prompt.md).

- Para obtener una introducción de 19 minutos a DEA y demostraciones, vea el siguiente vídeo:

  > [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-Database-Experimentation-Assistant/player]
