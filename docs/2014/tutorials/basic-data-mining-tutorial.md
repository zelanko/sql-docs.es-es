---
title: Tutorial de minería de datos básicos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- databases [Analysis Services], tutorials
- data mining [Analysis Services], tutorials
- tutorials [Data Mining]
ms.assetid: 6602edb6-d160-43fb-83c8-9df5dddfeb9c
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: d434df95a26485d4d7795d3ab960b8d2457b8ff6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63185575"
---
# <a name="basic-data-mining-tutorial"></a>Tutorial básico de minería de datos
  Este es el Tutorial básico de minería de datos de [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Proporciona un entorno integrado para crear modelos de minería de datos y realizar predicciones. En este tutorial, completará un escenario de una campaña de envío de correo directo en el que se utiliza aprendizaje automático para analizar y predecir el comportamiento de compra de los clientes. En el tutorial se muestra cómo utilizar tres de los algoritmos más importantes de minería de datos: agrupación en clústeres, árboles de decisión y Bayes Naive. También aprenderá a analizar los hallazgos con los visores de modelo de minería de datos, y crear predicciones y gráficos de precisión con las herramientas de minería de datos que se incluyen en [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. La compañía ficticia, [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)], se utiliza en todos los ejemplos.  
  
 Cuando esté familiarizado con el uso de las herramientas de minería de datos, recomendamos que también complete el [Tutorial intermedio de minería de datos &#40;Analysis Services - minería de datos&#41;](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md). En las lecciones se muestra cómo utilizar el pronóstico, análisis de la cesta de compras, series temporales, modelos de asociación, tablas anidadas y clústeres de secuencia.  
  
## <a name="tutorial-scenario"></a>Escenario del tutorial  
 En este tutorial, será un empleado de [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] con la tarea de obtener más información sobre los clientes de la compañía basándose en el historial de compras y utilizando a continuación ese datos históricos para realizar predicciones que se puedan utilizar en el mercado. La compañía no ha trabajado previamente con minería de datos, por lo que debe crear una nueva base de datos específica para minería de datos y configurar varios modelos de minería de datos.  
  
## <a name="what-you-will-learn"></a>Aprendizaje  
 Este tutorial le enseña a crear diferentes tipos de métodos de aprendizaje automático y a trabajar con ellos. También aprenderá a crear una copia de un modelo de minería de datos y aplicar un filtro a los datos de entrada para obtener resultados diferentes. Después, puede comparar los resultados de ambos modelos mediante un gráfico de elevación. Por último, utilizará la obtención de detalles para recuperar datos adicionales de la estructura de minería de datos subyacente.  
  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Minería de datos incluye las siguientes características que ayudan con facilidad, desarrollar y comparar varios modelos predictivos y, a continuación, realizar acciones en los resultados:  
  
-   *Conjuntos de pruebas de datos de exclusión*: al crear una estructura de minería de datos, ahora puede dividir los datos de la estructura en conjuntos de prueba y de entrenamiento. Esto permite probar modelos en conjuntos de datos similares y comparar la precisión de los modelos relacionados.  
  
-   *Filtros de modelo de minería de datos*: ahora puede adjuntar filtros a un modelo de minería de datos y aplicar el filtro durante el entrenamiento y las pruebas. Esto permite con facilidad generar modelos relacionados en diferentes subconjuntos de datos.  
  
-   *Obtención de detalles para casos de estructura y columnas de estructura* : ahora puede cambiar fácilmente de los patrones generales del modelo de minería de datos al detalle procesable en el origen de datos.  
  
 El tutorial está compuesto por las lecciones siguientes:  
  
 [Lección 1: Preparar el análisis de servicios de base de datos &#40;Tutorial de minería de datos básicos&#41;](../../2014/tutorials/lesson-1-preparing-the-analysis-services-database-basic-data-mining-tutorial.md)  
 En esta lección, aprenderá a crear una nueva base de datos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , agregar un origen de datos y una vista del origen de datos, y preparar la nueva base de datos que se va a utilizar para la minería de datos.  
  
 [Lección 2: Creación de una estructura de distribución de correo directo &#40;Tutorial de minería de datos básicos&#41;](../../2014/tutorials/lesson-2-building-a-targeted-mailing-structure-basic-data-mining-tutorial.md)  
 En esta lección, aprenderá a crear una estructura de modelos de minería de datos que se puede utilizar como parte de un escenario de distribución de correo directo.  
  
 [Lección 3: Agregar y procesar los modelos](../../2014/tutorials/lesson-3-adding-and-processing-models.md)  
 En esta lección obtendrá información sobre cómo agregar modelos a una estructura. Los modelos que crea se generan con los algoritmos siguientes:  
  
-   Árboles de decisión de [!INCLUDE[msCoName](../includes/msconame-md.md)]  
  
-   Agrupación en clústeres de [!INCLUDE[msCoName](../includes/msconame-md.md)]  
  
-   Bayes naive de [!INCLUDE[msCoName](../includes/msconame-md.md)]  
  
 [Lección 4: Explorar los modelos de distribución de correo directo &#40;Tutorial de minería de datos básicos&#41;](../../2014/tutorials/lesson-4-exploring-the-targeted-mailing-models-basic-data-mining-tutorial.md)  
 En esta lección obtendrá información sobre cómo explorar e interpretar los hallazgos de cada modelo usando los visores.  
  
 [Lección 5: Probar modelos &#40;Tutorial de minería de datos básicos&#41;](../../2014/tutorials/lesson-5-testing-models-basic-data-mining-tutorial.md)  
 En esta lección, realiza una copia de uno de los modelos de distribución de correo directo, agrega un filtro de modelo de minería de datos para restringir los datos de entrenamiento a un conjunto determinado de clientes y, a continuación, evalúa la viabilidad del modelo.  
  
 [Lección 6: Crear y trabajar con predicciones &#40;Tutorial de minería de datos básicos&#41;](../../2014/tutorials/lesson-6-creating-and-working-with-predictions-basic-data-mining-tutorial.md)  
 En esta lección final del Tutorial básico de minería de datos, utiliza el modelo para predecir qué clientes tienen más probabilidad de comprar una bicicleta. A continuación, obtendrá detalles de los casos subyacentes para conseguir información de contacto.  
  
## <a name="requirements"></a>Requisitos  
 Asegúrese de que los siguientes componentes estén instalados:  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] en el modo multidimensional  
  
-   Las base de datos [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] .  
  
 Con el objeto de mejorar la seguridad, las bases de datos de ejemplo no se instalan con [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Para instalar las bases de datos oficiales para [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], visite la página [Bases de datos de ejemplo de Microsoft SQL](https://go.microsoft.com/fwlink/?LinkId=88417) y seleccione [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].  
  
> [!NOTE]  
>  Al trabajar con el tutorial, le resultará más fácil avanzar o retroceder pasos si agrega los botones **Tema siguiente** y **Tema anterior** a la barra de herramientas del visor de documentos.  
  
## <a name="see-also"></a>Vea también  
 [Soluciones de minería de datos](../../2014/analysis-services/data-mining/data-mining-solutions.md)   
 [Tareas y procedimientos de los modelos de minería de datos](../../2014/analysis-services/data-mining/mining-model-tasks-and-how-tos.md)   
 [Crear y consultar modelos de minería de datos con DMX: Tutoriales &#40;Analysis Services - minería de datos&#41;](../../2014/tutorials/create-query-data-mining-models-dmx-tutorials.md)  
  
  
