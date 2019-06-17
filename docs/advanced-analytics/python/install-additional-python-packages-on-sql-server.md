---
title: 'Instalar nuevos paquetes de idioma de Python: SQL Server Machine Learning'
description: Agregar nuevos paquetes de Python para SQL Server 2017 Machine Learning Services (In-Database) y Machine Learning Server (independiente).
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/16/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 0c6c4384dd6c02e35fe77a6fb2bfc4017a445b1b
ms.sourcegitcommit: a91c3f4fe2587d474cd4d470bda93239ba2693bb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/14/2019
ms.locfileid: "67140719"
---
# <a name="install-new-python-packages-on-sql-server"></a>Instalar nuevos paquetes de Python en SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este artículo se describe cómo instalar nuevos paquetes de Python en una instancia de SQL Server 2017 Machine Learning Services. En general, el proceso para instalar nuevos paquetes es similar de un entorno de Python estándar. Sin embargo, son necesarios algunos pasos adicionales si el servidor no tiene una conexión a internet.

Para obtener más información acerca de las rutas de acceso de ubicación e instalación del paquete, consulte [obtener R o Python información del paquete](../package-management/installed-package-information.md).

## <a name="prerequisites"></a>Requisitos previos

+ [SQL Server 2017 Machine Learning Services (In-Database)](../install/sql-machine-learning-services-windows-install.md) con la opción de lenguaje Python. 

+ Paquetes deben ser Python 3.5 conforme y se ejecutan en Windows. 

+ Se requiere acceso administrativo al servidor para instalar paquetes.

## <a name="considerations"></a>Consideraciones

Antes de agregar los paquetes, considere si el paquete es una buena elección para el entorno de SQL Server. Normalmente, un servidor de base de datos es un recurso compartido de acomodar varias cargas de trabajo. Si agrega los paquetes que se coloca demasiada presión de cálculo en el servidor, el rendimiento se verá afectado. 

Además, algunos paquetes de Python populares (como Flask) realizan tareas, como el desarrollo web, que son más adecuadas para un entorno independiente. Se recomienda que use Python en bases de datos para las tareas que se benefician de una estrecha integración con el motor de base de datos, como el aprendizaje automático, en lugar de las tareas que simplemente consultar la base de datos.

Servidores de base de datos con frecuencia están bloqueados. En muchos casos, el acceso a Internet está bloqueado por completo. Para los paquetes con una larga lista de dependencias, deberá identificar estas dependencias de antemano y estar dispuesto a instalar manualmente cada uno de ellos.

## <a name="add-a-new-python-package"></a>Agregar un nuevo paquete de Python

En este ejemplo, suponemos que desea instalar un nuevo paquete directamente en el equipo de SQL Server.

Instalación del paquete es por instancia. Si tiene varias instancias de servicios de Machine Learning, debe agregar el paquete a cada uno de ellos.

