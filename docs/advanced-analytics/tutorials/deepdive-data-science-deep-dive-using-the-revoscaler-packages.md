---
title: RevoScaleR función más profundamente tutorial - SQL Server Machine Learning
description: En este tutorial, aprenderá cómo llamar a funciones de RevoScaleR mediante la integración de R de SQL Server Machine Learning.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 28f3ebe1887e188513c01881f68d5d7f323e31f2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962244"
---
# <a name="tutorial-use-revoscaler-r-functions-with-sql-server-data"></a>Tutorial: Usar funciones de RevoScaleR R con datos de SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) es un paquete de Microsoft R que proporciona distribuido y el procesamiento en paralelo para las cargas de trabajo de aprendizaje automático y ciencia de datos. Para el desarrollo de R en SQL Server, **RevoScaleR** es uno de los principales paquetes integrados, con funciones para crear objetos de origen de datos, establecer un contexto de cálculo, administración de paquetes y lo más importante: trabajar con datos-to-end, en la importación para visualización y análisis. Algoritmos de aprendizaje automático en SQL Server tienen una dependencia en **RevoScaleR** orígenes de datos. Dada la importancia de **RevoScaleR**, saber cuándo y cómo llamar a sus funciones es una habilidad esencial. 

En este tutorial de varias partes, se introducen en un intervalo de **RevoScaleR** funciones para las tareas asociadas con la ciencia de datos. En el proceso, obtendrá información sobre cómo crear un contexto de cálculo remoto, movimiento de datos entre contextos de cálculo locales y remotos y ejecutar código R en un servidor SQL remoto. También aprenderá cómo analizar y representar los datos localmente y en el servidor remoto y cómo crear e implementar modelos.

## <a name="prerequisites"></a>Requisitos previos

+ [SQL Server 2017 Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) con la característica R, o [SQL Server 2016 R Services (en bases de datos)](../install/sql-r-services-windows-install.md)
  
+ [Permisos de base de datos](../security/user-permission.md) y un inicio de sesión de usuario de base de datos de SQL Server

+ [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)

+ Un IDE como RStudio o la herramienta RGUI integrada que se incluye con R

Para alternar entre los contextos de cálculo locales y remotos, necesita dos sistemas. Normalmente, local es una estación de trabajo de desarrollo con potencia suficiente para cargas de trabajo de ciencia de datos. Remoto en este caso es SQL Server 2017 ni SQL Server 2016 con la característica R habilitada. 

Cambiar contextos de cálculo se basa en tener la misma versión **RevoScaleR** en sistemas locales y remotos. En una estación de trabajo local, puede obtener el **RevoScaleR** proveedores relacionados mediante la instalación de Microsoft R Client y paquetes.

Si tiene que colocar el cliente y servidor en el mismo equipo, asegúrese de instalar un segundo conjunto de bibliotecas de R de Microsoft para enviar el script de R desde un cliente "remoto". No utilice las bibliotecas de R que se instalan en los archivos de programa de la instancia de SQL Server. En concreto, si usas un equipo, necesita el **RevoScaleR** biblioteca en ambas ubicaciones para admitir las operaciones de cliente y servidor.

+ C:\Program Files\Microsoft\R Client\R_SERVER\library\RevoScaleR 
+ C:\Program Files\Microsoft SQL Server\MSSQL14. MSSQLSERVER\R_SERVICES\library\RevoScaleR

Para obtener instrucciones sobre la configuración del cliente, consulte [configurar un cliente de ciencia de datos para el desarrollo de R](../r/set-up-a-data-science-client.md).


## <a name="r-development-tools"></a>Herramientas de desarrollo de R

Normalmente, los desarrolladores de R usarán IDE para escribir y depurar código de R. Estas son algunas sugerencias:

- **Herramientas de R para Visual Studio** (RTVS) es un complemento gratuito complemento que proporciona Intellisense, depuración y soporte técnico para Microsoft R. Puede usarlo con R Server y SQL Server Machine Learning Services. Para descargarlo, consulte la página sobre [Herramientas de R para Visual Studio](https://www.visualstudio.com/vs/rtvs/).

- **RStudio** es uno de los entornos de desarrollo de R más populares. Para obtener más información, consulte [ https://www.rstudio.com/products/RStudio/ ](https://www.rstudio.com/products/RStudio/).

- Herramientas básicas de R (R.exe, RTerm.exe, RScripts.exe) también se instalan de forma predeterminada al instalar R en SQL Server o cliente de R. Si no desea instalar un IDE, puede usar las herramientas integradas de R para ejecutar el código en este tutorial.

Recuerde que **RevoScaleR** es necesario en equipos locales y remotos. No se puede completar este tutorial con una instalación genérica de RStudio u otro entorno que carece de las bibliotecas de R de Microsoft. Para obtener más información, consulte [Configurar un cliente de ciencia de datos](../r/set-up-a-data-science-client.md).

## <a name="summary-of-tasks"></a>Resumen de tareas

+ Los datos se han obtenido inicialmente de archivos CSV o archivos XDF. Importar los datos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando las funciones en el **RevoScaleR** paquete.
+ Entrenamiento de modelos y de puntuación se realizan mediante el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contexto de proceso. 
+ Use **RevoScaleR** funciones para crear nuevos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tablas para guardar los resultados de puntuación.
+ Crear trazados tanto en el servidor y el contexto de proceso local.
+ Entrenar un modelo de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] base de datos, que se ejecuta R en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instancia.
+ Extraer un subconjunto de datos y guárdelo como un archivo XDF para volver a usar en el análisis en su estación de trabajo local.
+ Obtener nuevos datos para puntuación, abriendo una conexión ODBC a la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] base de datos. Se realiza la puntuación en la estación de trabajo local.
+ Cree una función personalizada de R y ejecutarlo en el servidor de contexto de proceso para realizar una simulación.

## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
> [Lección 1: Crear base de datos y permisos](deepdive-work-with-sql-server-data-using-r.md)