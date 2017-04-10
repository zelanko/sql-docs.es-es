---
title: "Ocultar o eliminar niveles en una jerarqu&#237;a derivada (Master Data Services) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "jerarquías derivadas, ocultar niveles"
  - "jerarquías derivadas, eliminar niveles"
ms.assetid: e00582b9-9415-4b66-b4a7-9f590d83875f
caps.latest.revision: 6
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 6
---
# Ocultar o eliminar niveles en una jerarqu&#237;a derivada (Master Data Services)
  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], oculte un nivel en una jerarquía derivada cuando requiera el nivel para agrupar, pero no necesite mostrarlo. Elimine un nivel cuando no desee usarlo para la agrupación.  
  
## Requisitos previos  
 Para realizar este procedimiento:  
  
-   Debe disponer de permiso para tener acceso al área funcional de **Administración del sistema** .  
  
-   Debe ser administrador de modelo. Para obtener más información, vea [Administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
### Para ocultar o eliminar niveles en una jerarquía derivada  
  
1.  En [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], haga clic en **Administración del sistema**.  
  
2.  En la barra de menús, seleccione **Administrar** y haga clic en **Jerarquías derivadas**.  
  
3.  En la página **Mantenimiento de jerarquías derivadas** , en la lista **Modelo** , seleccione un modelo.  
  
4.  Seleccione la fila de la jerarquía derivada que desea modificar.  
  
5.  Haga clic en **Editar**.  
  
6.  En el panel **Niveles actuales** :  
  
    -   Para ocultar un nivel, haga clic en un nivel distinto de la parte superior o inferior. En la lista **Visible** , seleccione **No**. A continuación, haga clic en **Guardar elemento de jerarquía seleccionado**.  
  
    -   Para eliminar el nivel superior, haga clic en **Eliminar elemento de jerarquía seleccionado**. En el cuadro de diálogo de confirmación, haga clic en **Aceptar**. Solo puede eliminar el nivel superior.  
  
## Vea también  
 [Mover miembros dentro de una jerarquía &#40;Master Data Services&#41;](../Topic/Move%20Members%20within%20a%20Hierarchy%20\(Master%20Data%20Services\).md)   
 [Jerarquías derivadas &#40;Master Data Services&#41;](../master-data-services/derived-hierarchies-master-data-services.md)  
  
  