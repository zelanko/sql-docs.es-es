---
title: "Definir una dimensión | Documentos de Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 112696db-3838-4b50-91bd-d2ce5fa04ee5
caps.latest.revision: 18
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b6969c73bc6f466eb1a2acfd9d41ff21e80d727c
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="lesson-2-1---defining-a-dimension"></a>Lección 2-1: definir una dimensión
En la tarea siguiente, usará el Asistente para dimensiones con objeto de generar una dimensión Date.  
  
> [!NOTE]  
> Para realizar esta lección es necesario haber completado todos los procedimientos de la lección 1.  
  
### <a name="to-define-a-dimension"></a>Para definir una dimensión  
  
1.  En el Explorador de soluciones (en el margen derecho de Microsoft Visual Studio), haga clic con el botón derecho en **Dimensiones**y haga clic en **Nueva dimensión**. Aparece el Asistente para dimensiones.  
  
2.  En la página **Asistente para dimensiones** , haga clic en **Siguiente**.  
  
3.  En la página **Seleccionar método de creación** , compruebe que la opción **Usar una tabla existente** está seleccionada y, a continuación, haga clic en **Siguiente**.  
  
4.  En la página **Especificar información de origen** , compruebe que la vista del origen de datos **Adventure Works DW 2012** está seleccionada.  
  
5.  En la lista **Tabla principal** , seleccione **Fecha**.  
  
6.  Haga clic en **Siguiente**.  
  
7.  En la página **Seleccionar los atributos de la dimensión** , active las casillas situadas junto a los siguientes atributos:  
  
    -   **Date Key**  
  
    -   **Full Date Alternate Key**  
  
    -   **Spanish Month Name**  
  
    -   **Trimestre del calendario**  
  
    -   **Año del calendario**  
  
    -   **Semestre del calendario**  
  
8.  Cambie el valor de la columna **Tipo de atributo** del atributo **Full Date Alternate Key** de **Normal** a **Fecha**. Para ello, haga clic en **Normal** en la columna **Tipo de atributo** . A continuación, haga clic en la flecha para expandir las opciones. Después, haga clic en **Fecha** > **Calendario** > **Fecha**. Haga clic en **Aceptar**. Repita estos pasos para cambiar el tipo de atributo de los siguientes atributos como se indica a continuación:  
  
    -   **English Month Name** a **Month**  
  
    -   **Calendar Quarter** a **Quarter**  
  
    -   **Calendar Year** a **Year**  
  
    -   **Calendar Semester** a **Half Year**  
  
9. Haga clic en **Siguiente**.  
  
10. En la página **Finalización del asistente** , en el panel de vista previa, puede ver la dimensión **Fecha** y sus atributos.  
  
11. Haga clic en **Finalizar** para completar el asistente.  
  
    En el Explorador de soluciones, en el proyecto Tutorial de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , la dimensión Fecha aparece en la carpeta **Dimensiones** . En el centro del entorno de desarrollo, el Diseñador de dimensiones muestra la dimensión Date.  
  
12. En el menú **Archivo** , haga clic en **Guardar todo**.  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
[Definir un cubo](../analysis-services/lesson-2-2-defining-a-cube.md)  
  
## <a name="see-also"></a>Vea también  
[Dimensiones en modelos multidimensionales](../analysis-services/multidimensional-models/dimensions-in-multidimensional-models.md)  
[Crear una dimensión usando una tabla existente](../analysis-services/multidimensional-models/create-a-dimension-by-using-an-existing-table.md)  
[Crear una dimensión usando el Asistente para dimensiones](../analysis-services/multidimensional-models/create-a-dimension-using-the-dimension-wizard.md)  
  
  
  

