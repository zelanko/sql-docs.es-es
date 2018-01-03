---
title: "Lección 1: Descargar los datos de ejemplo | Documentos de Microsoft"
ms.custom: 
ms.date: 07/26/2016
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to: SQL Server 2016
dev_langs:
- R
- TSQL
ms.assetid: 32a5d5ad-c58a-4669-a90d-ef296b48fcd8
caps.latest.revision: "10"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9a5c5a5ab4bfe841ec7e06ffd44fef9ca9c15e85
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/20/2017
---
# <a name="lesson-1-download-the-sample-data"></a>Lección 1: Descargar los datos de ejemplo

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
