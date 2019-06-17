---
title: Creación de una estructura de modelo de minería de datos de distribución de correo directo (Tutorial de minería de datos básicos) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: a9c67f29-0c47-4a5a-862b-db0f5213c2c9
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 2bd2e9d0decc730a59b63ee600bec2d080cc85fb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62856162"
---
# <a name="creating-a-targeted-mailing-mining-model-structure-basic-data-mining-tutorial"></a>Crear una estructura del modelo de minería de datos de distribución de correo directo (Tutorial básico de minería de datos)
  El primer paso para crear un escenario de correo directo (Targeted Mailing) consiste en usar el Asistente para minería de datos de [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] con el fin de crear una estructura de minería de datos y un modelo de minería de datos de árbol de decisión.  
  
 En esta tarea se configurará una nueva estructura de minería de datos y agregar un modelo de minería de datos inicial según la [!INCLUDE[msCoName](../includes/msconame-md.md)] algoritmo de árboles de decisión. Para crear la estructura, primero seleccionará las tablas y vistas, y a continuación identificará qué columnas se utilizarán para el entrenamiento y cuáles para pruebas.  
  
### <a name="to-create-a-mining-structure-for-the-targeted-mailing-scenario"></a>Para crear una estructura de minería de datos para un escenario de distribución de correo directo  
  
1.  En el Explorador de soluciones, haga clic en **estructuras de minería de datos** y seleccione **nueva estructura de minería de datos** para iniciar el Asistente para minería de datos.  
  
2.  En la página de inicio del **Asistente para minería de datos** , haga clic en **Siguiente**.  
  
3.  En el **seleccionar el método de definición** , comprueba que **desde el almacén de datos o base de datos relacional existente** está seleccionada y, a continuación, haga clic en **siguiente**.  
  
4.  En el **crear la estructura de minería de datos** página, en **qué técnica de minería de datos desea utilizar?** , seleccione **Microsoft Decision Trees**.  
  
    > [!NOTE]  
    >  Si aparece una advertencia de que no se puede encontrar ningún algoritmo de minería de datos, puede que las propiedades del proyecto no estén configuradas correctamente. Esta advertencia se produce cuando el proyecto intenta recuperar una lista de algoritmos de minería de datos del servidor de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] y no puede encontrarlo. De forma predeterminada, [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] usará **localhost** como el servidor. Si está utilizando una instancia diferente o una instancia con nombre, debe cambiar las propiedades del proyecto. Para obtener más información, consulte [crear un proyecto de Analysis Services &#40;Basic Data Mining Tutorial&#41;](../../2014/tutorials/creating-an-analysis-services-project-basic-data-mining-tutorial.md).  
  
5.  Haga clic en **Siguiente**.  
  
6.  En el **seleccionar vista del origen de datos** página, en el **vistas del origen de datos disponibles** panel, seleccione **Targeted Mailing**. Puede hacer clic en **examinar** para ver las tablas en la vista del origen de datos y, a continuación, haga clic en **cerrar** para volver al asistente.  
  
7.  Haga clic en **Siguiente**.  
  
8.  En el **especificar tipos de tablas** , seleccione la casilla de verificación en la **caso** columna correspondiente a vtargetmail para usarla como tabla de casos y, a continuación, haga clic en **siguiente**. Utilizará la tabla ProspectiveBuyer posteriormente para pruebas; pásela por alto por ahora.  
  
9. En el **especificar los datos de entrenamiento** página, identificará al menos una columna de predicción, una columna de clave y una columna para el modelo de entrada. Active la casilla situada en la **Predictable** columna en el **BikeBuyer** fila.  
  
    > [!NOTE]  
    >  Observe la advertencia en la parte inferior de la ventana. No podrá navegar a la página siguiente hasta que seleccione al menos uno **entrada** y uno **Predictable** columna.  
  
10. Haga clic en **sugerir** para abrir el **Sugerir columnas relacionadas** cuadro de diálogo.  
  
     El **sugerir** botón está habilitado siempre que se ha seleccionado al menos un atributo de predicción. El **Sugerir columnas relacionadas** cuadro de diálogo muestra las columnas que están más relacionadas con la columna predecible y ordena los atributos por su correlación con el atributo de predicción. Las columnas con una correlación significativa (con una confianza mayor del 95%) se seleccionan automáticamente para incluirse en el modelo.  
  
     Revise las sugerencias y, a continuación, haga clic en **cancelar** to ignore las sugerencias.  
  
    > [!NOTE]  
    >  Si hace clic en **Aceptar**, todas las sugerencias se marcarán como columnas de entrada en el asistente. Si está de acuerdo con solamente algunas de las sugerencias, debe cambiar los valores manualmente.  
  
11. Compruebe que la casilla de verificación en la **clave** columna seleccionada en el **CustomerKey** fila.  
  
    > [!NOTE]  
    >  Si la tabla de origen de la vista del origen de datos muestra una clave, el Asistente para minería de datos elegirá automáticamente esa columna como clave para el modelo.  
  
12. Seleccione las casillas de verificación en la **entrada** columna en las filas siguientes. Puede activar varias columnas resaltando un rango de celdas y presionando CTRL mientras activa una casilla.  
  
    -   **Edad**  
  
    -   **CommuteDistance**  
  
    -   **EnglishEducation**  
  
    -   **EnglishOccupation**  
  
    -   **Sexo**  
  
    -   **GeographyKey**  
  
    -   **HouseOwnerFlag**  
  
    -   **MaritalStatus**  
  
    -   **NumberCarsOwned**  
  
    -   **NumberChildrenAtHome**  
  
    -   **Region**  
  
    -   **TotalChildren**  
  
    -   **YearlyIncome**  
  
13. En la columna izquierda de la página, active las casillas de las filas siguientes.  
  
    -   **AddressLine1**  
  
    -   **AddressLine2**  
  
    -   **DateFirstPurchase**  
  
    -   **EmailAddress**  
  
    -   **FirstName**  
  
    -   **LastName**  
  
     Asegúrese de que estas filas solo tienen marcas en la columna izquierda. Estas columnas se agregarán a la estructura, pero no se incluirán en el modelo. Sin embargo, una vez generado el modelo, estarán disponibles para la obtención de detalles y las pruebas. Para obtener más información sobre la obtención de detalles, consulte [consultas de obtención de detalles &#40;minería de datos&#41;](../../2014/analysis-services/data-mining/drillthrough-queries-data-mining.md)  
  
14. Haga clic en **Siguiente**.  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Especificar el tipo de datos y el tipo de contenido &#40;Tutorial de minería de datos básicos&#41;](../../2014/tutorials/specifying-the-data-type-and-content-type-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vea también  
 [Especificar tipos de tablas &#40;Asistente para minería de datos&#41;](../../2014/analysis-services/specify-table-types-data-mining-wizard.md)   
 [Diseñador de minería de datos](../../2014/analysis-services/data-mining/data-mining-designer.md)   
 [Algoritmo de árboles de decisión de Microsoft](../../2014/analysis-services/data-mining/microsoft-decision-trees-algorithm.md)  
  
  
