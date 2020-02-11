---
title: Agregar una vista del origen de datos con tablas anidadas (tutorial intermedio de minería de datos) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: a14cd7f1-7a10-4ec6-af6a-f5f0676a0308
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 648b9d561ae340b67ed5e2d1aa878969e5a3bc47
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62822787"
---
# <a name="adding-a-data-source-view-with-nested-tables-intermediate-data-mining-tutorial"></a>Agregar una vista del origen de datos con tablas anidadas (Tutorial intermedio de minería de datos)
  Para crear un modelo de cesta de la compra, debe usar una vista del origen de datos que admita datos asociativos. Esta vista del origen de datos también se utilizará para el escenario de agrupación en clústeres de secuencia.  
  
 Esta vista del origen de datos es diferente de la de otros usuarios con los que haya trabajado porque contiene una *tabla anidada*. Una *tabla anidada* es una tabla que contiene varias filas de información sobre una sola fila de la tabla de casos. Por ejemplo, si el modelo analiza los hábitos de compra de los clientes, lo normal sería usar una tabla que tuviese una única fila para cada cliente como tabla de casos. Sin embargo, cada cliente puede hacer varias compras y es posible que se desee analizar el orden en que se realizan las compras o los productos que suelen comprarse juntos. Para representar estas compras de manera lógica en el modelo, agregará a la vista del origen de datos otra tabla que muestre las compras de cada cliente.  
  
 Esta tabla de compras anidada se relaciona con la tabla de clientes mediante una relación de varios a uno. La tabla anidada podría contener muchas filas para cada cliente, cada una con un único producto que se compró, quizás con información adicional sobre el orden en el que se realizaron las compras, el precio en el momento del pedido o cualquier promoción que se aplicara. Puede utilizar la información de la tabla anidada como entrada para el modelo o como el atributo de predicción.  
  
 En esta lección, realizará las tareas siguientes:  
  
-   Agregue una vista del origen de datos al [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)] origen de datos.  
  
-   Agregará las tablas anidadas y de casos a esta vista.  
  
-   Especificará la relación de varios a uno entre la tabla de casos y la tabla anidada.  
  
    > [!NOTE]  
    >  . Es importante que siga el procedimiento descrito de forma exacta, para especificar correctamente la relación entre la tabla de casos y la tabla anidada, y evitar errores al procesar el modelo.  
  
-   Definirá cómo se utilizan las columnas de datos en el modelo.  
  
 Para obtener más información sobre cómo trabajar con tablas de casos y anidadas, y cómo elegir una clave de tabla anidada, vea [tablas anidadas &#40;Analysis Services-Data Mining&#41;](../../2014/analysis-services/data-mining/nested-tables-analysis-services-data-mining.md).  
  
### <a name="to-add-a-data-source-view"></a>Para agregar una vista del origen de datos  
  
1.  En Explorador de soluciones, haga clic con el botón secundario en **vistas del origen de datos**y seleccione **nueva vista del origen de datos**.  
  
     Se abrirá el Asistente para vistas del origen de datos.  
  
2.  En la página inicial del **Asistente para orígenes de datos**, haga clic en **Siguiente**.  
  
3.  En la página **seleccionar un origen de datos** , en **orígenes de datos relacionales**, seleccione el [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)] origen de datos que ha creado en el tutorial básico de minería de datos. Haga clic en **Next**.  
  
4.  En la página **seleccionar tablas y vistas** , seleccione las tablas siguientes y, a continuación, haga clic en la flecha derecha para incluirlas en la nueva vista del origen de datos:  
  
    -   `vAssocSeqOrders`  
  
    -   `vAssocSeqLineItems`  
  
5.  Haga clic en **Next**.  
  
6.  En la página **finalización del asistente** , la vista del origen de datos se [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)]denomina de forma predeterminada. Cambie el nombre a `Orders`y, a continuación, haga clic en **Finalizar**.  
  
     Se abre el diseñador de vistas del `Orders` origen de datos y aparece la vista del origen de datos.  
  
### <a name="to-create-a-relationship-between-tables"></a>Crear una relación entre tablas  
  
1.  En el Diseñador de vistas del origen de datos, coloque las dos tablas de modo que estén alineadas horizontalmente, con la tabla vAssocSeqLineItems en el lado izquierdo y la tabla vAssocSeqOrders en el lado derecho.  
  
2.  Seleccione la columna **OrderNumber** en la tabla vAssocSeqLineItems.  
  
3.  Arrastre la columna hasta la tabla vAssocSeqOrders y colóquela en la columna **OrderNumber** .  
  
    > [!IMPORTANT]  
    >  Asegúrese de arrastrar la columna **OrderNumber** de la tabla anidada vAssocSeqLineItems, que representa el lado "varios" de la combinación, a la tabla de casos vAssocSeqOrders, que representa el lado uno de la combinación.  
  
     Ahora existe una nueva *relación de varios a uno* entre las tablas VAssocSeqLineItems y vAssocSeqOrders. Si ha combinado correctamente las tablas, la vista del origen de datos debería aparecer como sigue:  
  
     ![combinación esperada de varios a uno en tabla de casos y anidada](../../2014/tutorials/media/dsv-nestedjoin-illustration.gif "combinación esperada de varios a uno en tabla de casos y anidada")  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Crear una estructura de cesta de la compra y un modelo &#40;tutorial intermedio de minería de datos&#41;](../../2014/tutorials/creating-a-market-basket-structure-and-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Consulte también  
 [Tutorial intermedio de minería de datos &#40;Analysis Services:&#41;de minería de datos](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md)   
 [Estructuras de minería de datos &#40;Analysis Services:&#41;de minería de datos](../../2014/analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)   
 [Modelos de minería de datos &#40;Analysis Services&#41;de minería de datos](../../2014/analysis-services/data-mining/mining-models-analysis-services-data-mining.md)  
  
  
