---
title: Tutorial sobre cómo RevoScaleR funciona con SQL Server Machine Learning | Microsoft Docs
description: En este tutorial, obtenga información sobre cómo llamar a una función de RevoScaleR en SQL Server Machine Learning con R compatibles que habilitado.
ms.prod: sql
ms.technology: machine-learning
ms.date: 07/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: ee810c998f8aecf17c3496540c65471e0b29e102
ms.sourcegitcommit: a083e9d59e2014a06cda9138b7e17c17ecab90e0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/11/2018
ms.locfileid: "44343090"
---
# <a name="tutorial-use-revoscaler-r-functions-with-sql-server-data"></a>Tutorial: Funciones de uso RevoScaleR R con datos de SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

RevoScaleR es un paquete de Microsoft R que proporciona procesamiento paralelo y distribuido para las cargas de trabajo de aprendizaje automático y ciencia de datos. Para el desarrollo de R en SQL Server, RevoScaleR es uno de los paquetes integrados de core, con funciones para establecer un contexto de cálculo, administración de paquetes y lo más importante: trabajar con datos-to-end, de importación para visualización y análisis. Algoritmos de aprendizaje automático en SQL Server tienen una dependencia en los orígenes de datos de RevoScaleR. Dada la importancia de RevoScaleR, saber cuándo y cómo llamar a sus funciones es una habilidad esencial. 

En este tutorial, obtendrá información sobre cómo crear un contexto de cálculo remoto, movimiento de datos entre contextos de cálculo locales y remotos y ejecutar código R en un servidor SQL remoto. También aprenderá cómo analizar y representar los datos localmente y en el servidor remoto y cómo crear e implementar modelos.

+ Los datos se han obtenido inicialmente de archivos CSV o archivos XDF. Importar los datos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante las funciones en el paquete RevoScaleR.
+ Entrenamiento de modelos y de puntuación se realizan mediante el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contexto de proceso. 
+ Usar funciones de RevoScaleR para crear nuevas [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tablas para guardar los resultados de puntuación.
+ Crear trazados tanto en el servidor y el contexto de proceso local.
+ Entrenar un modelo de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] base de datos, que se ejecuta R en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instancia.
+ Extraer un subconjunto de datos y guárdelo como un archivo XDF para volver a usar en el análisis en su estación de trabajo local.
+ Obtener nuevos datos para puntuación, abriendo una conexión ODBC a la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] base de datos. Se realiza la puntuación en la estación de trabajo local.
+ Cree una función personalizada de R y ejecutarlo en el servidor de contexto de proceso para realizar una simulación.

## <a name="target-audience"></a>Audiencia de destino

Este tutorial está diseñado para científicos de datos o para las personas que ya están bastante familiarizadas con R y tareas de ciencia de datos como resúmenes y creación de modelos. Sin embargo, se proporciona todo el código, por lo que incluso si está familiarizado con R, puede ejecutar el código y seguir el tutorial, suponiendo que dispone de los entornos de cliente y servidor requeridos.

También debe estar familiarizado con [!INCLUDE[tsql](../../includes/tsql-md.md)] sintaxis y saber cómo obtener acceso a un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] base de datos mediante herramientas como las siguientes:

+ [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 
+ Herramientas de base de datos en Visual Studio 
+ La versión gratuita [extensión mssql para Visual Studio Code](https://docs.microsoft.com/sql/linux/sql-server-linux-develop-use-vscode).
  
> [!TIP]
> Guarde el área de trabajo de R entre lecciones para que pueda seguir fácilmente desde donde se ha quedado.

## <a name="prerequisites"></a>Requisitos previos

- **SQL Server compatible con R**
  
    Instalar [Machine Learning Services de SQL Server 2017](../install/sql-machine-learning-services-windows-install.md) con la característica R o instale [SQL Server 2016 R Services (en bases de datos)](../install/sql-r-services-windows-install.md).

    Asegúrese de que el scripting externo está habilitado, servicio Launchpad se está ejecutando y que tiene permisos para acceder al servicio.
  
-  **Permisos de base de datos**
  
    Para ejecutar las consultas usadas para entrenar el modelo, debe tener privilegios **db_datareader** en la base de datos donde se almacenan los datos. Para ejecutar R, el usuario debe tener el permiso EXECUTE ANY EXTERNAL SCRIPT.

-   **Equipo de desarrollo de ciencia de datos**
  
    Para alternar entre los contextos de cálculo locales y remotos, necesita dos sistemas. Normalmente, local es una estación de trabajo de desarrollo con potencia suficiente para cargas de trabajo de ciencia de datos. Remoto en este caso es SQL Server 2017 ni SQL Server 2016 con la característica R habilitada. 
    
    Cambiar contextos de cálculo se basa en tener la misma versión RevoScaleR en sistemas locales y remotos. En una estación de trabajo local, puede obtener los paquetes de RevoScaleR y proveedores relacionados mediante la instalación o mediante cualquiera de las siguientes acciones: [Data Science Virtual Machine en Azure](https://docs.microsoft.com/azure/machine-learning/data-science-virtual-machine/overview), [(gratis) de Microsoft R Client](https://docs.microsoft.com/en-us/machine-learning-server/r-client/what-is-microsoft-r-client), o [ Microsoft Machine Learning Server (independiente)](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-install). Para la opción de servidor independiente, instale la edición de desarrollador gratuita, mediante los instaladores de Linux o Windows. También puede usar el programa de instalación de SQL Server para instalar a un servidor independiente.
      
-   **Paquetes adicionales de R**
  
    En este tutorial, instala los siguientes paquetes: **dplyr**, **ggplot2**, **ggthemes**, **reshape2**, y **e1071** . Se proporcionan instrucciones como parte del tutorial.
  
    Todos los paquetes deben instalarse en dos lugares: en la estación de trabajo que se usa para el desarrollo de soluciones de R y en el equipo de SQL Server donde se ejecutan los scripts de R. Si no tiene permiso para instalar paquetes en el equipo servidor, pida a un administrador. 
    
    **No instale los paquetes en una biblioteca de usuario.** Los paquetes deben instalarse en la biblioteca de paquetes de R que se usa la instancia de SQL Server.

## <a name="r-development-tools"></a>Herramientas de desarrollo de R

Normalmente, los desarrolladores de R usarán IDE para escribir y depurar código de R. Estas son algunas sugerencias:

- **Herramientas de R para Visual Studio** (RTVS) es un complemento gratuito complemento que proporciona Intellisense, depuración y soporte técnico para Microsoft R. Puede usarlo con R Server y SQL Server Machine Learning Services. Para descargarlo, consulte la página sobre [Herramientas de R para Visual Studio](https://www.visualstudio.com/vs/rtvs/).

- **RStudio** es uno de los entornos de desarrollo de R más populares. Para obtener más información, consulte [ https://www.rstudio.com/products/RStudio/ ](https://www.rstudio.com/products/RStudio/).

- Herramientas básicas de R (R.exe, RTerm.exe, RScripts.exe) también se instalan de forma predeterminada al instalar R en SQL Server o cliente de R. Si no desea instalar un IDE, puede usar las herramientas integradas de R para ejecutar el código en este tutorial.

Recuerde que es necesario RevoScaleR en equipos locales y remotos. No se puede completar este tutorial con una instalación genérica de RStudio u otro entorno que carece de las bibliotecas de R de Microsoft. Para obtener más información, consulte [Configurar un cliente de ciencia de datos](../r/set-up-a-data-science-client.md).

## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
> [Lección 1: Crear la base de datos y permisos](deepdive-work-with-sql-server-data-using-r.md)

