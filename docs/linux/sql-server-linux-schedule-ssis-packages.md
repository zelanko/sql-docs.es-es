---
title: Programar paquetes SSIS en Linux con cron | Documentos de Microsoft
description: "Este artículo muestra cómo programar paquetes de SQL Server Integration Services en Linux con el servicio de cron."
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.date: 09/26/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: 31d5fb63a9c2a4d8825aa39c6fa7e3377ddc8d91
ms.contentlocale: es-es
ms.lasthandoff: 09/27/2017

---
# <a name="schedule-sql-server-integration-services-package-execution-on-linux-with-cron"></a>Ejecución en Linux con cron del paquete de programación de SQL Server Integration Services

Al ejecutar SQL Server Integration Services (SSIS) y SQL Server en Windows, puede automatizar la ejecución de paquetes SSIS mediante el Agente SQL Server. Cuando se ejecutan SQL Server y SSIS en Linux, sin embargo, la utilidad Agente SQL Server no está disponible para programar trabajos en Linux. En su lugar use **Cron** servicio que se usa ampliamente en plataformas Linux para automatizar la ejecución del paquete.

Este artículo proporciona ejemplos que muestran cómo automatizar la ejecución de paquetes SSIS. Los ejemplos se han escrito para ejecutarlos en Red Hat Enterprise. El código es similar para otras distribuciones de Linux como Ubuntu.

## <a name="prerequisites"></a>Requisitos previos

Para poder usar el servicio Cron para ejecutar trabajos, se tiene que comprobar si el servicio Cron se está ejecutando en el equipo.

Use el siguiente comando para comprobar el estado del servicio Cron.

`systemctl status crond.service`

Si el servicio no está activo (es decir, no se está ejecutando), consulte al administrador para instalar y configurar el servicio Cron correctamente.

## <a name="create-jobs"></a>Crear trabajos

Un trabajo Cron es una tarea que se puede configurar para ejecutarse periódicamente en un intervalo especificado. El trabajo puede ser tan simple como un comando que normalmente podría escribir directamente en la consola o de identificación de un script de shell.

Para facilitar la administración y con fines de mantenimiento, se recomienda para colocar los comandos de ejecución del paquete en una secuencia de comandos con un nombre descriptivo.

Este es un ejemplo sencillo de una secuencia de comandos de shell que contiene solo un comando único para ejecutar un paquete. Puede agregar más comandos según sea necesario.

```bash
# A simple shell script that contains a simple package execution command
# Script name: SSISpackageName.daily

/opt/ssis/bin/dtexec /F yourSSISpackageName.dtsx >> $HOME/tmp/out 2>&1
```

## <a name="schedule-jobs-with-the-cron-service"></a>Programar trabajos con el servicio de Cron

Después de haber definido los trabajos, puede programar que se ejecuten automáticamente mediante el servicio de Cron.

Para agregar el trabajo de Cron ejecutar, tendrá que agregar el trabajo en el `crontab` archivo. Para abrir el `crontab` archivo en un editor, donde puede agregar o actualizar el trabajo, use el siguiente comando:

`crontab -e`

Para programar el trabajo se ejecute diariamente a las 2:10 a.m. descrito anteriormente, agregue el siguiente línea a la `crontab` archivo:

```
# run SSIS package Name at 2:10AM every day
10 2 \* \* \* $/HOME/SSIS/jobs/SSISpackageName.daily
```

Guardar el `crontab` de archivo y salga del editor.

Para entender el formato del comando de ejemplo, revise la información en la sección siguiente.
 
## <a name="format-of-a-crontab-file"></a>Formato de un archivo Crontab

La siguiente imagen muestra la descripción del formato de la línea de trabajo agregada a la `crontab` archivo.

![Descripción de formato de entrada de archivo crontab](media/sql-server-linux-schedule-ssis-packages/ssis-linux-cron-job-definition.png)

Para obtener una descripción más detallada de los `crontab` formato de archivo, use el comando siguiente:

`man 5 crontab`

Este es un ejemplo parcial de la salida que ayuda a explicar el ejemplo de este artículo:

![Descripción detallada de parcial del formato de crontab](media/sql-server-linux-schedule-ssis-packages/ssis-linux-cron-crontab-format.png)

