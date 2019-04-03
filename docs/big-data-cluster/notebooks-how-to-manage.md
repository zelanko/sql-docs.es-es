---
title: Administración de blocs de notas en Azure Data Studio
titleSuffix: SQL Server big data clusters
description: Obtenga información sobre cómo administrar los cuadernos en Azure Data Studio. Esto incluye la apertura de blocs de notas, guardarlos y cambiar la conexión de clúster de macrodatos.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 12/06/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: ab731e3f657a629dbb1b4058bd94b32677c2def0
ms.sourcegitcommit: 2de5446fbc57787f18a907dd5deb02a7831ec07d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/02/2019
ms.locfileid: "58860516"
---
# <a name="how-to-manage-notebooks-in-azure-data-studio"></a>Administración de blocs de notas en Azure Data Studio

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este artículo muestra cómo abrir y guardar archivos del Bloc de notas en Azure Data Studio con la versión preliminar de SQL Server 2019. También se muestra cómo cambiar la conexión a su clúster de macrodatos de SQL Server.

## <a name="prerequisites"></a>Requisitos previos

En este artículo se da por supuesto que ya tiene un bloc de notas que desea usar en Azure Data Studio. Si desea crear un bloc de notas, consulte [para usar cuadernos en versión preliminar de SQL Server 2019](notebooks-guidance.md). Para usar cuadernos en Azure Data Studio, debe cumplir los siguientes requisitos previos:

- [Implementar un clúster de macrodatos](quickstart-big-data-cluster-deploy.md).
- [Herramientas de SQL Server 2019 macrodatos](deploy-big-data-tools.md):
   - **Azure Data Studio **
   - **Extensión de SQL Server 2019**
   - **kubectl**

## <a name="open-a-notebook"></a>Abre un bloc de notas

Hay varias maneras de abrir el **Abrir Bloc de notas** cuadro de diálogo. Puede usar el menú archivo, el panel y la paleta de comandos. Las secciones siguientes describen cada método.

### <a name="file-menu"></a>Menú archivo

Seleccione **abrir archivo** en el menú archivo CTRL+o (en Windows) y Cmd + O (en Mac).

![Abrir el cuadro de diálogo Abrir archivo, seleccione Abrir archivo](./media/notebooks-how-to-manage/open-file-1.png) 

### <a name="dashboard"></a>Panel

Haga clic en **Abrir Bloc de notas** en el panel para abrir el cuadro de diálogo Abrir archivo.

![Abrir el cuadro de diálogo Abrir archivo, seleccione Abrir Bloc de notas en el panel](./media/notebooks-how-to-manage/open-file-2.png) 

### <a name="command-palette"></a>Paleta de comandos

Use el comando **archivo: Abra** desde la paleta de comandos escribiendo Ctrl + Mayús + P (en Windows) y Cmd + Mayús + P (en Mac).

![Abra el cuadro de diálogo Abrir archivo escribiendo File:Open en la paleta de comandos](./media/notebooks-how-to-manage/open-file-3.png)

## <a name="save-a-notebook"></a>Guarde un bloc de notas

Actualmente hay una manera de guardar un bloc de notas. Debe seleccionar **guardar** desde la barra de herramientas del Bloc de notas.

![Guarde el archivo haciendo clic en Guardar en la barra de herramientas del Bloc de notas](./media/notebooks-how-to-manage/save-file-1.png)

> [!NOTE]
> Actualmente los siguientes métodos no guarda los cambios en blocs de notas:
>
> - **Archivo/Guardar**, **archivo/Guardar como...**  y **archivo Guardar todo** comandos en el menú archivo.
> - **Archivo: Guardar** los comandos escritos en la paleta de comandos.

## <a name="change-the-big-data-cluster"></a>Cambiar el clúster de macrodatos

Para cambiar el clúster de macrodatos de SQL Server para un bloc de notas:

1. Haga clic en el **adjuntar a** menú de la barra de herramientas del Bloc de notas.

   ![Haga clic en la asociación al menú de la barra de herramientas del Bloc de notas](./media/notebooks-how-to-manage/select-attach-to-1.png)

2. Haga clic en un servidor desde el **adjuntar a** menú.

   ![Seleccione un servidor de la asociación al menú](./media/notebooks-how-to-manage/select-attach-to-2.png)

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información acerca de los cuadernos en Azure Data Studio, consulte [para usar cuadernos en versión preliminar de SQL Server 2019](notebooks-guidance.md).