---
title: Copia de seguridad y restaurar una base de datos con las operaciones de SQL Studio (versión preliminar) | Documentos de Microsoft
description: Obtenga información acerca de cómo una copia de seguridad y restaurar una base de datos con las operaciones de SQL Studio (versión preliminar)
ms.custom: tools|sos
ms.date: 11/15/2017
ms.prod: sql
ms.reviewer: alayu; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: tutorial
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: df4eca076f18ce5b75a36d05c8ee26965d6a3bae
ms.sourcegitcommit: b3bb41424249de198f22d9c6d40df4996f083aa6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/18/2018
---
# <a name="backup-and-restore-using-includename-sosincludesname-sos-shortmd"></a>Copia de seguridad y restauración con [!INCLUDE[name-sos](../includes/name-sos-short.md)]

En este tutorial, aprenderá a utilizar [!INCLUDE[name-sos](../includes/name-sos-short.md)] para:
> [!div class="checklist"]
> * Copia de seguridad de una base de datos 
> * Puede ver el estado de copia de seguridad
> * Generar el script utilizado para realizar la copia de seguridad
> * Restaurar una base de datos
> * Ver el estado de la tarea de restauración

## <a name="prerequisites"></a>Prerequisites

Este tutorial requiere que el servidor SQL *TutorialDB*. Para crear el *TutorialDB* base de datos, complete uno de los siguientes tutoriales:

- [Conectarse y consultar mediante SQL Server [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-server.md)


## <a name="backup-a-database"></a>Copia de seguridad de una base de datos

1. Abra el panel de la base de datos TutorialDB (abra la **servidores** sidebar (**CTRL + G**), expanda **bases de datos**, haga clic en **TutorialDB**, y seleccione **administrar**). 

2. Abra la **base de datos de copia de seguridad** diálogo (haga clic en **copia de seguridad** en el **tareas** widget).

   ![Widget de tareas](./media/tutorial-backup-restore-sql-server/tasks.png)

3. Este tutorial utiliza las opciones de copia de seguridad de forma predeterminada, haga clic en **copia de seguridad**.
   ![cuadro de diálogo copia de seguridad](./media/tutorial-backup-restore-sql-server/backup-dialog.png)

Después de hacer clic **copia de seguridad**, **base de datos de copia de seguridad** diálogo desaparece y comienza el proceso de copia de seguridad.

## <a name="view-the-backup-status-and-view-the-backup-script"></a>Ver el estado de la copia de seguridad y la secuencia de comandos de copia de seguridad

1. Abra la **historial de tareas** sidebar, haga clic en el icono de reloj en la *barra de acciones* o presione **CTRL+T**.

   ![Historial de tareas](./media/tutorial-backup-restore-sql-server/task-history.png)

2. Para ver la secuencia de comandos de copia de seguridad en el editor, haga clic en **base de datos de copia de seguridad se realizó correctamente** y seleccione **Script**.

   ![secuencia de comandos de copia de seguridad](./media/tutorial-backup-restore-sql-server/task-script.png) 

## <a name="restore-a-database-from-a-backup-file"></a>Restaurar una base de datos desde un archivo de copia de seguridad


1. Abra la **servidores** sidebar (**CTRL + G**), haga clic en el servidor y seleccione **administrar**. 

2. Abra la **Restaurar base de datos** diálogo (haga clic en **restaurar** en el **tareas** widget).

2. Seleccione **archivo de copia de seguridad** en el **restaurar a partir de** campo. 

3. Haga clic en el botón de puntos suspensivos (...) en el **ruta de acceso de archivo de copia de seguridad** campo y seleccione el archivo de copia de seguridad más reciente para *TutorialDB*.

3. Tipo de **TutorialDB_Restored** en el **base de datos de destino** campo el **destino** sección para restaurar el archivo de copia de seguridad en una base de datos.

   ![restaurar](./media/tutorial-backup-restore-sql-server/restore.png)

4. Haga clic en **restaurar**

5. Para ver el estado de la operación de restauración, haga clic en **CTRL+T** para abrir el **historial de tareas** sidebar.

   ![restaurar](./media/tutorial-backup-restore-sql-server/task-history-restore.png)


En este tutorial, ha aprendido cómo:
> [!div class="checklist"]
> * Copia de seguridad de una base de datos 
> * Puede ver el estado de copia de seguridad
> * Generar el script utilizado para realizar la copia de seguridad
> * Restaurar una base de datos
> * Ver el estado de la tarea de restauración

