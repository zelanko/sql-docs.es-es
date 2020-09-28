---
title: Cuadernos con kernel de Kusto en Azure Data Studio
description: En este tutorial se muestra cómo crear un cuaderno de Python y ejecutarlo.
ms.topic: how-to
ms.prod: azure-data-studio
ms.technology: azure-data-studio
author: markingmyname
ms.author: maghan
ms.reviewer: jukoesma
ms.custom: ''
ms.date: 09/22/2020
ms.openlocfilehash: efcea597a431d33cfbd2978e36f3b95d27986772
ms.sourcegitcommit: 8f062015c2a033f5a0d805ee4adabbe15e7c8f94
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/25/2020
ms.locfileid: "91226965"
---
# <a name="create-and-run-a-kusto-kql-notebook-preview"></a>Creación y ejecución de un cuaderno de Kusto (KQL) (versión preliminar)

En este artículo se muestra cómo crear y ejecutar un [cuaderno de Azure Data Studio](../notebooks-guidance.md) mediante la [extensión de Kusto (KQL)](../extensions/kusto-extension.md), que se conecta a un clúster de Azure Data Explorer.

Con la extensión de Kusto (KQL), puede cambiar la opción de kernel a **Kusto**.

Esta funcionalidad actualmente está en su versión preliminar.

## <a name="prerequisites"></a>Requisitos previos

Si no tiene una suscripción a Azure, cree una [cuenta gratuita de Azure](https://azure.microsoft.com/free/) antes de empezar.

- [Clúster de Azure Data Explorer con una base de datos a la que puede conectarse](https://docs.microsoft.com/azure/data-explorer/create-cluster-database-portal).
- [Azure Data Studio](../download-azure-data-studio.md)
- [Extensión de Kusto (KQL) para Azure Data Studio](../extensions/kusto-extension.md).

## <a name="create-a-kusto-kql-notebook"></a>Creación de un cuaderno de Kusto (KQL)

En los pasos siguientes, se muestra cómo crear un archivo de cuaderno en Azure Data Studio:

1. En Azure Data Studio, conéctese al clúster de Azure Data Explorer.

2. Vaya al panel **Conexiones** y, en la ventana **Servidores**, haga clic con el botón secundario en la base de datos Kusto y seleccione *Nuevo cuaderno*. También puede ir a **Archivo** > **Nuevo cuaderno**.

   :::image type="content" source="media/notebooks-kusto-kernel/kusto-new-notebook.png" alt-text="Abrir el cuaderno":::

3. Seleccione *Kusto* para el **Kernel**. Confirme que el menú **Adjuntar a** está establecido en el nombre y la base de datos del clúster. En este artículo, usamos el clúster de help.kusto.windows.net con los datos de la base de datos Samples.

   :::image type="content" source="media/notebooks-kusto-kernel/set-kusto-kernel.png" alt-text="Establecer el Kernel y Conectar a":::

Puede guardar el cuaderno mediante los comandos **Guardar** o **Guardar como...** del menú **Archivo**.

Para abrir un cuaderno, puede usar el comando **Abrir archivo...** del menú **Archivo**, seleccionar **Abrir archivo** en la página de **bienvenida** o usar el comando **Archivo: Abrir** de la paleta de comandos.

## <a name="change-the-connection"></a>Cambio de conexión

Para cambiar la conexión Kusto de un cuaderno:

1. Seleccione el menú **Adjuntar a** en la barra de herramientas del cuaderno y elija **Cambiar conexión**.

   :::image type="content" source="media/notebooks-kusto-kernel/kusto-select-attach-to-change-connections.png" alt-text="cambio de conexiones":::

   > [!Note]
   > Asegúrese de que el valor de la base de datos se ha rellenado. Los cuadernos de Kusto requieren que la base de datos esté especificada.

2. Ahora puede seleccionar un servidor de conexión reciente o especificar nuevos detalles de conexión para conectarse.

   :::image type="content" source="media/notebooks-kusto-kernel/kusto-change-connection-cluster.png" alt-text="Selección de un clúster distinto":::

   > [!Note]
   > Especifique el nombre del clúster sin `https://`.

## <a name="run-a-code-cell"></a>Ejecución de una celda de código

Puede crear celdas que contengan consultas de KQL que puede ejecutar donde están mediante la selección del botón **Ejecutar celda** a la izquierda de la celda. Cuando la celda se ejecute, los resultados se mostrarán en el cuaderno.

Por ejemplo:

1. Para agregar una nueva celda de código, seleccione el comando **+Código** de la barra de herramientas.

   :::image type="content" source="media/notebooks-kusto-kernel/kusto-kernel-code.png" alt-text="Bloque de código del kernel de Kusto":::

2. Copie y pegue el ejemplo siguiente en la celda y seleccione **Ejecutar celda**. En este ejemplo se consultan los datos de StormEvents de un tipo de evento concreto.

   ```kusto
    StormEvents
    | where EventType == "Waterspout"
   ```

   :::image type="content" source="media/notebooks-kusto-kernel/run-kusto-notebook-cell.png" alt-text="Ejecución de una celda":::

## <a name="save-the-result-or-show-chart"></a>Guardado de un resultado o muestra del gráfico

Si ejecuta un script que devuelve un resultado, puede guardarlo en distintos formatos mediante la barra de herramientas que se muestra sobre el resultado.

- Guardar como CSV
- Guardar como Excel
- Guardar como JSON
- Guardar como XML
- Muestra del gráfico

```kusto
    StormEvents
    | limit 10
```

:::image type="content" source="media/notebooks-kusto-kernel/run-notebook-save-results.png" alt-text="Guardado de un resultado":::

## <a name="limitations-and-considerations"></a>Limitaciones y consideraciones

- Debe elegir una base de datos para el clúster de Azure Data Explorer antes de ejecutar una consulta Kusto.
- Si deja el clúster de Azure Data Explorer inactivo durante demasiado tiempo, este puede desconectarse.
    - Solución alternativa: Desconéctese del clúster y vuelva a conectarse.

## <a name="next-steps"></a>Pasos siguientes

Obtenga más información sobre los cuadernos:

- [Extensión de Kusto (KQL) para Azure Data Studio](../extensions/kusto-extension.md)
- [Uso de cuadernos en Azure Data Studio](../notebooks-guidance.md)
- [Creación y ejecución de un cuaderno de Python](../notebooks-tutorial-python-kernel.md)
- [Creación y ejecución de un cuaderno de SQL Server](../notebooks-tutorial-sql-kernel.md)