El paquete instalado en este ejemplo es [CNTK](https://docs.microsoft.com/cognitive-toolkit/), un marco para el aprendizaje profundo de Microsoft que admite la personalización, entrenamiento y el uso compartido de tipos diferentes de las redes neuronales.

### <a name="step-1-download-the-windows-version-of-the-python-package"></a>Paso 1. Descargue la versión de Windows del paquete de Python

+ Si va a instalar los paquetes de Python en un servidor sin acceso a internet, debe descargar el archivo WHL en un equipo diferente y, a continuación, copiarlo en el servidor.

    Por ejemplo, en un equipo independiente, puede descargar el archivo WHL desde este sitio [ https://cntk.ai/PythonWheel/CPU-Only ](https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl)y, a continuación, copie el archivo `cntk-2.1-cp35-cp35m-win_amd64.whl` en una carpeta local en el equipo de SQL Server.

+ SQL Server 2017 usa Python 3.5. 

> [!IMPORTANT]
> Asegúrese de que obtiene la versión de Windows del paquete. Si el archivo termina en .gz, probablemente no es la versión correcta.

Esta página contiene las descargas para varias plataformas y para varias versiones de Python: [Configuración de CNTK](https://docs.microsoft.com/cognitive-toolkit/Setup-CNTK-on-your-machine)

### <a name="step-2-open-a-python-command-prompt"></a>Paso 2. Abra un símbolo del sistema de Python

Busque la ubicación de biblioteca de Python predeterminado utilizada por SQL Server. Si tiene instaladas varias instancias, busque la carpeta PYTHON_SERVICE para la instancia donde desea agregar el paquete.

Por ejemplo, si se ha instalado Machine Learning Services con los valores predeterminados y aprendizaje automático está habilitado en la instancia predeterminada, la ruta de acceso sería como sigue:

    `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES`

Abra el símbolo del sistema de Python asociado a la instancia.

> [!TIP]
> Para futuras depurar y probar, puede configurar un entorno de Python específico a la biblioteca de la instancia.

### <a name="step-3-install-the-package-using-pip"></a>Paso 3. Instale el paquete con pip

+ Si está acostumbrado a utilizar la línea de comandos de Python, use PIP.exe para instalar nuevos paquetes. Puede encontrar el **pip** instalador en el `Scripts` subcarpeta. 

  El programa de instalación de SQL Server no agregar Scripts a la ruta de acceso del sistema. Si se produce un error que `pip` no se reconoce como un comando interno o externo, puede agregar la carpeta de Scripts a la variable de ruta de acceso en Windows.

  La ruta de acceso completa de la **Scripts** carpeta en una instalación predeterminada es como sigue:

    C:\Program Files\Microsoft SQL Server\MSSQL14. MSSQLSERVER\PYTHON_SERVICES\Scripts

+ Si usa Visual Studio 2017 o Visual Studio 2015 con las extensiones de Python, puede ejecutar `pip install` desde el **entornos de Python** ventana. Haga clic en **paquetes**y en el cuadro de texto, proporcione el nombre o la ubicación del paquete para instalar. No es necesario escribir `pip install`; se rellena automáticamente automáticamente. 

    - Si el equipo tiene acceso a Internet, proporcione el nombre del paquete o la dirección URL de un paquete específico y una versión. 
    
    Por ejemplo, para instalar la versión de CNTK que es compatible con Windows y Python 3.5, especifique la dirección URL de descarga: `https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl`

    - Si el equipo no tiene acceso a internet, debe descargar el archivo WHL antes de comenzar la instalación. A continuación, especifique el nombre y ruta de acceso local. Por ejemplo, pegue la ruta de acceso y el archivo para instalar el archivo WHL descargado desde el sitio siguiente: `"C:\Downloads\CNTK\cntk-2.1-cp35-cp35m-win_amd64.whl"`

Es posible que se le elevar los permisos para completar la instalación.

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

Cuando se complete la instalación, puede empezar inmediatamente con el paquete como se describe en el paso siguiente.

Para obtener ejemplos de aprendizaje profundo con CNTK, consulte estos tutoriales: [API de Python de CNTK](https://cntk.ai/pythondocs/tutorials.html)

Para utilizar las funciones del paquete en el script, inserte el estándar `import <package_name>` instrucción en las primeras líneas del script:

```python
import numpy as np
import cntk as cntk
cntk._version_
```

## <a name="list-installed-packages-using-conda"></a>Enumerar los paquetes instalados mediante conda

Hay distintas maneras en que puede obtener una lista de los paquetes instalados. Por ejemplo, puede ver los paquetes instalados en el **entornos de Python** windows de Visual Studio.

Si está utilizando la línea de comandos de Python, puede usar **Pip** o **conda** Administrador de paquetes, incluido con el entorno Anaconda Python que se agregó el programa de instalación de SQL Server.

1. Vaya a C:\Program Files\Microsoft SQL Server\MSSQL14. MSSQLSERVER\PYTHON_SERVICES\Scripts

1. Haga clic en **conda.exe** > **ejecutar como administrador**y escriba `conda list` para devolver una lista de los paquetes instalados en el entorno actual.

1. De forma similar, haga clic en **pip.exe** > **ejecutar como administrador**y escriba `pip list` para devolver la misma información. 

Para obtener más información acerca de **conda** y cómo puede utilizarlo para crear y administrar varios entornos de Python, consulte [administración de entornos de conda](https://conda.io/docs/user-guide/tasks/manage-environments.html).

> [!Note]
> El programa de instalación de SQL Server no agrega Pip o Conda mantener archivos ejecutables que no sean esenciales fuera de la ruta de acceso a la ruta de acceso del sistema y en una instancia de SQL Server de producción, es una práctica recomendada. Sin embargo, para entornos de desarrollo y pruebas, puede agregar la carpeta de Scripts a la variable de entorno PATH del sistema para ejecutar Pip y Conda en comandos desde cualquier ubicación.
