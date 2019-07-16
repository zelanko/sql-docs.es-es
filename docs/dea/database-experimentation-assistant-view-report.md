---
title: Ver informes de análisis en el Asistente de experimentación de base de datos para las actualizaciones de SQL Server
description: Ver informes de análisis en el Asistente de experimentación de base de datos
ms.custom: ''
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
ms.openlocfilehash: 066297daff3393304b83b77238277f873e1c97fb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68050449"
---
# <a name="view-analysis-reports-in-database-experimentation-assistant"></a>Ver informes de análisis en el Asistente de experimentación de base de datos

Después de [crear el informe de análisis](database-experimentation-assistant-create-report.md) en base de datos experimentación Assistant (DEA), complete los pasos descritos en este artículo para ver el informe y obtener información de rendimiento de su prueba A/b.

## <a name="select-a-server"></a>Seleccione un servidor

En DEA, seleccione el icono de menú. En el menú expandido, seleccione **informes de análisis** junto al icono de la lista de comprobación para abrir la ventana de informes de análisis.

En **informes de análisis de**, escriba el nombre de un equipo que ejecuta SQL Server que tiene una base de datos de análisis. Seleccione **Conectar**. 

![Conectarse a un informe existente](./media/database-experimentation-assistant-view-report/dea-view-report-connect.png)

Si faltan las dependencias, el **requisitos previos** le pide página con vínculos a instalarlos. Instalar los requisitos previos y, a continuación, seleccione **intentarlo**.

![Página de requisitos previos](./media/database-experimentation-assistant-view-report/dea-view-report-prereq.png)

## <a name="select-an-analysis-report-to-view"></a>Seleccione un informe de análisis para ver

En la lista de informes de análisis, haga doble clic en un informe para abrirlo.

![Ver un informe existente](./media/database-experimentation-assistant-view-report/dea-view-report-view-existing.png)

Puede obtener información sobre cómo se representa la carga de trabajo, como se muestra en este gráfico de ejemplo:

![Gráficos del representante de la carga de trabajo](./media/database-experimentation-assistant-view-report/dea-view-report-workload-compare.png)

## <a name="view-and-understand-the-analysis-report"></a>Ver y entender el informe de análisis

En esta sección le guiará a través del informe de análisis.

### <a name="query-categories"></a>Categorías de consulta

Seleccione los distintos segmentos del gráfico circular izquierdo para mostrar solo las consultas que se encuentran en esa categoría.

![Informes gráficos circulares](./media/database-experimentation-assistant-view-report/dea-view-report-pie-slices.png)

- **Degradado consultas**: Consultas que realizan mejor en el que en B.  
- **Errores**: Consultas que se muestran errores en la instancia B pero no en la instancia de A.  
- **Mejorar las consultas**: Consultas que se ejecutaron mejor en la instancia B que en la instancia de A.  
- **Las consultas indeterminadas**: Consultas que han tenido un cambio de rendimiento indeterminado.  
- **Mismo**: Consultas en el que rendimiento sigue siendo igual en todas las instancias A y B.

### <a name="individual-query-drill-down"></a>Exploración en profundidad de consulta individual

Puede seleccionar los vínculos de la plantilla de consulta para ver información más detallada sobre consultas concretas.

![Consulta de exploración en profundidad](./media/database-experimentation-assistant-view-report/dea-view-report-drilldown.png)

Seleccione una consulta específica para abrir una comparación de resumen para la consulta.

![Resumen de comparación](./media/database-experimentation-assistant-view-report/dea-view-report-comparison-summary.png)

Puede ver las instancias de A y B que se ejecutó la consulta en. También puede ver una plantilla del aspecto que podría tener la consulta. Una tabla muestra información de consulta que es específico de instancias A y B.

### <a name="error-queries"></a>Consultas de error

El informe de resumen de comparación tiene expandible **información de Error** y **información del Plan de consulta** secciones. Las secciones muestran los errores e información para ambas instancias del plan.

Seleccione el gráfico circular de error (rojo) para mostrar estos tipos de errores:
- **Los errores existentes**: Errores que estaban en A.
- **Nuevos errores**: Errores que estaban en B.
- **Resolver errores**: Errores que estaban en una, pero no en B.

![Gráficos de error](./media/database-experimentation-assistant-view-report/dea-view-report-error-charts.png)

## <a name="next-steps"></a>Pasos siguientes

- Para obtener información sobre cómo generar un informe de análisis en un símbolo del sistema, consulte [ejecutar en el símbolo del sistema](database-experimentation-assistant-run-command-prompt.md).

- Para obtener una introducción minutos 19 DEA y demostración, vea el vídeo siguiente:

  > [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-Database-Experimentation-Assistant/player]
