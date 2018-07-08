---
title: Bike Buyer DMX Tutorial | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- DMX [Analysis Services], tutorials
- data mining [Analysis Services], tutorials
- statements [DMX], tutorials
- Data Mining Extensions [Analysis Services], tutorials
- tutorials [Data Mining]
ms.assetid: 4b634cc1-86dc-42ec-9804-a19292fe8448
caps.latest.revision: 33
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 788cdb0ccd3f8093972c45db1463412c5f41a765
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37187672"
---
# <a name="bike-buyer-dmx-tutorial"></a>Tutorial DMX de Bike Buyer
  En este tutorial aprenderá a crear, entrenar y explorar modelos de minería de datos utilizando el lenguaje de consulta Extensiones de minería de datos (DMX). A continuación, estos modelos de minería de datos se utilizarán para crear predicciones que determinan si un cliente adquirirá una bicicleta.  
  
 Los modelos de minería de datos se crearán a partir de los datos incluidos en la base de datos de ejemplo [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)], que almacena datos de la empresa ficticia [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)]. [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] es una gran empresa multinacional de fabricación. La empresa fabrica y vende bicicletas de metal y de materiales compuestos en los mercados de Norteamérica, Europa y Asia. Su sede central de operaciones se encuentra en Bothell, Washington, con 290 empleados, y tiene distribuidos varios equipos regionales de ventas en toda su base de mercado internacional.  
  
## <a name="tutorial-scenario"></a>Escenario del tutorial  
 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] ha decidido ampliar su análisis de datos mediante la creación de una aplicación personalizada que use la funcionalidad de minería de datos. El objetivo de la aplicación personalizada es poder:  
  
-   Tomar como datos de entrada características concretas acerca de un cliente potencial y predecir si adquirirá una bicicleta.  
  
-   Tomar como datos de entrada una lista de clientes potenciales, así como características acerca de los clientes, y predecir qué clientes adquirirán una bicicleta.  
  
 En el primer caso, los datos del cliente provienen de una página de registro de clientes y, en el segundo caso, el departamento de marketing de [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] proporciona una lista de clientes potenciales.  
  
 Además, el departamento de marketing ha solicitado la capacidad de agrupar clientes existentes en categorías basadas en características como, por ejemplo, su lugar de residencia, el número de hijos que tienen y la distancia que tienen que recorrer para llegar al trabajo. Desean ver si estos clústeres se pueden usar para ayudar a dirigir campañas a tipos concretos de clientes. Esto requerirá un modelo de minería de datos adicional.  
  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] proporciona varias herramientas que pueden usarse para realizar estas tareas:  
  
-   El lenguaje de consulta DMX  
  
-   El [algoritmo de árboles de decisión de Microsoft](../../2014/analysis-services/data-mining/microsoft-decision-trees-algorithm.md) y [algoritmo de clústeres de Microsoft](../../2014/analysis-services/data-mining/microsoft-clustering-algorithm.md)  
  
-   El Editor de consultas de [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]  
  
 Extensiones de minería de datos (DMX) es un lenguaje de consulta proporcionado por [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] que sirve para crear y trabajar con modelos de minería de datos. El algoritmo de árboles de decisión de [!INCLUDE[msCoName](../includes/msconame-md.md)] crea modelos que se pueden utilizar para predecir si alguien adquirirá una bicicleta. El modelo resultante puede tomar un cliente individual o una tabla de clientes como entrada. El algoritmo de clústeres de [!INCLUDE[msCoName](../includes/msconame-md.md)] puede crear agrupaciones de clientes basadas en características compartidas. El objetivo de este tutorial es proporcionar los scripts DMX que se utilizarán en la aplicación personalizada.  
  
 **Para obtener más información:** [soluciones de minería de datos](../../2014/analysis-services/data-mining/data-mining-solutions.md)  
  
