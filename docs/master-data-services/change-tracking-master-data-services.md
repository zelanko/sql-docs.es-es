---
title: "Seguimiento de cambios [Master Data Services] | Microsoft Docs"
ms.custom: ""
ms.date: "03/15/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "seguimiento de cambios [SQL Server]"
ms.assetid: 5e879c65-0d38-454f-9a20-62a6e72c89f7
caps.latest.revision: 7
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 7
---
# Seguimiento de cambios [Master Data Services]
  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], puede usar grupos de seguimiento de cambios para realizar una acción cuando cambie un valor de atributo. Use el seguimiento de cambios cuando no conozca cuál será el nuevo valor, pero desee, sin embargo, saber si se produjo algún cambio.  
  
## Configurar el seguimiento de cambios  
 Para configurar el seguimiento de cambios, agregue un atributo a un grupo de seguimiento de cambios. El grupo puede contener uno o muchos atributos. A continuación, cree una regla de negocios para definir la acción que se realizará cuando alguno de los atributos del grupo cambie.  
  
> [!NOTE]  
>  Las reglas de negocios del seguimiento de cambios consideran los cambios en lo datos almacenados (importados) provisionalmente.  
  
## Tareas relacionadas  
  
|Descripción de la tarea|Tema|  
|----------------------|-----------|  
|Agregar atributos a un grupo de seguimiento de cambios.|[Agregar atributos a un grupo de seguimiento de cambios &#40;Master Data Services&#41;](../master-data-services/add-attributes-to-a-change-tracking-group-master-data-services.md)|  
|Crear una regla de negocios para iniciar acciones según los cambios en los atributos.|[Iniciar acciones según los cambios de valores de atributos &#40;Master Data Services&#41;](../master-data-services/initiate-actions-based-on-attribute-value-changes-master-data-services.md)|  
  
## Contenido relacionado  
  
-   [Validación &#40;Master Data Services&#41;](../master-data-services/validation-master-data-services.md)  
  
-   [Reglas de negocios &#40;Master Data Services&#41;](../master-data-services/business-rules-master-data-services.md)  
  
-   [Atributos &#40;Master Data Services&#41;](../master-data-services/attributes-master-data-services.md)  
  
  