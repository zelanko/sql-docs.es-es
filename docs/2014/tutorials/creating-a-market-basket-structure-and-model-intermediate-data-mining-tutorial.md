---
title: Crear una estructura y un modelo de cesta de la compra (tutorial intermedio de minería de datos) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 659b7a4e-f687-44d9-a60a-86490ccbf90f
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 207d82f740b7b5ff174e220e647d67d5bac7f9ea
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "63190833"
---
# <a name="creating-a-market-basket-structure-and-model-intermediate-data-mining-tutorial"></a>Crear una estructura y un modelo de cesta de la compra (Tutorial intermedio de minería de datos)
  Ahora que ha creado una vista del origen de datos, utilizará el Asistente para minería de datos con el fin de crear una nueva estructura de minería de datos. En esta tarea, creará una estructura y un modelo de minería de datos que se basen en el algoritmo de asociación de [!INCLUDE[msCoName](../includes/msconame-md.md)].  
  
> [!NOTE]  
>  Si encuentra un error que indica que vAssocSeqLineItems no se puede usar como una tabla anidada, vuelva a la tarea anterior de la lección y asegúrese de crear la combinación de varios a uno arrastrando desde la tabla vAssocSeqLineItems (el lado de varios) a la tabla vAssocSeqOrders (el lado de uno). También puede modificar la relación entre las tablas haciendo clic con el botón secundario en la línea de combinación.  
  
### <a name="to-create-an-association-mining-structure"></a>Para crear una estructura de minería de datos de asociación  
  
1.  En Explorador de soluciones en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], haga clic con el botón secundario en **estructuras de minería** de datos y seleccione **nueva estructura de minería** de datos para abrir el Asistente para minería de datos.  
  
2.  En la página de inicio del **Asistente para minería de datos** , haga clic en **Siguiente**.  
  
3.  En la página **seleccionar el método de definición** , compruebe que la opción **de base de datos relacional o del almacenamiento de datos existente** está seleccionada y, a continuación, haga clic en **siguiente**.  
  
4.  En la página **crear la estructura de minería de datos** , en **¿qué técnica de minería de datos desea utilizar?**, seleccione **reglas de Asociación de Microsoft** en la lista y, a continuación, haga clic en **siguiente**. Aparece la página **seleccionar vista del origen de datos** .  
  
5.  Seleccione **pedidos**en **vistas del origen de datos disponibles**y, a continuación, haga clic en **siguiente**.  
  
6.  En la página **especificar tipos de tablas** , en la fila de la tabla vAssocSeqLineItems, active la casilla **anidada** y, en la fila de la tabla anidada vAssocSeqOrders, active la casilla **caso** . Haga clic en **Siguiente**.  
  
7.  En la página **especificar los datos de entrenamiento** , desactive los cuadros que puedan estar comprobados. Establezca la clave para la tabla de casos, vAssocSeqOrders, activando la casilla **clave** junto a OrderNumber.  
  
     Dado que el propósito del análisis de la cesta de la compra es determinar qué productos se incluyen en una sola transacción, no es necesario usar el campo **CustomerKey** .  
  
8.  Establezca la clave para la tabla anidada, vAssocSeqLineItems, activando la casilla **clave** junto a modelo. La casilla **entrada** también se selecciona automáticamente al hacer esto. Active también la casilla de `Model` **predicción** .  
  
     En un modelo de cesta de la compra, no le interesa la secuencia de productos de la cesta de la compra y, por lo tanto, no debe incluir **lineNumber** como clave para la tabla anidada. Usaría **lineNumber** como clave solo en un modelo en el que la secuencia sea importante. Creará un modelo que use el algoritmo de clústeres de secuencia de [!INCLUDE[msCoName](../includes/msconame-md.md)] en la lección 4.  
  
9. Active la casilla situada a la izquierda de IncomeGroup y Region, pero no realice ninguna otra selección. Al activar la columna situada más a la izquierda se agregan las columnas a la estructura como referencia posterior, pero las columnas no se usarán en el modelo. Las selecciones tendrán la apariencia siguiente:  
  
     ![cuál debería ser la apariencia del cuadro de diálogo](../../2014/tutorials/media/tutorial-configassocmodel.gif "cuál debería ser la apariencia del cuadro de diálogo")  
  
10. Haga clic en **Siguiente**.  
  
11. En la página **especificar el contenido y el tipo de datos de las columnas**, revise las selecciones, que deben ser como se muestra en la tabla siguiente y, a continuación, haga clic en **siguiente**.  
  
    |Columnas|Tipo de contenido|Tipo de datos|  
    |-------------|------------------|---------------|  
    |IncomeGroup|Discrete|Text|  
    |Order Number|Key|Text|  
    |Region|Discrete|Text|  
    |vAssocSeqLineItems|||  
    |Modelo|Key|Text|  
  
12. En la página **crear conjunto de pruebas** , el valor predeterminado de la opción **porcentaje de datos para pruebas** es el 30 por ciento. Cámbielo a **0**. Haga clic en **Siguiente**.  
  
    > [!NOTE]  
    >  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] proporciona varios gráficos para medir la precisión del modelo. Sin embargo, algunos tipos de gráficos de precisión, como el gráfico de elevación y el informe de validación cruzada, están diseñados para la clasificación y la estimación. No se pueden usar en la predicción asociativa.  
  
13. En la página **finalización del asistente** , en nombre de la estructura `Association`de minería de **datos**, escriba.  
  
14. En **nombre del modelo**de minería `Association`de datos, escriba.  
  
15. Seleccione la opción **permitir obtención de detalles**y, a continuación, haga clic en **Finalizar**.  
  
     El diseñador de minería de datos se `Association` abre para mostrar la estructura de minería de datos que acaba de crear.  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Modificar y procesar el modelo de cesta de la compra &#40;tutorial intermedio de minería de datos&#41;](../../2014/tutorials/modify-process-market-basket-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Consulte también  
 [Algoritmo de Asociación de Microsoft](../../2014/analysis-services/data-mining/microsoft-association-algorithm.md)   
 [Tipos de contenido &#40;minería de datos&#41;](../../2014/analysis-services/data-mining/content-types-data-mining.md)  
  
  
