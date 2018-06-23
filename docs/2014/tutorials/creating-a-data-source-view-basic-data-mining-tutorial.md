---
title: Crear un tipo de datos del origen de vista (Tutorial de minería de datos básicos) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: c1e68a88-0f82-415d-becc-78d180d4f845
caps.latest.revision: 38
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 37c1548820bfe40478cdd5a8fd7b7ed051722056
ms.sourcegitcommit: 8c040e5b4e8c7d37ca295679410770a1af4d2e1f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/21/2018
ms.locfileid: "36311853"
---
# <a name="creating-a-data-source-view-basic-data-mining-tutorial"></a>Crear una vista del origen de datos (Tutorial básico de minería de datos)
  Una vista del origen de datos se genera en un origen de datos y define un subconjunto de los datos, que puede usar en las estructuras de minería de datos. También puede usar la vista del origen de datos para agregar columnas, crear columnas calculadas y agregados, y agregar vistas con nombre. Mediante el uso de vistas del origen de datos, puede seleccionar los datos relacionados con un proyecto, establecer relaciones entre tablas y modificar la estructura de los datos sin modificar el origen de datos original. Para más información, vea [Vistas del origen de datos en modelos multidimensionales](../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md).  
  
### <a name="to-create-a-data-source-view"></a>Para crear una vista del origen de datos  
  
1.  En **el Explorador de soluciones**, haga clic en **vistas del origen de datos**y seleccione **nueva vista del origen de datos**.  
  
2.  En la página **Asistente para vistas del origen de datos** , haga clic en **Siguiente**.  
  
3.  En el **seleccionar un origen de datos** página, en **orígenes de datos relacionales**, seleccione el origen de datos de Adventure Works DW 2012 que creó en la última tarea. Haga clic en **Siguiente**.  
  
    > [!NOTE]  
    >  Si desea crear un origen de datos, haga clic en **orígenes de datos** y, a continuación, haga clic en **nuevo origen de datos** para iniciar el Asistente para orígenes de datos.  
  
4.  En el **seleccionar tablas y vistas** , seleccione los siguientes objetos y, a continuación, haga clic en la flecha derecha para incluirlas en la nueva vista de origen de datos:  
  
    -   **ProspectiveBuyer (dbo)** -tabla de compradores de bicicleta  
  
    -   **vTargetMail (dbo)** -vista de datos históricos sobre los compradores de bicicletas anteriores  
  
5.  Haga clic en **Siguiente**.  
  
6.  En el **finalización del Asistente para** página, de forma predeterminada, la vista del origen de datos se denomina Adventure Works DW 2012. Cambie el nombre a `Targeted Mailing`y, a continuación, haga clic en **finalizar**.  
  
     La nueva vista de origen de datos se abre en el **Targeted Mailing.dsv [Design]** ficha.  
  
## <a name="previous-task-in-lesson"></a>Tarea anterior de la lección  
 [Crear un origen de datos &#40;Tutorial de minería de datos básicos&#41;](../../2014/tutorials/creating-a-data-source-basic-data-mining-tutorial.md)  
  
## <a name="next-lesson"></a>Lección siguiente  
 [Lección 2: Generar una estructura de distribución de correo directo &#40;Tutorial de minería de datos básicos&#41;](../../2014/tutorials/lesson-2-building-a-targeted-mailing-structure-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vea también  
 [Definir los datos de una vista del origen &#40;Analysis Services&#41;](../analysis-services/multidimensional-models/defining-a-data-source-view-analysis-services.md)  
  
  