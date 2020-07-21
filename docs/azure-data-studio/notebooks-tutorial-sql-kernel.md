---
title: Cuadernos con kernel de SQL en Azure Data Studio
description: En este tutorial se muestra cómo crear y ejecutar un cuaderno de SQL Server.
author: markingmyname
ms.author: maghan
ms.reviewer: mikeray, alayu
ms.topic: tutorial
ms.prod: azure-data-studio
ms.technology: ''
ms.custom: ''
ms.date: 03/30/2020
ms.openlocfilehash: 64e5bcfa188707e784d33a6504b120c4ce0ea553
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85735324"
---
# <a name="create-and-run-a-sql-server-notebook"></a>Creación y ejecución de un cuaderno de SQL Server

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

En este tutorial se muestra cómo crear y ejecutar un cuaderno en Azure Data Studio con SQL Server.

## <a name="prerequisites"></a>Prerrequisitos

- [Azure Data Studio instalado](download-azure-data-studio.md)
- SQL Server instalado
  - [Windows](../database-engine/install-windows/install-sql-server.md)
  - [Linux](../linux/sql-server-linux-setup.md)

## <a name="new-notebook"></a>Nuevo cuaderno

En los pasos siguientes, se muestra cómo crear un archivo de cuaderno en Azure Data Studio:

1. En Azure Data Studio, conéctese a su instancia de SQL Server.

2. Seleccione las **Conexiones** en la ventana **Servidores**. Después, seleccione **Nuevo cuaderno**.

   ![Abrir el cuaderno](media/notebook-tutorial/azure-data-studio-open-notebook.png)

3. Espere hasta que se rellenen el **Kernel** y el contexto del destino (**Conectar a**). Confirme que el **Kernel** está establecido en **SQL** y establezca **Adjuntar a** para la instancia de SQL Server (en este caso, su *localhost*).

   ![Establecer el Kernel y Conectar a](media/notebook-tutorial/set-kernel-and-attach-to.png)

## <a name="run-a-notebook-cell"></a>Ejecución de una celda del cuaderno

Para ejecutar cada celda del cuaderno, pulse el botón Reproducir a la izquierda de la celda. Cuando la celda termine de ejecutarse, los resultados se mostrarán en el cuaderno.

### <a name="code"></a>Código

Para agregar una nueva celda de código, seleccione el comando **+Código** de la barra de herramientas.

![Barra de herramientas de los cuaderno](media/notebooks-guidance/notebook-toolbar.png)

En este ejemplo se crea una base de datos.

```sql
USE master
GO

   -- Drop the database if it already exists
IF  EXISTS (
        SELECT name
        FROM sys.databases
        WHERE name = N'TestNotebookDB'
   )
DROP DATABASE TestNotebookDB
GO

-- Create the database
CREATE DATABASE TestNotebookDB
GO
```

   ![Ejecutar la celda del cuaderno](media/notebook-tutorial/run-notebook-cell.png)

Si ejecuta un script que devuelve un resultado, puede guardar este en formatos diferentes.

- Guardar como CSV
- Guardar como Excel
- Guardar como JSON
- Guardar como XML

En este caso, se devuelve el resultado de [PI](../t-sql/functions/pi-transact-sql.md).

```sql
SELECT PI() AS PI;
GO
```

![Ejecutar la celda del cuaderno](media/notebook-tutorial/run-notebook-cell-2.png)

### <a name="text"></a>Texto

Para agregar una nueva celda de texto, seleccione el comando **+Texto** de la barra de herramientas.

![Barra de herramientas de los cuaderno](media/notebooks-guidance/notebook-toolbar.png)

La celda cambia al modo de edición; ahora escriba Markdown para ver la versión preliminar al mismo tiempo.

![Celda de Markdown](media/notebooks-guidance/notebook-markdown-cell.png)

Al seleccionar fuera de la celda de texto, se muestra el texto de Markdown.

![Texto de Markdown](media/notebooks-guidance/notebook-markdown-preview.png)

## <a name="next-steps"></a>Pasos siguientes

Obtenga más información sobre los cuadernos:

- [Cómo usar cuadernos con SQL Server](notebooks-guidance.md)

- [Cómo se administran los cuadernos en Azure Data Studio](notebooks-manage-sql-server.md)

- [Ejecución de un cuaderno de ejemplo con Spark](../big-data-cluster/notebooks-tutorial-spark.md)