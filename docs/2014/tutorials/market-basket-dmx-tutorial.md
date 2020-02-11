---
title: Tutorial DMX de la cesta de la compra | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- DMX [Analysis Services], tutorials
- data mining [Analysis Services], tutorials
- statements [DMX], tutorials
- Data Mining Extensions [Analysis Services], tutorials
- market basket analysis [Analysis Services]
- tutorials [Data Mining]
- tutorials [DMX]
ms.assetid: 6e262a1d-c89e-4033-8368-46cf25168ef5
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: fe12f1c4ca1c0946572c61e89f4f4edb8ba9a762
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "63185640"
---
# <a name="market-basket-dmx-tutorial"></a>Tutorial DMX de Market Basket
  En este tutorial aprenderá a crear, entrenar y explorar modelos de minería de datos utilizando el lenguaje de consulta Extensiones de minería de datos (DMX). A continuación, estos modelos de minería de datos se utilizarán para crear predicciones que describen los productos que tienden a adquirirse simultáneamente.  
  
 Los modelos de minería de datos se crearán a partir de los datos incluidos en la base de datos de ejemplo [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] , que almacena datos de la empresa ficticia [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)]. 
  [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] es una gran empresa multinacional de fabricación. La empresa fabrica y vende bicicletas de metal y de materiales compuestos en los mercados de Norteamérica, Europa y Asia. Su sede central de operaciones se encuentra en Bothell, Washington, con 290 empleados, y tiene distribuidos varios equipos regionales de ventas en toda su base de mercado internacional.  
  
## <a name="tutorial-scenario"></a>Escenario del tutorial  
 
  [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] ha decidido crear una aplicación personalizada que utiliza la funcionalidad de minería de datos para predecir los tipos de productos que los clientes tienden a adquirir simultáneamente. El objetivo de la aplicación personalizada es poder especificar un conjunto de productos y predecir los productos adicionales que se adquirirán con los productos especificados. A continuación, [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] utilizará esta información para agregar una característica de "sugerencia" a su sitio web y también para organizar mejor la forma en que presenta la información a sus clientes.  
  
 [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] proporciona varias herramientas que se pueden usar para realizar esta [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] tarea:  
  
-   El lenguaje de consulta DMX  
  
-   [Algoritmo de Asociación de Microsoft](../../2014/analysis-services/data-mining/microsoft-association-algorithm.md)  
  
-   El Editor de consultas de [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]  
  
 Extensiones de minería de datos (DMX) es un lenguaje de consulta proporcionado por [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] que sirve para crear y trabajar con modelos de minería de datos. El [!INCLUDE[msCoName](../includes/msconame-md.md)] algoritmo de Asociación de crea modelos que pueden predecir los productos que es probable que se compren juntos.  
  
 El objetivo de este tutorial es proporcionar las consultas DMX que se utilizarán en la aplicación personalizada.  
  
 **Para obtener más información: soluciones de minería de** [datos](../../2014/analysis-services/data-mining/data-mining-solutions.md)  
  
