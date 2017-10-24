---
title: "Instalar modelos de aprendizaje automático previamente entrenado en SQL Server | Documentos de Microsoft"
ms.custom:
- SQL2016_New_Updated
ms.date: 10/18/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 21456462-e58a-44c3-9d3a-68b4263575d7
caps.latest.revision: 1
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: aecf422ca2289b2a417147eb402921bb8530d969
ms.openlocfilehash: 8f4a145700d12f31a868cc3fc20a9dbdbe6f45ea
ms.contentlocale: es-es
ms.lasthandoff: 10/24/2017

---
# <a name="install-pretrained-machine-learning-models-on-sql-server"></a>Instalar previamente entrenado máquina aprendizaje de los modelos en SQL Server

En este artículo se describe cómo agregar modelos previamente entrenados a una instancia de SQL Server que ya tiene servicios de R o instalado servicios de aprendizaje de máquina.

Modelos previamente entrenados se proporcionan como una opción al instalar Microsoft R Server o servidor de aprendizaje de máquina mediante el instalador independiente. Puede usar a este instalador para obtener solo los modelos previamente entrenados, o puede usar para actualizar los componentes en una instancia de SQL Server 2016 o SQl Server 2017 de aprendizaje automático.

Después de haber descargado los modelos previamente entrenados ejecutando el programa de instalación, hay algunos pasos adicionales para configurar los modelos para su uso con SQL Server. En este artículo se describe el proceso.

Para más información, vea estos artículos:

+ [Modelos para la detección de análisis y la imagen de opinión de aprendizaje de automático previamente entrenado](https://docs.microsoft.com/machine-learning-server/install/microsoftml-install-pretrained-models)

+ [Actualizar los componentes de R en una instancia de R Services](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md).

## <a name="benefits-of-using-pretrained-models"></a>Ventajas del uso de modelos previamente entrenados

Estos modelos previamente entrenados se crearon para ayudar a los clientes que necesitan realizar tareas como el análisis de opiniones o características de la imagen, pero no dispone de recursos para obtener los conjuntos de datos grandes o entrenar un modelo complejo. El uso de modelos previamente entrenados le permite empezar a trabajar en text e image procesar de forma más eficaz.

Actualmente, los modelos que están disponibles son modelos de redes neurales profundas (DNN) para las opiniones de análisis y la imagen. Todos los modelos previamente entrenados se entrenó mediante el uso de Microsoft [Kit de herramientas de cálculo de la red](https://cntk.ai/Features/Index.html), o **CNTK**. 

La configuración de cada red se basa en las implementaciones de referencia siguientes:

+ ResNet-18
+ ResNet-50
+ ResNet-101
+ AlexNet

Para obtener más información acerca de redes de aprendizaje profundo y su implementación con CNTK, vea estos artículos:

+ [Algoritmo los investigadores de Microsoft establece ImageNet desafío hito](https://www.microsoft.com/research/blog/microsoft-researchers-algorithm-sets-imagenet-challenge-milestone/)

+ [Kit de herramientas de cálculo red Microsoft ofrece más eficaz profunda distribuida un rendimiento de cálculo de aprendizaje](https://www.microsoft.com/research/blog/microsoft-computational-network-toolkit-offers-most-efficient-distributed-deep-learning-computational-performance/)

## <a name="how-to-install-the-models-on-sql-server"></a>Cómo instalar los modelos en SQL Server

1. Ejecute al instalador independiente basado en Windows para el servidor de aprendizaje de máquina. Para ubicaciones de descarga, vea:

    + [Instalar para Windows Server de aprendizaje automático](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)
    + [Instalar a R Server 9.1 para Windows](https://docs.microsoft.com/r-server/install/r-server-install-windows)

2. La selección de características para instalar depende de si se obtener solo los modelos o realizar otras actualizaciones mediante el programa de instalación.
 
    + Si se trata de una nueva instalación de servidor de aprendizaje de máquina y no desea realizar otros cambios en los componentes de R o Python, seleccionados **sólo** la opción de modelos previamente entrenado. Acepte todos los demás mensajes, incluidos los contratos de licencia.

    + Para actualizar los componentes de R o Python al mismo tiempo, seleccione el idioma (R, Python o ambos) que desea actualizar y seleccione la opción de modelos previamente entrenado. Seleccione una o varias instancias para aplicar estos cambios.

    + Si anteriormente ha instalado servidor de aprendizaje de máquina y actualizar los componentes de R o Python mediante la opción de enlace, deje todas las selecciones anteriores **sea**y seleccione las opciones de modelos previamente entrenado. No anule la selección de las opciones seleccionadas previamente o se va a quitar.

3. Cuando una vez completada la instalación, abra un símbolo del sistema de Windows **como administrador**y navegue hasta la carpeta de arranque en el programa de instalación de SQL Server, que también contiene el programa de instalación de Microsoft R. En una instancia predeterminada de SQL Server 2017, la carpeta sería:
    
    `C:\Program Files\Microsoft SQL Server\140\Setup Bootstrap\SQL2017\x64\`

4. Especifique el componente para instalar, la versión y la carpeta que contiene los archivos de origen del modelo, utilizando los argumentos a RSetup.exe, como se muestra en estos ejemplos:

  + Usar modelos con **R_SERVICES**, use la sintaxis y las rutas de acceso siguientes:

    `RSetup.exe /install /component MLM /version <version> /language 1033 /destdir <SQL_DB_instance_folder>\R_SERVICES\library\MicrosoftML\mxLibs\x64`

    Por ejemplo, para habilitar el uso de la versión más reciente de los modelos previamente entrenados para R, en una instancia predeterminada de SQL Server de 2017 se ejecute esta instrucción:

    `RSetup.exe /install /component MLM /version 9.2.0.24 /language 1033 /destdir "C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library\MicrosoftML\mxLibs\x64"`

    En una instancia con nombre, el comando sería algo parecido a esto:

    `RSetup.exe /install /component MLM /version 9.2.0.24 /language 1033 /destdir "C:\Program Files\Microsoft SQL Server\MSSQL14.MyInstanceName\R_SERVICES\library\MicrosoftML\mxLibs\x64"`

  + Usar modelos con **PYTHON_SERVICES**, use la sintaxis y las rutas de acceso siguientes:

    `RSetup.exe /install /component MLM /version <version> /language 1033 /destdir <SQL_DB_instance_folder>\PYTHON_SERVICES\Lib\site-packages\microsoftml\mxLibs`

    Por ejemplo, para habilitar el uso de la versión más reciente de los modelos previamente entrenados para Python, en una instancia predeterminada de SQL Server de 2017 se ejecute esta instrucción:

    `RSetup.exe /install /component MLM /version 9.2.0.24 /language 1033 /destdir "C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\Lib\site-packages\microsoftml\mxLibs"`

    En una instancia con nombre, el comando sería algo parecido a esto:

    `RSetup.exe /install /component MLM /version 9.2.0.24 /language 1033 /destdir "C:\Program Files\Microsoft SQL Server\MSSQL14.MyInstanceName\PYTHON_SERVICES\Lib\site-packages\microsoftml\mxLibs"`

5. Para el parámetro de versión, se admiten los siguientes valores:

    + Candidato de versión comercial 0: **9.1.0.0**
    + Versión Release candidate 1: **9.2.0.22**
    + RTM: **9.2.0.100**
    + La actualización acumulativa 1: **9.2.0.24**

6. Si la instalación es correcta, los modelos siguientes deben agregarse a la R\_servicios o PYTHON\_carpetas de servicios:

    - AlexNet\_Updated.model
    - ImageNet1K\_mean.xml
    - pretrained.Model
    - ResNet\_101\_Updated.model
    - ResNet\_18\_Updated.model
    - ResNet\_50\_Updated.model

## <a name="examples"></a>Ejemplos

Después de haber instalado los modelos, puede usar los modelos mediante una llamada a ellos desde el código.

### <a name="image-featurization-example"></a>Ejemplo de imagen de características

El modelo previamente entrenado para imágenes admite características de imágenes que suministre. Este modelo determinado se entrenó utilizando [CNTK](https://docs.microsoft.com/cognitive-toolkit/). 

Para utilizar el modelo, se llama a la **featurizeImage** transformar.

+ [featurizeImage: transformar de características de imagen de aprendizaje de máquina](https://docs.microsoft.com/r-server/r-reference/microsoftml/featurizeimage)

En este ejemplo, vea el segundo bloque de código. Se carga la imagen, cambiar el tamaño y caracterizará por el modelo DNN convolutional previamente entrenado. El resultado de la caracterizador DNN, a continuación, se utiliza para entrenar un modelo lineal para la clasificación de imágenes.

La imagen debe cambiarse de tamaño para cumplir los requisitos del modelo entrenado: las imágenes que se utilizan para el entrenamiento se produjeron 224 x 224 px. Si se utiliza un modelo de AlexNet, la imagen podría ajustarse 227 x 227 px.

```R
 model <- rxFastLinear(
     Label ~ Features,
     data = train,
     mlTransforms = list(
         loadImage(vars = list(Features = "Path")),
         resizeImage(vars = "Features", width = 224, height = 224), 
         extractPixels(vars = "Features"),
         featurizeImage(var = "Features")
         ),
     mlTransformVars = "Path")
```

> [!NOTE]
> No es posible leer o modificar los modelos previamente entrenados, ya que se comprimen con un formato nativo, para mejorar el rendimiento.


### <a name="text-analysis-example"></a>Ejemplo de análisis de texto

Vea el ejemplo siguiente para ver una demostración de cómo utilizar el modelo de características de texto previamente entrenado de clasificación del texto:

[Análisis de opiniones con Caracterizador texto](https://github.com/Microsoft/microsoft-r/tree/master/microsoft-ml/Samples/101/BinaryClassification/SimpleSentimentAnalysis)

