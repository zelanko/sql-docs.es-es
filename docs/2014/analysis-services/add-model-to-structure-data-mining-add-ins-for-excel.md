---
title: Agregar modelo a estructura (complementos de minería de datos para Excel) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining models, creating
ms.assetid: 8efd5bf4-4e6a-4ee8-971a-6efaed5f3b76
author: minewiskan
ms.author: owend
ms.openlocfilehash: 606d453235529fbfed4dc0f07178ce2ae7132067
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/08/2020
ms.locfileid: "84528261"
---
# <a name="add-model-to-structure-data-mining-add-ins-for-excel"></a>Agregar modelo a estructura (Complementos de minería de datos para Excel)
  ![Botón Agregar un modelo a una estructura](media/dmc-addmodel.gif "Botón Agregar un modelo a una estructura")  
  
 Al hacer clic en **Agregar modelo a estructura**, se inicia un asistente que le ayuda a crear un nuevo modelo de minería de datos para utilizarlo con una estructura de minería de datos existente. Esta opción es útil porque permite comparar modelos basados en los mismos datos o crear modelos personalizados.  
  
 Si la instancia de Analysis Services aún no contiene los datos que necesita, use el Asistente para la creación de una estructura de minería de [datos &#40;SQL Server complementos de minería de datos&#41;](create-mining-structure-sql-server-data-mining-add-ins.md) para configurar una estructura de minería de datos. O bien, puede iniciar uno de los asistentes de modelado y agregar después un modelo nuevo a la estructura creada por el asistente.  
  
 Para crear modelos avanzados mediante algoritmos no admitidos por los asistentes, cree una estructura de minería de datos y, a continuación, agregue un modelo mediante el **Editor de consultas avanzadas de minería de datos**.  
  
## <a name="add-a-new-model-to-an-existing-structure"></a>Agregar un modelo nuevo a una estructura existente  
  
1.  En la cinta de opciones **minería de datos** , haga clic en la flecha situada debajo de **avanzadas**y, a continuación, seleccione **Agregar modelo a estructura**.  
  
2.  En el cuadro de diálogo **seleccionar estructura** , elija la estructura que contiene los datos que desea utilizar y, a continuación, haga clic en **siguiente**.  
  
     **Sugerencia**: Si no está seguro de qué estructura de minería de datos contiene los datos que necesita, use el Asistente para **documentar modelo** para ver las columnas y estadísticas básicas de los datos.  
  
     Si no encuentra una estructura de minería de datos, Compruebe la conexión que está usando actualmente. Quizás necesite abrir una conexión a un servidor diferente.  
  
3.  En el cuadro de diálogo **seleccionar algoritmo de minería** de datos, elija un algoritmo de minería de datos que se utilizará en el nuevo modelo de minería de datos.  
  
     Tenga en cuenta que el cuadro de diálogo proporciona muchas más opciones de las que verá en los asistentes. Puede crear un modelo con cualquiera de los algoritmos admitidos en el servidor de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], siempre y cuando los datos sean compatibles.  
  
4.  Se recomienda hacer clic también en el botón **parámetros** para abrir el cuadro de diálogo **parámetros de algoritmo** y personalizar los parámetros en el algoritmo. Esta opción es la manera más fácil de crear modelos de minería de datos personalizados.  
  
5.  Haga clic en **Next**.  
  
6.  En el cuadro de diálogo **seleccionar columnas** , revise la lista de columnas y, si es necesario, cambie el uso de las columnas a uno de estos valores:  
  
    -   **Entrada**. Indica que la columna contiene variables que pueden afectar al resultado y se deben usar como entradas en el modelo.  
  
    -   **Entrada y predicción**. Indica que los datos se deben usar como entrada y que también desea predecir estos valores.  
  
    -   **Solo predicción**. Indica que los datos no se deben usar como entrada para el modelo.  
  
    -   **Clave**. Cada modelo requiere al menos una clave. Dependiendo del tipo de modelo, también puede tener la opción de claves especiales adicionales, como **SequenceKey** o **TimeKey**.  
  
    -   **No use**. Indica que los datos no se deben usar en el modelo, aunque estén presentes en la estructura.  
  
