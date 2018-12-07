---
title: Crear un mapa del documento (Generador de informes y SSRS) | Microsoft Docs
ms.date: 05/24/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: c200a97b-67f2-499f-8374-3ed1ebe3f33c
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 48b1d2e88389ac19c2c2d3bcf753ece1df952689
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/28/2018
ms.locfileid: "52542413"
---
# <a name="create-a-document-map-report-builder-and-ssrs"></a>Crear un mapa del documento (Generador de informes y SSRS)

Un mapa del documento proporciona un conjunto de vínculos de navegación a los elementos de informe de un informe representado. Cuando se ve un informe que incluya un mapa del documento, aparece un panel lateral separado junto al informe. Un usuario puede hacer clic en los vínculos del mapa del documento para saltar a la página del informe que muestra el elemento. Las secciones y los grupos del informe se organizan en una jerarquía de vínculos. Cada vez que se hace clic en un elemento del mapa del documento, se actualiza el informe y se muestra el área del mismo correspondiente a dicho elemento en el mapa del documento.  
  
 Para agregar vínculos al mapa del documento, se establece la propiedad **DocumentMapLabel** del elemento de informe en un texto o en una expresión que se evalúa como el texto que se desea mostrar en el mapa del documento. También puede agregar los valores únicos para un grupo de tablas o de matrices al mapa del documento. Por ejemplo, para un grupo basado en colores, cada color único es un vínculo a la página del informe que muestra la instancia de grupo para ese color.  
  
 También puede crear una dirección URL a un informe que invalide la presentación del mapa del documento, lo que le permite ejecutar el informe sin mostrar el mapa del documento y, después, hacer clic en el botón **Mostrar u ocultar mapa del documento** de la barra de herramientas del visor de informes para alternar la presentación.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="DocMapRenderExtensions"></a> Mapas de documento y extensiones de representación  
 El mapa del documento está pensado para usarlo en la extensión de representación de HTML, por ejemplo, en la vista previa y el visor de informes. Otras extensiones de representación tienen diferentes formas de articular un mapa del documento:  
  
-   PDF representa un mapa del documento como el panel Marcadores.  
  
-   Excel representa un mapa del documento como una hoja con nombre que incluye una jerarquía de vínculos. Las secciones del informe se representan en hojas separadas que se incluyen con el mapa del documento en el mismo libro.  
  
-   Word representa el mapa del documento como la tabla de contenido.  
  
-   Atom, TIFF, XML y CSV omiten los mapas de documento.  
  
 Para más información, vea [Funcionalidad interactiva para diferentes extensiones de representación de informes &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-builder/interactive-functionality-different-report-rendering-extensions.md).  
  
##  <a name="AddRptItemToMap"></a>   
#### <a name="to-add-a-report-item-to-a-document-map"></a>Para agregar un elemento de informe a un mapa del documento  
  
1.  En la vista de diseño, seleccione el elemento de informe (tabla, matriz o medidor, por ejemplo) que desea agregar al mapa del documento. Las propiedades del elemento de informe aparecen en el panel de propiedades.  
  
    > [!NOTE]  
    >  Para seleccionar una región de datos Tablix, haga clic en cualquier celda para mostrar los identificadores de fila y de columna y, a continuación, haga clic en el controlador de tabla.  
  
2.  En el panel de propiedades, en la propiedad **DocumentMapLabel** , escriba el texto que desea que aparezca en el mapa del documento o escriba una expresión que se evalúe como una etiqueta. Por ejemplo, escriba **Gráfico de ventas**.  
  
    > [!NOTE]  
    >  Si no ve el panel de propiedades, en la pestaña **Vista** , en el grupo **Mostrar u ocultar** , seleccione **Propiedades**.  
  
3.  Repita los pasos 1 y 2 para cada elemento de informe que desee que aparezca en el mapa del documento.  
  
4.  Haga clic en **Ejecutar**. El informe se ejecuta y el mapa del documento muestra las etiquetas que ha creado. Haga clic en cualquier vínculo para saltar a la página del informe que contiene ese elemento.  

  
##  <a name="AddUniqueValuesToMap"></a>   
#### <a name="to-add-unique-group-values-to-a-document-map"></a>Para agregar valores de grupo únicos a un mapa del documento  
  
1.  En la vista Diseño, seleccione la tabla, la matriz o la lista que contiene el grupo que desea mostrar en el mapa del documento. El Panel de agrupación muestra los grupos de filas y de columnas.  
  
2.  En el panel Grupos de filas, haga clic con el botón derecho en el grupo y, después, haga clic en **Editar grupo**. Se abre la página **General** del cuadro de diálogo **Propiedades de grupo de Tablix** .  
  
3.  Haga clic en **Avanzado**.  
  
4.  En el cuadro de lista **Mapa del documento** , escriba o seleccione una expresión que coincida con la expresión de grupo.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
6.  Repita los pasos 1 a 4 para cada grupo que desee que aparezca en el mapa del documento.  
  
7.  Haga clic en **Ejecutar**. El informe se ejecuta y el mapa del documento muestra los valores de grupo. Haga clic en cualquier vínculo para saltar a la página del informe que contiene ese elemento.  
  
##  <a name="HideMapWhenViewRpt"></a>   
#### <a name="to-hide-the-document-map-when-you-view-a-report"></a>Para ocultar el mapa del documento al ver un informe  
  
1.  En el portal web, busque el informe que contiene el mapa del documento.  
  
     Por ejemplo, para los informes de ejemplo de [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] , la dirección URL siguiente especifica el informe denominado Product Catalog.  
  
    ```  
    https://localhost/Reports/Pages/Report.aspx?ItemPath=%2fAdventureWorks2012+Sample+Reports%2fProduct+Catalog  
    ```  
  
2.  Copie la ruta de acceso del informe en el servidor. En el ejemplo, la ruta de acceso del informe es `%2fAdventureWorks2012+Sample+Reports%2fProduct+Catalog`.  
  
3.  Cree una nueva dirección URL con los tres componentes siguientes:  
  
    -   El visor de informes en el servidor de informes: `https://localhost/ReportServer/Pages/ReportViewer.aspx?`  
  
    -   El nombre del informe que copió en el paso 1, por ejemplo: `%2fAdventureWorks2012+Sample+Reports%2fProduct+Catalog`  
  
    -   Los parámetros de información de dispositivo que especifican que se oculte el mapa del documento: `&rs%3aCommand=Render&rc%3aFormat=HTML4.0&rc%3aDocMap=False`  
  
     La dirección URL siguiente consta de estos tres componentes anexados en el orden de la lista.  
  
    ```  
    https://localhost/ReportServer/Pages/ReportViewer.aspx?  
    %2fAdventureWorks2012+Sample+Reports%2fProduct+Catalog  
    &rs%3aCommand=Render&rc%3aFormat=HTML4.0&rc%3aDocMap=False  
    ```  
  
     Para usar esta dirección URL, cópiela y quite todos los saltos de línea.  
  
4.  Pegue la dirección URL en el portal web y, después, presione ENTRAR. El informe se ejecuta con el mapa del documento oculto.  
  
> [!NOTE]  
>  Para obtener más información sobre cómo descargar los informes de ejemplo, consulte [Informes de ejemplo del Generador de informes y el Diseñador de informes](https://go.microsoft.com/fwlink/?LinkId=198283).  
>   
>  Para obtener más información, vea el tema acerca del acceso URL en la [documentación de Reporting Services](https://go.microsoft.com/fwlink/?linkid=121312) en los Libros en pantalla de SQL Server.  


¿Tiene alguna pregunta más? [Puede plantear sus dudas en el foro de Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231).
