---
title: Creación de un modelo (Tutorial de minería de datos intermedio) y la estructura Market Basket | Microsoft Docs
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
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63190833"
---
# <a name="creating-a-market-basket-structure-and-model-intermediate-data-mining-tutorial"></a>Crear una estructura y un modelo de cesta de la compra (Tutorial intermedio de minería de datos)
  Ahora que ha creado una vista del origen de datos, utilizará el Asistente para minería de datos con el fin de crear una nueva estructura de minería de datos. En esta tarea, creará una estructura y un modelo de minería de datos que se basen en el algoritmo de asociación de [!INCLUDE[msCoName](../includes/msconame-md.md)].  
  
> [!NOTE]  
>  Si encuentra un error que indica que vAssocSeqLineItems no se puede usar como una tabla anidada, vuelva a la tarea anterior de la lección y asegúrese de crear la combinación de varios a uno arrastrando desde la tabla vAssocSeqLineItems (el lado de varios) a la tabla vAssocSeqOrders (el lado de uno). También puede modificar la relación entre las tablas haciendo clic con el botón secundario en la línea de combinación.  
  
### <a name="to-create-an-association-mining-structure"></a>Para crear una estructura de minería de datos de asociación  
  
1.  En el Explorador de soluciones en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], haga clic en **estructuras de minería de datos** y seleccione **nueva estructura de minería de datos** para abrir el Asistente para minería de datos.  
  
2.  En la página de inicio del **Asistente para minería de datos** , haga clic en **Siguiente**.  
  
3.  En el **seleccionar el método de definición** , comprueba que **desde el almacén de datos o base de datos relacional existente** está seleccionada y, a continuación, haga clic en **siguiente**.  
  
4.  En el **crear la estructura de minería de datos** página, en **qué técnica de minería de datos desea utilizar?**, seleccione **reglas de asociación de Microsoft** en la lista y, a continuación, haga clic en **Siguiente**. El **seleccionar vista del origen de datos** aparece la página.  
  
5.  Seleccione **pedidos**en **vistas del origen de datos disponibles**y, a continuación, haga clic en **siguiente**.  
  
6.  En el **especificar tipos de tablas** página, en la fila de la tabla vAssocSeqLineItems, active la **Nested** casilla de verificación y, en la fila de la tabla anidada vAssocSeqOrders, seleccione el **caso** casilla de verificación. Haga clic en **Siguiente**.  
  
7.  En el **especificar los datos de entrenamiento** página, desactive las casillas que estén activadas. Establezca la clave para la tabla de casos, vAssocSeqOrders, activando el **clave** casilla de verificación al lado de OrderNumber.  
  
     Dado que es el propósito del análisis de cesta determinar qué productos se incluyen en una sola transacción, no es necesario usar el **CustomerKey** campo.  
  
8.  Establezca la clave de la tabla anidada, vAssocSeqLineItems, activando el **clave** casilla de verificación junto al modelo. El **entrada** casilla de verificación se selecciona automáticamente al hacer esto. Seleccione el **Predictable** casilla de verificación para `Model` también.  
  
     En un modelo de cesta, no te importa acerca de la secuencia de productos de la cesta de compra y, por lo tanto, no debe incluir **LineNumber** como clave para la tabla anidada. Usaría **LineNumber** como clave solo en un modelo donde la secuencia es importante. Creará un modelo que use el algoritmo de clústeres de secuencia de [!INCLUDE[msCoName](../includes/msconame-md.md)] en la lección 4.  
  
9. Active la casilla situada a la izquierda de IncomeGroup y Region, pero no realice ninguna otra selección. Al activar la columna situada más a la izquierda se agregan las columnas a la estructura como referencia posterior, pero las columnas no se usarán en el modelo. Las selecciones tendrán la apariencia siguiente:  
  
     ![cómo debe ser el cuadro de diálogo](../../2014/tutorials/media/tutorial-configassocmodel.gif "cómo debe ser el cuadro de diálogo")  
  
10. Haga clic en **Siguiente**.  
  
11. En el **contenido y el tipo de datos de columnas especificar**página, revise las selecciones, que deben ser como se muestra en la tabla siguiente y, a continuación, haga clic en **siguiente**.  
  
    |Columnas|Tipo de contenido|Tipo de datos|  
    |-------------|------------------|---------------|  
    |IncomeGroup|Discrete|Text|  
    |Número de pedido|Key|Text|  
    |Region|Discrete|Text|  
    |vAssocSeqLineItems|||  
    |Modelo|Key|Text|  
  
12. En el **crear pruebas establezca** página, el valor predeterminado para la opción **porcentaje de datos de prueba** es 30 por ciento. Cámbielo a **0**. Haga clic en **Siguiente**.  
  
    > [!NOTE]  
    >  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] proporciona varios gráficos para medir la precisión del modelo. Sin embargo, algunos tipos de gráficos de precisión, como el gráfico de elevación y el informe de validación cruzada, están diseñados para la clasificación y la estimación. No se pueden usar en la predicción asociativa.  
  
13. En el **completando el Asistente para** página **nombre de la estructura de minería de datos**, tipo `Association`.  
  
14. En **nombre del modelo de minería de datos**, tipo `Association`.  
  
15. Seleccione la opción **permitir obtención de detalles**y, a continuación, haga clic en **finalizar**.  
  
     Se abre el Diseñador de minería de datos para mostrar el `Association` estructura de minería de datos que acaba de crear.  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Modificar y procesar el modelo de cesta &#40;intermedio de Tutorial de minería de datos&#41;](../../2014/tutorials/modify-process-market-basket-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vea también  
 [Algoritmo de asociación de Microsoft](../../2014/analysis-services/data-mining/microsoft-association-algorithm.md)   
 [Tipos de contenido &#40;minería de datos&#41;](../../2014/analysis-services/data-mining/content-types-data-mining.md)  
  
  
