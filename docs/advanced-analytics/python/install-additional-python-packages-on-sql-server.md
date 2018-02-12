---
title: Instalar nuevos paquetes de Python en SQL Server | Documentos de Microsoft
ms.date: 01/04/2018
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: python
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 21456462-e58a-44c3-9d3a-68b4263575d7
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: 68c3c0c3699455854ac23fed7befb042eaf17155
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2018
---
# <a name="install-new-python-packages-on-sql-server"></a>Instalar nuevos paquetes de Python en SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este artículo se describe cómo instalar nuevos paquetes de Python en una instancia de SQL Server 2017.

También describe cómo enumerar los paquetes que están instalados en el entorno actual.

## <a name="prerequisites"></a>Requisitos previos

El proceso para instalar nuevos paquetes es muy probable que en un entorno estándar de Python. Sin embargo, son necesarios algunos pasos adicionales si el servidor no tiene una conexión a internet.

+ Debe instalar Machine Learning Services (In-Database) con la opción de lenguaje de Python. Para obtener instrucciones, consulte [configurar los servicios de aprendizaje de máquina de Python](setup-python-machine-learning-services.md).

+ Para cada instancia del servidor, debe instalar una copia independiente del paquete. Los paquetes no se pueden compartir entre instancias.

+ Determinar si el paquete que se va a utilizar funcionará con Python 3.5 y en el entorno de Windows. 

    En general, existen algunas limitaciones en los paquetes que se pueden importar y utilizar en el entorno de SQL Server. Los problemas posibles incluyen los paquetes que utilizan la funcionalidad de red que está bloqueada en el servidor o el firewall, o con dependencias que no se puede instalar en un equipo Windows.

+ Se requiere acceso administrativo al servidor para instalar paquetes.

## <a name="add-a-new-python-package"></a>Agregue un nuevo paquete de Python

En este ejemplo, se supone que va a instalar un nuevo paquete directamente en el equipo de SQL Server.