7.  Haga clic en el botón examinar **(...)** para abrir el cuadro de diálogo **establecer marcadores de modelo de columna** .  
  
     Dedique un minuto a comprobar que el uso de cada columna de datos es adecuado para el modelo. Se trata de un paso importante para evitar errores al intentar procesar el modelo.  
  
     Por ejemplo, si vuelve a usar una estructura que se creó para un modelo de árboles de decisión y le aplica el algoritmo Bayes Naive, las columnas que tengan el tipo de datos `Numeric` y el tipo de contenido deberán `Continuous` ser discretizan o cambiar a variables discretas.  
  
     Si las columnas de la estructura no son aplicables al nuevo algoritmo, puede omitirlas si selecciona **no usar**.  
  
8.  En el cuadro de diálogo **establecer marcas de modelo de columna** , revise o establezca las marcas de modelado, si las hay.  
  
     Los marcadores de modelado permiten controlar cómo se tratan los valores NULL, entre otras cosas. Para obtener más información, vea [Marcas de modelado &#40;Minería de datos&#41;](data-mining/modeling-flags-data-mining.md).  
  
     Haga clic en **Aceptar** cuando haya terminado para cerrar el cuadro de diálogo.  
  
9. En el cuadro de diálogo **Finalizar** , escriba un nombre y una descripción para el nuevo modelo de minería de datos.  
  
     Según el tipo de modelo que creó, puede tener también estas opciones:  
  
    -   Examinar el modelo de minería de datos completado una vez generado.  
  
    -   Usar la obtención de detalles del modelo en los datos de origen.  
  
         Para obtener más información, vea [obtención de detalles en los modelos de minería de datos](data-mining/drillthrough-on-mining-models.md).  
  
10. Haga clic en **Finalizar** para guardar los cambios. El nuevo modelo se implementa en el servidor y se procesa.  
  
### <a name="related-options"></a>Opciones relacionadas  
  
|Opción|Comentarios|  
|------------|--------------|  
|Cuadro **de diálogo Seleccionar estructura o modelo**|Elija una estructura de minería de datos existente para usarla como base para generar un nuevo modelo.  La estructura que elija debe estar en la conexión actual. Si no es así, cambie las conexiones con la herramienta [conectar con datos de origen &#40;cliente de minería de datos para Excel&#41;](connect-to-source-data-data-mining-client-for-excel.md) .|  
|**Seleccionar algoritmo de minería de datos** (cuadro de diálogo)|La lista de los algoritmos de minería de datos depende del servidor al que está conectado. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] proporciona diferentes algoritmos en las ediciones Standard y Enterprise. El administrador puede haber agregado también algoritmos personalizados.<br /><br /> Si no puede ver ningún algoritmo, compruebe que está conectado a una instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .|  
|**Parámetros de algoritmo** Cuadro de diálogo|En estos valores, puede personalizar cada algoritmo usando parámetros específicos del método analítico. También puede establecer un valor de inicialización para asegurarse de que los resultados del modelo se pueden reproducir en varios pasos de entrenamiento.<br /><br /> Para obtener más información, vea [parámetros de algoritmo &#40;SQL Server complementos de minería de datos&#41;](algorithm-parameters-sql-server-data-mining-add-ins.md).|  
|**Establecer marcas de modelo de columna** Cuadro de diálogo|Los marcadores de modelado pueden mejorar el modelo especificando cómo se deben tratar los datos que faltan. Para obtener más información, vea [Marcas de modelado &#40;Minería de datos&#41;](data-mining/modeling-flags-data-mining.md).|  
  
###  <a name="setting-column-usage"></a><a name="Bkmk_mdlcolumn"></a>Establecer el uso de las columnas  
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
 Para crear modelos de minería de datos, primero debe tener una conexión a una instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Para obtener más información acerca de cómo crear o cambiar una conexión, vea [conectarse a los datos de origen &#40;cliente de minería de datos para Excel&#41;](connect-to-source-data-data-mining-client-for-excel.md).  
  
 Si no ve la estructura de minería de datos que desea, es posible que se guardara en otra instancia o en otra base de datos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Para obtener información acerca de cómo cambiar a una conexión de minería de datos diferente, vea [conectarse a un servidor de minería de datos](connect-to-a-data-mining-server.md).  
  
## <a name="see-also"></a>Consulte también  
 [Crear un modelo de minería de datos](creating-a-data-mining-model.md)   
