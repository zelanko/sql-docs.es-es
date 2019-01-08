---
title: Agregar modelo a estructura (complementos de minería de datos para Excel de datos) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining models, creating
ms.assetid: 8efd5bf4-4e6a-4ee8-971a-6efaed5f3b76
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1aa72d2c9e2fcf953e8c34d7fdddd656c76b0685
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/28/2018
ms.locfileid: "52521039"
---
# <a name="add-model-to-structure-data-mining-add-ins-for-excel"></a>Agregar modelo a estructura (Complementos de minería de datos para Excel)
  ![Agregar modelo a botón estructura](media/dmc-addmodel.gif "Agregar modelo a botón estructura")  
  
 Al hacer clic en **Agregar modelo a estructura**, se inicia un asistente que le ayuda a crea un nuevo modelo de minería de datos para usar con una estructura de minería de datos existente. Esta opción es útil porque permite comparar modelos basados en los mismos datos o crear modelos personalizados.  
  
 Si la instancia de Analysis Services aún no contiene los datos que necesita, use el [Create Mining Structure &#40;complementos de minería de datos de SQL Server&#41; ](create-mining-structure-sql-server-data-mining-add-ins.md) Asistente para configurar una estructura de minería de datos. O bien, puede iniciar uno de los asistentes de modelado y agregar después un modelo nuevo a la estructura creada por el asistente.  
  
 Para crear modelos avanzados mediante algoritmos no compatibles con los asistentes, crear una estructura de minería de datos y, a continuación, agregar un modelo con el **Editor de consultas avanzadas de minería de datos**.  
  
## <a name="add-a-new-model-to-an-existing-structure"></a>Agregar un modelo nuevo a una estructura existente  
  
1.  En el **minería de datos** la cinta de opciones, haga clic en la flecha situada debajo **avanzadas**y, a continuación, seleccione **Agregar modelo a estructura**.  
  
2.  En el **seleccionar estructura** diálogo cuadro, elija la estructura que contiene los datos que desea usar y, a continuación, haga clic en **siguiente**.  
  
     **Sugerencia**: Si no estás seguro de qué estructura de minería de datos contiene los datos que necesita, use el **documentar modelo** Asistente para ver las columnas y estadísticas básicas sobre los datos.  
  
     Si no se encuentra una estructura de minería de datos, compruebe la conexión que está usando actualmente. Quizás necesite abrir una conexión a un servidor diferente.  
  
3.  En el **seleccionar algoritmo de minería de datos** cuadro de diálogo, seleccione un algoritmo de minería de datos para usar en el nuevo modelo de minería de datos.  
  
     Tenga en cuenta que el cuadro de diálogo proporciona muchas más opciones que verá en los asistentes. Puede crear un modelo con cualquiera de los algoritmos admitidos en el servidor de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], siempre y cuando los datos sean compatibles.  
  
4.  Se recomienda que hacer clic en el **parámetros** botón para abrir el **parámetros de algoritmo** diálogo cuadro y personalizar los parámetros del algoritmo. Esta opción es la manera más fácil de crear modelos de minería de datos personalizados.  
  
5.  Haga clic en **Siguiente**.  
  
6.  En el **seleccionar columnas** cuadro de diálogo, revise la lista de columnas y si es necesario, cambie el uso de las columnas en uno de estos valores:  
  
    -   **Entrada**. Indica que la columna contiene variables que pueden afectar al resultado y se deben usar como entradas en el modelo.  
  
    -   **Entrada y predicción**. Indica que los datos se deben usar como entrada y que también desea predecir estos valores.  
  
    -   **Sólo predicción**. Indica que los datos no se deben usar como entrada para el modelo.  
  
    -   **Clave**. Cada modelo requiere al menos una clave. Según el tipo de modelo, es posible que también tiene la opción de claves especiales adicionales, como el **SequenceKey** o **TimeKey**.  
  
    -   **No use**. Indica que los datos no se deben usar en el modelo, aunque estén presentes en la estructura.  
  
7.  Haga clic en el **(...)**  botón para abrir el **establecer marcadores de modelo de columna** cuadro de diálogo.  
  
     Dedique un minuto a comprobar que el uso de cada columna de datos es adecuado para el modelo. Se trata de un paso importante para evitar errores al intentar procesar el modelo.  
  
     Por ejemplo, si vuelve a usar una estructura que se creó para los árboles de decisión del modelo y aplican el algoritmo Naïve Bayes a ella, las columnas que tener el tipo de datos `Numeric` y el tipo de contenido `Continuous` deberá se agrupan o se ha cambiado a variables discretas.  
  
     Si las columnas de la estructura no son aplicables para el nuevo algoritmo, se puede omitir seleccionando **no use**.  
  
