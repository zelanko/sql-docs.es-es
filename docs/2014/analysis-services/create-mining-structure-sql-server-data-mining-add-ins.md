---
title: Crear estructura de minería de datos (complementos de minería de datos de SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining structures, creating
ms.assetid: b8b1eedc-4d6d-4429-a578-e629ec573934
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ae5244110e6b95434f9008fd7dc99cee259acf8c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66086818"
---
# <a name="create-mining-structure-sql-server-data-mining-add-ins"></a>Crear estructura de minería de datos (Complementos de minería de datos de SQL Server)
  ![Botón Crear estructura de minería de datos, cinta de opciones Minería de datos](media/dmc-createstruct.gif "Botón Crear estructura de minería de datos, cinta de opciones Minería de datos")  
  
 Utilice la opción **Opciones avanzadas** del grupo de **modelado de datos** cuando desee crear un conjunto de datos que se utilizará para el análisis sin crear necesariamente un modelo. Esto es útil si desea hacer pruebas con distintos algoritmos.  
  
 Después de crear la estructura de minería de datos, use el Asistente para [Agregar modelo a estructura](add-model-to-structure-data-mining-add-ins-for-excel.md) para crear un modelo basado en esa estructura. También puede crear nuevos modelos mediante el editor de **consultas avanzadas de minería de datos**.  
  
 También puede usar esta opción si desea generar modelos mediante uno de los algoritmos avanzados, que [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] admite pero no están disponibles a través de un asistente, como regresión lineal o clústeres de secuencia, o si está empleando un algoritmo personalizado.  
  
> [!NOTE]  
>  Al crear la estructura de minería de datos, también puede establecer un conjunto de datos de pruebas seleccionado aleatoriamente que puede usar para validar todos los modelos. Esto resulta cómodo porque permite comparar fácilmente la precisión del modelo con un conjunto de datos común. Simplemente seleccione la opción, **Divida los datos en conjuntos de entrenamiento y de prueba** , y especifique un porcentaje adecuado de datos para reservarlos para las pruebas, normalmente en torno al 30 por ciento.  
  
## <a name="use-the-wizard-to-create-a-mining-structure"></a>Usar el asistente para crear una estructura de minería de datos  
  
1.  En la cinta de opciones **minería de datos** , haga clic en **avanzadas**y seleccione **crear estructura**.  
  
2.  En el cuadro de diálogo **seleccionar datos de origen** , especifique el intervalo de Excel, la tabla de datos de Excel o el origen de datos externo que contiene los datos que desea utilizar para el análisis.  
  
     Haga clic en **Next**.  
  
3.  En el cuadro de diálogo **seleccionar columnas** , revise la lista de columnas disponibles en el origen de datos seleccionado.  
  
4.  Haga clic en la flecha situada a la derecha del nombre de columna para cambiar el **uso** de la columna y elija entre estos valores:  
  
    -   **Clave**. Se necesita al menos una clave para cada modelo.  
  
    -   **Key Time**. Esta opción solo está disponible para los modelos de pronóstico, donde es necesaria.  
  
    -   **Incluya**. Indica que la columna debe estar disponible en la estructura de minería de datos pero no es una columna de clave.  
  
    -   **No use**. Indica que la columna no se debe incluir en la estructura de minería de datos.  
  
     Recuerde que siempre puede omitir columnas al generar el modelo, pero para agregar columnas más adelante hay que volver a procesar la estructura y el modelo.  
  
5.  Haga clic en el botón examinar **(...)** para establecer el tipo de contenido, el tipo de datos y las marcas de modelado.  
  
    > [!NOTE]  
    >  Si la columna contiene datos numéricos, debe abrir siempre este cuadro de diálogo para asegurarse de que se ha elegido el tipo de datos correcto. En algunos casos, aunque los datos de entrada sean un número, le interesará tratarlos como una variable de categoría, o un valor discreto, en lugar de como un número continuo.  
    >   
    >  Por ejemplo, una columna de código postal se podría mostrar de forma predeterminada como un tipo de datos Long continuo, pero si desea obtener mejores resultados, puede especificar que se trate como un valor de texto discreto.  
    >   
    >  Para obtener más información, vea la sección sobre los tipos de contenido en [elegir datos para minería de datos](choosing-data-for-data-mining.md).  
  
     Haga clic en **Aceptar** para cerrar el cuadro de diálogo.  
  
6.  Haga clic en **Next**.  
  
     Según el tipo de datos que esté usando, puede completar el asistente después de este paso. En ese caso, vaya a la página **Finalizar** para asignar un nombre a la estructura de minería de datos.  
  
     Para otros modelos, tiene la opción adicional para crear un conjunto de datos de prueba.  
  
7.  En el cuadro de diálogo **dividir datos en conjuntos de datos de entrenamiento y de prueba** , especifique cómo desea que se particionen los datos. De forma predeterminada, para las pruebas se usa el 30 por ciento de los datos.  
  
     Opcionalmente, escriba el número máximo de filas que desea usar para las pruebas.  
  
     Haga clic en **Next**.  
  
8.  En el cuadro de diálogo **Finalizar** , escriba un nombre y una descripción para la nueva estructura de minería de datos.  
  
9. Haga clic en **Finalizar**  
  
### <a name="related-options"></a>Opciones relacionadas  
  
|Opción|Comentarios|  
|------------|--------------|  
|Cuadro de diálogo **seleccionar datos de origen**|Al seleccionar una tabla de Excel, debe indicar si los datos ya tienen encabezados. Si omite este paso, la primera fila de datos se usará como nombre de columna.<br /><br /> Si usa la opción origen de **datos externo**, puede usar cualquier tipo de datos que se pueda definir en un [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] origen de datos. Sin embargo, el cuadro de diálogo del complemento para crear nuevos orígenes de datos no incluye todos los orígenes de datos compatibles con Analysis Services, por lo que se recomienda crear de antemano los orígenes de datos en el servidor de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] y conectarse después mediante los complementos.|  
|Cuadro de diálogo **Editor de consultas de origen de datos**|Después de haberse conectado al origen de datos especificado, puede agregar columnas o crear una consulta personalizada para generar columnas personalizadas.|  
|**Dividir datos en conjuntos de entrenamiento y de prueba**|Un valor recomendado para el entrenamiento y los conjuntos de pruebas es del 70 por ciento para el entrenamiento y el 30 por ciento para las pruebas; sin embargo, si tiene muchos datos, puede especificar un número máximo de filas para las pruebas.|  
|Cuadro de diálogo Finalizar|En algunos tipos de modelo hay disponibles opciones de obtención de detalles, que son muy útiles si incluyó columnas de detalles en la estructura de minería de datos. Por ejemplo, si crea un modelo de clústeres, puede incluir detalles como el nombre o la dirección de correo electrónico para la obtención de detalles pero no para el análisis, lo que facilitar ponerse en contacto con los clientes de un clúster determinado.|  
  