## <a name="mining-structure-and-mining-models"></a>Estructura de minería de datos y modelos de minería de datos  
 Antes de empezar a crear instrucciones DMX, es importante comprender los objetos principales utilizados por [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] para crear modelos de minería de datos. La estructura de minería de datos es una estructura de datos que define el dominio de datos a partir del cual se generan los modelos de minería de datos. Una estructura de minería de datos sencilla puede contener varios modelos de minería de datos que comparten el mismo dominio. Un modelo de minería de datos aplica un algoritmo de modelo de minería a los datos, que se representan en una estructura de minería de datos.  
  
 Las unidades de creación de la estructura de minería de datos son las columnas de la estructura de minería de datos, que describen los datos que contiene el origen de datos. Estas columnas contienen información como el tipo de datos, el tipo de contenido y el modo en que se distribuyen los datos.  
  
 Las columnas de los modelos de minería de datos deben incluir la columna de clave descrita en la estructura de minería de datos, así como un subconjunto de las columnas restantes. El modelo de minería de datos define el uso de cada columna y el algoritmo utilizado para crearlo. Por ejemplo, en DMX puede especificar que una columna sea una columna de clave o una columna PREDICT. Si una columna no se especifica, se considera que es una columna de entrada.  
  
 En DMX, hay dos formas de crear modelos de minería de datos. Puede crear la estructura de minería de datos y el modelo de minería de datos asociado juntos, utilizando la instrucción CREATE MINING MODEL, o bien, puede crear primero una estructura de minería de datos, utilizando la instrucción CREATE MINING STRUCTURE, y, a continuación, agregar un modelo de minería de datos a la estructura, utilizando la instrucción ALTER STRUCTURE. Estos métodos se describen en la siguiente tabla.  
  
 CREATE MINING MODEL  
 Utilice esta instrucción para crear una estructura de minería de datos y el modelo de minería de datos asociado juntos, con el mismo nombre. Se anexa "Structure" al nombre del modelo de minería de datos para diferenciarlo de la estructura de minería de datos. Esta instrucción resulta útil si crea una estructura de minería de datos que incluirá un único modelo de minería de datos.  
  
 Para obtener más información,vea [CREATE MINING MODEL &#40;DMX&#41;](/sql/dmx/create-mining-model-dmx).  
  
 ALTER MINING STRUCTURE  
 Utilice esta instrucción para agregar un modelo de minería de datos a una estructura de minería de datos que ya existe en el servidor. Esta instrucción resulta útil si desea crear una estructura de minería de datos que incluya varios modelos de minería de datos. Hay varios motivos por los que puede desear agregar más de un modelo de minería de datos en una única estructura de minería de datos. Por ejemplo, podría crear varios modelos de minería de datos que utilizase algoritmos distintos para ver cuál funciona mejor. Podría crear varios modelos de minería de datos que utilizara el mismo algoritmo, pero con un parámetro establecido de forma distinta para cada uno de ellos, para encontrar el mejor valor para el parámetro.  
  
 Para obtener más información, consulte [ALTER MINING STRUCTURE &#40;DMX&#41;] ((~/dmx/alter-mining-structure-dmx.md).  
  
 Puesto que creará una estructura de minería de datos que contiene varios modelos de minería de datos, utilizará el segundo método en este tutorial.  
  
 **Para obtener más información**  
  
 [Extensiones de minería de datos &#40;DMX&#41; referencia](/sql/dmx/data-mining-extensions-dmx-reference), [descripción DMX instrucción Select](/sql/dmx/understanding-the-dmx-select-statement), [estructura y el uso de consultas de predicción DMX](/sql/dmx/structure-and-usage-of-dmx-prediction-queries)  
  
## <a name="what-you-will-learn"></a>Aprendizaje  
 El tutorial está compuesto por las lecciones siguientes:  
  
 [Lección 1: Crear la estructura de minería de datos de Bike Buyer](../../2014/tutorials/lesson-1-creating-the-bike-buyer-mining-structure.md)  
 En esta lección aprenderá a usar la instrucción `CREATE` para crear estructuras de minería de datos.  
  
 [Lección 2: Agregar modelos de minería de datos a la estructura de minería de datos de Bike Buyer](../../2014/tutorials/lesson-2-adding-mining-models-to-the-bike-buyer-mining-structure.md)  
 En esta lección aprenderá a usar la instrucción `ALTER` para agregar modelos de minería de datos a una estructura de minería de datos.  
  
 [Lección 3: Procesar la estructura de minería de datos de Bike Buyer](../../2014/tutorials/lesson-3-processing-the-bike-buyer-mining-structure.md)  
 En esta lección aprenderá a usar la instrucción `INSERT INTO` para procesar estructuras de minería de datos y sus modelos de minería de datos asociados.  
  
 [Lección 4: Examinar los modelos de minería de datos de Bike Buyer](../../2014/tutorials/lesson-4-browsing-the-bike-buyer-mining-models.md)  
 En esta lección aprenderá a utilizar la instrucción `SELECT` para explorar el contenido de los modelos de minería de datos.  
  
 [Lección 5: Ejecutar consultas de predicción](../../2014/tutorials/lesson-5-executing-prediction-queries.md)  
 En esta lección aprenderá a usar la instrucción `PREDICTION JOIN` para crear predicciones basadas en modelos de minería de datos.  
  
## <a name="requirements"></a>Requisitos  
 Antes de hacer este tutorial, asegúrese de que los siguientes componentes estén instalados:  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssASversion2005](../includes/ssasversion2005-md.md)], [!INCLUDE[ssASversion10](../includes/ssasversion10-md.md)], [!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)], o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]  
  
-   Las base de datos [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]. Con el fin de mejorar la seguridad, las bases de datos de ejemplo no se instalan de forma predeterminada. Para instalar las bases de datos de ejemplo oficiales para [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], visite la [bases de datos de ejemplo de Microsoft SQL](http://go.microsoft.com/fwlink/?LinkId=88417) página y seleccione las bases de datos que desea instalar...  
  
> [!NOTE]  
>  Para consultar los tutoriales, se recomienda agregar los botones **Siguiente** y **Anterior** a la barra de herramientas del visor de documentos.  
  
## <a name="see-also"></a>Vea también  
 [Tutorial DMX de Market Basket](../../2014/tutorials/market-basket-dmx-tutorial.md)   
 [Tutorial básico de minería de datos](../../2014/tutorials/basic-data-mining-tutorial.md)  
  
  
