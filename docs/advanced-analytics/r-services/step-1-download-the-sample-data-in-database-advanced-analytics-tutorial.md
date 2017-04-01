---
title: "Paso 1: Descargar los datos de ejemplo (Tutorial de base de datos de an&#225;lisis avanzado) | Microsoft Docs"
ms.custom: ""
ms.date: "04/19/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
dev_langs: 
  - "R"
  - "TSQL"
ms.assetid: 32a5d5ad-c58a-4669-a90d-ef296b48fcd8
caps.latest.revision: 10
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 10
---
# Paso 1: Descargar los datos de ejemplo (Tutorial de base de datos de an&#225;lisis avanzado)
En este paso, descargará el conjunto de datos de ejemplo y los archivos de script de [!INCLUDE[tsql](../../includes/tsql-md.md)] que se usan en este tutorial. Los datos y los archivos de script que se comparten en Github, pero el script de PowerShell descargará los archivos de datos y los archivos de script en un directorio local de su elección.  
  
## Descargar los datos y los scripts  
  
1.  Abra una consola de comandos de Windows PowerShell.  
  
    Use la opción **Ejecutar como administrador** si se necesitan privilegios administrativos para crear el directorio de destino o para escribir archivos en el destino especificado.  
  
2.  Ejecute los siguientes comandos de PowerShell, y cambie el valor del parámetro *DestDir* por cualquier directorio local.  El valor predeterminado que hemos usado aquí es **TempRSQL**.  
  
    ```  
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
  
3.  Cuando se descarguen todos los archivos, el script de PowerShell se abre en la carpeta especificada por *DestDir*. En el símbolo del sistema de PowerShell, ejecute el siguiente comando y revise los archivos que se han descargado.  
  
    ```  
    ls  
    ```  
  
    **Resultados:**  
  
    ![list of files downloaded by PowerShell script](../../advanced-analytics/r-services/media/rsql-devtut-filelist.PNG "list of files downloaded by PowerShell script")  
  
## Paso siguiente  
[Paso 2: Importar datos a SQL Server mediante PowerShell](../../advanced-analytics/r-services/step-2-import-data-to-sql-server-using-powershell.md)  
  
## Paso anterior  
[In-Database Advanced Analytics for SQL Developers &#40;Tutorial&#41; (Análisis avanzado en base de datos para desarrolladores de SQL &#40;Tutorial&#41;)](../../advanced-analytics/r-services/in-database-advanced-analytics-for-sql-developers-tutorial.md)  
  
## Vea también  
[Tutoriales de SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services-tutorials.md)  
  
  
  
