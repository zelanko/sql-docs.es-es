---
title: Administración de cuadernos en Azure Data Studio
titleSuffix: SQL Server big data clusters
description: Aprenda a administrar cuadernos en Azure Data Studio. Esto incluye abrir cuadernos, guardarlos y cambiar la conexión del clúster de macrodatos.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 12/06/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 5417166ea69abe726f47b6bf2adede4b937d5b00
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/25/2019
ms.locfileid: "67958281"
---
# <a name="how-to-manage-notebooks-in-azure-data-studio"></a>Cómo administrar cuadernos en Azure Data Studio

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En este artículo se muestra cómo abrir y guardar archivos de cuaderno en Azure Data Studio con la versión preliminar de SQL Server 2019. También se muestra cómo cambiar la conexión al clúster de macrodatos de SQL Server.

## <a name="prerequisites"></a>Prerequisites

En este artículo se supone que ya tiene un cuaderno que quiere usar en Azure Data Studio. Si quiere crear un cuaderno, vea [Uso de los cuadernos en la versión preliminar de SQL Server 2019](notebooks-guidance.md). Para usar cuadernos en Azure Data Studio, debe cumplir los siguientes requisitos previos:

- [Implementar un clúster de macrodatos](quickstart-big-data-cluster-deploy.md).
- [Herramientas de macrodatos de SQL Server 2019](deploy-big-data-tools.md):
   - **Azure Data Studio**
   - **Extensión de SQL Server 2019**
   - **kubectl**

## <a name="open-a-notebook"></a>Apertura de un cuaderno

Hay varias maneras de abrir el cuadro de diálogo **Abrir cuaderno**. Puede usar el menú Archivo, el panel y la paleta de comandos. En las siguientes secciones se describe cada método.

### <a name="file-menu"></a>Menú Archivo

Seleccione **Abrir archivo** en el menú Archivo Ctrl + A (en Windows) y Cmd + A (en Mac).

![Apertura del cuadro de diálogo Abrir archivo mediante la selección de Abrir archivo](./media/notebooks-how-to-manage/open-file-1.png) 

### <a name="dashboard"></a>Panel

Haga clic en **Abrir cuaderno** en el panel para abrir el cuadro de diálogo Abrir archivo.

![Para abrir el cuadro de diálogo Abrir archivo, seleccione Abrir cuaderno en el panel.](./media/notebooks-how-to-manage/open-file-2.png) 

### <a name="command-palette"></a>Paleta de comandos

Use el comando **Archivo: Abrir** de la paleta de comandos al escribir Ctrl + Mayús + P (en Windows) y Cmd + Mayús + P (en Mac).

![Apertura del cuadro de diálogo Abrir archivo al escribir Archivo: Abrir en la paleta de comandos](./media/notebooks-how-to-manage/open-file-3.png)

## <a name="save-a-notebook"></a>Guardado de un cuaderno

Actualmente hay una manera de guardar un cuaderno. Debe seleccionar **Guardar** en la barra de herramientas del cuaderno.

![Guardado de archivo al hacer clic en Guardar en la barra de herramientas del cuaderno](./media/notebooks-how-to-manage/save-file-1.png)

> [!NOTE]
> Actualmente los siguientes métodos no guardan los cambios en los cuadernos:
>
> - **Archivo: Guardar**, **Archivo: Guardar como...** y **Archivo: Guardar todo** del menú Archivo.
> - Comandos **Archivo: Guardar** especificados en la paleta de comandos.

## <a name="change-the-big-data-cluster"></a>Cambio del clúster de macrodatos

Para cambiar el clúster de macrodatos de SQL Server de un cuaderno:

1. Haga clic en el menú **Asociar a** de la barra de herramientas del cuaderno.

   ![Clic en el menú Asociar a de la barra de herramientas del cuaderno](./media/notebooks-how-to-manage/select-attach-to-1.png)

2. Haga clic en un servidor en el menú **Asociar a**.

   ![Selección de un servidor desde el menú Asociar a](./media/notebooks-how-to-manage/select-attach-to-2.png)

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre los cuadernos en Azure Data Studio, vea [Uso de los cuadernos en la versión preliminar de SQL Server 2019](notebooks-guidance.md).