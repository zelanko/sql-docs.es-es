---
title: Programar paquetes SSIS en Linux con cron | Microsoft Docs
description: Este artículo describe cómo programar los paquetes de SQL Server Integration Services (SSIS) en Linux con el servicio de cron.
author: lrtoyou1223
ms.author: lle
ms.reviewer: maghan
manager: craigg
ms.date: 10/02/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 6d78190f5c6acf1f5dc8bfaccbf072a290faa908
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2019
ms.locfileid: "66705317"
---
# <a name="schedule-sql-server-integration-services-package-execution-on-linux-with-cron"></a>Ejecución en Linux con cron de paquetes de programación de SQL Server Integration Services

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Cuando se ejecutan SQL Server Integration Services (SSIS) y SQL Server en Windows, puede automatizar la ejecución de paquetes SSIS mediante el uso del Agente SQL Server. Cuando se ejecutan SQL Server y SSIS en Linux, sin embargo, la utilidad del Agente SQL Server no está disponible para programar trabajos en Linux. En su lugar, use el servicio cron, que se usa ampliamente en las plataformas Linux para automatizar la ejecución del paquete.

Este artículo proporcionan ejemplos que muestran cómo automatizar la ejecución de paquetes SSIS. Los ejemplos están escritos para ejecutarse en Red Hat Enterprise. El código es similar para otras distribuciones de Linux, como Ubuntu.

## <a name="prerequisites"></a>Requisitos previos

Antes de usar el servicio cron para ejecutar trabajos, compruebe si se está ejecutando en el equipo.

Para comprobar el estado del servicio cron, use el siguiente comando: `systemctl status crond.service`.

Si el servicio no está activo (es decir, no se está ejecutando), consulte al administrador para instalar y configurar correctamente el servicio de cron.

## <a name="create-jobs"></a>Creación de trabajos

Un trabajo cron es una tarea que se puede configurar para que se ejecute con regularidad en un intervalo especificado. El trabajo puede ser tan simple como un comando que normalmente podría escribir directamente en la consola o de identificación de un script de shell.

Con fines de mantenimiento y de fácil administración, se recomienda colocar los comandos de ejecución del paquete en un script que contiene un nombre descriptivo.

Este es un ejemplo de un script de shell sencilla para ejecutar un paquete. Contiene solo un único comando, pero puede agregar más comandos según sea necesario.

```bash
# A simple shell script that contains a simple package execution command
# Script name: SSISpackageName.daily

/opt/ssis/bin/dtexec /F yourSSISpackageName.dtsx >> $HOME/tmp/out 2>&1
```

## <a name="schedule-jobs-with-the-cron-service"></a>Programación de trabajos con el servicio cron

Después de haber definido los trabajos, puede programar que se ejecuten automáticamente mediante el servicio de cron.

Para agregar el trabajo de cron ejecutar, agregar el trabajo en el archivo crontab. Para abrir el archivo crontab en un editor donde puede agregar o actualizar el trabajo, use el siguiente comando: `crontab -e`.

Para programar el trabajo para ejecutarse diariamente a las 2:10 A.M. descrito anteriormente, agregue la siguiente línea al archivo crontab:

```
# run <SSIS package name> at 2:10 AM every day
10 2 \* \* \* $/HOME/SSIS/jobs/SSISpackageName.daily
```

Guarde el archivo crontab y, a continuación, salga del editor.

Para comprender el formato del comando de ejemplo, revise la información en la sección siguiente.
 
## <a name="format-of-a-crontab-file"></a>Formato de un archivo crontab

La siguiente imagen muestra la descripción del formato de la línea de trabajo que se agrega al archivo crontab.

![Descripción de formato de entrada en el archivo crontab](media/sql-server-linux-schedule-ssis-packages/ssis-linux-cron-job-definition.png)

Para obtener una descripción más detallada crontab el formato de archivo, use el siguiente comando: `man 5 crontab`.

Este es un ejemplo parcial de la salida que ayuda a explicar el ejemplo de este artículo:

![Descripción parcial detallada crontab formato](media/sql-server-linux-schedule-ssis-packages/ssis-linux-cron-crontab-format.png)

## <a name="related-content-about-ssis-on-linux"></a>Contenido relacionado sobre SSIS en Linux
-   [Extraer, transformar y cargar datos en Linux con SSIS](sql-server-linux-migrate-ssis.md)
-   [Instalar SQL Server Integration Services (SSIS) en Linux](sql-server-linux-setup-ssis.md)
-   [Configurar SQL Server Integration Services en Linux con ssis-conf](sql-server-linux-configure-ssis.md)
-   [Limitaciones y problemas conocidos de SSIS en Linux](sql-server-linux-ssis-known-issues.md)
