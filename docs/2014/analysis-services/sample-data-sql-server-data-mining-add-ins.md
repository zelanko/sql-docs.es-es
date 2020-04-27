---
title: Datos de ejemplo (complementos de minería de datos de SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining models, validating
- holdout
- testing cases
- training cases
- partitioning data [data mining]
- mining models, testing
ms.assetid: 35907ae6-887f-4cb3-a750-cff3d7683d90
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9a69b2286abbc1ba4289fd482b1bbf5a2dfb3e7b
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66070034"
---
# <a name="sample-data-sql-server-data-mining-add-ins"></a>Datos de muestra (Complementos de minería de datos de SQL Server)
  ![Asistente para partición de datos, cinta de opciones Minería de datos](media/dmc-partition.gif "Asistente para partición de datos, cinta de opciones Minería de datos")  
  
 El Asistente para **datos de muestra** facilita la división de los datos de origen en dos conjuntos: uno para compilar (entrenar) el modelo y otro para probar el modelo. Este asistente también dispone de una opción para volver a muestrear los datos con la que podrá generar un conjunto de datos nuevo que represente mejor el destino.  
  
 La creación del tipo de datos más apropiado para entrenar y probar los modelos es una parte importante de la minería de datos, pero también puede resultar una tarea tediosa si no se dispone de las herramientas adecuadas. El asistente realiza el muestreo estratificado para asegurarse de que los conjuntos de entrenamiento y de prueba están bien equilibrados.  
  
## <a name="random-sampling-and-oversampling"></a>Muestreo aleatorio y sobremuestreo  
 . El muestreo aleatorio es la mejor manera de asegurarse de que los datos usados para probar un modelo constituyen una buena representación de los datos usados para crear el modelo. Puede realizar un muestreo aleatorio de los datos que se encuentran almacenados en Excel o en un origen de datos externos.  
  
 Si usa la opción de muestreo aleatorio, el Asistente para **datos de muestra** crea automáticamente conjuntos de datos de entrenamiento y de prueba, y los envía en hojas de cálculo de Excel independientes para su posterior referencia.  
  
 Si los datos están almacenados en un libro de Excel y no en un origen de datos externo, también tiene la opción de usar el *sobremuestreo*. Con esta opción, especifica un valor de destino que podría ser escaso en los datos y el asistente recopilará un conjunto equilibrado que incluya más aparte del valor de destino. Puede dirigir el asistente para que alcance un porcentaje concreto o cree un cierto número de filas.  
  
 Si usa la opción de sobremuestreo, el Asistente para **datos de muestra** crea una nueva hoja de cálculo que contiene los datos de ejemplo recién equilibrados.  
  
## <a name="using-the-sample-data-wizard"></a>Usar el Asistente para datos de muestra  
  
#### <a name="to-separate-data-into-training-and-testing-sets"></a>Para separa los datos en conjuntos de aprendizaje y de prueba  
  
1.  En la cinta de opciones **minería de datos** , haga clic en **datos de ejemplo**.  
  
2.  En la página **seleccionar datos de origen** , especifique si los **datos** que desea particionar están en un intervalo o una tabla de Excel o en un origen de datos externo.  
  
3.  En la página **Seleccionar tipo de muestreo** , especifique si desea crear conjuntos de datos de entrenamiento y de prueba mediante muestreo aleatorio, o crear un nuevo conjunto de datos mediante el sobremuestreo.  
  
    > [!NOTE]  
    >  Si usa un origen de datos externos, solo estará disponible la opción de muestreo aleatorio. Si desea usar el sobremuestreo con datos externos, puede importar los datos a un libro de Excel mediante una conexión de datos de Excel y, a continuación, usar el Asistente para datos de muestra.  
  
4.  Establezca opciones que sean específicas del método de muestreo que ha seleccionado.  
  
    -   Para el muestreo aleatorio, especifique el porcentaje de los datos originales que desea usar para pruebas o el número total de filas que desea usar en el conjunto de datos de prueba.  
  
    -   Para el sobremuestreo, seleccione la columna y el valor en los que desea hacer hincapié. A continuación, especifique el número total de filas existentes en el nuevo conjunto de datos y el porcentaje de ellas que deben incluir el valor de destino.  
  
         El valor de destino para el sobremuestreo debe ser un valor discreto; no se pueden sobremuestrear datos numéricos continuos.  
  
5.  En la **Página finalizar**, acepte los nombres predeterminados de los nuevos conjuntos de datos o escriba un nombre nuevo.  
  
     El asistente crea hojas de cálculo nuevas para cada conjunto de datos.  
  
 La mayoría de los asistentes del Cliente de minería de datos para Excel también disponen de una opción que permite separar los datos aleatoriamente en conjuntos de entrenamiento y de prueba. Sin embargo, si usa los asistentes, los datos permanecen en la misma hoja de cálculo (u otro origen de datos) y la información sobre si una determinada fila es un caso de prueba o un caso de entrenamiento se almacena internamente. Por el contrario, cuando se usa el Asistente para **datos de muestra** , los datos de entrenamiento y de prueba se muestran en hojas de cálculo independientes para facilitar su consulta.  
  
## <a name="related-options"></a>Opciones relacionadas  
 A medida que avanza a través del asistente, tendrá estas opciones:  
  
|Opciones|Comentarios|  
|-------------|--------------|  
|Seleccionar datos de origen (cuadro de diálogo del Cliente de minería de datos para Excel)|Seleccione un intervalo o una tabla de Excel que contenga los datos. Si desea utilizar datos externos, los datos pueden ser relacionales pero deben incluirse en un origen de datos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. T|  
|Seleccionar tipo de muestreo (página del Cliente de minería de datos para Excel)|Si usa un origen de datos externos, solo podrá usar la opción de muestreo aleatorio. Además, debe especificar el número de filas que se crearán en el conjunto de datos final mediante la opción **recuento de filas** . No puede especificar ningún porcentaje de los datos de origen.|  
|Muestreo aleatorio (página del Cliente de minería de datos para Excel)|Puede copiar un porcentaje de filas del origen o un número de filas especificado.|  
|Sobremuestreo (página del Cliente de minería de datos para Excel)|**Estado de destino**<br /><br /> Seleccione en la lista un valor que está representado de forma insuficiente en el conjunto de datos original. El sobremuestreo aumentará la proporción de filas de datos que incluyen este estado.<br /><br /> **Tamaño de muestra**<br /><br /> Seleccione el número total de filas que se van a extraer. Este valor representa el tamaño del conjunto de datos final.|  
  
## <a name="other-sampling-options"></a>Otras opciones de muestreo  
 Si las opciones de muestreo de este asistente no satisfacen sus necesidades, puede usar la transformación de muestreo de SQL Server Integration Services (SSIS) para muestrear filas de varios orígenes de datos.  
  
 Para obtener más información, vea [transformación muestreo de fila](../integration-services/data-flow/transformations/row-sampling-transformation.md) y [transformación muestreo de porcentaje](../integration-services/data-flow/transformations/percentage-sampling-transformation.md).  
  
## <a name="see-also"></a>Consulte también  
 [Lista de comprobación de la preparación para la minería de datos](checklist-of-preparation-for-data-mining.md)  
  
  
