---
title: "¿Qué &#39; s de servicios de aprendizaje de máquina | Documentos de Microsoft"
ms.custom:
- SQL2016_New_Updated
ms.date: 07/31/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6aff043a-8b37-4f3f-9827-10a671e1ad1c
caps.latest.revision: 36
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 8719ec8be1c0f7b7b0dc72093707829c30ebbb3f
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="whats-new-in-machine-learning-services-in-sql-server"></a>Novedades en servicios de aprendizaje de máquina en SQL Server

En SQL Server 2016, Microsoft introdujo SQL Server R Services, una característica que admita la ciencia de datos de escala empresarial, integrando el lenguaje R con el motor de base de datos de SQL Server.

En SQL Server 2017, aprendizaje automático pasa a ser más eficaz, con la adición de compatibilidad con el popular lenguaje de Python. Y la compatibilidad con nuevos idiomas incluye un nuevo nombre: **Machine Learning Services (In-Database)**.

¡Detectar el último anuncio! [Python en SQL Server 2017: mejorada de aprendizaje automático en bases de datos](https://blogs.technet.microsoft.com/dataplatforminsider/2017/04/19/python-in-sql-server-2017-enhanced-in-database-machine-learning/)

## <a name="whats-new-in-sql-server-2017-release-candidate-2"></a>Novedades de SQL Server de 2017 Release Candidate 2

Servidor de aprendizaje de máquina de Microsoft en SQL Server proporciona ahora compatibilidad completa para crear e implementar soluciones de aprendizaje de máquina. Estos son los aspectos destacados de esta versión:

> [!IMPORTANT]
> 
> Servicios de aprendizaje de máquina, incluido el uso de R o Python, no se admiten cuando se ejecuta SQL Server en Linux o en la base de datos SQL de Azure. Buscar cambios en una versión posterior.
> 
> Sin embargo, la puntuación nativo mediante la función de PREDICCIÓN se admite actualmente en la edición de Linux. 
 
### <a name="in-database-python-integration"></a>Integración de Python en bases de datos

Puede ejecutar Python en procedimientos almacenados, o ejecutar de forma remota con el equipo de SQL Server como el contexto de ejecución de Python. Esta integración se abre nuevos caminos para la amplia comunidad de Python a los desarrolladores y los datos científicos aprovechar la eficacia de SQL Server y para explorar las innovaciones de Microsoft como **revoscalepy** y **microsoftml**.

Los desarrolladores de SQL Server obtienen acceso a las bibliotecas de Python amplia desde el ecosistema de código abierto, incluidos los marcos conocidos como scikit-obtener, Tensorflow, Caffe y Theano/Keras. 

Pero se ejecuta en bases de datos no es solo para; de aprendizaje automático de Python hay una gran cantidad de otras aplicaciones posibles para la integración de Python con SQL, aprovechando las ventajas de los lenguajes respectivos para entregar soluciones más inteligentes y eficaces.

+ **revoscalepy**

    Esta versión incluye la versión final de **revoscalepy**, lo que proporciona Pythonic equivalentes de escalable, algoritmos de RevoScaleR de transmisión por secuencias. Puede crear modelos de Python para las regresiones lineales y logísticas, árboles de decisión, los árboles impulsados y bosques aleatorios, paralelizar todas y puede que se ejecutan en contextos de proceso remoto.

    Para obtener más información, consulte [¿qué es revoscalepy](python/what-is-revoscalepy.md).

+ Contextos de proceso remoto de Python

    Esta versión admite el uso de varios orígenes de datos y contextos de proceso remoto. El científico de datos o el desarrollador puede ejecutar código Python en un servidor SQL Server remoto, para explorar datos o crear modelos sin mover los datos. El uso de contextos de proceso remoto requiere **revoscalepy**.

+ Compatibilidad con Python en aprendizaje de máquina de Microsoft Server (independiente)

    SQL Server 2017 incluye la opción para instalar una versión independiente de las plataformas de Python y R. Mediante el uso de servidor de aprendizaje de máquina, puede distribuir y escalar código R o Python sin usar SQL Server.

    Para obtener un ejemplo de uso de Python en aprendizaje de máquina de Microsoft Server, vea [publicar y consumir código Python](python/publish-consume-python-code.md).

### <a name="new-algorithms"></a>Nuevos algoritmos

El **MicrosoftML** paquete de R y Python contiene algoritmos de aprendizaje automático de última generación y contextos de proceso de transformación de datos que puede ser escalado ni se ejecutarán en remoto. Los algoritmos incluyen redes neurales profundas personalizables, árboles de decisión rápida y bosques de decisión, regresión lineal y regresión logística.

El paquete MicrosoftML viene con interfaces de R y Python y se basa en la versión 9.2.0 del servidor de aprendizaje de máquina de Microsoft.

Para obtener más información, consulte [Introducción a MicrosoftML](using-the-microsoftml-package.md) y [microsoftml para Python](https://docs.microsoft.com/r-server/python-reference/microsoftml/microsoftml-package).

### <a name="operationalization"></a>Puesta en marcha

Esta versión contiene varias opciones y características para ayudarle a implementar y distribuir tareas de aprendizaje automático:

+ Puesta en marcha con T-SQL

    La integración de Python con T-SQL significa que se puede llamar a cualquier código de Python mediante `sp_execute_external_script`. Esta infraestructura segura permite la implementación de nivel empresarial de los modelos de Python y las secuencias de comandos que se pueda llamar desde una aplicación mediante un procedimiento almacenado simple. El rendimiento adicional es mediante transmisión por secuencias de datos de SQL a procesos de Python y la paralelización de anillo MPI.

+ **mrsdeploy** para Python

    El **mrsdeploy** el paquete para Microsoft R Server ahora admite la implementación de modelos de Python y las secuencias de comandos como servicios web y está disponible como una opción en el servidor de aprendizaje de máquina (independiente). Para obtener un ejemplo de cómo funciona, consulte [publicar y consumir código Python](python/publish-consume-python-code.md).

+ Rendimiento

    Microsoft ha impulsado sus límites de rendimiento de la puntuación. Con la puntuación en bases de datos, se procesa un millón de filas por segundo a través de modelos de R. En esta versión, nuevas características para **en tiempo real de puntuación** y **puntuación nativo** compatibilidad con un mejor rendimiento en varias filas puntuación y pequeñas procesa por lotes así. 

### <a name="realtime-scoring-and-native-scoring"></a>En tiempo real de puntuación y de puntuación nativo

En tiempo real de puntuación se basa en las bibliotecas de C++ nativo para leer un modelo que se almacenan en un formato binario optimizado y, a continuación, generar predicciones sin tener que llamar al runtime de R. Esto hace que las operaciones de puntuación mucho más rápidas.

Además, esta versión de SQL Server 2017 incluye una función nativa de T-SQL para puntuar rápido que se pueden ejecutar en cualquier edición de SQL Server, incluso en Linux. La función no requiere ninguna instalación de R o una configuración adicional. Esto significa que puede entrenar un modelo en otra parte, guárdela en SQL Server y, a continuación, realizar puntuaciones sin llamar nunca a R. Esta característica se conoce como _puntuación native_.

  - Puntuación nativo solo está disponible en SQL Server 2017. Utiliza una función de T-SQL que se puede ejecutar en cualquier edición de SQL Server, como Linux.
 - En tiempo real de puntuación se admite en SQL Server 2017 y en el servidor de aprendizaje de máquina de Microsoft. Puede runa del procedimiento almacenado o realizar en tiempo real desde el código de R de puntuación.
 - En tiempo real de puntuación también está disponible para SQL Server 2016, si la instancia se actualiza a la versión más reciente de Microsoft R Server.

Para más información, vea estos artículos:

 + [En tiempo real de puntuación](real-time-scoring.md)
 + [Nativo de puntuación](sql-native-scoring.md)
 + [Cómo realizar la puntuación en tiempo real o puntuación nativo](r/how-to-do-realtime-scoring.md)

### <a name="upgrade-your-ml-experience-and-get-pre-trained-models"></a>Actualice su experiencia de aprendizaje automático y obtener modelos previamente entrenados

Si instaló una versión anterior de SQL Server 2016 R Services, ahora puede actualizar a la versión más reciente al cambiar el servidor para usar la directiva de ciclo de vida moderna. Al hacerlo, puede sacar provecho de un ciclo de versiones más rápido para R y actualizar automáticamente todos los componentes de R. Para más información, consulte [Microsoft R Server 9.0.1](https://docs.microsoft.com/r-server/whats-new-in-r-server).

El instalador también ofrece la opción para instalar una colección de modelos previamente entrenados en formato binario. Estos modelos soportan aprendizaje automático en escenarios como reconocimiento de imágenes, que puede ser difícil para los clientes buscar grandes conjuntos de datos para entrenar un modelo. Después de instalar uno de los modelos previamente entrenados, puede usar para la predicción en sus propios datos sin el tiempo y el gasto que supone en el entrenamiento de dicho modelo grande y complejo.

Para obtener más información, vea [instalar modelos previamente entrenados en SQL Server](r/install-pretrained-models-sql-server.md)

### <a name="package-management"></a>Administración de paquetes

Esta versión incluye muchas mejoras en administración de paquetes de SQL Server. Estos incluyen:

- roles de base de datos para ayudar a lo DBA administrar y permisos de auditoría
- la instrucción CREATE externa LIBRARY en T-SQL
- un amplio conjunto de funciones de R que ayuden a instalar, quitar o enumerar los paquetes que pertenecen a los usuarios.

Para obtener más información, consulte [administración del paquete](r/r-package-management-for-sql-server-r-services.md).

### <a name="get-started"></a>Introducción

+ [Configurar Python en servicios de aprendizaje de máquina de SQL Server](../advanced-analytics/python/setup-python-machine-learning-services.md)

+ [Configurar R en servicios de aprendizaje de máquina de SQL Server](r/set-up-sql-server-r-services-in-database.md)

+ [Tutoriales de aprendizaje de máquina](tutorials/machine-learning-services-tutorials.md)
