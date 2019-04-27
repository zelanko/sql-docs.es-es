---
title: Crear una nueva estructura de minería de datos relacional | Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e111345276fdf2895b7eb4d056b046efe20b32e9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62740525"
---
# <a name="create-a-new-relational-mining-structure"></a>Crear una estructura de minería de datos relacional
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Use el Asistente para minería de datos para crear una nueva estructura de minería de datos, utilizando los datos de la base de datos relacional o de otro origen, y guarde la estructura y un modelo relacionado en una base de datos de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
## <a name="to-create-a-relational-mining-structure"></a>Para crear una estructura de minería de datos relacional  
  
1.  En el Explorador de soluciones, haga clic con el botón derecho en la carpeta **Estructuras de minería de datos** en un proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] y, después, haga clic en **Nueva estructura de minería de datos**.  
  
     Se abrirá el Asistente para minería de datos.  
  
2.  En la página de inicio del **Asistente para minería de datos** , haga clic en **Siguiente**.  
  
3.  En la página **Seleccionar el método de definición** , seleccione **A partir de una base de datos relacional o un almacenamiento de datos**y, a continuación, haga clic en **Siguiente**.  
  
4.  En la página **Seleccionar la técnica de minería de datos** , seleccione el algoritmo de minería de datos que desee utilizar y, a continuación, haga clic en **Siguiente**.  
  
     Para más información sobre los algoritmos de minería de datos, vea [Algoritmos de minería de datos &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md).  
  
5.  En la página **Seleccionar vista del origen de datos** , en **Vistas del origen de datos disponibles**, haga clic en la vista del origen de datos que desee utilizar y, a continuación, haga clic en **Siguiente**.  
  
     Para más información sobre cómo crear una vista del origen de datos, vea [Vistas del origen de datos en modelos multidimensionales](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md).  
  
6.  En la página **Especificar tipos de tablas** , en **Tablas de entrada**, seleccione una tabla de casos y una tabla anidada.  
  
7.  En la página **Especificar los datos de entrenamiento** , en **Estructura del modelo de minería de datos**, seleccione las columnas clave, de entrada y de predicción.  
  
     Después de seleccionar la columna de predicción, puede hacer clic en el botón **Sugerir** para abrir el cuadro de diálogo **Sugerir columnas relacionadas** . Para aceptar las columnas sugeridas, haga clic en **Aceptar** en este cuadro de diálogo para incluir las columnas seleccionadas en la estructura de minería de datos, o cambie primero las selecciones de la columna **Entrada** y, a continuación, haga clic en **Aceptar**. Para hacer caso omiso de las sugerencias, haga clic en **Cancelar**.  
  
8.  Haga clic en **Siguiente**.  
  
9. En la página **Especificar el contenido y el tipo de datos de las columnas** , en **Estructura del modelo de minería de datos**, puede ajustar el tipo de contenido y el tipo de datos de cada columna.  
  
    > [!NOTE]  
    >  Puede hacer clic en **Detectar** para detectar automáticamente si una columna contiene datos continuos o discretos. Después de hacer clic en este botón, el contenido de la columna y los tipos de datos se actualizarán en las columnas **Tipo de contenido** y **Tipo de datos** . Para más información sobre tipos de contenido y tipos de datos, vea [Tipos de contenido &#40;minería de datos&#41;](../../analysis-services/data-mining/content-types-data-mining.md) y [Tipos de datos &#40;minería de datos&#41;](../../analysis-services/data-mining/data-types-data-mining.md).  
  
10. Haga clic en **Siguiente**.  
  
11. En la página **Finalización del asistente** , asigne un nombre a la estructura de minería de datos y al modelo de minería de datos inicial relacionado que se creará y, a continuación, haga clic en **Finalizar**.  
  
## <a name="see-also"></a>Vea también  
 [Tareas y procedimientos de las estructuras de minería de datos](../../analysis-services/data-mining/mining-structure-tasks-and-how-tos.md)  
  
  