## <a name="mining-structure-and-mining-models"></a>Estructura de minería de datos y modelos de minería de datos  
 Antes de empezar a crear instrucciones DMX, es importante comprender los objetos principales utilizados por [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] para crear modelos de minería de datos. La *estructura de minería* de datos es una estructura de datos que define el dominio de datos desde el que se generan los modelos de minería de datos. Una sola estructura de minería de datos puede contener varios *modelos de minería de datos* que comparten el mismo dominio. Un modelo de minería de datos aplica un algoritmo de modelo de minería a los datos, que se representan en una estructura de minería de datos.  
  
 Las unidades de creación de la estructura de minería de datos son las columnas de la estructura de minería de datos, que describen los datos que contiene el origen de datos. Estas columnas contienen información como el tipo de datos, el tipo de contenido y el modo en que se distribuyen los datos.  
  
 Las columnas de los modelos de minería de datos deben incluir la columna de clave descrita en la estructura de minería de datos, así como un subconjunto de las columnas restantes. El modelo de minería de datos define el uso de cada columna y el algoritmo utilizado para crearlo. Por ejemplo, en DMX puede especificar que una columna sea una columna de clave o una columna PREDICT. Si una columna no se especifica, se considera que es una columna de entrada.  
  
 En DMX, hay dos formas de crear modelos de minería de datos. Puede crear la estructura de minería de datos y el modelo de minería de datos asociado juntos usando la instrucción `CREATE MINING MODEL` o bien, puede crear primero una estructura de minería de datos usando la instrucción `CREATE MINING STRUCTURE` y, a continuación, agregar un modelo de minería de datos a la estructura usando la instrucción `ALTER STRUCTURE`. Estos métodos se describen a continuación.  
  
 `CREATE MINING MODEL`  
 Utilice esta instrucción para crear una estructura de minería de datos y el modelo de minería de datos asociado juntos, con el mismo nombre. Se anexa "Structure" al nombre del modelo de minería de datos para diferenciarlo de la estructura de minería de datos.  
  
 Esta instrucción resulta útil si crea una estructura de minería de datos que incluirá un único modelo de minería de datos.  
  
 Para obtener más información,vea [CREATE MINING MODEL &#40;DMX&#41;](/sql/dmx/create-mining-model-dmx).  
  
 CREATE MINING STRUCTURE  
 Utilice esta instrucción para crear una nueva estructura de minería de datos sin ningún modelo.  
  
 Cuando usa la instrucción CREATE MINING STRUCTURE, también puede crear un conjunto de datos de exclusiones que se puede utilizar para probar cualquier modelo que esté basado en la misma estructura de minería de datos.  
  
 Para obtener más información, consulte [CREATE MINING STRUCTURE &#40;DMX&#41;](/sql/dmx/create-mining-structure-dmx).  
  
 `ALTER MINING STRUCTURE`  
 Utilice esta instrucción para agregar un modelo de minería de datos a una estructura de minería de datos que ya existe en el servidor.  
  
 Hay varios motivos por los que puede desear agregar más de un modelo de minería de datos en una única estructura de minería de datos. Por ejemplo, podría crear varios modelos de minería de datos utilizando algoritmos distintos para ver cuál funciona mejor. O bien, podría crear varios modelos de minería de datos usando el mismo algoritmo, pero con un parámetro establecido de forma distinta para cada uno de ellos, con el fin de encontrar el mejor valor para el parámetro.  
  
 Para obtener más información, consulte [ALTER Mining STRUCTURE &#40;DMX&#41;](/sql/dmx/alter-mining-structure-dmx?view=sql-server-2016).  
  
 Puesto que creará una estructura de minería de datos que contiene varios modelos de minería de datos, utilizará el segundo método en este tutorial.  
  
 **Para obtener más información**  
  
 [Extensiones de minería de datos &#40;referencia de dmx&#41;](/sql/dmx/data-mining-extensions-dmx-reference), [Descripción de la instrucción DMX Select](/sql/dmx/understanding-the-dmx-select-statement), [estructura y uso de las consultas de predicción DMX](/sql/dmx/structure-and-usage-of-dmx-prediction-queries)  
  
## <a name="what-you-will-learn"></a>Aprendizaje  
 El tutorial está compuesto por las lecciones siguientes:  
  
 [Lección 1: Crear la estructura de minería de la cesta de la compra](../../2014/tutorials/lesson-1-creating-the-market-basket-mining-structure.md)  
 En esta lección aprenderá a usar la instrucción `CREATE` para crear estructuras de minería de datos.  
  
 [Lección 2: Agregar modelos de minería a la estructura de minería cesta de la compra](../../2014/tutorials/lesson-2-adding-mining-models-to-the-market-basket-mining-structure.md)  
 En esta lección aprenderá a usar la instrucción `ALTER` para agregar modelos de minería de datos a una estructura de minería de datos.  
  
 [Lección 3: Procesar la estructura de minería de datos de la cesta de la compra](../../2014/tutorials/lesson-3-processing-the-market-basket-mining-structure.md)  
 En esta lección aprenderá a usar la instrucción `INSERT INTO` para procesar estructuras de minería de datos y sus modelos de minería de datos asociados.  
  
 [Lección 4: Ejecutar predicciones de cesta de la compra](../../2014/tutorials/lesson-4-executing-market-basket-predictions.md)  
 En esta lección aprenderá a usar la instrucción `PREDICTION JOIN` para crear predicciones basadas en modelos de minería de datos.  
  
## <a name="requirements"></a>Requisitos  
 Antes de hacer este tutorial, asegúrese de que los siguientes componentes estén instalados:  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]  
  
-   La base de datos [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]  
  
 Con el fin de mejorar la seguridad, las bases de datos de ejemplo no se instalan de forma predeterminada. Para instalar las bases de datos de ejemplo oficiales [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]de, vaya [http://www.CodePlex.com/MSFTDBProdSamples](https://go.microsoft.com/fwlink/?LinkId=88417) a o en la Página principal de ejemplos y proyectos de la comunidad de la sección Microsoft SQL Server ejemplos Microsoft SQL Server del producto. Haga clic en **Databases**y, a continuación en la pestaña **Releases** y seleccione las bases de datos que desee.  
  
> [!NOTE]  
>  Para consultar los tutoriales, se recomienda agregar los botones **Siguiente** y **Anterior** a la barra de herramientas del visor de documentos.  
  
## <a name="see-also"></a>Consulte también  
 [Tutorial DMX de Bike Buyer](../../2014/tutorials/bike-buyer-dmx-tutorial.md)   
 [Tutorial básico de minería de datos](../../2014/tutorials/basic-data-mining-tutorial.md)   
 [Lección 3: generar un escenario de cesta de la compra &#40;tutorial intermedio de minería de datos&#41;](../../2014/tutorials/lesson-3-building-a-market-basket-scenario-intermediate-data-mining-tutorial.md)  
  
  
