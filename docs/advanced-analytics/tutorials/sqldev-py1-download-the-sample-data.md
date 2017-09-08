---
title: 'Paso 1: Descargar los datos de ejemplo | Documentos de Microsoft'
ms.custom: 
ms.date: 05/25/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2017
dev_langs:
- Python
- TSQL
ms.assetid: 
caps.latest.revision: 2
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 147860e9af8cce86d1a7ccbd3e53f20d240fcd49
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="step-1-download-the-sample-data"></a>Paso 1: Descargar los datos de ejemplo

En este paso, se descargará el conjunto de datos de ejemplo y las secuencias de comandos. Los datos y los archivos de script que se comparten en Github, pero el script de PowerShell descargará los archivos de datos y los archivos de script en un directorio local de su elección.

## <a name="download-the-data-and-scripts"></a>Descargar los datos y los scripts

1. Abra una consola de comandos de Windows PowerShell.

    Utilice la opción **ejecutar como administrador**, si se necesitan privilegios de administrador para crear el directorio de destino o para escribir archivos en el destino especificado.

2. Ejecute los siguientes comandos de PowerShell, y cambie el valor del parámetro *DestDir* por cualquier directorio local.  El valor predeterminado que hemos usado aquí es **TempPythonSQL**.

    ```
    $source = 'https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/PythonSQL/Download_Scripts_SQL_Walkthrough.ps1'
    $ps1_dest = "$pwd\Download_Scripts_SQL_Walkthrough.ps1"
    $wc = New-Object System.Net.WebClient
    $wc.DownloadFile($source, $ps1_dest)
    .\Download_Scripts_SQL_Walkthrough.ps1 –DestDir 'C:\tempPythonSQL'
    ```
    
    Si la carpeta que especifique en *DestDir* no existe, el script de PowerShell la creará.
    
    Si se produce un error, puede establecer temporalmente la directiva para la ejecución de scripts de PowerShell para **sin restricciones** sólo para este tutorial, mediante el uso de la **omisión** argumento y el ámbito de los cambios al actual sesión. Ejecutar este comando no produce un cambio de configuración.
    
    `Set\-ExecutionPolicy Bypass \-Scope Process`

3. Dependiendo de la conexión a Internet, es posible que la descarga tarde un rato. Cuando se descarguen todos los archivos, el script de PowerShell se abre en la carpeta especificada por  *DestDir*. En el símbolo del sistema de PowerShell, ejecute el siguiente comando y revise los archivos que se han descargado.

    ```
    ls
    ```
**Resultados:**

![lista de los archivos descargados por el script de PowerShell](media/sqldev-python-filelist.png "lista de los archivos descargados por el script de PowerShell")

## <a name="next-step"></a>Paso siguiente

[Paso 2: Importar datos a SQL Server mediante PowerShell](sqldev-py2-import-data-to-sql-server-using-powershell.md)

## <a name="previous-step"></a>Paso anterior

[En bases de datos análisis de Python para que el programador SQL](sqldev-in-database-python-for-sql-developers.md)

## <a name="see-also"></a>Vea también

[Los servicios con Python de aprendizaje automático](../python/sql-server-python-services.md)



