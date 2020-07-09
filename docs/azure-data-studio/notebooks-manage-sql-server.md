---
title: Procedimiento para administrar un cuaderno
description: Aprenda a administrar cuadernos en Azure Data Studio. Esto incluye abrir cuadernos, guardarlos y cambiar la conexión de SQL o el kernel de Python.
author: markingmyname
ms.author: maghan
ms.reviewer: achatter, alayu, mikeray
ms.metadata: seo-lt-2019
ms.topic: conceptual
ms.prod: azure-data-studio
ms.technology: ''
ms.custom: ''
ms.date: 04/27/2020
ms.openlocfilehash: 326e0b0afc4809d13cf2fdfdbd76f53dafe1cbb9
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85774583"
---
# <a name="how-to-manage-notebooks-in-azure-data-studio"></a>Cómo administrar cuadernos en Azure Data Studio

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

En este artículo se muestra cómo abrir y guardar archivos de cuaderno en Azure Data Studio. También se muestra cómo cambiar la conexión a la instancia SQL Server o al kernel de Python.

## <a name="open-a-notebook"></a>Apertura de un cuaderno

Hay varias maneras de abrir el cuadro de diálogo **Abrir cuaderno**. Puede usar el menú Archivo, el panel y la paleta de comandos. En las siguientes secciones se describe cada método.

### <a name="file-menu"></a>Menú Archivo

Seleccione **Abrir archivo** en el menú Archivo Ctrl + A (en Windows) y Cmd + A (en Mac).

![Apertura del cuadro de diálogo Abrir archivo mediante la selección de Abrir archivo](./media/notebooks-manage-sql-server/open-file-1.png)

### <a name="dashboard"></a>Panel

Haga clic en **Abrir cuaderno** en el panel para abrir el cuadro de diálogo Abrir archivo.

![Para abrir el cuadro de diálogo Abrir archivo, seleccione Abrir cuaderno en el panel.](./media/notebooks-manage-sql-server/open-file-2.png) 

### <a name="command-palette"></a>Paleta de comandos

Use el comando **Archivo: Abrir** de la paleta de comandos al escribir Ctrl + Mayús + P (en Windows) y Cmd + Mayús + P (en Mac).

![Apertura del cuadro de diálogo Abrir archivo mediante Archivo: Abrir en la paleta de comandos](./media/notebooks-manage-sql-server/open-file-3.png)

## <a name="save-a-notebook"></a>Guardado de un cuaderno

Actualmente hay una manera de guardar un cuaderno. Seleccione **Guardar** en la barra de herramientas del cuaderno.

![Guardado de archivo al seleccionar Guardar en la barra de herramientas del cuaderno](./media/notebooks-manage-sql-server/save-file-1.png)

> [!NOTE]
> Actualmente los siguientes métodos no guardan los cambios en los cuadernos:
>
> - **Archivo: Guardar**, **Archivo: Guardar como...** y **Archivo: Guardar todo** del menú Archivo.
> - Comandos **Archivo: Guardar** especificados en la paleta de comandos.

## <a name="change-the-sql-connection"></a>Cambio de la conexión SQL

Para cambiar la conexión SQL de un cuaderno:

1. Seleccione el menú **Adjuntar a** en la barra de herramientas del cuaderno y elija **Cambiar conexión**.

   ![Clic en el menú Asociar a de la barra de herramientas del cuaderno](./media/notebooks-manage-sql-server/select-attach-to-1.png)

2. Ahora puede seleccionar un servidor de conexión reciente o especificar nuevos detalles de conexión para conectarse.

   ![Selección de un servidor desde el menú Asociar a](./media/notebooks-manage-sql-server/select-attach-to-2.png)

## <a name="change-the-python-kernel"></a>Cambio del kernel de Python

La primera vez que abra Azure Data Studio, se mostrará la página **Configurar Python para Notebooks**. Puede seleccionar una de las dos opciones siguientes:

- **Nueva instalación de Python**, para instalar una nueva copia de Python para Azure Data Studio;
- **Usar la instalación de Python existente**, para especificar la ruta de acceso a una instalación existente de Python para que Azure Data Studio la use.

Para ver la ubicación y la versión del kernel de Python activo, cree una celda de código y ejecute los siguientes comandos de Python:

```python
import os
import sys
print(sys.version_info)
print(os.path.dirname(sys.executable))
```

Para cambiar a otra instalación de Python:

1. En el menú **Archivo**, seleccione **Preferencias** y, después, **Configuración**.
1. Desplácese hasta **Configuración de Notebook** en **Extensiones**.
1. En **Usar la instalación de Python existente**, desactive la opción "Ruta de acceso local a una instalación de Python preexistente utilizada por Notebooks".
1. Reinicie Azure Data Studio.

Cuando se muestre la página **Configurar Python para Notebooks**, podrá crear una instalación de Python o especificar una ruta de acceso a una instalación existente.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre los cuadernos de SQL en Azure Data Studio, vea [Uso de los cuadernos en SQL Server 2019](notebooks-guidance.md).
