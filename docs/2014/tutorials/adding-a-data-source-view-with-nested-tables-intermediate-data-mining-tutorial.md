---
title: Agregar datos de un origen de vista con tablas anidadas (Tutorial de minería de datos intermedio) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a14cd7f1-7a10-4ec6-af6a-f5f0676a0308
caps.latest.revision: 44
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 4ce47827cefcd626e8bda03de7f76800a16abf8c
ms.sourcegitcommit: 8c040e5b4e8c7d37ca295679410770a1af4d2e1f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/21/2018
ms.locfileid: "36313183"
---
# <a name="adding-a-data-source-view-with-nested-tables-intermediate-data-mining-tutorial"></a>Agregar una vista del origen de datos con tablas anidadas (Tutorial intermedio de minería de datos)
  Para crear un modelo de cesta de la compra, debe usar una vista del origen de datos que admita datos asociativos. Esta vista del origen de datos también se utilizará para el escenario de agrupación en clústeres de secuencia.  
  
 Esta vista del origen de datos es diferente de otras personas que puede trabajar con porque contiene un *tabla anidada*. A *tabla anidada* es una tabla que contenga varias filas de información sobre una única fila en la tabla de casos. Por ejemplo, si el modelo analiza los hábitos de compra de los clientes, lo normal sería usar una tabla que tuviese una única fila para cada cliente como tabla de casos. Sin embargo, cada cliente puede hacer varias compras y es posible que se desee analizar el orden en que se realizan las compras o los productos que suelen comprarse juntos. Para representar estas compras de manera lógica en el modelo, agregará a la vista del origen de datos otra tabla que muestre las compras de cada cliente.  
  
 Esta tabla de compras anidada se relaciona con la tabla de clientes mediante una relación de varios a uno. La tabla anidada podría contener muchas filas para cada cliente, cada una con un único producto que se compró, quizás con información adicional sobre el orden en el que se realizaron las compras, el precio en el momento del pedido o cualquier promoción que se aplicara. Puede utilizar la información de la tabla anidada como entrada para el modelo o como el atributo de predicción.  
  
 En esta lección, realice las siguientes tareas:  
  
-   Agregar una vista del origen de datos para el [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)] origen de datos.  
  
-   Agregará las tablas anidadas y de casos a esta vista.  
  
-   Especificará la relación de varios a uno entre la tabla de casos y la tabla anidada.  
  
    > [!NOTE]  
    >  . Es importante que siga el procedimiento descrito de forma exacta, para especificar correctamente la relación entre la tabla de casos y la tabla anidada, y evitar errores al procesar el modelo.  
  
-   Definirá cómo se utilizan las columnas de datos en el modelo.  
  
 Para obtener más información acerca de cómo trabajar con casos y tablas anidadas y cómo elegir una clave de tabla anidada, vea [tablas anidadas &#40;Analysis Services: minería de datos&#41;](../../2014/analysis-services/data-mining/nested-tables-analysis-services-data-mining.md).  
  
### <a name="to-add-a-data-source-view"></a>Para agregar una vista del origen de datos  
  
1.  En el Explorador de soluciones, haga clic en **vistas del origen de datos**y, a continuación, seleccione **nueva vista del origen de datos**.  
  
     Se abrirá el Asistente para vistas del origen de datos.  
  
2.  En la página **Asistente para vistas del origen de datos** , haga clic en **Siguiente**.  
  
3.  En el **seleccionar un origen de datos** página, en **orígenes de datos relacionales**, seleccione el [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)] origen de datos que creó en el Tutorial básico de minería de datos. Haga clic en **Siguiente**.  
  
4.  En el **seleccionar tablas y vistas** , seleccione las tablas siguientes y, a continuación, haga clic en la flecha derecha para incluirlas en la nueva vista de origen de datos:  
  
    -   `vAssocSeqOrders`  
  
    -   `vAssocSeqLineItems`  
  
5.  Haga clic en **Siguiente**.  
  
6.  En el **finalización del Asistente para** página, de forma predeterminada la vista del origen de datos se denomina [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)]. Cambie el nombre a `Orders`y, a continuación, haga clic en **finalizar**.  
  
     Abre el Diseñador de vistas del origen de datos y la `Orders` aparece la vista del origen de datos.  
  
### <a name="to-create-a-relationship-between-tables"></a>Crear una relación entre tablas  
  
1.  En el Diseñador de vistas del origen de datos, coloque las dos tablas de modo que estén alineadas horizontalmente, con la tabla vAssocSeqLineItems en el lado izquierdo y la tabla vAssocSeqOrders en el lado derecho.  
  
2.  Seleccione el **OrderNumber** columna en la tabla vAssocSeqLineItems.  
  
3.  Arrastre la columna a la tabla vAssocSeqOrders y colóquela la **OrderNumber** columna.  
  
    > [!IMPORTANT]  
    >  Asegúrese de arrastrar el **OrderNumber** columna de la tabla anidada vAssocSeqLineItems, que representa el lado "varios" de la combinación, en la tabla de casos de vAssocSeqOrders, que representa el uno lado de la combinación.  
  
     Un nuevo *relación de varios a uno* ahora existe entre las tablas vAssocSeqLineItems y vAssocSeqOrders. Si ha combinado correctamente las tablas, la vista del origen de datos debería aparecer como sigue:  
  
     ![combinación de varios a uno esperado en la tabla de casos y anidada](../../2014/tutorials/media/dsv-nestedjoin-illustration.gif "esperado combinación de varios a uno en la tabla de casos y anidada")  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Crear un modelo y estructura Market Basket &#40;intermedio de Tutorial de minería de datos&#41;](../../2014/tutorials/creating-a-market-basket-structure-and-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vea también  
 [Intermedio de Tutorial de minería de datos &#40;Analysis Services: minería de datos&#41;](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md)   
 [Estructuras de minería de datos &#40;Analysis Services: minería de datos&#41;](../../2014/analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)   
 [Modelos de minería de datos &#40;Analysis Services: minería de datos&#41;](../../2014/analysis-services/data-mining/mining-models-analysis-services-data-mining.md)  
  
  