---
title: 'Tutorial: Crear un informe de gráfico rápido sin conexión (Generador de informes) | Microsoft Docs'
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- reports, creating
- tutorials, getting started
- creating reports
ms.assetid: 6b1db67a-cf75-494c-b70c-09f1e6a8d414
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: da0f35362a329974f8044da21b125d545c7bb323
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48091375"
---
# <a name="tutorial-create-a-quick-chart-report-offline-report-builder"></a>Tutorial: Crear un informe de gráfico rápido sin conexión (Generador de informes)
  En este tutorial, creará un gráfico circular usando un asistente y, a continuación, lo modificará un poco, solo para hacerse una idea de las posibilidades. Puede hacerlo de dos maneras diferentes: Ambos métodos tienen el mismo resultado; un gráfico circular como el de la siguiente ilustración:  
  
 ![Ver "Mi primer gráfico circular" en ejecución](../media/rs-my1stpierunview.gif "mi primer gráfico circular en la vista de ejecución")  
  
## <a name="prerequisites"></a>Requisitos previos  
 Si usa datos XML o una consulta [!INCLUDE[tsql](../../../includes/tsql-md.md)], necesita tener acceso al Generador de informes [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. Puede ejecutar la versión independiente o la versión de ClickOnce disponible en el Administrador de informes o en un sitio de SharePoint. El primer paso, cómo abrir el generador de informes es diferente para las versiones de ClickOnce. Para obtener más información, consulte [instalar, desinstalar y asistencia del generador de informes](../install-uninstall-and-report-builder-support.md).  
  
##  <a name="TwoWays"></a> Dos maneras de hacer este tutorial  
  
-   [Crear el gráfico circular con datos XML](#CreatePieChartXML)  
  
-   [Crear el gráfico circular con una consulta Transact-SQL que contenga datos](#CreatePieQueryData)  
  
### <a name="using-xml-data-for-this-tutorial"></a>Usar datos XML para este tutorial  
 Puede utilizar los datos XML que copia de este tema y pegarlos en el asistente. No necesita estar conectado a un servidor de informes o a un servidor de informes en modo integrado de SharePoint, y no necesita acceso a una instancia de [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
 [Crear el gráfico circular con datos XML](#CreatePieChartXML)  
  
### <a name="using-a-transact-sql-query-that-contains-data-for-this-tutorial"></a>Usar una consulta Transact SQL que contenga los datos de este tutorial  
 Puede copiar desde este tema una consulta con datos incluidos en él y pegarlos en el asistente. Necesitará el nombre de una instancia de [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] y credenciales suficientes para tener acceso de solo lectura a cualquier base de datos. La consulta del conjunto de datos en el tutorial usa datos literales, pero la consulta debe ser procesada por una instancia de [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] para que devuelva los metadatos requeridos por un conjunto de datos de informe.  
  
 La ventaja de usar la consulta [!INCLUDE[tsql](../../../includes/tsql-md.md)] es que todos los demás tutoriales del Generador de informes usan el mismo método, de modo que cuando realice los otros tutoriales ya sabrá lo que debe hacer.  
  
 El [!INCLUDE[tsql](../../../includes/tsql-md.md)] consulta requieren algunos otros requisitos previos. Para obtener más información, consulte [Requisitos previos para los tutoriales&#40;Generador de informes&#41;](../report-builder-tutorials.md).  
  
 [Crear el gráfico circular con una consulta Transact-SQL que contenga datos](#CreatePieQueryData)  
  
## <a name="also-in-this-article"></a>También en este artículo  
 [Después de ejecutar el Asistente](#AfterWizard)  
  
 [Próxima Novedades](#WhatsNext)  
  
##  <a name="CreatePieChartXML"></a> Crear el gráfico circular con datos XML  
  
#### <a name="to-create-the-pie-chart-with-xml-data"></a>Para crear el gráfico circular con datos XML  
  
1.  Haga clic en **Inicio**, seleccione **Programas**, **Generador de informes de Microsoft SQL Server 2012**y, a continuación, haga clic en **Generador de informes**.  
  
     Aparecerá el cuadro de diálogo **Introducción** .  
  
    > [!NOTE]  
    >  Si el **Introducción** no aparece el cuadro de diálogo, desde el **Report Builder** botón, haga clic en **New**.  
  
2.  En el panel de la izquierda, compruebe que está seleccionada la opción **Informe** .  
  
3.  En el panel derecho, haga clic en **Asistente para gráfico**y, a continuación, haga clic en **Crear**.  
  
4.  En la página **Elegir un conjunto de datos** , haga clic en **Crear un conjunto de datos**y, a continuación, haga clic en **Siguiente**.  
  
5.  En la página **Elegir una conexión a un origen de datos** , haga clic en **Nueva**.  
  
     Se abre el cuadro de diálogo **Propiedades del origen de datos** .  
  
6.  Puede dar el nombre que desee a un origen de datos. En el cuadro **Nombre** , escriba: **MiGráficoCircular**.  
  
7.  En el **Seleccionar tipo de conexión** cuadro, haga clic en **XML.**  
  
8.  Haga clic en la pestaña **Credenciales** y seleccione **Usar usuario de Windows actual. Es posible que se requiera la delegación de Kerberos**y, a continuación, haga clic en **Aceptar**.  
  
9. En la página **Elegir una conexión a un origen de datos** , haga clic en **miGráficoCircular**y, a continuación, haga clic en **Siguiente**.  
  
10. Copie el texto siguiente y péguelo en el cuadro grande en el centro de la **diseñar una consulta** página.  
  
    ```  
    <Query>  
    <ElementPath>Root /S  {@Sales (Integer)} /C {@FullName} </ElementPath>  
    <XmlData>  
    <Root>  
    <S Sales="150">  
      <C FullName="Jae Pak" />  
    </S>  
    <S Sales="350">  
      <C FullName="Jillian  Carson" />  
    </S>  
    <S Sales="250">  
      <C FullName="Linda C Mitchell" />  
    </S>  
    <S Sales="500">  
      <C FullName="Michael Blythe" />  
    </S>  
    <S Sales="450">  
      <C FullName="Ranjit Varkey" />  
    </S>  
    </Root>  
    </XmlData>  
    </Query>  
    ```  
  
11. (Opcional) Haga clic en el botón Ejecutar (**!**) para ver los datos en los que se basará su gráfico.  
  
12. Haga clic en **Siguiente**.  
  
13. En la página **Elegir un tipo de gráfico** , haga clic en **Circular**y, a continuación, haga clic en **Siguiente**.  
  
14. En la página **Organizar campos del gráfico**, haga doble clic en el campo **Ventas** en el cuadro **Campos disponibles**.  
  
     Observe que se desplaza automáticamente al cuadro de diálogo **Valores** , porque es un valor numérico.  
  
15. Arrastre el campo **FullName** desde el cuadro **Campos disponibles** hasta **Categorías** (o haga doble clic en él; se desplazará al cuadro **Categorías**) y, después, haga clic en **Siguiente**.  
  
16. En el **elegir un estilo** página, **Océano** está activada de forma predeterminada. Haga clic en otros estilos para ver su apariencia.  
  
17. Haga clic en **Finalizar**.  
  
     Se ve ahora el nuevo informe de gráfico circular en la superficie de diseño. Lo que ve es figurativo. La leyenda dice Full Name 1, Full Name 2, etc., en lugar de los nombres de los vendedores, y el tamaño de los sectores del gráfico circular no es preciso. Únicamente es para que se haga una idea de cómo será el informe.  
  
18. Para ver el gráfico circular real, haga clic en **Ejecutar** en la pestaña **Inicio** de la cinta de opciones.  
  
 ![Icono de flecha usado con el vínculo Volver al principio](../../2014-toc/media/uparrow16x16.gif "Icono de flecha usado con el vínculo Volver al principio")[Volver al principio](#TwoWays)  
  
##  <a name="CreatePieQueryData"></a> Crear el gráfico circular con un [!INCLUDE[tsql](../../../includes/tsql-md.md)] consulta  
  
#### <a name="to-create-the-pie-chart-with-a-includetsqlincludestsql-mdmd-query-that-contains-data"></a>Para crear el gráfico circular con una consulta [!INCLUDE[tsql](../../../includes/tsql-md.md)] que contenga los datos  
  
1.  Haga clic en **Inicio**, seleccione **Programas**, **Generador de informes de Microsoft SQL Server 2012**y, a continuación, haga clic en **Generador de informes**.  
  
2.  En el **nuevo informe o conjunto de datos** diálogo cuadro, compruebe que **informe** está seleccionado en el panel izquierdo.  
  
3.  En el panel derecho, haga clic en **Asistente para gráfico**y, a continuación, haga clic en **Crear**.  
  
4.  En la página **Elegir un conjunto de datos** , haga clic en **Crear un conjunto de datos**y, a continuación, haga clic en **Siguiente**.  
  
5.  En la página **Elegir una conexión a un origen de datos** , seleccione un origen de datos existente o vaya al servidor de informes y seleccione un origen de datos y, a continuación, haga clic en **Siguiente**. Puede que necesite escribir un nombre de usuario y contraseña.  
  
    > [!NOTE]  
    >  El origen de datos que elija no importa, con tal de que tenga los permisos adecuados. No está recibiendo datos del origen de datos. Para obtener más información, consulte [Requisitos previos para los tutoriales&#40;Generador de informes&#41;](../report-builder-tutorials.md).  
  
6.  En la página **Diseñar una consulta** , haga clic en **Editar como texto**.  
  
7.  Pegue la siguiente consulta en el panel de consulta:  
  
    ```  
    SELECT 150 AS Sales, 'Jae Pak' AS FullName   
    UNION SELECT 350 AS Sales, 'Jillian Carson' AS FullName   
    UNION SELECT 250 AS Sales, 'Linda C Mitchell' AS FullName   
    UNION SELECT 500 AS Sales, 'Michael Blythe' AS FullName   
    UNION SELECT 450 AS Sales, 'Ranjit Varkey' AS FullName   
    ```  
  
8.  (Opcional) Haga clic en el botón Ejecutar (**!**) para ver los datos en los que se basará su gráfico.  
  
9. Haga clic en **Siguiente**.  
  
10. En la página **Elegir un tipo de gráfico** , haga clic en **Circular**y, a continuación, haga clic en **Siguiente**.  
  
11. En la página **Organizar campos del gráfico**, haga doble clic en el campo **Ventas** en el cuadro **Campos disponibles**.  
  
     Observe que se desplaza automáticamente al cuadro **Valores** , porque es un valor numérico.  
  
12. Arrastre el campo **FullName** desde el cuadro **Campos disponibles** hasta **Categorías** (o haga doble clic en él; se desplazará al cuadro **Categorías**) y, después, haga clic en **Siguiente**.  
  
13. En la página **Elegir un estilo** , Océano está seleccionado de forma predeterminada. Haga clic en otros estilos para ver su apariencia.  
  
14. Haga clic en **Finalizar**.  
  
     Se ve ahora el nuevo informe de gráfico circular en la superficie de diseño. Lo que ve es figurativo. La leyenda dice Full Name 1, Full Name 2, etc., en lugar de los nombres de los vendedores, y el tamaño de los sectores del gráfico circular no es preciso. Únicamente es para que se haga una idea de cómo será el informe.  
  
15. Para ver el gráfico circular real, haga clic en **Ejecutar** en la pestaña **Inicio** de la cinta de opciones.  
  
 ![Icono de flecha usado con el vínculo Volver al principio](../../2014-toc/media/uparrow16x16.gif "Icono de flecha usado con el vínculo Volver al principio")[Volver al principio](#TwoWays)  
  
##  <a name="AfterWizard"></a> Después de ejecutar el asistente  
 Ahora que tiene el informe del gráfico circular, puede trabajar con él. En la pestaña **Ejecutar** de la cinta de opciones, haga clic en **Diseño**, de modo que pueda seguir modificándolo.  
  
### <a name="make-the-chart-bigger"></a>Agrandar el gráfico  
 Quizá quiera que el gráfico circular sea más grande. Haga clic en el gráfico, pero no en ningún elemento del gráfico, para seleccionarlo y arrastre la esquina inferior derecha para cambiar el tamaño.  
  
### <a name="add-a-report-title"></a>Agregar un título de informe  
 Seleccione las palabras **Título de gráfico** en la parte superior del gráfico y, a continuación, escriba un título, como **Gráfico circular de ventas**.  
  
### <a name="add-percentages"></a>Agregar porcentajes  
  
##### <a name="to-display-percentage-values-as-labels-on-a-pie-chart"></a>Para mostrar los valores de porcentaje como etiquetas en un gráfico circular  
  
1.  Haga doble clic en el gráfico circular y seleccione **Mostrar etiquetas de datos**. Las etiquetas de datos aparecerán dentro de cada sector del gráfico circular.  
  
2.  Haga doble clic en las etiquetas y seleccione **propiedades de la etiqueta de serie**. Aparece el cuadro de diálogo **Propiedades de la etiqueta de la serie** .  
  
3.  Tipo `#PERCENT{P0}` para el **etiquetar datos** opción.  
  
     El `{P0}` le da el porcentaje sin decimales. Si simplemente escribe `#PERCENT`, los números tendrán dos posiciones decimales. `#PERCENT` es una palabra clave que realiza un cálculo o función automáticamente; Hay muchas otras.  
  
 Para obtener más información acerca de cómo personalizar las etiquetas del gráfico y las leyendas, consulte [Mostrar valores de porcentaje en un gráfico circular &#40;Generador de informes y SSRS&#41;](../report-design/display-percentage-values-on-a-pie-chart-report-builder-and-ssrs.md) y [Cambiar el texto de un elemento de leyenda&#40;Generador de informes y SSRS&#41;](../report-design/chart-legend-change-item-text-report-builder.md).  
  
 ![Icono de flecha usado con el vínculo Volver al principio](../../2014-toc/media/uparrow16x16.gif "Icono de flecha usado con el vínculo Volver al principio")[Volver al principio](#TwoWays)  
  
##  <a name="WhatsNext"></a> ¿Qué debe hacer a continuación?  
 Ahora que ha creado su primer informe en el Generador de informes, está listo para leer los demás tutoriales y empezar a crear informes a partir de sus propios datos. Para ejecutar el generador de informes, necesita permiso para tener acceso a los orígenes de datos, como bases de datos, con un *cadena de conexión*, que le conecta al origen de datos. El administrador del sistema tiene esta información y puede facilitársela.  
  
 Para trabajar con otros tutoriales, necesita el nombre de una instancia de [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] y credenciales suficientes para tener acceso de solo lectura a cualquier base de datos. El administrador del sistema puede facilitárselo también.  
  
 Finalmente, para guardar los informes en un servidor de informes o en un sitio de SharePoint integrado con un servidor de informes, necesitará la dirección URL y los permisos necesarios. Puede ejecutar cualquier informe que cree directamente desde su equipo, pero los informes tienen más funcionalidad cuando se ejecutan desde el servidor de informes o desde el sitio de SharePoint. Necesita permisos para ejecutar sus informes u otros desde el servidor de informes o desde el sitio de SharePoint donde estén publicados. Hable con el administrador del sistema para obtener acceso.  
  
 Podría resultarle de ayuda leer sobre algunos conceptos y términos antes de empezar. Para obtener más información, consulte [conceptos de creación de informes &#40;generador de informes y SSRS&#41;](../report-design/report-authoring-concepts-report-builder-and-ssrs.md). Además, dedique algún tiempo al planeamiento antes de crear su primer informe. Será tiempo bien invertido. Para obtener más información, consulte [planear un informe &#40;Report Builder&#41;](../report-design/planning-a-report-report-builder.md).  
  
 ![Icono de flecha usado con el vínculo Volver al principio](../../2014-toc/media/uparrow16x16.gif "Icono de flecha usado con el vínculo Volver al principio")[Volver al principio](#TwoWays)  
  
## <a name="see-also"></a>Vea también  
 [Tutoriales &#40;generador de informes&#41;](../report-builder-tutorials.md)   
 [Generador de informes en SQL Server 2014](report-builder-in-sql-server-2016.md)  
  
  
