---
title: "Lecci&#243;n 14: Implementar | Microsoft Docs"
ms.custom: ""
ms.date: "02/27/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
applies_to: 
  - "SQL Server 2016"
ms.assetid: 24863a8a-9017-415a-a97b-fbac76ed0675
caps.latest.revision: 25
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Lecci&#243;n 14: Implementar
En esta lección, configurará propiedades de implementación, especificará una instancia del servidor de implementación de Analysis Services que se ejecute en modo tabular y asignará un nombre al modelo que va a implementar. A continuación, implementará el modelo en esa instancia. Una vez implementado, los usuarios podrán conectarse al modelo mediante una aplicación cliente de informes. Para obtener más información, vea [Implementación de soluciones de modelos tabulares &#40;SSAS tabular&#41;](../analysis-services/tabular-models/tabular-model-solution-deployment-ssas-tabular.md).  
  
Tiempo estimado para completar esta lección: **5 minutos**  
  
## Requisitos previos  
Este tema es parte de un tutorial de creación de modelos tabulares, que se debe completar en orden. Antes de realizar las tareas de esta lección, debe haber completado la lección anterior: [Lección 13: Analizar en Excel](../analysis-services/lesson-13-analyze-in-excel.md).  
  
## Implementar el modelo  
  
#### Para configurar propiedades de implementación  
  
1.  En [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], en **Explorador de soluciones**, haga clic con el botón derecho en **Modelo tabular de ventas por Internet de Adventure Works** y, en el menú contextual, haga clic en **Propiedades**.  
  
2.  En el cuadro de diálogo **Páginas de propiedades del modelo tabular de ventas por Internet de AW**, bajo **Servidor de implementación**, en la propiedad **Server**, escriba el nombre de una instancia de Analysis Services que se ejecute en modo Tabular. Esta será la instancia en la que se implementará el modelo.  
  
    > [!IMPORTANT]  
    > Debe tener permisos de administrador en una instancia de Analysis Services remota para poder implementarlo.  
  
3.  En la propiedad **Database**, escriba **Modelo de ventas por Internet de Adventure Works**.  
  
4.  En la propiedad **Cube name**, escriba **Modelo de ventas por Internet de Adventure Works**.  
  
5.  Compruebe las opciones seleccionadas y, después, haga clic en **Aceptar**.  
  
#### Para implementar el modelo tabular Ventas por Internet de Adventure Works  
  
1.  En [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], haga clic en el menú **Generar** y, después, haga clic en **Implementar modelo tabular de ventas por Internet de AW**.  
  
    Aparece el cuadro de diálogo Implementar en el que se muestra el estado de implementación de los metadatos y las tablas incluidas en el modelo.  
  
2. Cuando se complete correctamente la implementación, continúe y haga clic en **Cerrar**.  
  
## Conclusión  
¡Enhorabuena! Ha terminado de crear e implementar su primer modelo tabular de Analysis Services. Este tutorial le ha guiado por las tareas más comunes para crear un modelo tabular. Ahora que su modelo Ventas por Internet de Adventure Works está implementado, puede utilizar el SQL Server Management Studio para administrarlo, crear scripts de proceso y realizar un plan de copia de seguridad. Los usuarios pueden conectarse al modelo mediante una aplicación cliente de informes como Microsoft Excel o [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)].  
  
## Recursos adicionales  
Para obtener más información sobre las propiedades de modelo tabular que admiten informes de [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)], vea [Propiedades de informes de Power View &#40;SSAS tabular&#41;](../analysis-services/tabular-models/power-view-reporting-properties-ssas-tabular.md).  
  
## Vea también  
[Modo DirectQuery &#40;SSAS tabular&#41;](../analysis-services/tabular-models/directquery-mode-ssas-tabular.md)  
[Configurar las propiedades predeterminadas de modelado de datos y de implementación &#40;SSAS tabular&#41;](../analysis-services/tabular-models/configure-default-data-modeling-and-deployment-properties-ssas-tabular.md)  
[Bases de datos de modelo tabular &#40;SSAS tabular&#41;](../analysis-services/tabular-models/tabular-model-databases-ssas-tabular.md)  
  
  
  
