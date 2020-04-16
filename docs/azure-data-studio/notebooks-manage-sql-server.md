---
title: Administración de un cuaderno de SQL Server
description: Aprenda a administrar cuadernos en Azure Data Studio. Esto incluye abrir cuadernos, guardarlos y cambiar la conexión del clúster de macrodatos.
author: markingmyname
ms.author: maghan
ms.reviewer: achatter, alayu, mikeray
ms.metadata: seo-lt-2019
ms.topic: conceptual
ms.prod: sql
ms.technology: azure-data-studio
ms.custom: ''
ms.date: 03/30/2020
ms.openlocfilehash: 9b071a9d1b9e770e1443e5df539208baa4399a30
ms.sourcegitcommit: 1124b91a3b1a3d30424ae0fec04cfaa4b1f361b6
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/01/2020
ms.locfileid: "80531598"
---
# <a name="how-to-manage-notebooks-in-azure-data-studio"></a>Cómo administrar cuadernos en Azure Data Studio

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En este artículo se muestra cómo abrir y guardar archivos de cuaderno en Azure Data Studio con SQL Server. También se muestra cómo cambiar la conexión a SQL Server.

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

## <a name="change-the-connection"></a>Cambio de conexión

Para cambiar la conexión de un cuaderno:

1. Seleccione el menú **Adjuntar a** en la barra de herramientas del cuaderno y elija **Cambiar conexión**.

   ![Clic en el menú Asociar a de la barra de herramientas del cuaderno](./media/notebooks-manage-sql-server/select-attach-to-1.png)

2. Ahora puede seleccionar un servidor de conexión reciente o especificar nuevos detalles de conexión para conectarse.

   ![Selección de un servidor desde el menú Asociar a](./media/notebooks-manage-sql-server/select-attach-to-2.png)

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre los cuadernos en Azure Data Studio, vea [Uso de los cuadernos en SQL Server 2019](notebooks-guidance.md).
