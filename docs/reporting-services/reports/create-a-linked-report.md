---
title: "Crear un informe vinculado | Microsoft Docs"
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
  - "informes vinculados [Reporting Services], crear"
ms.assetid: 12be8341-cb57-45e8-a421-2bf66b50234d
caps.latest.revision: 44
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 44
---
# Crear un informe vinculado
  Un informe vinculado es un elemento del servidor de informes que proporciona un punto de acceso a un informe existente. Conceptualmente, es similar a los accesos directos a programa que se usan para ejecutar un programa o abrir un archivo.  
  
 Un informe vinculado se deriva de otro informe existente y conserva la definición de informe original. El informe vinculado siempre hereda el diseño de informe y las propiedades del origen de datos del informe original. El resto de propiedades y parámetros pueden ser distintos de los del informe original, incluyendo la seguridad, los parámetros, la ubicación, las suscripciones y las programaciones.  
  
 Se puede crear un informe vinculado cuando se desean crear versiones adicionales de un informe existente. Por ejemplo, se podría usar un único informe de ventas regional para crear informes específicos de regiones para todos los territorios de ventas.  
  
 Si bien los informes vinculados se basan normalmente en informes con parámetros, no es necesario disponer de este tipo de informe. Puede crear informes vinculados siempre que desee implementar un informe existente con diferentes parámetros.  
  
### Crear un informe vinculado  
  
1.  En el Administrador de informes, navegue hasta la carpeta que contiene el informe al que desea vincular y, a continuación, abra el menú de opciones para hacer clic en **Crear informe vinculado**.  
  
2.  Escriba un nombre para el nuevo informe vinculado. Si lo desea, escriba una descripción.  
  
3.  Para guardar el informe en una carpeta diferente, haga clic en **Cambiar ubicación**. Haga clic en la carpeta que desee utilizar o escriba el nombre de la carpeta en el cuadro **Ubicación** . [!INCLUDE[clickOK](../../includes/clickok-md.md)] Si no selecciona una carpeta distinta, el informe vinculado se creará en la carpeta actual (donde está almacenado el informe en que se basa).  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)] Se abre el informe vinculado.  
  
     El icono de un informe vinculado es distinto de otros elementos administrados por un servidor de informes. El siguiente icono distingue los informes vinculados:  
  
     ![Icono de informe vinculado](../../reporting-services/report-server/media/hlp-16linked.png "Icono de informe vinculado")  
  
## Vea también  
 [Abrir y cerrar un informe &#40;Administrador de informes&#41;](../../reporting-services/reports/open-and-close-a-report-report-manager.md)   
 [Nuevo informe vinculado &#40;página del Administrador de informes&#41;](../Topic/New%20Linked%20Report%20Page%20\(Report%20Manager\).md)   
 [Elegir página de ubicación del elemento &#40;Administrador de informes&#41;](../Topic/Choose%20Item%20Location%20Page%20\(Report%20Manager\).md)   
 [Página de propiedades generales, informes &#40;Administrador de informes&#41;](../Topic/General%20Properties%20Page,%20Reports%20\(Report%20Manager\).md)   
 [Conceptos de Reporting Services &#40;SSRS&#41;](../../reporting-services/reporting-services-concepts-ssrs.md)   
 [Administrador de informes &#40;Modo nativo de SSRS&#41;](../Topic/Report%20Manager%20%20\(SSRS%20Native%20Mode\).md)  
  
  