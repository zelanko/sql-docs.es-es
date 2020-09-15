---
title: Instalación de modelos previamente entrenados
description: Agregue modelos previamente entrenados para el análisis de sentimiento y las características de imagen para SQL Server Machine Learning Services (R o Python) o SQL Server R Services.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 07/30/2019
ms.topic: how-to
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 86aad616cc8c9fc54adc2fffd14bfc663acf3887
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/13/2020
ms.locfileid: "88179732"
---
# <a name="install-pre-trained-machine-learning-models-on-sql-server"></a>Instalación de modelos de aprendizaje automático entrenados previamente en SQL Server
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

En este artículo se explica cómo usar PowerShell para agregar modelos gratuitos de aprendizaje automático entrenados previamente para el *análisis de sentimiento* y las *características de imagen* a una instancia de SQL Server que tenga integración con R o Python. Los modelos entrenados previamente están compilados por Microsoft y listos para su uso, que se agregan a una instancia como una tarea posterior a la instalación. Para obtener más información acerca de estos modelos, vea la sección [Recursos](#bkmk_resources) de este artículo.

Una vez instalados, los modelos previamente entrenados se consideran un detalle de implementación que tiene funciones específicas de energía en las bibliotecas de MicrosoftML (R) y microsoftml (Python). No debe (y no puede) ver, personalizar, ni volver a entrenar los modelos, ni puede tratarlos como un recurso independiente en el código personalizado o emparejar otras funciones. 

Para usar los modelos previamente entrenados, llame a las funciones que se enumeran en la tabla siguiente.

| Función de R (MicrosoftML) | Función de Python (microsoftml) | Uso |
|--------------------------|-------------------------------|-------|
| [getSentiment](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/getsentiment) | [get_sentiment](https://docs.microsoft.com//machine-learning-server/python-reference/microsoftml/get-sentiment) | Genera una puntuación de opinión positiva-negativa sobre las entradas de texto. |
| [featurizeImage](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/featurizeimage) | [featurize_image](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/featurize-image) | Extrae información de texto de entradas de archivo de imagen. |

## <a name="prerequisites"></a>Prerrequisitos

Los algoritmos de aprendizaje automático son de cálculo intensivo. Se recomienda 16 GB de RAM para cargas de trabajo de baja a moderada, incluida la finalización de tutoriales con todos los datos de ejemplo.

Debe tener derechos de administrador en el equipo y SQL Server para agregar modelos previamente entrenados.

Los scripts externos deben estar habilitados y el servicio SQL Server LaunchPad debe estar en ejecución. Las instrucciones de instalación proporcionan los pasos para habilitar y comprobar estas capacidades. 

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
El [paquete MicrosoftML R](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package) o el [paquete microsoftml de Python](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) contienen los modelos entrenados previamente.

[SQL Server Machine Learning Services](sql-machine-learning-services-windows-install.md) incluye las versiones de ambos lenguajes de la biblioteca de aprendizaje automático, por lo que se cumple este requisito previo sin necesidad de realizar ninguna acción por su parte. Dado que las bibliotecas están presentes, puede usar el script de PowerShell que se describe en este artículo para agregar los modelos entrenados previamente a estas bibliotecas.
::: moniker-end

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
El [paquete MicrosoftML R](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package) contiene los modelos entrenados previamente.

[SQL Server R Services](sql-r-services-windows-install.md), que solo admite R, no incluye el [paquete MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package) de serie. Para agregar MicrosoftML, debe realizar una [actualización de componentes](../install/upgrade-r-and-python.md). Una ventaja de la actualización de componentes es que puede agregar simultáneamente los modelos entrenados previamente, lo que hace que no sea necesario ejecutar el script de PowerShell. Sin embargo, si ya ha realizado la actualización pero ha perdido la adición de los modelos previamente entrenados la primera vez, puede ejecutar el script de PowerShell como se describe en este artículo. Funciona en ambas versiones de SQL Server. Antes de hacerlo, confirme que la biblioteca MicrosoftML existe en `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library`.
::: moniker-end

<a name="file-location"></a>

## <a name="check-whether-pre-trained-models-are-installed"></a>Comprobación de si los modelos previamente entrenados están instalados

Las rutas de acceso de instalación para los modelos R y Python son las siguientes:

+ Para R: `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library\MicrosoftML\mxLibs\x64`

+ Para Python: `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\Lib\site-packages\microsoftml\mxLibs`

Los nombres de archivo de modelo se enumeran a continuación:

+ AlexNet\_Updated.model
+ ImageNet1K\_mean.xml
+ pretrained.model
+ ResNet\_101\_Updated.model
+ ResNet\_18\_Updated.model
+ ResNet\_50\_Updated.model

Si los modelos ya están instalados, vaya al [paso de validación](#verify) para confirmar la disponibilidad.

## <a name="download-the-installation-script"></a>Descargue el script de instalación.

Haga clic en [https://aka.ms/mlm4sql](https://aka.ms/mlm4sql) para descargar el archivo **Install-MLModels.ps1**.

## <a name="execute-with-elevated-privileges"></a>Ejecución con privilegios elevados

1. Inicie PowerShell. En la barra de tareas, haga clic con el botón derecho en el icono del programa PowerShell y seleccione **Ejecutar como administrador**.
2. Escriba una ruta de acceso completa al archivo de script de instalación e incluya el nombre de la instancia. Asumiendo la carpeta descargas y una instancia predeterminada, el comando podría ser similar al siguiente:

   ```powershell
   PS C:\WINDOWS\system32> C:\Users\<user-name>\Downloads\Install-MLModels.ps1 MSSQLSERVER
   ```

**Salida**

En una instancia predeterminada de SQL Server Machine Learning Services conectada a Internet con R y Python, debería ver mensajes similares a los siguientes.

   ```powershell
   MSSQL14.MSSQLSERVER
        Verifying R models [9.2.0.24]
        Downloading R models [C:\Users\<user-name>\AppData\Local\Temp]
        Installing R models [C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\]
        Verifying Python models [9.2.0.24]
        Installing Python models [C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\]
   PS C:\WINDOWS\system32>
   ```

<a name="verify"> </a>

## <a name="verify-installation"></a>Comprobar la instalación

En primer lugar, busque los nuevos archivos en la [carpeta mxlibs](#file-location). A continuación, ejecute el código de demostración para confirmar que los modelos están instalados y funcionan. 

### <a name="r-verification-steps"></a>Pasos de comprobación de R

1. Inicie **RGUI. EXE** en C:\Archivos de programa\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64.

2. Pegue el siguiente script de R en el símbolo del sistema.

    ```R
    # Create the data
    CustomerReviews <- data.frame(Review = c(
    "I really did not like the taste of it",
    "It was surprisingly quite good!",
    "I will never ever ever go to that place again!!"),
    stringsAsFactors = FALSE)

    # Get the sentiment scores
    sentimentScores <- rxFeaturize(data = CustomerReviews, 
                                    mlTransforms = getSentiment(vars = list(SentimentScore = "Review")))

    # Let's translate the score to something more meaningful
    sentimentScores$PredictedRating <- ifelse(sentimentScores$SentimentScore > 0.6, 
                                            "AWESOMENESS", "BLAH")

    # Let's look at the results
    sentimentScores
    ```

3. Pulse Entrar para ver las puntuaciones de opinión. El resultado debería ser el siguiente:

    ```R
    > sentimentScores
                                            Review SentimentScore
    1           I really did not like the taste of it      0.4617899
    2                 It was surprisingly quite good!      0.9601924
    3 I will never ever ever go to that place again!!      0.3103435
    PredictedRating
    1            BLAH
    2     AWESOMENESS
    3            BLAH
    ```

### <a name="python-verification-steps"></a>Pasos de comprobación de Python

1. Inicie **Python.exe** en C:\Archivos de programa\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES.

2. Pegue el siguiente script de Python en el símbolo del sistema

    ```python
    import numpy
    import pandas
    from microsoftml import rx_logistic_regression, rx_featurize, rx_predict, get_sentiment

    # Create the data
    customer_reviews = pandas.DataFrame(data=dict(review=[
                "I really did not like the taste of it",
                "It was surprisingly quite good!",
                "I will never ever ever go to that place again!!"]))
                
    # Get the sentiment scores
    sentiment_scores = rx_featurize(
        data=customer_reviews,
        ml_transforms=[get_sentiment(cols=dict(scores="review"))])
        
    # Let's translate the score to something more meaningful
    sentiment_scores["eval"] = sentiment_scores.scores.apply(
                lambda score: "AWESOMENESS" if score > 0.6 else "BLAH")
    print(sentiment_scores)
    ```

3. Presione Entrar para imprimir las puntuaciones. El resultado debería ser el siguiente:

    ```python
    >>> print(sentiment_scores)
                                                review    scores         eval
    0            I really did not like the taste of it  0.461790         BLAH
    1                  It was surprisingly quite good!  0.960192  AWESOMENESS
    2  I will never ever ever go to that place again!!  0.310344         BLAH
    >>>
    ```

> [!NOTE]
> Si se produce un error en los scripts de demostración, compruebe primero la ubicación del archivo. En los sistemas que tienen varias instancias de SQL Server, o para las instancias que se ejecutan en paralelo con versiones independientes, es posible que el script de instalación no lea el entorno y coloque los archivos en la ubicación equivocada. Normalmente, la copia manual de los archivos en la carpeta mxlib correcta corrige el problema.

## <a name="examples-using-pre-trained-models"></a>Ejemplos de uso de modelos previamente entrenados

El siguiente vínculo incluye el código de ejemplo que invoca los modelos previamente entrenados.

+ [Ejemplo de código: análisis de sentimiento mediante Caracterizador de texto](https://github.com/Microsoft/microsoft-r/tree/master/microsoft-ml/Samples/101/BinaryClassification/SimpleSentimentAnalysis)

<a name="bkmk_resources"></a> 

## <a name="research-and-resources"></a>Investigación y recursos

Actualmente, los modelos que están disponibles son modelos de red neuronal profunda (DNN) para el análisis de sentimiento y la clasificación de imágenes. Todos los modelos entrenados previamente se entrenaron mediante el uso del [kit de herramientas de red computacional de Microsoft](https://cntk.ai/Features/Index.html) o **CNTK**.

La configuración de cada red se basó en las siguientes implementaciones de referencia:

+ ResNet-18
+ ResNet-50
+ ResNet-101
+ AlexNet

Para obtener más información sobre los algoritmos que se usan en estos modelos de aprendizaje profundo y cómo se implementan y se entrenan con CNTK, vea estos artículos:

+ [El algoritmo de los investigadores de Microsoft marca un hito en el reto ImageNet](https://www.microsoft.com/research/blog/microsoft-researchers-algorithm-sets-imagenet-challenge-milestone/)

+ [El kit de herramientas de red computacional de Microsoft ofrece un rendimiento de cálculo de aprendizaje profundo distribuido más eficaz](https://www.microsoft.com/research/blog/microsoft-computational-network-toolkit-offers-most-efficient-distributed-deep-learning-computational-performance/)

## <a name="see-also"></a>Consulte también

+ [SQL Server Machine Learning Services](sql-machine-learning-services-windows-install.md)
+ [Actualización de los componentes de R y Python en instancias de SQL Server](../install/upgrade-r-and-python.md)
+ [Paquete MicrosoftML para R](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)
+ [Paquete microsoftml para Python](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package)
