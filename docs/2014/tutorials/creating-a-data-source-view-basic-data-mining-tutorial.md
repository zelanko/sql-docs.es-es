---
title: Crear una vista del origen de datos (tutorial básico de minería de datos) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: c1e68a88-0f82-415d-becc-78d180d4f845
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: ac7730e8437eaed304ed69c40e45fc93ee9b5531
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "68888647"
---
# <a name="creating-a-data-source-view-basic-data-mining-tutorial"></a>Crear una vista del origen de datos (Tutorial básico de minería de datos)
  Una vista del origen de datos se genera en un origen de datos y define un subconjunto de los datos, que puede usar en las estructuras de minería de datos. También puede usar la vista del origen de datos para agregar columnas, crear columnas calculadas y agregados, y agregar vistas con nombre. Mediante el uso de vistas del origen de datos, puede seleccionar los datos relacionados con un proyecto, establecer relaciones entre tablas y modificar la estructura de los datos sin modificar el origen de datos original. Para más información, vea [Vistas del origen de datos en modelos multidimensionales](https://docs.microsoft.com/analysis-services/multidimensional-models/data-source-views-in-multidimensional-models).  
  
### <a name="to-create-a-data-source-view"></a>Para crear una vista del origen de datos  
  
1.  En **Explorador de soluciones**, haga clic con el botón secundario en **vistas del origen de datos**y seleccione **nueva vista del origen de datos**.  
  
2.  En la página inicial del **Asistente para orígenes de datos**, haga clic en **Siguiente**.  
  
3.  En la página **seleccionar un origen de datos** , en **orígenes de datos relacionales**, seleccione el origen de datos Adventure Works DW 2012 que creó en la última tarea. Haga clic en **Next**.  
  
    > [!NOTE]  
    >  Si desea crear un origen de datos, haga clic con el botón secundario en **orígenes de datos** y, a continuación, haga clic en **nuevo origen de datos** para iniciar el Asistente para orígenes de datos.  
  
4.  En la página **seleccionar tablas y vistas** , seleccione los objetos siguientes y, a continuación, haga clic en la flecha derecha para incluirlos en la nueva vista del origen de datos:  
  
    -   **ProspectiveBuyer (DBO)** : tabla de compradores de bicicletas posibles  
  
    -   **vTargetMail (DBO)** : vista de los datos históricos sobre los compradores de bicicletas anteriores  
  
5.  Haga clic en **Next**.  
  
6.  En la página **finalización del asistente** , de forma predeterminada, la vista del origen de datos se denomina Adventure Works DW 2012. Cambie el nombre a `Targeted Mailing`y, a continuación, haga clic en **Finalizar**.  
  
     La nueva vista del origen de datos se abre en la pestaña **Targeted mailing. DSV [Design]** .  
  
## <a name="previous-task-in-lesson"></a>Tarea anterior de la lección  
 [Crear un origen de datos &#40;tutorial básico de minería de datos&#41;](../../2014/tutorials/creating-a-data-source-basic-data-mining-tutorial.md)  
  
## <a name="next-lesson"></a>Lección siguiente  
 [Lección 2: crear una estructura de distribución de correo directo &#40;tutorial básico de minería de datos&#41;](../../2014/tutorials/lesson-2-building-a-targeted-mailing-structure-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Consulte también  
 [Definir una vista del origen de datos &#40;Analysis Services&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/defining-a-data-source-view-analysis-services)  
  
  
