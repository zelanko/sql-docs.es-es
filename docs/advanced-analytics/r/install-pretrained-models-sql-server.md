---
title: "Instalar modelos de aprendizaje automático previamente entrenado en SQL Server | Documentos de Microsoft"
ms.custom:
- SQL2016_New_Updated
ms.date: 07/15/2017
ms.prod: sql-server-2016
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
ms.translationtype: MT
ms.sourcegitcommit: c6ea46c5187f00190cb39ba9a502b3ecb6a28bc6
ms.openlocfilehash: b52fcc1e4ac77df2968a4ea6cbd6e546ff1b74ac
ms.contentlocale: es-es
ms.lasthandoff: 09/19/2017

---
# <a name="install-pretrained-machine-learning-models-on-sql-server"></a>Instalar previamente entrenado máquina aprendizaje de los modelos en SQL Server

Este tema describe cómo agregar modelos previamente entrenados a una instancia de SQL Server que ya tiene R Services o Machine Learning Services instalado.

Modelos previamente entrenados se proporcionan con la actualización a Microsoft R Server (o la actualización al servidor de aprendizaje de máquina de Microsoft). Para obtener información acerca de cómo actualizar la instancia y obtener la versión más reciente de Microsoft R, consulte [actualizar los componentes de R en una instancia de R Services](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md).

Puede instalar estos modelos sólo si se ejecuta al instalador independiente basado en Windows para R Server.
Sin embargo, hay algunos pasos adicionales que se utilizará al instalar los modelos en SQL Server. En este tema se describe el proceso.

## <a name="benefits-of-using-pretrained-models"></a>Ventajas del uso de modelos previamente entrenados

Se han realizado previamente entrenados modelos disponibles para admitir a clientes que necesitan realizar tareas como el análisis de opiniones o características de la imagen, pero no dispone de recursos para obtener los conjuntos de datos grandes o entrenar un modelo complejo. El uso de modelos previamente entrenados le permite empezar a trabajar en text e image procesar de forma más eficaz.

Actualmente, los modelos que están disponibles son modelos de redes neurales profundas (DNN) para las opiniones de análisis y la imagen. Todos los modelos previamente entrenados cuatro se entrenó en CNTK. La configuración de cada red se basa en las implementaciones de referencia siguientes:

+ ResNet-18
+ ResNet-50
+ ResNet-101
+ AlexNet

Para obtener más información acerca de redes profundas residuales y su implementación con CNTK, vea estos artículos:

+ [Algoritmo los investigadores de Microsoft establece ImageNet desafío hito](https://www.microsoft.com/research/blog/microsoft-researchers-algorithm-sets-imagenet-challenge-milestone/)

+ [Kit de herramientas de cálculo red Microsoft ofrece más eficaz profunda distribuida un rendimiento de cálculo de aprendizaje](https://www.microsoft.com/research/blog/microsoft-computational-network-toolkit-offers-most-efficient-distributed-deep-learning-computational-performance/)

## <a name="how-to-install-the-models-on-sql-server"></a>Cómo instalar los modelos en SQL Server

   > [!NOTE]
   > 
   > Si utiliza al instalador independiente basado en Windows para instalar a Microsoft R Server o para actualizar la instancia de SQL Server, los modelos previamente entrenados están disponibles en el programa de instalación. Vea [instalar R Server para Windows](https://docs.microsoft.com/en-us/r-server/install/r-server-install-windows).
   > 
   > Podrían ser necesario realizar algunos pasos adicionales para usar los modelos con Microsoft R Server. Para obtener más información, vea [cómo instalar e implementar previamente entrenado modelos de aprendizaje automático con MicrosoftML](https://docs.microsoft.com/r-server/install/microsoftml-install-pretrained-models)

1. Los modelos previamente entrenados no se instalan de forma predeterminada al instalar SQL Server; debe agregarlos mediante la ejecución de una utilidad de línea de comandos de instalación una vez terminada la instalación de SQL Server.

2. Abra un símbolo del sistema con privilegios elevados y vaya a la carpeta de instalación de arranque para SQL Server, que también contiene el programa de instalación de Microsoft R.

    En una instancia predeterminada de SQL Server de 2017 RC 1, esto sería:
    
    `C:\Program Files\Microsoft SQL Server\140\Setup Bootstrap\SQL2017RC1\x64\`

3. Especifique el componente para instalar y la carpeta donde deben agregarse los modelos previamente entrenados con los argumentos siguientes:

  + Usar modelos con **R_SERVICES**

    `RSetup.exe /install /component MLM /version <version> /language 1033 /destdir <SQL_DB_instance_folder>\R_SERVICES`

    Por ejemplo, para habilitar el uso de los modelos previamente entrenados con R en una instancia predeterminada de SQL Server 2017, se ejecute esta instrucción:

    `RSetup.exe /install /component MLM /version 9.2.0.22 /language 1033 /destdir "C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES"`

  + Usar modelos con **PYTHON_SERVICES**

    `RSetup.exe /install /component MLM /version <version> /language 1033 /destdir <SQL_DB_instance_folder>\PYTHON_SERVICES`

    Por ejemplo, para habilitar el uso de los modelos previamente entrenados con Python, para una instancia predeterminada de SQL Server de 2017 se ejecute esta instrucción:

    `RSetup.exe /install /component MLM /version 9.2.0.22 /language 1033 /destdir "C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES"`

4. Para el parámetro de versión, se admiten los siguientes valores:

    + Candidato de versión comercial 0: **9.1.0.0**
    + Versión Release candidate 1: **9.2.0.22**
    + Número de versión final (no publicada): **9.2.0.100**

5. Si la instalación es correcta, los modelos siguientes deben agregarse a la R\_servicios o PYTHON\_carpetas de servicios:

    - AlexNet_Updated.model
    - ImageNet1K_mean.xml
    - pretrained.Model
    - ResNet_101_Updated.model
    - ResNet_18_Updated.model
    - ResNet_50_Updated.model

## <a name="examples"></a>Ejemplos

Después de haber instalado los modelos, puede usar los modelos mediante una llamada a ellos desde el código de R.

### <a name="image-featurization-example"></a>Ejemplo de imagen de características

El modelo previamente entrenado para imágenes admite características de imágenes que suministre. Para utilizar el modelo, se llama a la **featurizeImage** transformar.

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
> 
> No es posible leer o modificar el propio modelo previamente entrenado. Este modelo determinado se basa en [CNTK](https://docs.microsoft.com/cognitive-toolkit/) de modelo, pero se han comprimido con un formato nativo por motivos de rendimiento.

### <a name="text-analysis-example"></a>Ejemplo de análisis de texto

Este ejemplo muestra el uso del modelo previamente entrenado para la clasificación:

[Análisis de opiniones con Caracterizador texto](https://github.com/Microsoft/microsoft-r/tree/master/microsoft-ml/Samples/101/BinaryClassification/SimpleSentimentAnalysis)

