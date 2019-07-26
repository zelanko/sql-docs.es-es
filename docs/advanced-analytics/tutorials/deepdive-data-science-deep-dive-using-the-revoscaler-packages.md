---
title: 'Tutorial detallado de la función RevoScaleR: SQL Server Machine Learning'
description: En este tutorial, obtendrá información sobre cómo llamar a las funciones de RevoScaleR mediante la integración de SQL Server Machine Learning R.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: c326d51e9b3ac4edac61f97bf5f7fa3143d8d350
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470630"
---
# <a name="tutorial-use-revoscaler-r-functions-with-sql-server-data"></a>Tutorial: Uso de funciones de RevoScaleR R con datos de SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) es un paquete de Microsoft R que proporciona procesamiento paralelo y distribuido para cargas de trabajo de ciencia de datos y aprendizaje automático. Para el desarrollo de R en SQL Server, **RevoScaleR** es uno de los paquetes integrados principales, con funciones para crear objetos de origen de datos, establecer un contexto de proceso, administrar paquetes y, lo más importante: trabajar con datos de un extremo a otro, desde importar a visualización y análisis. Machine Learning algoritmos en SQL Server tener una dependencia en los orígenes de datos de **RevoScaleR** . Dada la importancia de **RevoScaleR**, saber cuándo y cómo llamar a sus funciones es una habilidad esencial. 

En este tutorial de varias partes, se presenta una serie de funciones de **RevoScaleR** para las tareas asociadas a la ciencia de datos. En el proceso, obtendrá información sobre cómo crear un contexto de cálculo remoto, cómo trasladar datos entre contextos de cálculo locales y remotos, y cómo ejecutar código R en un SQL Server remoto. También aprenderá a analizar y trazar datos tanto localmente como en el servidor remoto, y cómo crear e implementar modelos.

## <a name="prerequisites"></a>Requisitos previos

+ [SQL Server 2017 Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) con la característica de R o [SQL Server 2016 R Services (en base de datos)](../install/sql-r-services-windows-install.md)
  
+ [Permisos de base de datos](../security/user-permission.md) y un inicio de sesión de usuario de SQL Server Database

+ [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)

+ Un IDE como RStudio o la herramienta de RGUI integrada incluida con R

Para alternar entre los contextos de cálculo locales y remotos, se necesitan dos sistemas. Local suele ser una estación de trabajo de desarrollo con una capacidad suficiente para cargas de trabajo de ciencia de datos. En este caso, remoto es SQL Server 2017 o SQL Server 2016 con la característica de R habilitada. 

El cambio de los contextos de cálculo se basa en tener la misma versión de **RevoScaleR** en sistemas locales y remotos. En una estación de trabajo local, puede obtener los paquetes de **RevoScaleR** y los proveedores relacionados mediante la instalación de Microsoft R Client.

Si necesita poner el cliente y el servidor en el mismo equipo, asegúrese de instalar un segundo conjunto de bibliotecas de Microsoft R para enviar scripts de R desde un cliente "remoto". No use las bibliotecas de R que están instaladas en los archivos de programa de la instancia de SQL Server. En concreto, si usa un equipo, necesita la biblioteca **RevoScaleR** en ambas ubicaciones para admitir las operaciones de cliente y de servidor.

+ C:\Archivos de Files\Microsoft\R Client\R_SERVER\library\RevoScaleR 
+ C:\Archivos de Programa\microsoft SQL Server\MSSQL14. MSSQLSERVER\R_SERVICES\library\RevoScaleR

Para obtener instrucciones sobre la configuración de cliente, consulte Configuración de [un cliente de ciencia de datos para el desarrollo en R](../r/set-up-a-data-science-client.md).


## <a name="r-development-tools"></a>Herramientas de desarrollo de R

Los desarrolladores de r suelen usar IDE para escribir y depurar código de R. Estas son algunas sugerencias:

- **Herramientas de R para Visual Studio** (RTVS) es un complemento gratuito que proporciona IntelliSense, depuración y soporte técnico para Microsoft R. Puede utilizarlo con R Server y SQL Server Machine Learning Services. Para descargarlo, consulte la página sobre [Herramientas de R para Visual Studio](https://www.visualstudio.com/vs/rtvs/).

- **RStudio** es uno de los entornos de desarrollo de R más populares. Para obtener más información, [https://www.rstudio.com/products/RStudio/](https://www.rstudio.com/products/RStudio/)vea.

- Las herramientas básicas de R (R. exe, RTerm. exe, RScripts. exe) también se instalan de forma predeterminada al instalar R en SQL Server o en el cliente de R. Si no desea instalar un IDE, puede usar las herramientas de R integradas para ejecutar el código de este tutorial.

Recuerde que **RevoScaleR** es necesario en equipos locales y remotos. No puede completar este tutorial con una instalación genérica de RStudio u otro entorno que no tenga las bibliotecas de Microsoft R. Para obtener más información, consulte [Configurar un cliente de ciencia de datos](../r/set-up-a-data-science-client.md).

## <a name="summary-of-tasks"></a>Resumen de tareas

+ Los datos se han obtenido inicialmente de archivos CSV o archivos XDF. Los datos se importan [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en mediante las funciones del paquete **RevoScaleR** .
+ El entrenamiento y la puntuación del modelo se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] realizan mediante el contexto de cálculo. 
+ Use las funciones de **RevoScaleR** para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] crear nuevas tablas con el fin de guardar los resultados de puntuación.
+ Cree trazados tanto en el servidor como en el contexto de proceso local.
+ Entrenar un modelo en los datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de la base de datos, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ejecutando R en la instancia.
+ Extraiga un subconjunto de datos y guárdelo como un archivo XDF para reutilizarlo en el análisis en su estación de trabajo local.
+ Obtener datos nuevos para la puntuación, abriendo una conexión ODBC con la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] base de datos. La puntuación se realiza en la estación de trabajo local.
+ Cree una función personalizada de R y ejecútela en el contexto de proceso del servidor para realizar una simulación.

## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
> [Lección 1: Crear base de datos y permisos](deepdive-work-with-sql-server-data-using-r.md)