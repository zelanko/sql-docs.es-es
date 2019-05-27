---
title: Definir un cubo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 8aa4ac2d-857f-4048-baa0-0f314e207cf6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 167121188939bcf82ed359ac3f8cf7e3aae47635
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66079060"
---
# <a name="defining-a-cube"></a>Definir un cubo
  El Asistente para cubos le ayuda a definir los grupos de medida y las dimensiones de un cubo. En la tarea siguiente, usará el Asistente para cubos para generar un cubo.  
  
### <a name="to-define-a-cube-and-its-properties"></a>Para definir un cubo y sus propiedades  
  
1.  En el Explorador de soluciones, haga clic con el botón derecho en **Cubos**y, después, haga clic en **Nuevo cubo**. Aparece el Asistente para cubos.  
  
2.  En la página **Asistente para cubos** , haga clic en **Siguiente**.  
  
3.  En la página **Seleccionar método de creación** , compruebe que la opción **Usar tablas existentes** está seleccionada y, después, haga clic en **Siguiente**.  
  
4.  En la página **Seleccionar tablas de grupo de medida** , compruebe que la vista del origen de datos **Adventure Works DW 2012** está seleccionada.  
  
5.  Haga clic en **Sugerir** para que el Asistente para cubos sugiera las tablas que se deben usar para crear los grupos de medida.  
  
     El asistente examinará las tablas y sugerirá **InternetSales** como tabla de grupos de medida. Las tablas de grupos de medida, también denominadas tablas de hechos, contienen las medidas que son de su interés, como el número de unidades vendidas.  
  
6.  Haga clic en **Siguiente**.  
  
7.  En la página **Seleccionar medidas** , revise las medidas seleccionadas en el grupo de medida **Internet Sales** y luego desactive las casillas de las medidas siguientes:  
  
    -   **Promotion Key**  
  
    -   **Currency Key**  
  
    -   **Sales Territory Key**  
  
    -   **Revision Number**  
  
     De forma predeterminada, el asistente selecciona como medidas todas las columnas numéricas de la tabla de hechos que no están vinculadas a dimensiones. No obstante, estas cuatro columnas no son miembros reales. Las tres primeras son valores clave que vinculan la tabla de hechos con tablas de dimensiones que no se utilizan en la versión inicial de este cubo.  
  
8.  Haga clic en **Siguiente**.  
  
9. En la página **Seleccionar dimensiones existentes** , asegúrese de que la dimensión **Date** que ha creado anteriormente está seleccionada y haga clic en **Siguiente**.  
  
10. En la página **Seleccionar nuevas dimensiones** , seleccione las nuevas dimensiones que se van a crear. Para ello, compruebe que las casillas **Customer**, **Geography**y **Product** están activadas y, después, desactive la casilla **InternetSales** .  
  
11. Haga clic en **Siguiente**.  
  
12. En el **completando el Asistente para** página, cambie el nombre del cubo para `Analysis Services Tutorial`. En el panel de vista previa, puede ver el grupo de medida **InternetSales** y sus medidas. También puede ver las dimensiones **Date**, **Customer** y **Product** .  
  
13. Haga clic en **Finalizar** para completar el asistente.  
  
     En el Explorador de soluciones, en el proyecto Tutorial de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , el cubo Tutorial de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] aparece en la carpeta **Cubos** , y las dimensiones de base de datos Customer y Product aparecen en la carpeta **Dimensiones** . Asimismo, en el centro del entorno de desarrollo, la pestaña Estructura de cubo muestra el cubo Tutorial de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
14. En la barra de herramientas de la pestaña Estructura de cubo, cambie el nivel de **Zoom** al 50 por ciento, de modo que pueda ver mejor las tablas de dimensiones y hechos del cubo. Observe que la tabla de hechos es amarilla y las tablas de dimensiones son azules.  
  
15. En el menú **Archivo** , haga clic en **Guardar todo**.  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Agregar atributos a dimensiones](lesson-2-3-adding-attributes-to-dimensions.md)  
  
## <a name="see-also"></a>Vea también  
 [Cubos en modelos multidimensionales](multidimensional-models/cubes-in-multidimensional-models.md)   
 [Dimensiones en modelos multidimensionales](multidimensional-models/dimensions-in-multidimensional-models.md)  
  
  
