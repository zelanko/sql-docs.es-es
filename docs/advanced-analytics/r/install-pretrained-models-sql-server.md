---
title: Instalar modelos de aprendizaje automático previamente entrenado en SQL Server | Documentos de Microsoft
ms.date: 03/14/2018
ms.reviewer: ''
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 21456462-e58a-44c3-9d3a-68b4263575d7
caps.latest.revision: ''
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.workload: Inactive
ms.openlocfilehash: a1228597a1781ca13952a249f554bdea0a990a4d
ms.sourcegitcommit: 2e130e9f3ce8a7ffe373d7fba8b09e937c216386
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/28/2018
---
# <a name="install-pre-trained-machine-learning-models-on-sql-server"></a>Instalar previamente entrenado máquina aprendizaje de los modelos en SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artículo describe cómo agregar modelos previamente entrenados a una instancia de SQL Server que ya tiene R Services o servicios de aprendizaje de máquina de SQL Server instalado. 

Existen modelos de previamente entrenados para ayudar a los clientes que necesitan realizar tareas como las características de análisis o imagen de opinión, pero no disponen de los recursos para obtener los conjuntos de datos grandes o entrenar un modelo complejo. El equipo de servidor de aprendizaje de máquina crea y entrena estos modelos para ayudarle a empezar a trabajar en text e image procesar eficazmente. Para obtener más información, consulte el [recursos](#bkmk_resources) sección de este artículo.

Para obtener un ejemplo de cómo usar los modelos previamente entrenados con datos de SQL Server, consulte este blog del equipo de aprendizaje automático de SQL Server: [análisis de opiniones con Python en servicios de aprendizaje de máquina de SQL Server](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2017/11/01/sentiment-analysis-with-python-in-sql-server-machine-learning-services/)

## <a name="pre-trained-model-availability"></a>Disponibilidad de modelo previamente entrenado

Modelos previamente entrenados se instalan mediante los medios de instalación del servidor de aprendizaje de máquina de Microsoft (o Microsoft R Server, si va a agregar modelos a una instalación de SQL Server 2016). Puede utilizar la edición gratuita de desarrollador para instalar los modelos. No hay ningún extra costo asociado a la instalación del modelo. 

Modelos previamente entrenados trabajar con los siguientes productos e idiomas. El programa de instalación detecta la biblioteca de integración, el MicrosoftML o microsoftml de idioma y, a continuación, inserta los modelos entrenados previamente en la biblioteca correspondiente. Cuando finalice la instalación del modelo, tiene acceso a los modelos mediante funciones de la biblioteca.

+ SQL Server 2016 R Services (In-Database) - R, con el [MicrosoftML biblioteca](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)
+ SQL Server 2016 R Server (independiente) - R, con el [MicrosoftML biblioteca](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)
+ SQL Server de 2017 máquina aprendizaje Services (In-Database) - R con la [biblioteca MicrosoftML] (https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package), Python con el [microsoftml biblioteca](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package)
+ Servidor SQL Server 2017 Machine Learning (independiente) - R con la [biblioteca MicrosoftML] (https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package), Python con el [microsoftml biblioteca](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package)

El proceso de instalación puede variar ligeramente según la versión de SQL Server. Vea las secciones siguientes para obtener instrucciones para cada versión.

> [!NOTE]
> No es posible leer o modificar los modelos entrenados previamente. Se comprimen con un formato nativo para mejorar el rendimiento.

## <a name="obtain-files-for-an-offline-installation"></a>Obtener los archivos para una instalación sin conexión

Para instalar los modelos previamente entrenados en un servidor que no tiene acceso a internet, debe descargar a los instaladores adecuados de antemano y copie al instalador en una carpeta local en el servidor. 

Consulte esta página para ver los vínculos de descarga para todos los instaladores de R Server y servidor de aprendizaje de máquina: [instalación sin conexión](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-offline)

## <a name="install-pre-trained-models-on-sql-server-2016-r-services"></a>Instalar modelos previamente entrenados en SQL Server 2016 R Services

Con SQL Server 2016, puede instalar y usar los modelos de R previamente entrenados solo si primero actualiza los componentes en un proceso denominado de aprendizaje automático **enlace**. 

Para ello, ejecuta el instalador independiente de Windows para Microsoft R Server o servidor de aprendizaje de máquina en un equipo con una instalación de SQL Server 2016 R Services y seleccionar una instancia o instancias de **enlazar**. Un medio de la instancia que la directiva de soporte técnico asociada a la instancia de enlace se cambia para permitir las actualizaciones más frecuentes de R. 

1. Inicie el instalador independiente basado en Windows para cada uno [R Server](https://docs.microsoft.com/machine-learning-server/rebranding-microsoft-r-server) o [servidor de aprendizaje de máquina](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install).

2. Seleccione la instancia para actualizar y, a continuación, seleccione la opción para obtener los modelos entrenados previamente.

    Para obtener más información, consulte [actualizar componentes de aprendizaje de máquina utilizados por SQL Server](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md).

    Si previamente ha realizado el enlace para actualizar los componentes de R y sólo desea agregar los modelos previamente entrenados, deje todas las selecciones anteriores **sea**y seleccione la opción de modelos previamente entrenado. 
    
    No anule la selección de las opciones seleccionadas previamente; Si lo hace, el programa de instalación quita los componentes.

3. Se recomienda que acepte la configuración predeterminada para las ubicaciones de modelo.

4. Acepte todos los demás mensajes, incluidos los contratos de licencia.

Una vez completado el enlace, la versión de R y bibliotecas asociadas a la instancia se reemplazan por las versiones más recientes que se proporcionan en R Server o servidor de aprendizaje de máquina. 

Con SQL Server 2016, debe realizar algunos pasos adicionales para registrar los modelos de la biblioteca de instancia de SQL Server 2016. Repita estos pasos para cada instancia donde instaló los modelos entrenados previamente.

1. Abra un símbolo del sistema de Windows **como administrador**.

2. Navegue hasta la carpeta de instalación de arranque para SQL Server, que también contiene el programa de instalación de Microsoft R. En una instancia predeterminada de SQL Server 2016, la carpeta sería:
    
    `C:\Program Files\Microsoft SQL Server\130\Setup Bootstrap\SQL2017\x64\`

3. Ejecutar `RSetup.exe` e indicar el componente para instalar, la versión y la carpeta que contiene los archivos de origen del modelo, con esta sintaxis:

    `RSetup.exe /install /component MLM /version <version> /language 1033 /destdir "<SQL_DB_instance_folder>\R_SERVICES\library\MicrosoftML\mxLibs\x64"`. 

    Se admiten los siguientes valores para el parámetro de versión:

    + Candidato de versión comercial 0: **9.1.0.0**
    + Versión Release candidate 1: **9.2.0.22**
    + RTM: **9.2.0.100**
    + La actualización acumulativa 1: **9.2.0.24**
    + Actualización acumulativa 4: **9.3.0**

    > [!NOTE]
    > Se enumeran las versiones de SQL Server correspondientes para tener una idea del tiempo que se publicó la actualización. Si no estás seguro de la versión instalada con SQL Server, abra la carpeta R_SERVICES para la instancia y abra RGui (`~\R_SERVICES\bin\x64`). La pantalla inicial enumeran las versiones para la versión Microsoft R Open y el servidor de aprendizaje de máquina. 

    Por ejemplo usar R previamente entrenado modelos con una instancia predeterminada de **R_SERVICES**, ejecutaría este comando:

    `RSetup.exe /install /component MLM /version 9.2.0.24 /language 1033 /destdir "C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library\MicrosoftML\mxLibs\x64"`

    En una instancia con nombre, el comando sería algo parecido a esto:

    `RSetup.exe /install /component MLM /version 9.2.0.24 /language 1033 /destdir "C:\Program Files\Microsoft SQL Server\MSSQL13.MyInstanceName\R_SERVICES\library\MicrosoftML\mxLibs\x64"`

4. Si la instalación es correcta, los modelos siguientes deben agregarse a su `R_SERVICES` carpeta:

    + AlexNet\_Updated.model
    + ImageNet1K\_mean.xml
    + pretrained.model
    + ResNet\_101\_Updated.model
    + ResNet\_18\_Updated.model
    + ResNet\_50\_Updated.model

## <a name="install-pre-trained-models-on-sql-server-machine-learning-services-in-database"></a>Instalar modelos previamente entrenados en servicios de aprendizaje de máquina de SQL Server (In-Database)

Si ya ha instalado SQL Server 2017, puede obtener los modelos previamente entrenados de dos maneras:

+ Actualizar los componentes de Python y R mediante un enlace e instalar los modelos previamente entrenados al mismo tiempo
+ Instalar solo los modelos previamente entrenados

Las instrucciones siguientes describen el proceso para actualizar los componentes de aprendizaje de máquina y la obtención de los modelos previamente entrenados al mismo tiempo.

1. Ejecute al instalador basado en Windows para el servidor de aprendizaje de máquina. Puede descargar el instalador desde los vínculos en esta página: [instalar servidor para Windows del aprendizaje de máquina](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install).

2. Si va a instalar los modelos a un servidor que no tiene acceso a internet, asegúrese de descargar el instalador para los modelos entrenados previamente desde esta página: [instalación sin conexión del servidor de aprendizaje de máquina](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-offline).

3. Ejecute al instalador.

4. Para actualizar los componentes de R o Python al mismo tiempo, seleccione el idioma (R, Python o ambos) que desea actualizar.

    Si anteriormente ha instalado servidor de aprendizaje de máquina y actualizar los componentes de R o Python mediante la opción de enlace, deje todas las selecciones anteriores **sea**y seleccione las opciones de modelos previamente entrenado. No anule la selección de las opciones seleccionadas previamente; Si lo hace, el programa de instalación quita los componentes.

5. Acepte todos los demás mensajes, incluidos los contratos de licencia.

Con SQL Server 2017, se requiere ninguna configuración adicional.

> [!NOTE]
> 
> Para los modelos de Python, podría obtener un error al llamar al archivo de modelo de código de Python. Esto es debido a una limitación en la implementación actual de Python, que limita la longitud de la ruta de acceso del archivo del modelo. Este problema se ha solucionado y estará disponible en una versión de próximos servicios.

## <a name="install-pre-trained-models-with-sql-server-standalone-r-server"></a>Instalar modelos previamente entrenados con SQL Server R server independiente

Si instaló una versión anterior de R Server (independiente) utilizando el programa de instalación de SQL Server 2016, puede agregar la capacidad para usar los modelos entrenados previamente mediante la actualización de servidor de R mediante el programa de instalación más reciente basado en Windows. 

Los modelos previamente entrenados primero empezaron a estar disponibles como una opción con [Microsoft R Server 9.1](https://blogs.technet.microsoft.com/dataplatforminsider/2017/04/19/introducing-microsoft-r-server-9-1-release/), las actualizaciones que han sido agregados con cada versión. Le recomendamos que obtenga la versión más reciente posible, pero a continuación se enumeran las versiones anteriores [libera R Server](https://docs.microsoft.com/machine-learning-server/install/r-server-install)

Las instrucciones siguientes describen cómo actualizar los componentes de R y, al mismo tiempo, agregar los modelos entrenados previamente.

1. Inicie el instalador independiente basado en Windows para cada uno [R Server](https://docs.microsoft.com/machine-learning-server/rebranding-microsoft-r-server) o [servidor de aprendizaje de máquina](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install).

2. Seleccione los idiomas que desea actualizar y seleccione el **Pre-trained modelos** opción.

    > [!TIP]
    > Si ya ha ejecutado el programa de instalación para actualizar el servidor de R (independiente) y sólo desea agregar los modelos previamente entrenados, deje todas las selecciones anteriores **sea**y seleccione solo la anterior**-entrenar modelos** opción . **No** anule la selección de las opciones seleccionadas previamente; si lo hace, el programa de instalación quita los componentes.

    Se recomienda que acepte la configuración predeterminada para las ubicaciones de modelo.

3. Haga clic en **Continuar**. 

4. Acepte todos los demás mensajes, incluidos los contratos de licencia.

Una vez completada la instalación, debe realizar algunos pasos adicionales para registrar los modelos entrenados previamente.

1. Abra un símbolo del sistema de Windows **como administrador**.

2. Navegue hasta la carpeta de instalación de arranque para R Server (independiente), que también contiene el programa de instalación de Microsoft R. 

3. Ejecutar `RSetup.exe` e indicar el componente para instalar, la versión y la carpeta que contiene los archivos de origen del modelo, con esta sintaxis:

    `RSetup.exe /install /component MLM /version <version> /language 1033 /destdir "~\R_SERVER\library\MicrosoftML\mxLibs\x64"`

    Se admiten los siguientes valores para el parámetro de versión:

    + Candidato de versión comercial 0: **9.1.0.0**
    + Versión Release candidate 1: **9.2.0.22**
    + RTM: **9.2.0.100**
    + La actualización acumulativa 1: **9.2.0.24**
    + Actualización acumulativa 4: **9.3.0**

    Por ejemplo, para habilitar el uso de la versión más reciente de los modelos previamente entrenados para R, en una instalación predeterminada de R Server (independiente), se ejecute esta instrucción:

    `RSetup.exe /install /component MLM /version 9.3.0 /language 1033 /destdir "C:\Program Files\Microsoft SQL Server\130\R_SERVER\library\MicrosoftML\mxLibs\"`

## <a name="install-pre-trained-models-with-sql-server-2017-standalone-server"></a>Instalar modelos previamente entrenados con un servidor independiente de SQL Server 2017

Si ha instalado el servidor de aprendizaje de máquina mediante el programa de instalación de SQL Server 2017, agregue los modelos previamente entrenados ejecutando el programa de instalación basado en Windows. Puede seleccionar la opción para actualizar los componentes de R o Python y, al mismo tiempo, agregar los modelos previamente entrenados. 

Una vez completada la instalación, se requiere ninguna configuración adicional.

## <a name="bkmk_resources"></a> Investigación y recursos

Actualmente, los modelos que están disponibles son modelos de redes neurales profundas (DNN) para las opiniones de análisis y la imagen. Todos los modelos previamente entrenados se entrenó mediante el uso de Microsoft [Kit de herramientas de cálculo de la red](https://cntk.ai/Features/Index.html), o **CNTK**.

La configuración de cada red se basa en las implementaciones de referencia siguientes:

+ ResNet-18
+ ResNet-50
+ ResNet-101
+ AlexNet

Para obtener más información acerca de los algoritmos que se usa en estos modelos de aprendizaje profundo, y cómo se implementan y entrena con CNTK, vea estos artículos:

+ [Algoritmo los investigadores de Microsoft establece ImageNet desafío hito](https://www.microsoft.com/research/blog/microsoft-researchers-algorithm-sets-imagenet-challenge-milestone/)

+ [Kit de herramientas de cálculo red Microsoft ofrece más eficaz profunda distribuida un rendimiento de cálculo de aprendizaje](https://www.microsoft.com/research/blog/microsoft-computational-network-toolkit-offers-most-efficient-distributed-deep-learning-computational-performance/)

## <a name="how-to-use-pre-trained-models-for-text-analysis"></a>Cómo usar modelos previamente entrenados para el análisis de texto

Vea el ejemplo siguiente para ver una demostración de cómo utilizar el modelo de características de texto previamente entrenado de clasificación del texto:

[Análisis de opiniones con Caracterizador texto](https://github.com/Microsoft/microsoft-r/tree/master/microsoft-ml/Samples/101/BinaryClassification/SimpleSentimentAnalysis)

## <a name="how-to-use-pre-trained-models-for-image-detection"></a>Cómo usar modelos previamente entrenados para la detección de imagen

El modelo previamente entrenado para imágenes admite características de imágenes que suministre. Para utilizar el modelo, se llama a la **featurizeImage** transformar. Se carga la imagen, cambiar el tamaño y caracterizará por el modelo entrenado. El resultado de la caracterizador DNN, a continuación, se utiliza para entrenar un modelo lineal para la clasificación de imágenes.

Para usar este modelo, todas las imágenes deben cambiarse para cumplir los requisitos del modelo entrenado. Por ejemplo, si utiliza un modelo de AlexNet, la imagen debe ajustarse 227 x 227 px.

Para obtener más información, vea [previamente entrenados modelos para la detección de análisis y la imagen de opiniones](https://docs.microsoft.com/machine-learning-server/install/microsoftml-install-pretrained-models)
