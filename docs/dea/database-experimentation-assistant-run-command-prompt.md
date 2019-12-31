---
title: Ejecutar Asistente para experimentación con bases de datos en un símbolo del sistema
description: Ejecutar Asistente para experimentación con bases de datos en un símbolo del sistema
ms.custom: seo-lt-2019
ms.date: 11/22/2019
ms.prod: sql
ms.prod_service: dea
ms.suite: sql
ms.technology: dea
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: HJToland3
ms.author: jtoland
ms.reviewer: mathoma
ms.openlocfilehash: f5a0f7441dd17aec2587c772a678a3681fd3b423
ms.sourcegitcommit: 9e026cfd9f2300f106af929d88a9b43301f5edc2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/22/2019
ms.locfileid: "74317718"
---
# <a name="run-database-experimentation-assistant-at-a-command-prompt"></a>Ejecutar Asistente para experimentación con bases de datos en un símbolo del sistema

En este artículo se describe cómo capturar un seguimiento en Asistente para experimentación con bases de datos (DEA) y, a continuación, analizar los resultados en un símbolo del sistema.

## <a name="start-a-new-workload-capture-by-using-the-dea-command"></a>Inicio de una nueva captura de la carga de trabajo mediante el comando de DEA

Para iniciar una nueva captura de carga de trabajo, en un símbolo del sistema, ejecute el siguiente comando:

`Deacmd.exe -o startcapturetrace -s <SQLServerInstance> -e <encryptconnection> -u <trustservercertificate> -d <database name> -p <trace file path> -f <trace file name> -t <Max duration>`

**Ejemplo**

`Deacmd.exe -o startcapturetrace -s localhost -e -d adventureworks -p c:\test -f sql2008capture -t 60`

## <a name="replay-a-workload-capture"></a>Reproducir una captura de carga de trabajo

1. Inicie sesión en el equipo del controlador de Distributed Replay.
2. Para convertir el seguimiento de la carga de trabajo capturado con el comando de DEA en un archivo IRF, en un símbolo del sistema, ejecute el siguiente comando:

    `DReplay preprocess -m "dreplaycontroller" -i "Path to first trace file" -d "<Folder path on controller>\IrfFolder"`

3. Inicie una captura de seguimiento en el equipo de destino que ejecuta SQL Server mediante StartReplayCaptureTrace. SQL.

    a.  En SQL Server Management Studio (SSMS), abra <Dea_InstallPath\>\Scripts\StartReplayCaptureTrace.SQL.

    b.  Ejecute `Set @durationInMins=0` para que la captura de seguimiento no se detenga automáticamente después de un tiempo especificado.

    c.  Para establecer el tamaño máximo de archivo por archivo de seguimiento `Set @maxfilesize`, ejecute. El tamaño recomendado es 200 (en MB).

    d.  Edite `@Tracefile` para establecer un nombre único para el archivo de seguimiento.

    e.  Edite `@dbname` para especificar un nombre de base de datos si la carga de trabajo solo se debe capturar en una base de datos específica. De forma predeterminada, se captura la carga de trabajo en todo el servidor.

4. Para reproducir el archivo IRF en la instancia de SQL Server de destino, en un símbolo del sistema, ejecute el siguiente comando:

    `DReplay replay -m "dreplaycontroller" -d "<Folder Path on Dreplay Controller>\IrfFolder" -o -s "SQL2016Target" -w "dreplaychild1,dreplaychild2,dreplaycild3,dreplaychild4"`

    a.  Para supervisar el estado, en un símbolo del sistema, `DReplay status -f 1`ejecute.

    b.  Para detener la reproducción, por ejemplo, si ve que el porcentaje de paso es inferior al esperado, en un símbolo del sistema, `DReplay cancel`ejecute.

5. Detenga la captura de seguimiento en la instancia de SQL Server de destino.
6. En SSMS, Abra `<Dea_InstallPath>\Scripts\StopCaptureTrace.sql`.
7. Edite `@Tracefile` para que coincida con la ruta de acceso del archivo de seguimiento en el equipo de destino que ejecuta SQL Server.
8. Ejecute el script en el equipo de destino que ejecuta SQL Server.

## <a name="analyze-traces-using-the-dea-command"></a>Análisis de seguimientos mediante el comando de DEA

Para iniciar un nuevo análisis de seguimiento, en un símbolo del sistema, ejecute el siguiente comando:

`Deacmd.exe -o analysis -a <Target1 trace filepath> -b <Target2 trace filepath> -r reportname -s <SQLserverInstance> -e <encryptconnection> -u <trustservercertificate>`

**Ejemplo**

`Deacmd.exe -o analysis -a C:\Trace\SQL2008Source\Trace.trc -b C:\ Trace\SQL2014Trace\Trace.trc -r upgrade20082014 -s localhost -e`

## <a name="see-also"></a>Vea también

- Para obtener más información sobre el uso de DEA, consulte [información general de Asistente para experimentación con bases de datos](database-experimentation-assistant-overview.md).