El paquete instalado en este ejemplo es [CNTK](https://docs.microsoft.com/cognitive-toolkit/), un marco de aprendizaje profundo de Microsoft que admite la personalización, entrenamiento y de uso compartido de tipos diferentes de las redes neurales.

> [!TIP]
> ¿Necesita ayuda para configurar las herramientas Python? Consulte estos blogs:
> 
> [Introducción a servicios Web de Python con el servidor de aprendizaje de máquina](https://blogs.msdn.microsoft.com/mlserver/2017/12/13/getting-started-with-python-web-services-using-machine-learning-server/)
> 
> [David recodo: Kit de herramientas de Microsoft cognitivos + frente a código](http://dacrook.com/cntk-vs-code-awesome/)

### <a name="step-1-download-the-windows-version-of-the-python-package"></a>Paso 1. Descargue la versión de Windows del paquete Python

+ Si va a instalar los paquetes de Python en un servidor sin acceso a internet, debe descargar el archivo WHL en un equipo diferente y, a continuación, copiarlo en el servidor.

    Por ejemplo, en un equipo diferente, puede descargar el archivo WHL desde este sitio [https://cntk.ai/PythonWheel/CPU-Only](https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl)y, a continuación, copie el archivo `cntk-2.1-cp35-cp35m-win_amd64.whl` en una carpeta local en el equipo de SQL Server.

+ SQL Server 2017 utiliza 3.5 de Python. Asegúrese de obtener la versión de Windows del paquete y una versión que sea compatible con Python 3.5.

Esta página contiene descargas para varias plataformas y varias versiones de Python: [configurar CNTK](https://docs.microsoft.com/cognitive-toolkit/Setup-CNTK-on-your-machine)

### <a name="step-2-open-a-python-command-prompt"></a>Paso 2. Abra un símbolo del sistema de Python

Busque la ubicación predeterminada de la biblioteca de Python utilizada por SQL Server. Si tiene instaladas varias instancias, asegúrese de buscar la carpeta PYTHON_SERVICE para la instancia en la que desea agregar el paquete.

Por ejemplo, si se ha instalado servicios de aprendizaje de máquina con los valores predeterminados y aprendizaje automático está habilitado en la instancia predeterminada, la ruta de acceso sería como sigue:

    `C:\Program Files\Microsoft SQL  Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES`

Abra el símbolo del sistema de Python asociado a la instancia.

> [!TIP]
> Se recomienda que configure un entorno de Python específicos de servidor de aprendizaje de máquina o SQL Server.

### <a name="step-3-install-the-package-using-pip"></a>Paso 3. Instale el paquete mediante pip

+ Si está acostumbrado a utilizar la línea de comandos de Python, use PIP.exe para instalar nuevos paquetes. Puede encontrar el **pip** instalador en el `Scripts` subcarpeta. 

    Si se produce un error que **pip** no se reconoce como un comando interno o externo, puede agregar la ruta de acceso del ejecutable de Python y la carpeta de scripts de Python a la variable de ruta de acceso en Windows.

    La ruta de acceso completa de la **Scripts** carpeta en una instalación predeterminada es la siguiente:

    `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\Scripts`

+ Si usas 2017 de Visual Studio o Visual Studio 2015 con las extensiones de Python, puede ejecutar `pip install` desde el **entornos de Python** ventana. Haga clic en **paquetes**y en el cuadro de texto, proporcione el nombre o la ubicación del paquete para instalar. No es necesario escribir `pip install`; se rellena automáticamente automáticamente. 

    - Si el equipo tiene acceso a Internet, proporcione el nombre del paquete o la dirección URL de un paquete específico y una versión. Por ejemplo, para instalar la versión de CNTK que es compatible con Windows y 3.5 de Python, puede especificar la URL de descarga:`https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl`

    - Si el equipo no tiene acceso a internet, debe ha descargado el archivo WHL de antemano. A continuación, especifique el nombre y ruta de acceso local. Por ejemplo, pegue la ruta de acceso y el archivo para instalar el archivo WHL descargado desde el sitio siguiente:`"C:\Downloads\CNTK\cntk-2.1-cp35-cp35m-win_amd64.whl"`

Puede que deba elevar los permisos para completar la instalación.

A medida que progresa de instalación, puede ver mensajes de estado en la ventana de símbolo del sistema:

```python
pip install https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl
Collecting cntk==2.1 from https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl
  Downloading https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl (34.1MB)
    100% |################################| 34.1MB 13kB/s
...
Installing collected packages: cntk
Successfully installed cntk-2.1
```



### <a name="step-4-load-the-package-or-its-functions-as-part-of-your-script"></a>Paso 4. Cargar el paquete o sus funciones como parte de la secuencia de comandos

Cuando una vez completada la instalación, puede empezar inmediatamente con el paquete tal como se describe en el paso siguiente.

Para obtener ejemplos de aprendizaje profundo mediante CNTK, consulte estos tutoriales: [API de Python para CNTK](https://cntk.ai/pythondocs/tutorials.html)

Para utilizar las funciones del paquete en el script, inserte el estándar `import <package_name>` instrucción en las líneas iniciales de la secuencia de comandos:

```python
import numpy as np
import cntk as cntk
cntk._version_
```

##  <a name="how-to-view-installed-packages-using-conda"></a>Cómo ver los paquetes instalados con conda

Hay distintas maneras en que puede obtener una lista de los paquetes instalados. Por ejemplo, puede ver los paquetes instalados en la **entornos de Python** windows de Visual Studio.

Si está utilizando la línea de comandos de Python, puede usar el **conda** Administrador de paquetes que se incluye en el entorno Anaconda Python agregado por el programa de instalación de SQL Server.

Para ver los paquetes de Python que se hayan instalado en el entorno actual, ejecute este comando desde el símbolo del sistema de windows:

```python
conda list
```

Para obtener más información acerca de **conda** y cómo puede utilizarlo para crear y administrar varios entornos de Python, consulte [administrar entornos con conda](https://conda.io/docs/user-guide/tasks/manage-environments.html).
