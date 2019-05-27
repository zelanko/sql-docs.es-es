---
title: Ejecutar el Asistente de experimentación de base de datos en un símbolo del sistema para las actualizaciones de SQL Server
description: Ejecutar el Asistente de experimentación de base de datos en un símbolo del sistema
ms.custom: ''
ms.date: 10/22/2018
ms.prod: sql
ms.prod_service: dea
ms.suite: sql
ms.technology: dea
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: HJToland3
ms.author: ajaykar
ms.reviewer: mathoma
manager: craigg
ms.openlocfilehash: e18cbe09ec9394ffb3c57c5ffcffc788278cc374
ms.sourcegitcommit: 45a9d7ffc99502c73f08cb937cbe9e89d9412397
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/22/2019
ms.locfileid: "66011588"
---
# <a name="run-database-experimentation-assistant-at-a-command-prompt"></a>Ejecutar el Asistente de experimentación de base de datos en un símbolo del sistema

En este artículo se describe cómo usar la ventana de símbolo del sistema para capturar un seguimiento en base de datos experimentación Assistant (DEA) y, a continuación, analizar los resultados. 

## <a name="start-a-new-workload-capture-by-using-the-dea-command"></a>Iniciar una nueva carga de trabajo de captura mediante el comando DEA

Para iniciar una nueva captura de la carga de trabajo, ejecute el siguiente comando:

`Deacmd.exe -o startcapturetrace -s <SQLServerInstance> -e <encryptconnection> -u <trustservercertificate> -d <database name> -p <trace file path> -f <trace file name> -t <Max duration>`

**Ejemplo**

`Deacmd.exe -o startcapturetrace -s localhost -e -d adventureworks -p c:\test -f sql2008capture -t 60`

## <a name="replay-a-workload"></a>Reproducir una carga de trabajo

1.  Inicie sesión en la máquina del controlador de Distributed Replay.
2.  Convertir el seguimiento de carga de trabajo que captura mediante el comando DEA a un archivo IRF:

    `DReplay preprocess -m "dreplaycontroller" -i "Path to first trace file" -d "<Folder path on controller>\IrfFolder"`

3.  Inicie una captura de seguimiento en el equipo de destino que ejecuta SQL Server mediante el uso de StartReplayCaptureTrace.sql.
       
    a.  En SQL Server Management Studio (SSMS), abra < Dea_InstallPath\>\Scripts\StartReplayCaptureTrace.sql.
    
    b.  Ejecute `Set @durationInMins=0` para que la captura de seguimiento no se detiene automáticamente tras un tiempo especificado.
    
    c.  Para establecer el tamaño máximo de archivo por archivo de seguimiento, ejecute `Set @maxfilesize`. El tamaño recomendado es 200 (en MB).
    
    d.  Editar `@Tracefile` para establecer un nombre único para el archivo de seguimiento.
    
    e.  Editar `@dbname` para especificar un nombre de base de datos si la carga de trabajo se debe capturar solo en una base de datos específica. De forma predeterminada, se captura la carga de trabajo en todo el servidor. 
4.  Reproducir el archivo IRF frente a la instancia de SQL Server de destino:

    `DReplay replay -m "dreplaycontroller" -d "<Folder Path on Dreplay Controller>\IrfFolder" -o -s "SQL2016Target" -w "dreplaychild1,dreplaychild2,dreplaycild3,dreplaychild4"`
        
    a.  Para supervisar el estado, abra una ventana del símbolo del sistema y ejecute `DReplay status -f 1`.
        
    b.  Para detener la reproducción, tal como si observa que el paso es inferior al esperado, abra una ventana del símbolo del sistema y ejecute `DReplay cancel`.

5.  Detenga la captura de seguimiento en la instancia de SQL Server de destino.
6.  En SSMS, abra `<Dea_InstallPath>\Scripts\StopCaptureTrace.sql`.
7.  Editar `@Tracefile` para que coincida con la ruta de acceso del archivo de seguimiento en el equipo de destino que ejecuta SQL Server.
8.  Ejecute el script en el equipo de destino que ejecuta SQL Server.

## <a name="analyze-traces-by-using-the-dea-command"></a>Analizar los seguimientos mediante el comando DEA

Para iniciar un nuevo análisis de seguimiento, ejecute el siguiente comando:

`Deacmd.exe -o analysis -a <Target1 trace filepath> -b <Target2 trace filepath> -r reportname -s <SQLserverInstance> -e <encryptconnection> -u <trustservercertificate>`

**Ejemplo**

`Deacmd.exe -o analysis -a C:\Trace\SQL2008Source\Trace.trc -b C:\ Trace\SQL2014Trace\Trace.trc -r upgrade20082014 -s localhost -e`

## <a name="next-steps"></a>Pasos siguientes

Para obtener una introducción minutos 19 DEA y demostración, vea el vídeo siguiente:

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-Database-Experimentation-Assistant/player]