8.  En el **establecer marcadores de modelo de columna** cuadro de diálogo, revisar o conjunto de los marcadores de modelado, si existe.  
  
     Los marcadores de modelado permiten controlar cómo se tratan los valores NULL, entre otras cosas. Para obtener más información, vea [Marcas de modelado &#40;Minería de datos&#41;](data-mining/modeling-flags-data-mining.md).  
  
     Haga clic en **Aceptar** cuando termine para cerrar el cuadro de diálogo.  
  
9. En el **finalizar** diálogo cuadro, escriba un nombre y una descripción para el nuevo modelo de minería de datos.  
  
     Según el tipo de modelo que creó, puede tener también estas opciones:  
  
    -   Examinar el modelo de minería de datos completado una vez generado.  
  
    -   Usar la obtención de detalles del modelo en los datos de origen.  
  
         Para obtener más información, consulte [obtención de detalles en modelos de minería de datos](data-mining/drillthrough-on-mining-models.md).  
  
10. Haga clic en **finalizar** para guardar los cambios. El nuevo modelo se implementa en el servidor y se procesa.  
  
### <a name="related-options"></a>Opciones relacionadas  
  
|Opción|Comentarios|  
|------------|--------------|  
|**Seleccionar estructura o modelo** cuadro de diálogo|Elija una estructura de minería de datos existente para usarla como base para generar un nuevo modelo.  La estructura que elija debe estar en la conexión actual. Si no, cambie las conexiones mediante el [conectarse a los datos de origen &#40;cliente de minería de datos para Excel&#41; ](connect-to-source-data-data-mining-client-for-excel.md) herramienta.|  
|**Seleccione el algoritmo de minería de datos** cuadro de diálogo|La lista de los algoritmos de minería de datos depende del servidor al que está conectado. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] proporciona diferentes algoritmos en las ediciones Standard y Enterprise. El administrador puede haber agregado también algoritmos personalizados.<br /><br /> Si no se puede ver los algoritmos, compruebe que está conectado a una instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].|  
|**Parámetros de algoritmo** cuadro de diálogo|En estos valores, puede personalizar cada algoritmo usando parámetros específicos del método analítico. También puede establecer un valor de inicialización para asegurarse de que los resultados del modelo se pueden reproducir en varios pasos de entrenamiento.<br /><br /> Para obtener más información, consulte [parámetros de algoritmo &#40;complementos de minería de datos de SQL Server&#41;](algorithm-parameters-sql-server-data-mining-add-ins.md).|  
|**Establecer marcadores de modelo de columna** cuadro de diálogo|Los marcadores de modelado pueden mejorar el modelo especificando cómo se deben tratar los datos que faltan. Para obtener más información, vea [Marcas de modelado &#40;Minería de datos&#41;](data-mining/modeling-flags-data-mining.md).|  
  
###  <a name="Bkmk_mdlcolumn"></a> Establecer el uso de columna  
 Al agregar un nuevo modelo a una estructura de minería de datos existente, debe especificar la forma en que el modelo usará cada una de las columnas de datos en la estructura de minería de datos. Probablemente observará que las opciones de este asistente son mucho más detalladas que las opciones de la estructura de minería de datos. ¿Por qué?  
  
 El motivo es que cuando crea un modelo y una estructura a la vez con un asistente, muchas de las opciones que controlan cómo usa el algoritmo los datos se establecen automáticamente. Sin embargo, al agregar un modelo nuevo a uno existente, debe ver estas opciones manualmente y especificar si los datos se deben usar para el análisis, si el tipo de datos es correcto, etc.  
  
 Pueden aparecer mensajes de error al aplicar los nuevos algoritmos a los datos existentes, pero estos mensajes suelen proporcionar información detallada sobre las correcciones que tiene que realizar para que se pueda procesar el modelo. Entre los problemas habituales se incluyen los siguientes:  
  
-   El modelo espera un tipo de datos diferente al que contiene la estructura.  
  
     Algunos algoritmos solo funcionan con números, mientras que otros solo funcionan con texto. Si los datos son del tipo incorrecto para el nuevo modelo, puede que necesite modificar la estructura para permitir el procesamiento del modelo.  
  
-   La estructura de minería de datos no contiene ningún atributo de predicción.  
  
     Los modelos de clústeres se pueden generar sin un valor de predicción, pero en otros modelos suele ser necesario especificar una única columna para la predicción.  
  
-   La composición de los datos es incompatible con el algoritmo que ha elegido.  
  
     Algunos tipos de análisis requieren que los datos estén perfectamente estructurados según unas reglas únicas. Por ejemplo, los modelos de pronóstico y los modelos de asociación. Puede agregar fácilmente nuevos modelos del mismo tipo, quizás con personalizaciones, pero quizás los datos no funcionen con otros algoritmos.  
  
### <a name="requirements"></a>Requisitos  
 Para crear modelos de minería de datos, primero debe tener una conexión a una instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Para obtener más información acerca de cómo crear o cambiar una conexión, consulte [conectarse a los datos de origen &#40;cliente de minería de datos para Excel&#41;](connect-to-source-data-data-mining-client-for-excel.md).  
  
 Si no ve la estructura de minería de datos que desea, es posible que se guardara en otra instancia o en otra base de datos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Para obtener información acerca de cómo cambiar a una conexión de minería de datos diferentes, consulte [conectar con un servidor de minería de datos](connect-to-a-data-mining-server.md).  
  
## <a name="see-also"></a>Vea también  
 [Crear un modelo de minería de datos](creating-a-data-mining-model.md)   
