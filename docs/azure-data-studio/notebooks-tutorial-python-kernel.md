---
title: Cuadernos con kernel de Python en Azure Data Studio
description: En este tutorial se muestra cómo crear y ejecutar un cuaderno de Python.
author: garyericson
ms.author: garye
ms.reviewer: mikeray, alayu, maghan
ms.topic: tutorial
ms.prod: azure-data-studio
ms.technology: ''
ms.custom: ''
ms.date: 04/27/2020
ms.openlocfilehash: e4c431cba395b8e0c732fa7ac4ab96942cac7144
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85728861"
---
# <a name="create-and-run-a-python-notebook"></a>Creación y ejecución de un cuaderno de Python

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

En este tutorial se muestra cómo crear y ejecutar un cuaderno en Azure Data Studio con Python.

## <a name="prerequisites"></a>Prerrequisitos

- [Azure Data Studio instalado](download-azure-data-studio.md)

## <a name="new-notebook"></a>Nuevo cuaderno

En los pasos siguientes, se muestra cómo crear un archivo de cuaderno en Azure Data Studio:

1. Abra Azure Data Studio. Si se le pide que se conecte a un servidor SQL Server, puede conectarse o hacer clic en **Cancelar**.

1. Seleccione **Nuevo cuaderno** en el menú **Archivo**.

1. Seleccione **Python 3** para **Kernel**.

   :::image type="content" source="media/notebook-tutorial-python/set-kernel-and-attach-to-python.png" alt-text="Establecimiento del kernel":::

1. Si se le pide que configure Python, en **Configurar Python para Notebooks**, seleccione una de las dos opciones siguientes:

   - **Nueva instalación de Python**, para instalar una nueva copia de Python para Azure Data Studio;
   - **Usar la instalación de Python existente**, para especificar la ruta de acceso a una instalación existente de Python.

## <a name="run-a-notebook-cell"></a>Ejecución de una celda del cuaderno

Puede crear celdas que contengan código o texto. Puede ejecutar una celda de código en contexto; los resultados se mostrarán en el cuaderno cuando la celda haya terminado de ejecutarse. Las celdas de texto permiten intercalar documentación con formato con el código.

### <a name="code"></a>Código

Puede agregar una nueva celda de código de Python seleccionando el comando **+Código** de la barra de herramientas.

:::image type="content" source="media/notebook-tutorial-python/notebook-toolbar-python.png" alt-text="Barra de herramientas del cuaderno":::

En este ejemplo se realiza una sencilla operación matemática.

```python
a = 1
b = 2
c = a/b
print(c)
```
Ejecute la celda haciendo clic en el botón de reproducción situado a la izquierda de la celda. Los resultados aparecen en la parte inferior.

:::image type="content" source="media/notebook-tutorial-python/run-notebook-cell-python.png" alt-text="Ejecución de la celda del cuaderno":::

### <a name="text"></a>Texto

Para agregar una nueva celda de texto, seleccione el comando **+Texto** de la barra de herramientas.

:::image type="content" source="media/notebook-tutorial-python/notebook-toolbar-python-text.png" alt-text="Barra de herramientas del cuaderno":::

La celda cambia al modo de edición y ahora se puede escribir Markdown y ver la versión preliminar al mismo tiempo.

:::image type="content" source="media/notebook-tutorial-python/notebook-markdown-cell-python.png" alt-text="Celda de Markdown":::

Al seleccionar fuera de la celda de texto, solo se muestra el texto de Markdown.

:::image type="content" source="media/notebook-tutorial-python/notebook-markdown-preview-python.png" alt-text="Texto de Markdown":::

## <a name="next-steps"></a>Pasos siguientes

Obtenga más información sobre los cuadernos:

- [Cómo usar cuadernos con SQL Server](notebooks-guidance.md)

- [Creación y ejecución de un cuaderno de SQL Server](notebooks-tutorial-sql-kernel.md)

- [Cómo se administran los cuadernos en Azure Data Studio](notebooks-manage-sql-server.md)
