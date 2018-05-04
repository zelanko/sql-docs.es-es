---
title: Programar paquetes SSIS en Linux con cron | Documentos de Microsoft
description: En este artículo se describe cómo programar paquetes de SQL Server Integration Services (SSIS) en Linux con el servicio de cron.
author: leolimsft
ms.author: lle
ms.reviewer: douglasl
manager: craigg
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.openlocfilehash: 880f5f9060bb47e5cdf4de1567251f541c2628b6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="schedule-sql-server-integration-services-package-execution-on-linux-with-cron"></a>Ejecución en Linux con cron del paquete de programación de SQL Server Integration Services

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Al ejecutar SQL Server Integration Services (SSIS) y SQL Server en Windows, puede automatizar la ejecución de paquetes SSIS mediante el Agente SQL Server. Cuando se ejecutan SQL Server y SSIS en Linux, sin embargo, la utilidad Agente SQL Server no está disponible para programar trabajos en Linux. En su lugar, utilice el servicio cron, que es ampliamente utilizado en plataformas Linux para automatizar la ejecución del paquete.

Este artículo proporciona ejemplos que muestran cómo automatizar la ejecución de paquetes SSIS. Los ejemplos están escritos para ejecutarse en Red Hat Enterprise. El código es similar para otras distribuciones de Linux, como Ubuntu.

## <a name="prerequisites"></a>Requisitos previos

Antes de usar el servicio cron para ejecutar trabajos, compruebe si se está ejecutando en el equipo.

Para comprobar el estado del servicio cron, use el siguiente comando: `systemctl status crond.service`.

Si el servicio no está activo (es decir, no se está ejecutando), consulte a su administrador para instalar y configurar el servicio cron correctamente.

## <a name="create-jobs"></a>Crear trabajos

Un trabajo cron es una tarea que se puede configurar para ejecutarse periódicamente en un intervalo especificado. El trabajo puede ser tan simple como un comando que normalmente podría escribir directamente en la consola o de identificación de un script de shell.

Para facilitar la administración y con fines de mantenimiento, se recomienda colocar los comandos de ejecución del paquete en un script que contiene un nombre descriptivo.

Este es un ejemplo de una secuencia de comandos de shell sencillo para ejecutar un paquete. Contiene solo un único comando, pero puede agregar más comandos según sea necesario.

```bash
# A simple shell script that contains a simple package execution command
# Script name: SSISpackageName.daily

/opt/ssis/bin/dtexec /F yourSSISpackageName.dtsx >> $HOME/tmp/out 2>&1
```

## <a name="schedule-jobs-with-the-cron-service"></a>Programar trabajos con el servicio de cron

Después de haber definido los trabajos, puede programar que se ejecuten automáticamente mediante el servicio de cron.

Para agregar el trabajo de cron para ejecutarse, agregue el trabajo en el archivo crontab. Para abrir el archivo crontab en un editor, donde puede agregar o actualizar el trabajo, use el siguiente comando: `crontab -e`.

Para programar el trabajo se ejecute diariamente a las 2:10 A.M. descrito anteriormente, agregue la siguiente línea al archivo crontab:

```
# run <SSIS package name> at 2:10 AM every day
10 2 \* \* \* $/HOME/SSIS/jobs/SSISpackageName.daily
```

Guarde el archivo crontab y, a continuación, salga del editor.

Para entender el formato del comando de ejemplo, revise la información en la sección siguiente.
 
## <a name="format-of-a-crontab-file"></a>Formato de un archivo crontab

La siguiente imagen muestra la descripción del formato de la línea de trabajo que se agrega al archivo crontab.

![Descripción de formato de entrada de archivo crontab](media/sql-server-linux-schedule-ssis-packages/ssis-linux-cron-job-definition.png)

Para obtener una descripción más detallada del formato de archivo crontab, use el siguiente comando: `man 5 crontab`.

Este es un ejemplo parcial de la salida que ayuda a explicar el ejemplo de este artículo:

![Descripción detallada de parcial del formato de crontab](media/sql-server-linux-schedule-ssis-packages/ssis-linux-cron-crontab-format.png)

## <a name="related-content-about-ssis-on-linux"></a>Contenido relacionado sobre SSIS en Linux
-   [Extraer, transformar y cargar datos en Linux con SSIS](sql-server-linux-migrate-ssis.md)
-   [Instalar SQL Server Integration Services (SSIS) en Linux](sql-server-linux-setup-ssis.md)
-   [Configurar SQL Server Integration Services en Linux con ssis-conf](sql-server-linux-configure-ssis.md)
-   [Limitaciones y problemas conocidos de SSIS en Linux](sql-server-linux-ssis-known-issues.md)
