---
title: Instalar nuevos paquetes de idioma de Python
description: Agregue nuevos paquetes de Python a SQL Server 2017 Machine Learning Services (in-Database) y Machine Learning Server (independiente).
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/16/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: fc8c7148369ec1a501106e573e195a8f0b7f060a
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470256"
---
# <a name="install-new-python-packages-on-sql-server"></a>Instalar nuevos paquetes de Python en SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

En este artículo se describe cómo instalar nuevos paquetes de Python en una instancia de SQL Server 2017 Machine Learning Services. En general, el proceso de instalación de nuevos paquetes es similar al de un entorno estándar de Python. Sin embargo, se requieren algunos pasos adicionales si el servidor no tiene conexión a Internet.

Para obtener más información sobre la ubicación del paquete y las rutas de instalación, vea [obtener información de paquetes de R o Python](../package-management/installed-package-information.md).

## <a name="prerequisites"></a>Requisitos previos

+ [SQL Server 2017 Machine Learning Services (in-Database)](../install/sql-machine-learning-services-windows-install.md) con la opción del lenguaje Python. 

+ Los paquetes deben ser compatibles con Python 3,5 y ejecutarse en Windows. 

+ Se requiere acceso administrativo al servidor para instalar paquetes.

## <a name="considerations"></a>Consideraciones

Antes de agregar paquetes, considere si el paquete es una buena opción para el entorno de SQL Server. Normalmente, un servidor de base de datos es un recurso compartido que alberga varias cargas de trabajo. Si agrega paquetes que imponen demasiada presión computacional en el servidor, el rendimiento se verá afectado. 

Además, algunos paquetes conocidos de Python (por ejemplo, el frasco) realizan tareas, como el desarrollo web, que son más adecuadas para un entorno independiente. Se recomienda usar Python en la base de datos para las tareas que se benefician de la estrecha integración con el motor de base de datos, como machine learning, en lugar de tareas que simplemente consultan la base de datos.

Los servidores de bases de datos suelen estar bloqueados. En muchos casos, el acceso a Internet se bloquea por completo. En el caso de los paquetes con una larga lista de dependencias, tendrá que identificar estas dependencias de antemano y estar dispuesto a instalarlas manualmente.

## <a name="add-a-new-python-package"></a>Agregar un nuevo paquete de Python

En este ejemplo, se supone que desea instalar un nuevo paquete directamente en el SQL Server equipo.

La instalación del paquete es por instancia. Si tiene varias instancias de Machine Learning Services, debe agregar el paquete a cada uno de ellos.

