---
title: "Mover o eliminar un elemento (Administrador de informes) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "mover elementos"
  - "elementos [Reporting Services], mover"
ms.assetid: 980a66c7-a18b-4af7-8954-45726fa517d6
caps.latest.revision: 45
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 45
---
# Mover o eliminar un elemento (Administrador de informes)
  Los informes y los elementos relacionados con los informes que se publican en un servidor de informes se almacenan en carpetas. Puede mover los elementos a una carpeta diferente, y el servidor de informes se ocupará de mantener las referencias a ellos automáticamente. Antes de eliminar un elemento, piense si otros elementos dependen de él.  
  
## Mover un elemento  
 Puede mover elementos del servidor de informes a diversas ubicaciones de carpeta en la jerarquía de carpetas del servidor de informes. Al mover un elemento, también se mueven todas las propiedades (incluida la configuración de seguridad) a la nueva ubicación. Cuando mueve una carpeta, se mueven todos los elementos de la carpeta.  
  
 En el Administrador de informes, los elementos que se pueden mover aparecen indicados en la jerarquía de carpetas. La siguiente tabla muestra el icono correspondiente a cada uno de los elementos que se pueden mover.  
  
|Icono|Elemento que puede moverse|  
|----------|-------------------|  
|![Icono de informe](../../reporting-services/report-server/media/hlp-16doc.png "Icono de informe")|Informe|  
|![Icono de informe vinculado](../../reporting-services/report-server/media/hlp-16linked.png "Icono de informe vinculado")|Informe vinculado|  
|![Icono de carpeta](../../reporting-services/report-server/media/hlp-16folder.png "Icono de carpeta")|Carpeta|  
|![Icono de recurso genérico](../../reporting-services/report-server/media/hlp-16file.png "Icono de recurso genérico")|Recurso genérico|  
|![Icono de origen de datos compartido](../../reporting-services/report-data/media/hlp-16datasource.png "Icono de origen de datos compartido")|Origen de datos compartido|  
||Conjunto de datos compartidos|  
  
 No todos los elementos se pueden mover. Por ejemplo, los elementos asociados a un informe, tales como las suscripciones o el historial del informe, no pueden moverse. Estos elementos se mueven con los informes asociados. Asimismo, tampoco pueden moverse elementos como las programaciones compartidas que existen fuera de la jerarquía de carpetas. No pueden moverse elementos para los que no se tienen los permisos adecuados. Este permiso se concede mediante la selección de las siguientes tareas durante la asignación de roles del elemento en cuestión: "Administrar informes", "Administrar modelos", "Administrar carpetas" y "Administrar orígenes de datos".  
  
#### Para mover un elemento de la página Contenido  
  
1.  Inicie el [Administrador de informes &#40;Modo nativo de SSRS&#41;](../Topic/Report%20Manager%20%20\(SSRS%20Native%20Mode\).md).  
  
2.  En el Administrador de informes, navegue a la página **Contenido** y localice el elemento que desee mover.  
  
3.  Mantenga el mouse sobre el elemento y haga clic en la flecha de lista desplegable.  
  
4.  En el menú desplegable, haga clic en **Mover**.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
6.  Para **Ubicación**, especifique la carpeta a la que desea mover el elemento. Puede escribir el nombre completo de la carpeta o utilizar el control de árbol para navegar hasta la carpeta.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 O bien puede navegar hasta el objeto que desea mover, hacer clic en **Propiedades**y, a continuación, en **Mover** al principio de la página.  
  
## Eliminar un elemento  
 Antes de eliminar un elemento, piense si lo utilizan otros elementos. Por ejemplo, si elimina un origen de datos compartido, ya no se ejecutarán los informes y los modelos que usan dicho origen de datos. Si elimina un informe, también se eliminarán las suscripciones y el historial de informes asociado a dicho informe. Para buscar elementos dependientes para un elemento, vea [Página de elementos dependientes &#40;Administrador de informes&#41;](../Topic/Dependent%20Items%20Page%20\(Report%20Manager\).md).  
  
#### Para eliminar un informe o un elemento  
  
1.  Inicie el [Administrador de informes &#40;Modo nativo de SSRS&#41;](../Topic/Report%20Manager%20%20\(SSRS%20Native%20Mode\).md).  
  
2.  En el Administrador de informes, navegue a la página **Contenido** y localice el elemento que desee eliminar.  
  
3.  Mantenga el mouse sobre el elemento y haga clic en la flecha de lista desplegable.  
  
4.  En el menú desplegable, haga clic en **Eliminar**.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## Vea también  
 [Contenido &#40;página del Administrador de informes&#41;](../Topic/Contents%20Page%20\(Report%20Manager\).md)   
 [Buscar, ver y administrar informes &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)  
  
  