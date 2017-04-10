---
title: "Creaci&#243;n de un &#237;ndice personalizado (Master Data Services) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d694a105-69b1-4ff6-99d3-1f408b916b81
caps.latest.revision: 6
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 6
---
# Creaci&#243;n de un &#237;ndice personalizado (Master Data Services)
  Cree un índice personalizado en una lista de atributos que se consulta con frecuencia para mejorar el rendimiento de las consultas.  
  
## Requisitos previos  
 Para realizar este procedimiento:  
  
-   Debe disponer de permiso para tener acceso al área funcional de Administración del sistema. Para obtener más información, consulte [Permisos del área funcional &#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md).  
  
-   Debe ser administrador de modelo. Para obtener más información, vea [Administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
 **Para crear un índice**  
  
1.  En Master Data Manager, haga clic en **Administración del sistema**.  
  
2.  En la página **Manage Model** (Administrar modelo), seleccione un modelo de la cuadrícula y después haga clic en **Entidades**.  
  
3.  En la página **Manage Entity** (Administrar entidad), en la **cuadrícula** , seleccione la fila de la entidad para la que desea crear un índice.  
  
4.  Haga clic en **Índices**.  
  
5.  En el cuadro **Nombre** , escriba un nombre para el índice.  
  
6.  Seleccione **Is Unique** (Es único) si desea crear un índice único. Para obtener más información sobre los tipos de índices, consulte [Índice personalizado &#40;Master Data Services&#41;](../master-data-services/custom-index-master-data-services.md).  
  
7.  Haga clic en los atributos en el cuadro **Atributos disponibles** y luego haga clic en la flecha **Agregar** . Para agregar todos los atributos, haga clic en la flecha **Agregar todo** .  
  
8.  Haga clic en **Guardar**.  
  
 Por cada índice creado, se agrega una fila con cuatro columnas a la cuadrícula. En la siguiente tabla se describen las columnas.  
  
|Nombre de la columna|Description|  
|-----------------|-----------------|  
|Estado|El estado del índice.<br /><br /> Al hacer clic en **Guardar**, se muestra la imagen ![Icon for updating status](../master-data-services/media/mds-statusicon-updating.png "Icon for updating status"), lo que indica que el índice se está actualizando.<br /><br /> Si aparecen errores al crear o editar un índice, se muestra la imagen ![Icon for error status](../master-data-services/media/mds-statusicon-error.png "Icon for error status").<br /><br /> De lo contrario, el estado es correcto y se muestra la imagen ![Icon for OK status](../master-data-services/media/mds-statusicon-ok.png "Icon for OK status").|  
|Nombre|Nombre de índice.|  
|Is Unique|Especifica si el índice es único.|  
|En atributos|Muestra los nombres para mostrar de los atributos en los que está definido el índice.|  
  
 Cuando se hace clic en un índice, se muestra la siguiente información.  
  
-   **Creado por:**Nombre del usuario que creó el índice.  
  
-   **El:**Fecha y hora en que se creó el índice.  
  
-   **Actualizado por:**Nombre del usuario que actualizó el índice por última vez.  
  
-   **El:**Fecha y hora en que se el índice se actualizó por última vez.  
  
## Pasos siguientes  
 [Editar y eliminar un índice &#40;Master Data Services&#41;](../master-data-services/edit-and-delete-an-index-master-data-services.md)  
  
## Vea también  
 [Índice personalizado &#40;Master Data Services&#41;](../master-data-services/custom-index-master-data-services.md)  
  
  