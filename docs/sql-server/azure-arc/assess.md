---
title: Configuración de la evaluación de SQL de SQL Server habilitado para Azure Arc
titleSuffix: ''
description: Configuración de la evaluación a petición de la instancia de SQL Server habilitada para Azure Arc
author: anosov1960
ms.author: sashan
ms.reviewer: mikeray
ms.date: 09/10/2020
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: 41a7f1f4edc247f211ee5b3cdcaddfd139c5027c
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/13/2020
ms.locfileid: "91988021"
---
# <a name="configure-on-demand-sql-assessment-for-azure-arc-enabled-sql-server-instance"></a>Configuración de la evaluación de SQL a petición de la instancia de SQL Server habilitada para Azure Arc

Puede habilitar la evaluación de SQL para las instancias de SQL Server siguiendo estos pasos.

## <a name="prerequisites"></a>Requisitos previos

* La instancia de SQL Server está conectada a Azure Arc. Siga estas instrucciones para la [incorporación de la instancia de SQL Server a SQL Server habilitado para Arc](connect.md).

* La extensión de MMA está instalada y configurada en la máquina. Siga estas instrucciones para la [Instalación de Microsoft Monitoring Agent (MMA)](configure-advanced-data-security.md#install-microsoft-monitoring-agent-mma). Para obtener más información, vea [Agente de Log Analytics](/azure/azure-monitor/platform/log-analytics-agent).

* SQL Server tiene el [protocolo TCP/IP habilitado](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md).

* El [explorador de SQL Server](../../tools/configuration-manager/sql-server-browser-service.md) se ejecuta en caso de que trabaje con una instancia con nombre de SQL Server.

* Ha revisado el documento de SQL Server en [Requisitos previos de las evaluaciones a petición del Centro de servicios](/services-hub/health/assessment-prereq-docs#on-demand-assessment-prerequisite-documents).

## <a name="enable-on-demand-sql-assessment"></a>Habilitación de SQL Assessment a petición

1. Abra el recurso de SQL Server: Azure Arc y seleccione __Environment Health__ (Estado del entorno) en el menú izquierdo.

   ![Selección de SQL Assessment](media/assess/sql-assessment-heading-sql-server-arc.png)

1. Especifique un directorio de trabajo en la máquina de recopilación de datos. De forma predeterminada, se usará `C:\sql_assessment\work_dir`. Durante la recopilación y el análisis, los datos se almacenan temporalmente en esa carpeta. Si la carpeta no existe, se creará automáticamente.

1. Haga clic en __Descargar script de configuración__ y copie el script descargado en la máquina de destino.

1. Inicie una instancia de administrador de __powershell.exe__ y realice una de las acciones siguientes: 
   * Si utiliza una cuenta de dominio, ejecute los comandos siguientes. Se le pedirá la cuenta de usuario y la contraseña. 

      ```powershell
      Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass -Force
      & '.\AddSqlAssessment.ps1'
      ```

    * Si utiliza una cuenta de MSA, ejecute los comandos siguientes.

      ```powershell
      Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass -Force
      & '.\AddSqlAssessment.ps1' -ManagedServiceAccountName <MSA account name>
      ```

   > [!NOTE]
   > El script programará una tarea llamada *SQLAssessment* para que se ejecute en un plazo de una hora después de ejecutar el script anterior y, después, cada 7 días. La tarea se puede modificar para que se ejecute en otras fecha y hora, o incluso forzarse a ejecutarse inmediatamente desde la biblioteca del programador de tareas > Microsoft > Operations Management Suite > AOI*** > Evaluaciones > SQLAssessment. Esta tarea desencadena la recopilación de datos.

## <a name="view-the-assessment-results"></a>Visualización de los resultados de la evaluación

El botón __View SQL assessment result__ (Ver el resultado de la evaluación de SQL) en la hoja _Environment Health_ (Estado del entorno) está deshabilitado hasta que los resultados estén listos en Log Analytics. Una vez que el botón esté activado, puede hacer clic en él para ver los resultados. Puede tardar hasta dos horas en que se muestren los resultados en Log Analytics una vez procesados los archivos de datos en la máquina de destino.

![Resultados de la evaluación de SQL](media/assess/sql-assessment-results.png)

Puede ver el estado del procesamiento de datos en la máquina de recopilación mediante la comprobación de los archivos en la carpeta de trabajo. Una vez completada la tarea programada, debería ver varios archivos con el prefijo _new._ en el directorio de trabajo:

![Archivos de datos listos](media/assess/sql-assessment-data-files-ready.png)

Microsoft Monitoring Agent examina la carpeta de trabajo cada 15 minutos para buscar archivos _new.*_ y envía los datos al área de trabajo de Log Analytics. Una vez cargado el archivo, el prefijo cambiará de _new._ a _processed._ :

![Archivos de datos procesados](media/assess/sql-assessment-data-files-processed.png)

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información, vea el documento de SQL Server en [Requisitos previos de las evaluaciones a petición del Centro de servicios](/services-hub/health/assessment-prereq-docs#on-demand-assessment-prerequisite-documents).

Para obtener soporte técnico completo del SQL Assessment a petición, se requiere una suscripción de soporte técnico de tipo Premier o unificado. Consulte [Soporte técnico Premier de Microsoft Azure](https://azure.microsoft.com/support/plans/premier) para obtener más información.