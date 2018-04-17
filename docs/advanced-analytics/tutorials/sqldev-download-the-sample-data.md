---
title: Lección 1 descargar los datos de ejemplo | Documentos de Microsoft
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: a87d307dafa733e449c6ec893ece21645fe65640
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="lesson-1-download-the-sample-data"></a>Lección 1: Descargar los datos de ejemplo
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artículo forma parte de un tutorial para desarrolladores de SQL sobre cómo usar R en SQL Server.

En este paso, se descargará el conjunto de datos de ejemplo y los [!INCLUDE[tsql](../../includes/tsql-md.md)] archivos que se utilizan en este tutorial de script. Los datos y los archivos de script se comparten en GitHub, pero la secuencia de comandos de PowerShell descargará los archivos de datos y la secuencia de comandos en un directorio local de su elección.

## <a name="download-the-data-and-scripts"></a>Descargar los datos y las secuencias de comandos

1.  Abra una consola de comandos de Windows PowerShell.
  
    Use la opción **Ejecutar como administrador**si se necesitan privilegios administrativos para crear el directorio de destino o para escribir archivos en el destino especificado.
  
2.  Ejecute los siguientes comandos de PowerShell, y cambie el valor del parámetro *DestDir* por cualquier directorio local.  El valor predeterminado que hemos usado aquí es **TempRSQL**.
  
    ```ps
    $source = ‘https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/RSQL/Download_Scripts_SQL_Walkthrough.ps1’  
    $ps1_dest = “$pwd\Download_Scripts_SQL_Walkthrough.ps1”
    $wc = New-Object System.Net.WebClient
    $wc.DownloadFile($source, $ps1_dest)
    .\Download_Scripts_SQL_Walkthrough.ps1 –DestDir ‘C:\tempRSQL’
    ```
  
    Si la carpeta que especifique en *DestDir* no existe, el script de PowerShell la creará.
  
    > [!TIP]
    > Si se produce un error, puede establecer temporalmente la directiva para la ejecución de scripts de PowerShell **sin restricciones** solo para este tutorial, mediante el argumento de omisión y definir el ámbito de los cambios en la sesión actual.
    >   
    >````
    > Set\-ExecutionPolicy Bypass \-Scope Process
    >````
    > Ejecutar este comando no produce un cambio de configuración.
  
    Dependiendo de la conexión a Internet, es posible que la descarga tarde un rato.
  
3.  Cuando se descarguen todos los archivos, el script de PowerShell se abre en la carpeta especificada por  *DestDir*. En el símbolo del sistema de PowerShell, ejecute el siguiente comando y revise los archivos que se han descargado.
  
    ```
    ls
    ```
  
    **Resultados:**
  
    ![lista de los archivos descargados por el script de PowerShell](media/rsql-devtut-filelist.png "lista de los archivos descargados por el script de PowerShell")
  
## <a name="next-lesson"></a>Lección siguiente

[Lección 2: Importar datos a SQL Server usando PowerShell](../r/sqldev-import-data-to-sql-server-using-powershell.md)

## <a name="previous-lesson"></a>Lección anterior

[Análisis de R en bases de datos para desarrolladores de SQL](../tutorials/sqldev-in-database-r-for-sql-developers.md)
