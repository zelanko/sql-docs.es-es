---
title: Cuadernos con Kqlmagic (lenguaje de consulta Kusto) en Azure Data Studio
description: En este tutorial se muestra cómo crear y ejecutar Kqlmagic en Azure Data Studio.
author: markingmyname
ms.author: maghan
ms.reviewer: jukoesma
ms.topic: tutorial
ms.prod: azure-data-studio
ms.technology: ''
ms.custom: ''
ms.date: 04/27/2020
ms.openlocfilehash: 2ee07ea6d3999d7ab3f0c32f7d5d47e1429f844d
ms.sourcegitcommit: 8515bb2021cfbc7791318527b8554654203db4ad
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/08/2020
ms.locfileid: "86091875"
---
# <a name="kqlmagic-extension-in-azure-data-studio"></a>Extensión Kqlmagic en Azure Data Studio

**Kqlmagic** es un comando que amplía las capacidades del kernel de Python en **[cuadernos de Azure Data Studio](notebooks-guidance.md)** . Puede combinar Python y el **[lenguaje de consulta Kusto (KQL)](https://docs.microsoft.com/azure/data-explorer/kusto/query)** para consultar y ver datos mediante la biblioteca Plot.ly enriquecida integrada con comandos de `render`. Kqlmagic ofrece la ventaja de reunir los cuadernos, el análisis de datos y las completas funcionalidades de Python en la misma ubicación. Entre los orígenes de datos compatibles con Kqlmagic se incluyen **[Azure Data Explorer](https://docs.microsoft.com/azure/data-explorer/data-explorer-overview)** , **[Application Insights](https://docs.microsoft.com/azure/azure-monitor/app/app-insights-overview)** y **[registros de Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/platform/data-platform-logs)** .

En este artículo se muestra cómo crear y ejecutar un cuaderno en Azure Data Studio con la extensión Kqlmagic para un clúster de Azure Data Explorer, un registro de Application Insights y registros de Azure Monitor.

## <a name="prerequisites"></a>Requisitos previos

- [Azure Data Studio](download-azure-data-studio.md)
- [Python](https://www.python.org/downloads/)

## <a name="install-and-set-up-kqlmagic-in-a-notebook"></a>Instalación y configuración de Kqlmagic en un cuaderno

Todos los pasos de esta sección se ejecutan en un cuaderno de Azure Data Studio.

1. Cree un cuaderno y cambie el **Kernel** a *Python 3*.

   ![Nuevo cuaderno](media/notebooks-kql-magic/install-new-notebook.png)

2. Cuando se le pida, seleccione **Sí** para actualizar los paquetes de Python.

   ![Sí](media/notebooks-kql-magic/install-python-yes.png)

3. Instalar Kqlmagic:

   ```python
   !pip install Kqlmagic --no-cache-dir --upgrade
   ```

   Compruebe que está instalado:

   ```python
   !pip list
   ```

   ![List](media/notebooks-kql-magic/install-list.png)

4. Cargar Kqlmagic:

   ```python
   %reload_ext Kqlmagic
   ```

   > [!Note]
   > Si se produce un error en este paso, cierre el archivo y vuelva a abrirlo.

   ![Carga de la extensión Kqlmagic](media/notebooks-kql-magic/install-load-kql-magic-ext.png)

5. Puede comprobar si Kqlmagic se carga correctamente examinando la documentación de ayuda o comprobando la versión.

   ```python
   %kql --help "help"
   ```

   > [!Note]
   > Si `Samples@help` solicita una contraseña, puede dejarla en blanco y presionar **Entrar**.

   ![Ayuda](media/notebooks-kql-magic/install-help.png)

   Para ver qué versión de Kqlmagic está instalada, ejecute el comando siguiente.

   ```python
   %kql --version
   ```

## <a name="kqlmagic-with-an-azure-data-explorer-cluster"></a>Kqlmagic con un clúster de Azure Data Explorer

En esta sección se explica cómo ejecutar el análisis de datos mediante Kqlmagic con un clúster de Azure Data Explorer.

### <a name="load-and-authenticate-kqlmagic-for-azure-data-explorer"></a><a name="ade-load-auth"></a> Carga y autenticación de Kqlmagic para Azure Data Explorer

   > [!Note]
   > Cada vez que cree un cuaderno en Azure Data Studio, debe cargar la extensión Kqlmagic.

1. Compruebe que el **Kernel** está establecido en *Python 3*.

   ![Nuevo cuaderno](media/notebooks-kql-magic/change-kernel.png)

2. Cargar Kqlmagic:

   ```python
   %reload_ext Kqlmagic
   ```

   ![Carga de la extensión Kqlmagic](media/notebooks-kql-magic/install-load-kql-magic-ext.png)

3. Conéctese al clúster y autentíquese:

   ```python
   %kql azureDataExplorer://code;cluster='help';database='Samples'
   ```

   Utilice Inicio de sesión del dispositivo para autenticarse. Copie el código de la salida y seleccione **Autenticar**, lo que abre un explorador donde tiene que pegar el código. Cuando se haya autenticado correctamente, puede volver a Azure Data Studio para continuar con el resto del script.

   ![Autenticación en Azure Data Explorer](media/notebooks-kql-magic/ade-auth.png)

### <a name="query-and-visualize-for-azure-data-explorer"></a>Consulta y vista de Azure Data Explorer

Consulte datos mediante el [operador “render”](https://docs.microsoft.com/azure/data-explorer/kusto/query/renderoperator) y visualice datos mediante la biblioteca de ploy.ly. Esta consulta y visualización proporciona una experiencia integrada que usa KQL de forma nativa.

1. Analice los 10 eventos principales de Storm por estado y frecuencia:

   ```python
   %kql StormEvents | summarize count() by State | sort by count_ | limit 10
   ```

   Si está familiarizado con el lenguaje de consulta Kusto (KQL), puede escribir la consulta después de `%kql`.

   ![Análisis de eventos de Storm](media/notebooks-kql-magic/ade-analyze-storm-events.png)

2. Vea un gráfico de escala de tiempo:

   ```python
   %kql StormEvents \
   | summarize event_count=count() by bin(StartTime, 1d) \
   | render timechart title= 'Daily Storm Events'
   ```

   ![Vista del gráfico de tiempo](media/notebooks-kql-magic/ade-visualize-timechart.png)

3. Ejemplo de consulta multilínea con `%%kql`.

   ```python
   %%kql
   StormEvents
   | summarize count() by State
   | sort by count_
   | limit 10
   | render columnchart title='Top 10 States by Storm Event count'
   ```

   ![Ejemplo de consulta multilínea](media/notebooks-kql-magic/ade-multiline-query-sample.png)

## <a name="kqlmagic-with-application-insights"></a>Kqlmagic con Application Insights

### <a name="load-and-authenticate-kqlmagic-for-application-insights"></a><a name="appin-load-auth"></a> Carga y autenticación de Kqlmagic para Application Insights

1. Compruebe que el **Kernel** está establecido en *Python 3*.

   ![Nuevo cuaderno](media/notebooks-kql-magic/change-kernel.png)

2. Cargar Kqlmagic:

   ```python
   %reload_ext Kqlmagic
   ```

   ![Carga de la extensión Kqlmagic](media/notebooks-kql-magic/install-load-kql-magic-ext.png)

   > [!Note]
   > Cada vez que cree un cuaderno en Azure Data Studio, debe cargar la extensión Kqlmagic.

3. Conexión y autenticación.

   En primer lugar, debe generar una clave de API para el recurso de Application Insights. Después, use el identificador de aplicación y la clave de API para conectarse a Application Insights desde el cuaderno:

   ```python
   %kql appinsights://appid='DEMO_APP';appkey='DEMO_KEY'
   ```


### <a name="query-and-visualize-for-application-insights"></a>Consulta y vista de Application Insights

Consulte datos mediante el [operador “render”](https://docs.microsoft.com/azure/data-explorer/kusto/query/renderoperator) y visualice datos mediante la biblioteca de ploy.ly. Esta consulta y visualización proporciona una experiencia integrada que usa KQL de forma nativa.

1. Muestre vistas de página:

   ```python
   %%kql
   pageViews
   | limit 10
   ```

   ![Vistas de página](media/notebooks-kql-magic/appin-page-views.png)

   > [!Note]
   > Use el mouse para arrastrar un área del gráfico para acercar las fechas específicas.

2. Muestre vistas de página en un gráfico de escala de tiempo:

   ```python
   %%kql
   pageViews
   | summarize event_count=count() by name, bin(timestamp, 1d)
   | render timechart title= 'Daily Page Views'
   ```

   ![Gráfico de escala de tiempo](media/notebooks-kql-magic/appin-timechart.png)

## <a name="kqlmagic-with-azure-monitor-logs"></a>Kqlmagic con registros de Azure Monitor

### <a name="load-and-authenticate-kqlmagic-for-azure-monitor-logs"></a><a name="aml-load-auth"></a> Carga y autenticación de Kqlmagic para registros de Azure Monitor

1. Compruebe que el **Kernel** está establecido en *Python 3*.

   ![Nuevo cuaderno](media/notebooks-kql-magic/change-kernel.png)

2. Cargar Kqlmagic:

   ```python
   %reload_ext Kqlmagic
   ```

   ![Carga de la extensión Kqlmagic](media/notebooks-kql-magic/install-load-kql-magic-ext.png)

   > [!Note]
   > Cada vez que cree un cuaderno en Azure Data Studio, debe cargar la extensión Kqlmagic.

3. Conéctese y autentíquese:

   ```python
   %kql loganalytics://workspace='DEMO_WORKSPACE';appkey='DEMO_KEY';alias='myworkspace'
   ```

   ![Autenticación en Log Analytics](media/notebooks-kql-magic/aml-auth.png)

### <a name="query-and-visualize-for-azure-monitor-logs"></a>Consulta y vista de registros de Azure Monitor

Consulte datos mediante el [operador “render”](https://docs.microsoft.com/azure/data-explorer/kusto/query/renderoperator) y visualice datos mediante la biblioteca de ploy.ly. Esta consulta y visualización proporciona una experiencia integrada que usa KQL de forma nativa.

1. Vea un gráfico de escala de tiempo:

   ```python
   %%kql
   KubeNodeInventory
   | summarize event_count=count() by Status, bin(TimeGenerated, 1d)
   | render timechart title= 'Daily Kubernetes Nodes'
   ```

   ![Gráfico de tiempo de nodos de Kubernetes diarios de Log Analytics](media/notebooks-kql-magic/aml-timechart-daily-kubernetes-nodes.png)

## <a name="next-steps"></a>Pasos siguientes

Obtenga más información sobre los cuadernos y Kqlmagic:

- [Uso de Jupyter Notebook y una extensión Kqlmagic para analizar datos en Azure Data Explorer](https://docs.microsoft.com/azure/data-explorer/Kqlmagic)
- [Extensión (magic) en Jupyter Notebook y Jupyter Lab, que habilita la experiencia del cuaderno al trabajar con datos de Kusto, Application Insights y LogAnalytics](https://github.com/Microsoft/jupyter-Kqlmagic)
- [Kqlmagic](https://pypi.org/project/Kqlmagic/)
- [KustoMagicSamples](https://notebooks.azure.com/RknDzgn/projects/KustoMagicSamples/html/Getting%20Started%20with%20Kqlmagic%20on%20Azure%20Data%20Explorer-Copy.ipynb)
- [Procedimiento para usar cuadernos](notebooks-guidance.md)
- [Cómo se administran los cuadernos en Azure Data Studio](notebooks-manage-sql-server.md)
