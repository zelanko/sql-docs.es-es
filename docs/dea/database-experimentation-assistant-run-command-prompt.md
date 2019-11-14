---
title: Ejecutar Asistente para experimentación con bases de datos en un símbolo del sistema
description: Ejecutar Asistente para experimentación con bases de datos en un símbolo del sistema
ms.custom: seo-lt-2019
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
ms.openlocfilehash: c3b87eafa460cfef69666a3837f56626dab81d47
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056574"
---
# <a name="run-database-experimentation-assistant-at-a-command-prompt-sql-server"></a>Ejecutar Asistente para experimentación con bases de datos en un símbolo del sistema (SQL Server)

En este artículo se describe cómo usar la ventana del símbolo del sistema para capturar un seguimiento en Asistente para experimentación con bases de datos (DEA) y, a continuación, analizar los resultados. 

## <a name="start-a-new-workload-capture-by-using-the-dea-command"></a>Inicio de una nueva captura de la carga de trabajo mediante el comando de DEA

Para iniciar una nueva captura de carga de trabajo, ejecute el siguiente comando:

`Deacmd.exe -o startcapturetrace -s <SQLServerInstance> -e <encryptconnection> -u <trustservercertificate> -d <database name> -p <trace file path> -f <trace file name> -t <Max duration>`

**Ejemplo**

`Deacmd.exe -o startcapturetrace -s localhost -e -d adventureworks -p c:\test -f sql2008capture -t 60`

## <a name="replay-a-workload"></a>Reproducir una carga de trabajo

1.  Inicie sesión en la máquina del controlador de Distributed Replay.
2.  Convierta el seguimiento de la carga de trabajo capturado con el comando de DEA en un archivo IRF:

    `DReplay preprocess -m "dreplaycontroller" -i "Path to first trace file" -d "<Folder path on controller>\IrfFolder"`

3.  Inicie una captura de seguimiento en el equipo de destino que ejecuta SQL Server mediante StartReplayCaptureTrace. SQL.
       
    A.  En SQL Server Management Studio (SSMS), abra < Dea_InstallPath\>\Scripts\StartReplayCaptureTrace.sql.
    
    b.  Ejecute `Set @durationInMins=0` para que la captura de seguimiento no se detenga automáticamente después de un tiempo especificado.
    
    c.  Para establecer el tamaño máximo de archivo por archivo de seguimiento, ejecute `Set @maxfilesize`. El tamaño recomendado es 200 (en MB).
    
    d.  Edite `@Tracefile` para establecer un nombre único para el archivo de seguimiento.
    
    e.  Edite `@dbname` para especificar un nombre de base de datos si la carga de trabajo solo se debe capturar en una base de datos específica. De forma predeterminada, se captura la carga de trabajo en todo el servidor. 
4.  Reproducir el archivo IRF en la instancia de SQL Server de destino:

    `DReplay replay -m "dreplaycontroller" -d "<Folder Path on Dreplay Controller>\IrfFolder" -o -s "SQL2016Target" -w "dreplaychild1,dreplaychild2,dreplaycild3,dreplaychild4"`
        
    A.  Para supervisar el estado, abra una ventana del símbolo del sistema y ejecute `DReplay status -f 1`.
        
    b.  Para detener la reproducción, por ejemplo, si ve que el porcentaje de paso es inferior al esperado, abra una ventana del símbolo del sistema y ejecute `DReplay cancel`.

5.  Detenga la captura de seguimiento en la instancia de SQL Server de destino.
6.  En SSMS, abra `<Dea_InstallPath>\Scripts\StopCaptureTrace.sql`.
7.  Edite `@Tracefile` para que coincida con la ruta de acceso del archivo de seguimiento en el equipo de destino que ejecuta SQL Server.
8.  Ejecute el script en el equipo de destino que ejecuta SQL Server.

## <a name="analyze-traces-by-using-the-dea-command"></a>Análisis de seguimientos mediante el comando de DEA

Para iniciar un nuevo análisis de seguimiento, ejecute el siguiente comando:

`Deacmd.exe -o analysis -a <Target1 trace filepath> -b <Target2 trace filepath> -r reportname -s <SQLserverInstance> -e <encryptconnection> -u <trustservercertificate>`

**Ejemplo**

`Deacmd.exe -o analysis -a C:\Trace\SQL2008Source\Trace.trc -b C:\ Trace\SQL2014Trace\Trace.trc -r upgrade20082014 -s localhost -e`

## <a name="next-steps"></a>Pasos siguientes

Para obtener una introducción de 19 minutos a DEA y demostraciones, vea el siguiente vídeo:

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-Database-Experimentation-Assistant/player]