###  <a name="Bkmk_strctcolumn"></a>Establecer el uso de columnas en el Asistente para crear estructuras de minería de datos  
 Al crear una nueva estructura de minería de datos, puede especificar qué columnas del origen de datos deben incluirse en la estructura de minería de datos y cómo deben usarse esas columnas. Recuerde que una estructura de minería de datos puede admitir varios modelos de minería de datos.  
  
|Valores|Descripción|  
|------------|-----------------|  
|**Include**|Especifica que la columna contiene datos quede pueden usarse para análisis o para predicción.|  
|**Clave**|Especifica que la columna contiene un identificador de transacción, un identificador de serie u otra clave necesaria para el procesamiento.<br /><br /> Todos los algoritmos requieren una columna de clave. No obstante, algunos algoritmos admiten una sola clave, mientras que otros admiten varias.<br /><br /> Si la columna contiene una clave pero no es necesaria para el procesamiento, seleccione no **usar**.|  
|**Key Time**|Especifica que la columna contiene una fecha u otro valor numérico que puede usarse para identificar de forma única los elementos de una serie temporal.|  
|**No usar**|Especifica que la columna debe omitirse. No se procesarán los datos de la columna.|  
  
 Para procesar correctamente un modelo, el algoritmo debe conocer la columna de clave que identifica cada fila de manera única, la columna de destino para crear predicciones si se va a crear un modelo de predicción y las columnas que deben usarse como columnas de entrada para crear las relaciones que predicen la columna de destino.  
  
-   Las columnas que se especifican como no **usar** no estarán presentes en la estructura de minería de datos.  
  
     Si agrega columnas que son innecesarias o que incluyen valores que no son válidos, esto puede afectar negativamente a los resultados del análisis. Por lo tanto, debe asegurarse de incluir solamente aquellas columnas que sean relevantes. Sin embargo, recuerde que las columnas que no use en la estructura de minería de datos no estarán disponibles para la realización de consultas.  
  
-   Las columnas que se especifican como tipo de **inclusión** se incluirán en la estructura de minería de datos y, posteriormente, se pueden usar para el análisis o la predicción en los modelos de minería de datos.  
  
     Si no está seguro de que vaya a necesitar usar la columna, siempre puede incluir la columna en la estructura de minería de datos y, después, crear un modelo de minería de datos que no use esa columna. Por ejemplo, podría incluir una columna de número de teléfono en sus datos para consultarla posteriormente, pero crear un modelo de clústeres que omita los números de teléfono. Una vez creados los clústeres, puede crear una consulta que devuelva los números de teléfono de las personas que pertenecen a un clúster determinado.  
  
-   Todos los algoritmos requieren una columna de **clave** . Los valores de la columna de clave deben ser únicos. Solo se requiere una columna **key Time** para los modelos de serie temporal o de previsión. .  
  
### <a name="requirements"></a>Requisitos  
 Para crear una estructura de minería de datos, debe tener una conexión con una instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. La conexión es necesaria incluso aunque se trabaje con estructuras temporales. Para obtener más información acerca de cómo crear o cambiar una conexión, vea [conectarse a los datos de origen &#40;cliente de minería de datos para Excel&#41;](connect-to-source-data-data-mining-client-for-excel.md).  
  
## <a name="see-also"></a>Consulte también  
 [Crear un modelo de minería de datos](creating-a-data-mining-model.md)  
  
  
