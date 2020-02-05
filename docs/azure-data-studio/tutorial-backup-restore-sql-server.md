---
title: Copia de seguridad y restauración de una base de datos
titleSuffix: Azure Data Studio
description: Información sobre cómo realizar una copia de seguridad y restauración de una base de datos con Azure Data Studio
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: tutorial
author: markingmyname
ms.author: maghan
ms.reviewer: alayu; sstein
ms.custom: seodec18
ms.date: 11/04/2019
ms.openlocfilehash: bdf3bb3151cfac9f68a9765a2c59232b9fb59f56
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "73532472"
---
# <a name="backup-and-restore-databases-using-includename-sosincludesname-sos-shortmd"></a>Copia de seguridad y restauración de bases de datos con [!INCLUDE[name-sos](../includes/name-sos-short.md)]

En este tutorial, obtendrá información sobre cómo usar [!INCLUDE[name-sos](../includes/name-sos-short.md)] para:
> [!div class="checklist"]
> * Realizar una copia de seguridad de una base de datos 
> * Ver el estado de la copia de seguridad
> * Generar el script usado para realizar la copia de seguridad
> * Restaurar una base de datos
> * Ver el estado de la tarea de restauración

## <a name="prerequisites"></a>Prerequisites

Para este tutorial, es necesario usar *TutorialDB* de SQL Server. Para crear la base de datos *TutorialDB*, complete uno de los siguientes inicios rápidos:

* [Conectarse a una instancia de SQL Server y consultarla con [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-server.md)

Para este tutorial, es necesario conectarse a una base de datos de SQL Server. Azure SQL Database tiene copias de seguridad automatizadas, por lo que Azure Data Studio no realiza copias de seguridad y restauración de Azure SQL Database. Para obtener más información, vea [Copias de seguridad automatizadas](https://docs.microsoft.com/azure/sql-database/sql-database-automated-backups).

## <a name="back-up-a-database"></a>Realizar una copia de seguridad de una base de datos

1. Abra el panel de la base de datos TutorialDB (abra la barra lateral **SERVIDORES** [**CTRL+G**], expanda **Bases de datos**, haga clic con el botón derecho en **TutorialDB** y seleccione **Administrar**).

2. Abra el cuadro de diálogo **Copia de seguridad de la base de datos** (haga clic en **Copia de seguridad** en el widget **Tareas**).

   ![Widget Tareas](./media/tutorial-backup-restore-sql-server/tasks.png)

3. Como en este tutorial se usan las opciones de copia de seguridad predeterminadas, haga clic en **Copia de seguridad**.
   ![cuadro de diálogo Copia de seguridad](./media/tutorial-backup-restore-sql-server/backup-dialog.png)

Después de hacer clic en **Copia de seguridad**, desaparecerá el cuadro de diálogo **Copia de seguridad de la base de datos** y se iniciará proceso de copia de seguridad.

## <a name="view-the-backup-status-and-view-the-backup-script"></a>Ver el estado de la copia de seguridad y ver el script de copia de seguridad

1. Aparece el panel **Historial de tareas** o presione **CTRL+T**.

   ![Historial de tareas](./media/tutorial-backup-restore-sql-server/task-history.png)

2. Para ver el script de copia de seguridad en el editor, haga clic con el botón derecho en **Backup Database succeeded** (La copia de seguridad de la base de datos se ha completado correctamente) y seleccione **Script**.

   ![script de copia de seguridad](./media/tutorial-backup-restore-sql-server/task-script.png)

## <a name="restore-a-database-from-a-backup-file"></a>Restaurar una base de datos a partir de un archivo de copia de seguridad

1. Abra la barra lateral **SERVIDORES** (**CTRL+G**), haga clic con el botón derecho en el servidor y, después, seleccione **Administrar**.

2. Abra el cuadro de diálogo **Restaurar base de datos** (haga clic en **Restaurar** en el widget **Tareas**).

   ![Tarea Restaurar](media/tutorial-backup-restore-sql-server/tasks-restore.png)

3. Seleccione **Archivo de copia de seguridad** en el campo **Restaurar desde**.

4. Haga clic en el signo de puntos suspensivos (…) en el campo **Ruta de acceso del archivo de copia de seguridad** y seleccione el archivo de copia de seguridad más reciente de *TutorialDB*.

5. Escriba **TutorialDB_Restored** en el campo **Base de datos de destino** de la sección **Destino** para restaurar el archivo de copia de seguridad en una nueva base de datos. Después, seleccione **Restaurar**.

   ![Restauración](./media/tutorial-backup-restore-sql-server/restore.png)

6. Para ver el estado de la operación de restauración, presione **CTRL+T** para abrir el **Historial de tareas**.

   ![Restauración](./media/tutorial-backup-restore-sql-server/task-history-restore.png)