---
title: Paso 1 descargar los datos de ejemplo | Documentos de Microsoft
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 541066ac00efc1b15f8cae838097cfd8ee49df3d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="step-1-download-the-sample-data"></a>Paso 1: Descargar los datos de ejemplo
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artículo forma parte de un tutorial, [análisis de Python en bases de datos para desarrolladores de SQL](sqldev-in-database-python-for-sql-developers.md). 

Los datos y las secuencias de comandos para este tutorial se comparten en Github. En este paso, usa un script de PowerShell para descargar los archivos de datos y la secuencia de comandos en un directorio local de su elección.

## <a name="run-the-script"></a>Ejecute la secuencia de comandos

1. Abra una consola de comandos de Windows PowerShell.

    Utilice la opción **ejecutar como administrador**, si se necesitan privilegios de administrador para crear el directorio de destino o para escribir archivos en el destino especificado.

2. Ejecute los siguientes comandos de PowerShell, y cambie el valor del parámetro *DestDir* por cualquier directorio local.  El valor predeterminado que hemos usado aquí es `C:\temp\pysql`.

    ```ps
    $source = 'https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/PythonSQL/Download_Scripts_SQL_Walkthrough.ps1'
    $ps1_dest = "$pwd\Download_Scripts_SQL_Walkthrough.ps1"
    $wc = New-Object System.Net.WebClient
    $wc.DownloadFile($source, $ps1_dest)
    .\Download_Scripts_SQL_Walkthrough.ps1 –DestDir 'C:\temp\pysql'
    ```
    
    Si la carpeta que especifique en *DestDir* no existe, el script de PowerShell la creará.
    
    Si se produce un error, establezca temporalmente la directiva de ejecución de scripts de PowerShell para **sin restricciones** para este tutorial, mediante el uso de la **omisión** argumento y el ámbito de los cambios realizados en la sesión actual. Ejecutar este comando no produce un cambio de configuración.
    
    ```ps
    Set-ExecutionPolicy Bypass -Scope Process
    ```

3. Dependiendo de la conexión a internet, la descarga puede tardar un poco. 

## <a name="view-the-results"></a>Ver los resultados

Cuando se descarguen todos los archivos, el script de PowerShell se abre en la carpeta especificada por  *DestDir*. 

+ En el símbolo del sistema de PowerShell, ejecute el siguiente comando para enumerar los archivos que se hayan descargado.

    ```ps
    ls
    ```

![lista de los archivos descargados por el script de PowerShell](media/sqldev-python-filelist.png "lista de los archivos descargados por el script de PowerShell")

## <a name="next-step"></a>Paso siguiente

[Paso 2: Importar datos a SQL Server mediante PowerShell](sqldev-py2-import-data-to-sql-server-using-powershell.md)

## <a name="previous-step"></a>Paso anterior

[En bases de datos análisis de Python para que el programador SQL](sqldev-in-database-python-for-sql-developers.md)

## <a name="see-also"></a>Vea también

[Los servicios con Python de aprendizaje automático](../python/sql-server-python-services.md)