El paquete instalado en este ejemplo es [CNTK](https://docs.microsoft.com/cognitive-toolkit/), un marco de trabajo de aprendizaje profundo de Microsoft que admite la personalización, el entrenamiento y el uso compartido de distintos tipos de redes neuronal.

### <a name="step-1-download-the-windows-version-of-the-python-package"></a>Paso 1. Descargar la versión de Windows del paquete de Python

+ Si va a instalar paquetes de Python en un servidor sin acceso a Internet, debe descargar el archivo WHL en otro equipo y, a continuación, copiarlo en el servidor.

    Por ejemplo, en un equipo independiente, puede descargar el archivo WHL de este sitio [https://cntk.ai/PythonWheel/CPU-Only](https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl)y, a continuación, copiar el archivo `cntk-2.1-cp35-cp35m-win_amd64.whl` en una carpeta local del equipo SQL Server.

+ SQL Server 2017 usa Python 3,5. 

> [!IMPORTANT]
> Asegúrese de obtener la versión de Windows del paquete. Si el archivo termina en. gz, probablemente no sea la versión correcta.

Esta página contiene descargas para varias plataformas y para varias versiones de Python: [Configuración de CNTK](https://docs.microsoft.com/cognitive-toolkit/Setup-CNTK-on-your-machine)

### <a name="step-2-open-a-python-command-prompt"></a>Paso 2. Abra un símbolo del sistema de Python

Busque la ubicación predeterminada de la biblioteca de Python usada por SQL Server. Si ha instalado varias instancias, busque la carpeta PYTHON_SERVICE de la instancia en la que desea agregar el paquete.

Por ejemplo, si se ha instalado Machine Learning Services con los valores predeterminados y el aprendizaje automático está habilitado en la instancia predeterminada, la ruta de acceso sería la siguiente:

    `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES`

Abra el símbolo del sistema de Python asociado a la instancia.

> [!TIP]
> Para futuras depuraciones y pruebas, es posible que desee configurar un entorno de Python específico para la biblioteca de instancias.

### <a name="step-3-install-the-package-using-pip"></a>Paso 3. Instalación del paquete con PIP

+ Si está acostumbrado a usar la línea de comandos de Python, use PIP. exe para instalar nuevos paquetes. Puede encontrar el instalador de **PIP** en la `Scripts` subcarpeta. 

  SQL Server el programa de instalación no agrega scripts a la ruta de acceso del sistema. Si recibe un error que `pip` no se reconoce como un comando interno o externo, puede Agregar la carpeta scripts a la variable PATH en Windows.

  La ruta de acceso completa  de la carpeta de scripts en una instalación predeterminada es la siguiente:

    C:\Archivos de Programa\microsoft SQL Server\MSSQL14. MSSQLSERVER\PYTHON_SERVICES\Scripts

+ Si usa Visual Studio 2017 o Visual Studio 2015 con las extensiones de Python, puede ejecutar `pip install` desde la ventana entornos de **Python** . Haga clic en **paquetes**y, en el cuadro de texto, proporcione el nombre o la ubicación del paquete que desea instalar. No es necesario escribir `pip install`; se rellena automáticamente. 

    - Si el equipo tiene acceso a Internet, proporcione el nombre del paquete o la dirección URL de un paquete y versión específicos. 
    
    Por ejemplo, para instalar la versión de CNTK que se admite para Windows y Python 3,5, especifique la dirección URL de descarga:`https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl`

    - Si el equipo no tiene acceso a Internet, debe descargar el archivo WHL antes de comenzar la instalación. A continuación, especifique la ruta de acceso y el nombre del archivo local. Por ejemplo, pegue la ruta de acceso y el archivo siguientes para instalar el archivo WHL descargado desde el sitio:`"C:\Downloads\CNTK\cntk-2.1-cp35-cp35m-win_amd64.whl"`

Es posible que se le pida que eleve los permisos para completar la instalación.

A medida que la instalación progresa, puede ver los mensajes de estado en la ventana del símbolo del sistema:

```python
pip install https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl
Collecting cntk==2.1 from https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl
  Downloading https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl (34.1MB)
    100% |################################| 34.1MB 13kB/s
...
Installing collected packages: cntk
Successfully installed cntk-2.1
```


### <a name="step-4-load-the-package-or-its-functions-as-part-of-your-script"></a>Paso 4. Cargar el paquete o sus funciones como parte del script

Una vez completada la instalación, puede empezar a usar el paquete inmediatamente como se describe en el paso siguiente.

Para ver ejemplos de aprendizaje profundo con CNTK, consulte estos tutoriales: [API de Python para CNTK](https://cntk.ai/pythondocs/tutorials.html)

Para usar las funciones del paquete en el script, inserte la instrucción `import <package_name>` estándar en las líneas iniciales del script:

```python
import numpy as np
import cntk as cntk
cntk._version_
```

## <a name="list-installed-packages-using-conda"></a>Enumerar los paquetes instalados con Conda

Hay diferentes maneras de obtener una lista de los paquetes instalados. Por ejemplo, puede ver los paquetes instalados en las ventanas **entornos de Python** de Visual Studio.

Si usa la línea de comandos de Python, puede usar **PIP** o el administrador de  paquetes Conda, incluido en el entorno anaconda de Python agregado por SQL Server configuración.

1. Vaya a C:\Archivos de Programa\microsoft SQL Server\MSSQL14. MSSQLSERVER\PYTHON_SERVICES\Scripts

1. Haga clic con el botón secundario en **CONDA. exe** > **Ejecutar como administrador**y escriba `conda list` para que se devuelva una lista de los paquetes instalados en el entorno actual.

1. Del mismo modo, haga clic con el botón secundario en **PIP. exe** > **Ejecutar como administrador**y escriba `pip list` para devolver la misma información. 

Para más información sobre **Conda** y cómo puede usarlo para crear y administrar varios entornos de Python, consulte [Administración de entornos con Conda](https://conda.io/docs/user-guide/tasks/manage-environments.html).

> [!Note]
> SQL Server el programa de instalación no agrega PIP ni Conda a la ruta de acceso del sistema y en una instancia de SQL Server de producción, la práctica recomendada es mantener los ejecutables no esenciales fuera de la ruta de acceso. Sin embargo, en los entornos de desarrollo y pruebas, puede Agregar la carpeta scripts a la variable de entorno de ruta de acceso del sistema para ejecutar los comandos PIP y Conda on desde cualquier ubicación.
