---
title: Definir y examinar traducciones | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 0e60be99-3768-499c-a22c-a4ec37e61887
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 39db8cb33e2adbf24ff03b6ad84dfefe0e8bfb81
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/28/2018
ms.locfileid: "52504639"
---
# <a name="defining-and-browsing-translations"></a>Definir y examinar traducciones
  Una traducción es una representación de los nombres de objetos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] en un idioma específico. Entre estos objetos se incluyen grupos de medida, medidas, dimensiones, atributos, jerarquías, KPI, acciones y miembros calculados. Las traducciones ofrecen compatibilidad de servidor para aplicaciones cliente que admitan varios idiomas. Mediante el uso de dicho cliente, éste pasa el identificador local (LCID) a la instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], que utiliza el LCID para determinar el conjunto de traducciones que se va a utilizar al proporcionar metadatos para los objetos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . Si un objeto de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] no contiene una traducción para ese idioma o no contiene una traducción para un objeto determinado, al devolver los metadatos de objeto al cliente se usa el idioma predeterminado. Por ejemplo, si un usuario corporativo de Francia tiene acceso a un cubo de una estación de trabajo con configuración regional francesa, el usuario corporativo verá los títulos y valores de propiedades de miembro en francés si existe una traducción al francés. Sin embargo, si un usuario corporativo de Alemania tiene acceso al mismo cubo desde una estación de trabajo con una configuración regional alemana, verá los títulos y los valores de propiedades de miembro en alemán. Para obtener más información, consulte [traducciones de dimensiones](multidimensional-models-olap-logical-dimension-objects/dimension-translations.md), [traducciones de cubos](multidimensional-models-olap-logical-cube-objects/cube-translations.md), [traducciones &#40;Analysis Services&#41;](translations-analysis-services.md).  
  
 En las tareas de este tema, se definen las traducciones de metadatos de un conjunto limitado de objetos de dimensión de la dimensión Date y de objetos de cubo del cubo [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial. Entonces podrá buscar entre estos objetos de dimensión y de cubo para examinar las traducciones de metadatos.  
  
## <a name="specifying-translations-for-the-date-dimension-metadata"></a>Especificar traducciones para los metadatos de la dimensión Date  
  
1.  Abra el Diseñador de dimensiones para la dimensión **Date** y, después, haga clic en la pestaña **Traducciones** .  
  
     Aparecen los metadatos en el idioma predeterminado de dicho objeto de dimensión. El idioma predeterminado en el cubo [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial es el inglés.  
  
2.  En la barra de herramientas de la pestaña **Traducciones** , haga clic en el botón **Nueva traducción** .  
  
     Aparecerá una lista de idiomas en el cuadro de diálogo **Seleccionar idioma** .  
  
3.  Haga clic en **Español (España)** y, después, en **Aceptar**.  
  
     Aparecerá una nueva columna en la que podrá definir las traducciones españolas para los objetos de metadatos que desee traducir. En este tutorial, solo traduciremos un pequeño número de objetos para ilustrar el proceso.  
  
4.  En la barra de herramientas de la pestaña **Traducciones** , haga clic en el botón **Nueva traducción** , en **Francés (Francia)** en el cuadro de diálogo **Seleccionar idioma** y, después, haga clic en **Aceptar**.  
  
     Aparecerá otra columna de idioma en la que definirá las traducciones de francés.  
  
5.  En la fila de la **título** de objeto para el **fecha** de dimensión, escriba `Fecha` en el **español (España)** columna de traducción y `Temps` en el  **Francés (Francia)** columna de traducción.  
  
6.  En la fila de la **título** de objeto para el **Month Name** atributo, escriba `Mes del Año` en el **español (España)** columna de traducción y `Mois d'Année` en el **Francés (Francia)** columna de traducción.  
  
     Tenga en cuenta que al escribir estas traducciones, un botón de puntos suspensivos (**...** ) aparece. Si hace clic en estos puntos suspensivos podrá especificar una columna en la tabla subyacente que proporciona traducciones para cada miembro de la jerarquía de atributo.  
  
7.  Haga clic en el botón de puntos suspensivos (**...** ) para el **español (España)** traducción para el **Month Name** atributo.  
  
     Aparecerá el cuadro de diálogo **Traducción de datos de atributos** .  
  
8.  En la lista **Columnas de traducción** , seleccione **SpanishMonthName**, tal como se muestra en la siguiente imagen.  
  
     ![Cuadro de diálogo traducción de datos de atributo](../../2014/tutorials/media/l9-translations-4.gif "cuadro de diálogo traducción de datos de atributo")  
  
9. Haga clic en **Aceptar**y, a continuación, haga clic en el botón de puntos suspensivos (**...** ) para el **francés (Francia)** traducción para el **Month Name** atributo.  
  
10. En la lista **Columnas de traducción** , seleccione **FrenchMonthName**y, después, haga clic en **Aceptar**.  
  
     Los pasos de este procedimiento ilustran el proceso de definición de traducciones de metadatos para miembros y objetos de dimensiones.  
  
## <a name="specifying-translations-for-the-analysis-services-tutorial-cube-metadata"></a>Especificar traducciones para los metadatos del cubo Tutorial de Analysis Services  
  
1.  Cambie al Diseñador de cubos para el cubo Tutorial de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] y, después, cambie a la pestaña **Traducciones** .  
  
     Los metadatos en el idioma predeterminado de dicho objeto de cubo aparecen tal como se muestran en la siguiente imagen. El idioma predeterminado en el cubo [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial es el inglés.  
  
     ![En la pestaña traducciones del idioma predeterminado](../../2014/tutorials/media/l9-translations-5.gif "en la pestaña traducciones del idioma predeterminado")  
  
2.  En la barra de herramientas de la pestaña **Traducciones** , haga clic en el botón **Nueva traducción** .  
  
     Aparecerá una lista de idiomas en el cuadro de diálogo **Seleccionar idioma**.  
  
3.  Seleccione **Español (España)** y, después, haga clic en **Aceptar**.  
  
     Aparecerá una nueva columna en la que podrá definir las traducciones españolas para los objetos de metadatos que desee traducir. En este tutorial, solo traduciremos un pequeño número de objetos para ilustrar el proceso.  
  
4.  En la barra de herramientas de la pestaña **Traducciones** , haga clic en el botón **Nueva traducción** , seleccione **Francés (Francia)** en el cuadro de diálogo **Seleccionar idioma** y, después, haga clic en **Aceptar**.  
  
     Aparecerá otra columna de idioma en la que definirá las traducciones de francés.  
  
5.  En la fila de la **título** de objeto para el **fecha** de dimensión, escriba `Fecha` en el **español (España)** columna de traducción y `Temps` en el  **Francés (Francia)** columna de traducción.  
  
6.  En la fila de la **título** de objeto para el **Internet Sales** grupo de medida, el tipo `Ventas del lnternet` en el **español (España)** columna de traducción y `Ventes D'Internet` en el **francés (Francia)** columna de traducción.  
  
7.  En la fila de la **título** objeto para la medida Internet Sales-Sales Amount, escriba `Cantidad de las Ventas del Internet` en el **español (España)** columna de traducción y `Quantité de Ventes d'Internet` en el **francés () Francia)** columna de traducción.  
  
     Los pasos de este procedimiento ilustran el proceso de definición de traducciones de metadatos para objetos de cubos.  
  
## <a name="browsing-the-cube-by-using-translations"></a>Examinar el cubo utilizando traducciones  
  
1.  En el menú **Compilar** , haga clic en **Tutorial de Implementar Analysis Services**.  
  
2.  Cuando la implementación se haya completado correctamente, vaya a la pestaña **Explorador** y, después, haga clic en **Volver a conectar**.  
  
3.  Quite todas las jerarquías y medidas del panel **Datos** y seleccione Tutorial de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] en la lista **Perspectivas** .  
  
4.  En el panel de metadatos, expanda **Medidas** y, después, **Venta por Internet**.  
  
     Observe que la medida **Internet Sales-Sales Amount** aparece en inglés en este grupo de medida.  
  
5.  En la barra de herramientas, seleccione **Español (España)** en la lista **Idioma** .  
  
     Observe que los elementos del panel de metadatos se vuelven a rellenar. Una vez que los elementos del panel de metadatos se vuelvan a rellenar, observe cómo la medida Internet Sales-Sales Amount ya no aparece en la carpeta para mostrar Venta por Internet. En su lugar, aparecerá en español en una nueva carpeta para mostrar denominada `Ventas del lnternet`, tal y como se muestra en la siguiente imagen.  
  
     ![Panel de metadatos Repopulated](../../2014/tutorials/media/l9-translations-6.gif "Repopulated el panel de metadatos")  
  
6.  En el panel metadatos, haga clic en `Cantidad de las Ventas del Internet` y, a continuación, seleccione **agregar a consulta**.  
  
7.  En el panel metadatos, expanda `Fecha`, expanda **Fecha.Calendar Date**, haga clic en **Fecha.Calendar Date**y, a continuación, seleccione **agregar a filtro**.  
  
8.  En el panel **Filtro** , seleccione **CY 2007** como expresión de filtro.  
  
9. En el panel de metadatos, haga clic con el botón derecho en **Mes del año** y seleccione **Agregar a consulta**.  
  
     Observe que los nombres de los meses aparecen en español, tal como se muestra en la siguiente imagen.  
  
     ![Nombres de los meses en español en el panel datos](../../2014/tutorials/media/l9-translations-7.gif "nombres de los meses en español en el panel de datos")  
  
10. En la barra de herramientas, seleccione **Francés (Francia)** en la lista **Idioma** .  
  
     Observe que los nombres de los meses aparecen ahora en francés y que el nombre de la medida aparece ahora también en francés.  
  
## <a name="next-lesson"></a>Lección siguiente  
 [Lección 10: Definir Roles administrativos](../analysis-services/lesson-10-defining-administrative-roles.md)  
  
## <a name="see-also"></a>Vea también  
 [Traducciones de dimensiones](multidimensional-models-olap-logical-dimension-objects/dimension-translations.md)   
 [Traducciones de cubo](multidimensional-models-olap-logical-cube-objects/cube-translations.md)   
 [Traducciones &#40;Analysis Services&#41;](translations-analysis-services.md)  
  
  
