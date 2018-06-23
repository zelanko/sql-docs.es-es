---
title: Pestaña diagrama del clúster de clústeres de secuencia (Visor de modelos de minería de datos | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dm.miningmodeleditor.sequenceclustering.diagrams.f1
ms.assetid: 4b705397-9af4-4678-9eda-149bc5d762fa
caps.latest.revision: 26
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 56c384e39ae4ef364f608cef8fa507d20bb746ef
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36104782"
---
# <a name="sequence-clustering-cluster-diagram-tab-mining-model-viewer"></a>Pestaña Diagrama de agrupación en clústeres de secuencia (Visor de modelos de minería de datos)
  La pestaña **Diagrama del clúster** del **Visor de agrupación en clústeres de secuencia de Microsoft** proporciona una vista gráfica de todos los clústeres que contiene el modelo de agrupación en clústeres de secuencia.  
  
 Utilice esta vista de un modelo de agrupación en clústeres de secuencia para obtener detalles de cada clúster para llegar a los casos de apoyo, si la obtención de detalles se ha habilitado. También puede asignar nombres descriptivos a los clústeres y cambiar la variable de sombreado para evaluar la distribución de valores de un vistazo  
  
 **Para más información:** [Algoritmo de clústeres de secuencia de Microsoft](data-mining/microsoft-sequence-clustering-algorithm.md), [Examinar un modelo usando el Visor de clústeres de secuencia de Microsoft](data-mining/browse-a-model-using-the-microsoft-sequence-cluster-viewer.md)  
  
## <a name="options"></a>Opciones  
 **Actualizar el contenido del Visor**  
 Vuelva a cargar el modelo de minería de datos en el visor.  
  
 **Modelo de minería de datos**  
 Elija esta opción para ver un modelo de minería de datos que se encuentra en la estructura de minería de datos actual. El modelo de minería de datos se abrirá en el visor asociado.  
  
 **Visor**  
 Elija un visor que desee usar para explorar el modelo de minería de datos seleccionado. Puede utilizar el visor personalizado o el **Visor de árbol de contenido genérico de Microsoft**. También puede utilizar visores de complemento si están disponibles.  
  
 **Acercar**  
 Acerque el diagrama para obtener una vista más detallada de los clústeres.  
  
 **Alejar**  
 Aleje el diagrama, para ver todos los clústeres del modelo.  
  
 **Copiar vista del gráfico**  
 Copie la sección visible del diagrama en el portapapeles.  
  
 **Copiar todo el gráfico**  
 Copie el diagrama completo en el portapapeles.  
  
 **Ajustar diagrama a la ventana**  
 Aleje el diagrama hasta que el todo él se ajuste a la pantalla.  
  
 **Buscar nodo**  
 Use el cuadro de diálogo **Buscar nodo** para filtrar los clústeres en el gráfico y facilitar la búsqueda de un clúster concreto. Para más información, vea [Cuadro de diálogo Buscar nodo &#40;Visor de modelos de minería de datos&#41;](find-node-dialog-box-mining-model-viewer.md).  
  
 Observe que en este contexto, solo está buscando el nombre del clúster, no los atributos incluidos en el clúster; por consiguiente, esta opción es muy útil si ha asignado nombres descriptivos al clúster. Para asignar nombres a los clústeres en el visor, haga clic con el botón derecho en cada clúster y seleccione **Cambiar nombre**.  
  
 **Mejorar diseño**  
 Vuelva a ordenar los clústeres en el diagrama para mejorar el diseño.  
  
 **Densidad**  
 La apariencia del gráfico de barras de densidad y de los valores que contiene depende del atributo que seleccione en **Variable de sombreado**.  
  
-   Si no se selecciona ningún estado de atributo como la variable de sombreado, de forma predeterminada la densidad de sombreando que se aplica a cada clúster representa la compatibilidad del clúster, comparada con la población general de casos.  
  
-   Si selecciona un atributo para **Variable de sombreado**, deberá seleccionar también un valor para **Estado** . Al hacer esto, el gráfico de barras de densidad se actualiza para mostrar la probabilidad de este estado. Puede detener el mouse sobre cualquier clúster individual para ver la probabilidad del estado seleccionado para el clúster.  
  
 **Variable de sombreado**  
 Seleccione un atributo del modelo de minería de datos para utilizar para sombrear el diagrama del clúster.  
  
 **State**  
 Seleccione un estado que se corresponda con la **Variable de sombreado**. Por ejemplo, si quiere ver las secuencias en las que se incluye un producto determinado, seleccione la columna [Product] como el atributo de **Variable de sombreado**y seleccione el nombre del producto concreto como el valor de **Estado** .  
  
 **Vínculos**  
 Las líneas del diagrama indican las asociaciones entre los clústeres de secuencia. Puede ajustar el número de vínculos que muestra el visor ajustando el control deslizante situado a la derecha de los clústeres. Si desplaza el control deslizante hacia abajo, sólo se verán los vínculos más similares.  
  
## <a name="see-also"></a>Vea también  
 [Algoritmos de minería de datos &#40;Analysis Services: minería de datos&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Visores de modelos de minería de datos &#40;Diseñador de modelos de minería de datos&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [Visores de modelos de minería de datos](data-mining/data-mining-model-viewers.md)  
  
  