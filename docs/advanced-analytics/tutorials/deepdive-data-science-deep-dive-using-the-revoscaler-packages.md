---
title: Tutorial detallado de RevoScaleR
description: En esta serie de tutoriales, aprenderá a llamar a las funciones de RevoScaleR mediante la integración de SQL Server Machine Learning R.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: fc1f427659155b5379a681787a633b6037b4bd87
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "76918826"
---
# <a name="tutorial-use-revoscaler-r-functions-with-sql-server-data"></a>Tutorial: Uso de funciones de RevoScaleR de R con datos de SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

En esta serie de tutoriales de varias partes, conocerá una serie de funciones **RevoScaleR** para tareas asociadas a la ciencia de datos. En el proceso, aprenderá a crear un contexto de proceso remoto, trasladar datos entre contextos de proceso locales y remotos, y ejecutar código R en un servidor SQL Server remoto. También aprenderá a analizar y trazar datos tanto a nivel local como en el servidor remoto, y a crear e implementar modelos.

[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) es un paquete de Microsoft R que proporciona procesamiento paralelo y distribuido para cargas de trabajo de ciencia de datos y aprendizaje automático. Para el desarrollo de R en SQL Server, **RevoScaleR** es uno de los paquetes integrados principales, con funciones para crear objetos de origen de datos, establecer un contexto de proceso, administrar paquetes y, lo que es más importante, trabajar con datos de un extremo a otro, desde la importación hasta la visualización y el análisis. Los algoritmos de aprendizaje automático en SQL Server tienen una dependencia en orígenes de datos de **RevoScaleR**. Dada la importancia de **RevoScaleR**, es fundamental saber cuándo y cómo llamar a sus funciones. 

## <a name="prerequisites"></a>Prerequisites

+ [SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) con la función R o [SQL Server R Services (en la base de datos)](../install/sql-r-services-windows-install.md)
  
+ [Permisos de base de datos](../security/user-permission.md) y un inicio de sesión de usuario de base de datos de SQL Server

+ [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)

+ Un IDE como RStudio o la herramienta de RGUI integrada incluida con R

Para alternar entre los contextos de proceso locales y remotos, se necesitan dos sistemas. El contexto local suele ser una estación de trabajo de desarrollo con capacidad suficiente para cargas de trabajo de ciencia de datos. El contexto remoto, en este caso, es un servidor SQL Server con la característica R habilitada. 

El cambio de los contextos de proceso se basa en tener la misma versión de **RevoScaleR** en los sistemas locales y remotos. En una estación de trabajo local, puede obtener los paquetes de **RevoScaleR** y los proveedores relacionados si instala Microsoft R Client.

Si necesita colocar el cliente y el servidor en el mismo equipo, asegúrese de instalar un segundo conjunto de bibliotecas de Microsoft R para enviar scripts de R desde un cliente "remoto". No use las bibliotecas de R que están instaladas en los archivos de programa de la instancia de SQL Server. Concretamente, si usa un equipo, necesita tener la biblioteca **RevoScaleR** en ambas ubicaciones para admitir las operaciones de cliente y de servidor.

+ C:\Archivos de programa\Microsoft\R Client\R_SERVER\library\RevoScaleR 
+ C:\Archivos de programa\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library\RevoScaleR

Para obtener instrucciones sobre la configuración de cliente, vea [Configuración de un cliente de ciencia de datos para el desarrollo en R](../r/set-up-a-data-science-client.md).


## <a name="r-development-tools"></a>Herramientas de desarrollo en R

Los desarrolladores de R suelen usar varios IDE para escribir y depurar código de R. Estas son algunas sugerencias:

- **Herramientas de R para Visual Studio** (RTVS) es un complemento gratuito que proporciona IntelliSense, depuración y compatibilidad con Microsoft R. Puede usarse con R Server y SQL Server Machine Learning Services. Para descargarlo, consulte la página sobre [Herramientas de R para Visual Studio](https://marketplace.visualstudio.com/items?itemName=MikhailArkhipov007.RTVS2019).

- **RStudio** es uno de los entornos de desarrollo de R más populares. Para más información, vea [https://www.rstudio.com/products/RStudio/](https://www.rstudio.com/products/RStudio/).

- Las herramientas básicas de R (R.exe, RTerm.exe, RScripts.exe) también se instalan de forma predeterminada al instalar R en SQL Server o en el cliente de R. Si no quiere instalar un IDE, puede usar las herramientas de R integradas para ejecutar el código de este tutorial.

Recuerde que **RevoScaleR** es necesario en el equipo local y en el remoto. No puede completar este tutorial con una instalación genérica de RStudio u otro entorno que no tenga las bibliotecas de Microsoft R. Para obtener más información, consulte [Configurar un cliente de ciencia de datos](../r/set-up-a-data-science-client.md).

## <a name="summary-of-tasks"></a>Resumen de tareas

+ Los datos se han obtenido inicialmente de archivos CSV o archivos XDF. Ahora tiene que importar los datos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando las funciones del paquete **RevoScaleR**.
+ El entrenamiento de modelos y la puntuación se realiza en el contexto de proceso de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. 
+ Use las funciones de **RevoScaleR** para crear nuevas tablas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para guardar los resultados de puntuación.
+ Cree trazados tanto en el servidor como en el contexto de proceso local.
+ Entrene un modelo con los datos de la base de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ejecutando R en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
+ Extraiga un subconjunto de datos y guárdelos como un archivo XDF para volver a usarlos en el análisis en la estación de trabajo local.
+ Para obtener datos nuevos para la puntuación, abra una conexión ODBC con la base de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La puntuación se realiza en la estación de trabajo local.
+ Cree una función personalizada de R y ejecútela en el contexto de proceso del servidor para realizar una simulación.

## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
> [Tutorial 1: Crear bases de datos y permisos](deepdive-work-with-sql-server-data-using-r.md)