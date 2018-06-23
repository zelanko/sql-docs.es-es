---
title: Muestreo de los datos (datos de SQL Server a los complementos de minería de datos) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- mining models, validating
- holdout
- testing cases
- training cases
- partitioning data [data mining]
- mining models, testing
ms.assetid: 35907ae6-887f-4cb3-a750-cff3d7683d90
caps.latest.revision: 26
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: e7ea284256c53be5c0ffc62cf0938c288b965f22
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36106212"
---
# <a name="sample-data-sql-server-data-mining-add-ins"></a>Datos de muestra (Complementos de minería de datos de SQL Server)
  ![Asistente para datos de partición en la cinta de opciones de minería de datos](media/dmc-partition.gif "Asistente para crear particiones de datos en la cinta de opciones de minería de datos")  
  
 El **datos de ejemplo** asistente facilita la dividir los datos de origen en dos conjuntos, uno para generar (aprendizaje) el modelo y otro para probar el modelo. Este asistente también dispone de una opción para volver a muestrear los datos con la que podrá generar un conjunto de datos nuevo que represente mejor el destino.  
  
 La creación del tipo de datos más apropiado para entrenar y probar los modelos es una parte importante de la minería de datos, pero también puede resultar una tarea tediosa si no se dispone de las herramientas adecuadas. El asistente realiza el muestreo estratificado para asegurarse de que los conjuntos de entrenamiento y de prueba están bien equilibrados.  
  
## <a name="random-sampling-and-oversampling"></a>Muestreo aleatorio y sobremuestreo  
 . El muestreo aleatorio es la mejor manera de asegurarse de que los datos usados para probar un modelo constituyen una buena representación de los datos usados para crear el modelo. Puede realizar un muestreo aleatorio de los datos que se encuentran almacenados en Excel o en un origen de datos externos.  
  
 Si utiliza la opción de muestreo aleatorio, el **datos de ejemplo** asistente automáticamente crea conjuntos de datos de entrenamiento y prueba y los sitúa en hojas de cálculo de Excel independientes para consultarlos más adelante.  
  
 Si los datos se almacenan en un libro de Excel y no un origen de datos externos, también tiene la opción usar *sobremuestreo*. Con esta opción, especifica un valor de destino que podría ser escaso en los datos y el asistente recopilará un conjunto equilibrado que incluya más aparte del valor de destino. Puede dirigir el asistente para que alcance un porcentaje concreto o cree un cierto número de filas.  
  
 Si utiliza la opción de sobremuestreo, el **datos de ejemplo** asistente crea una nueva hoja de cálculo que contiene los datos de muestra recién equilibrados.  
  
## <a name="using-the-sample-data-wizard"></a>Usar el Asistente para datos de muestra  
  
#### <a name="to-separate-data-into-training-and-testing-sets"></a>Para separa los datos en conjuntos de aprendizaje y de prueba  
  
1.  En el **minería de datos** la cinta de opciones, haga clic en **datos de ejemplo**.  
  
2.  En el **seleccionar datos de origen** página, especifique si la **datos** que desea particionar está en un rango de Excel o una tabla o en un origen de datos externo.  
  
3.  En el **Seleccionar tipo de muestreo** página, especifique si desea crear entrenamiento y conjuntos de datos de pruebas muestreo aleatorio o crear un nuevo conjunto de datos gracias al sobremuestreo.  
  
    > [!NOTE]  
    >  Si usa un origen de datos externos, solo estará disponible la opción de muestreo aleatorio. Si desea usar el sobremuestreo con datos externos, puede importar los datos a un libro de Excel mediante una conexión de datos de Excel y, a continuación, usar el Asistente para datos de muestra.  
  
4.  Establezca opciones que sean específicas del método de muestreo que ha seleccionado.  
  
    -   Para el muestreo aleatorio, especifique el porcentaje de los datos originales que desea usar para pruebas o el número total de filas que desea usar en el conjunto de datos de prueba.  
  
    -   Para el sobremuestreo, seleccione la columna y el valor en los que desea hacer hincapié. A continuación, especifique el número total de filas existentes en el nuevo conjunto de datos y el porcentaje de ellas que deben incluir el valor de destino.  
  
         El valor de destino para el sobremuestreo debe ser un valor discreto; no se pueden sobremuestrear datos numéricos continuos.  
  
5.  En el **página Finalizar**, acepte los nombres predeterminados para los nuevos conjuntos de datos, o escriba un nombre nuevo.  
  
     El asistente crea hojas de cálculo nuevas para cada conjunto de datos.  
  
 La mayoría de los asistentes del Cliente de minería de datos para Excel también disponen de una opción que permite separar los datos aleatoriamente en conjuntos de entrenamiento y de prueba. Sin embargo, si usa los asistentes, los datos permanecen en la misma hoja de cálculo (u otro origen de datos) y la información sobre si una determinada fila es un caso de prueba o un caso de entrenamiento se almacena internamente. En cambio, cuando se usa el **datos de ejemplo** asistente, las pruebas y los datos de entrenamiento se sitúan en hojas de cálculo para facilitar su consulta independientes.  
  
## <a name="related-options"></a>Opciones relacionadas  
 A medida que avanza a través del asistente, tendrá estas opciones:  
  
|Opciones|Comentarios|  
|-------------|--------------|  
|Seleccionar datos de origen (cuadro de diálogo del Cliente de minería de datos para Excel)|Seleccione un intervalo o una tabla de Excel que contenga los datos. Si desea utilizar datos externos, los datos pueden ser relacionales pero deben incluirse en un origen de datos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. T|  
|Seleccionar tipo de muestreo (página del Cliente de minería de datos para Excel)|Si usa un origen de datos externos, solo podrá usar la opción de muestreo aleatorio. Además, debe especificar el número de filas que se va a crear en el conjunto de datos final mediante la **recuento de filas** opción. No puede especificar ningún porcentaje de los datos de origen.|  
|Muestreo aleatorio (página del Cliente de minería de datos para Excel)|Puede copiar un porcentaje de filas del origen o un número de filas especificado.|  
|Sobremuestreo (página del Cliente de minería de datos para Excel)|**Estado de destino**<br /><br /> Seleccione en la lista un valor que está representado de forma insuficiente en el conjunto de datos original. El sobremuestreo aumentará la proporción de filas de datos que incluyen este estado.<br /><br /> **Tamaño de muestra**<br /><br /> Seleccione el número total de filas que se van a extraer. Este valor representa el tamaño del conjunto de datos final.|  
  
## <a name="other-sampling-options"></a>Otras opciones de muestreo  
 Si las opciones de muestreo de este asistente no satisfacen sus necesidades, puede usar la transformación de muestreo de SQL Server Integration Services (SSIS) para muestrear filas de varios orígenes de datos.  
  
 Para obtener más información, consulte [transformación muestreo de fila](../integration-services/data-flow/transformations/row-sampling-transformation.md) y [transformación muestreo de porcentaje](../integration-services/data-flow/transformations/percentage-sampling-transformation.md).  
  
## <a name="see-also"></a>Vea también  
 [Lista de comprobación de preparación para la minería de datos](checklist-of-preparation-for-data-mining.md)  
  
  