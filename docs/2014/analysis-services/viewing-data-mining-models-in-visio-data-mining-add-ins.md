---
title: Ver modelos de minería de datos en Visio (complementos de minería de datos) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- diagram, modifying
- templates [Visio]
- shapes, data mining
- diagram
ms.assetid: 5841adea-6650-4fae-8526-26af33edbede
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c287e840c07d11a527e980f9f07fb39fb3852739
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66065518"
---
# <a name="viewing-data-mining-models-in-visio-data-mining-add-ins"></a>Ver los modelos de minería de datos en Visio (Complementos de minería de datos)
  Las formas de Visio para minería de datos le permiten conectarse a un servidor y crear un diagrama que represente un modelo de minería de datos existente. Posteriormente, se pueden personalizar los diagramas mediante los controles de Visio, pero también puede explorar en profundidad datos, exponer algunas de las estadísticas subyacentes y trabajar con el modelo subyacente.  
  
## <a name="building-a-model-diagram"></a>Crear un diagrama del modelo  
 Al abrir el archivo que contiene las formas de Visio para minería de datos, el **formas** panel muestra las formas siguientes.  
  
 Si no ve las formas de minería de datos al abrir Visio, abra el archivo de plantilla desde la carpeta de instalación.  
  
 ![DM](media/dm-stencil.gif "DM")  
  
 Para usar una forma, arrástrela hasta la página. Cada forma abre un asistente diferente que ayuda a seleccionar datos de origen, establecer opciones específicas del tipo de diagrama y especificar sombreado y otras opciones de presentación.  
  
 En la tabla siguiente se muestran los tipos de modelos que se pueden usar con cada tipo de diagrama.  
  
|Forma de Visio|Modelos admitidos|  
|-----------------|----------------------|  
|Árbol de decisión|Esta forma se usa para modelos basados en los algoritmos de árboles de decisión o de regresión linear.|  
|Red de dependencias|Esta forma se usa para modelos basados en cualquiera de los algoritmos siguientes: Bayes naive, árboles de decisión o reglas de asociación.|  
|Clúster|Esta forma se usa para modelos basados en algoritmos de clústeres.|  
  
 El asistente puede ofrecer distintas opciones en función del tipo de datos del modelo de minería de datos. Por ejemplo, las columnas que contienen números continuos se visualizan de forma diferente que las variables de categorías.  
  
## <a name="working-with-completed-shapes"></a>Trabajar con formas completadas  
 Una vez haya completado el diagrama, puede utilizarlo para examinar el modelo de minería de datos o para mejorara el diagrama e incluirlo en presentaciones.  
  
### <a name="visio-menus"></a>Menús de Visio  
 Visio proporciona una variedad de controles de representación, temas y menús contextuales para ayudarle a mejorar los diagramas.  
  
-   Los temas de Visio se usan para modificar los colores del diagrama.  
  
-   Cambie los conectores o el diseño del diagrama.  
  
### <a name="data-mining-menus"></a>Menús de minería de datos  
 Estas barras de herramientas y elementos de menú los proporcionan los complementos específicos de cada forma o tipo de modelo  
  
-   Cada tipo de diagrama tiene un menú contextual para la forma que permite tener acceso a opciones especiales. Aunque muchas de las opciones de este menú son comunes para todas las formas de Visio, algunas son exclusivas de las plantillas de minería de datos  
  
     Por ejemplo, en un diagrama de árbol de decisión, puede hacer clic en un nodo y, después, contraer los nodos secundarios para que el diagrama sea más sencillo, o trasladar los nodos secundarios a otra página distinta.  
  
-   Dado que la forma está vinculada a los datos del modelo, también se puede realizar cierto nivel de exploración con el diagrama:  
  
     Filtrar los nodos que se muestran, o cambiar el nivel del árbol o la profundidad del gráfico.  
  
     Acercar secciones específicas, buscar nodos que contengan un determinado atributo o filtrar un gráfico de dependencias por sus bordes (probabilidad).  
  
## <a name="walkthroughs"></a>Tutoriales  
 Para obtener ejemplos de cómo trabajar con un diagrama completado y cómo interpretarlo, vea los temas siguientes:  
  
 [Tutorial del diagrama del clúster](cluster-diagram-walkthrough-data-mining-add-ins.md)  
  
 [Tutorial del diagrama de red de dependencias](dependency-network-diagram-walkthrough-data-mining-add-ins.md)  
  
 [Tutorial del diagrama de árbol de decisión](decision-tree-diagram-walkthrough-data-mining-add-ins.md)  
  
## <a name="see-also"></a>Vea también  
 [Examinar modelos en Excel &#40;complementos de minería de datos de SQL Server&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md)  
  
  
