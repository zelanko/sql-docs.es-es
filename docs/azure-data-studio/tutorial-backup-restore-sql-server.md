---
title: Copia de seguridad y restaurar una base de datos
titleSuffix: Azure Data Studio
description: Obtenga información sobre cómo las copias de seguridad y restaurar una base de datos mediante Azure Data Studio
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: tutorial
author: markingmyname
ms.author: maghan
ms.reviewer: alayu; sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: 77679106577cd8f8374f932d8ddd22644beb63d8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67959102"
---
# <a name="backup-and-restore-databases-using-includename-sosincludesname-sos-shortmd"></a>Copia de seguridad y restaurar bases de datos mediante [!INCLUDE[name-sos](../includes/name-sos-short.md)]

En este tutorial, obtendrá información sobre cómo usar [!INCLUDE[name-sos](../includes/name-sos-short.md)] para:
> [!div class="checklist"]
> * Copia de seguridad de una base de datos 
> * Ver el estado de copia de seguridad
> * Generar el script utilizado para realizar la copia de seguridad
> * Restaurar una base de datos
> * Ver el estado de la tarea de restauración

## <a name="prerequisites"></a>Prerequisites

Este tutorial requiere que el servidor SQL *TutorialDB*. Para crear el *TutorialDB* base de datos, complete uno de los siguientes tutoriales:

- [Conectarse y consultar con SQL Server [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-server.md)

Este tutorial requiere conexión a una base de datos de SQL Server. Azure SQL Database ha automatizar las copias de seguridad, por lo que Azure Data Studio no realizar copia de seguridad de Azure SQL Database y restore. Para obtener más información, consulte [más información sobre copias de seguridad automáticas de SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-automated-backups).

## <a name="backup-a-database"></a>Copia de seguridad de una base de datos

1. Abra el panel de la base de datos TutorialDB (abra el **servidores** sidebar (**CTRL+G**), expanda **bases de datos**, haga clic en **TutorialDB**, y seleccione **administrar**).

2. Abra el **base de datos de copia de seguridad** diálogo (haga clic en **copia de seguridad** en el **tareas** widget).

   ![Widget de tareas](./media/tutorial-backup-restore-sql-server/tasks.png)

3. Este tutorial usa las opciones de copia de seguridad predeterminadas, así que haga clic en **copia de seguridad**.
   ![cuadro de diálogo copia de seguridad](./media/tutorial-backup-restore-sql-server/backup-dialog.png)

Después de hacer clic **copia de seguridad**, **base de datos de copia de seguridad** cuadro de diálogo desaparece y comienza el proceso de copia de seguridad.

## <a name="view-the-backup-status-and-view-the-backup-script"></a>Ver el estado de copia de seguridad y ver el script de copia de seguridad

1. Abra el **historial de tareas** sidebar, haga clic en el icono de reloj en la *barra de acciones* o presione **CTRL+T**.

   ![Historial de tareas](./media/tutorial-backup-restore-sql-server/task-history.png)

2. Para ver la secuencia de comandos de copia de seguridad en el editor, haga clic en **base de datos de copia de seguridad se realizó correctamente** y seleccione **Script**.

   ![script de copia de seguridad](./media/tutorial-backup-restore-sql-server/task-script.png) 

## <a name="restore-a-database-from-a-backup-file"></a>Restaurar una base de datos desde un archivo de copia de seguridad


1. Abra el **servidores** sidebar (**CTRL+G**), haga clic en el servidor y seleccione **administrar**. 

2. Abra el **Restaurar base de datos** diálogo (haga clic en **restaurar** en el **tareas** widget).

2. Seleccione **el archivo de copia de seguridad** en el **restaurar a partir de** campo. 

3. Haga clic en el botón de puntos suspensivos (...) en el **ruta del archivo de copia de seguridad** campo y seleccione el archivo de copia de seguridad más reciente para *TutorialDB*.

3. Tipo **TutorialDB_Restored** en el **base de datos de destino** campo el **destino** sección para restaurar el archivo de copia de seguridad en una base de datos.

   ![restaurar](./media/tutorial-backup-restore-sql-server/restore.png)

4. Haga clic en **restaurar**

5. Para ver el estado de la operación de restauración, presione **CTRL+T** para abrir el **historial de tareas** barra lateral.

   ![restaurar](./media/tutorial-backup-restore-sql-server/task-history-restore.png)


En este tutorial ha aprendido a:
> [!div class="checklist"]
> * Copia de seguridad de una base de datos 
> * Ver el estado de copia de seguridad
> * Generar el script utilizado para realizar la copia de seguridad
> * Restaurar una base de datos
> * Ver el estado de la tarea de restauración

