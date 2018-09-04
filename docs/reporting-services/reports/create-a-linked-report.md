---
title: Crear un informe vinculado | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: reports
ms.suite: pro-bi
ms.topic: conceptual
helpviewer_keywords:
- linked reports [Reporting Services], creating
ms.assetid: 12be8341-cb57-45e8-a421-2bf66b50234d
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 2fe56792237235d86a6ac59c8ac5e3e98c8f961f
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/30/2018
ms.locfileid: "43265432"
---
# <a name="create-a-linked-report"></a>Crear un informe vinculado
  Un informe vinculado es un elemento del servidor de informes que proporciona un punto de acceso a un informe existente. Conceptualmente, es similar a los accesos directos a programa que se usan para ejecutar un programa o abrir un archivo.  
  
 Un informe vinculado se deriva de otro informe existente y conserva la definición de informe original. El informe vinculado siempre hereda el diseño de informe y las propiedades del origen de datos del informe original. El resto de propiedades y parámetros pueden ser distintos de los del informe original, incluyendo la seguridad, los parámetros, la ubicación, las suscripciones y las programaciones.  
  
 Se puede crear un informe vinculado cuando se desean crear versiones adicionales de un informe existente. Por ejemplo, se podría usar un único informe de ventas regional para crear informes específicos de regiones para todos los territorios de ventas.  
  
 Si bien los informes vinculados se basan normalmente en informes con parámetros, no es necesario disponer de este tipo de informe. Puede crear informes vinculados siempre que desee implementar un informe existente con diferentes parámetros.  
  
### <a name="to-create-a-linked-report"></a>Crear un informe vinculado  
  
1.  En el Administrador de informes, navegue hasta la carpeta que contiene el informe al que desea vincular y, a continuación, abra el menú de opciones para hacer clic en **Crear informe vinculado**.  
  
2.  Escriba un nombre para el nuevo informe vinculado. Si lo desea, escriba una descripción.  
  
3.  Para guardar el informe en una carpeta diferente, haga clic en **Cambiar ubicación**. Haga clic en la carpeta que desee utilizar o escriba el nombre de la carpeta en el cuadro **Ubicación** . [!INCLUDE[clickOK](../../includes/clickok-md.md)] Si no selecciona una carpeta distinta, el informe vinculado se creará en la carpeta actual (donde está almacenado el informe en que se basa).  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)] Se abre el informe vinculado.  
  
     El icono de un informe vinculado es distinto de otros elementos administrados por un servidor de informes. El siguiente icono distingue los informes vinculados:  
  
     ![Icono de informe vinculado](../../reporting-services/report-server/media/hlp-16linked.gif "Icono de informe vinculado")  
  
## <a name="see-also"></a>Ver también  
 [Abrir y cerrar un informe &#40;Administrador de informes&#41;](../../reporting-services/reports/open-and-close-a-report-report-manager.md)   
 [Nuevo informe vinculado &#40;página del Administrador de informes&#41;](http://msdn.microsoft.com/library/fefb46e8-6901-4d50-a3f8-7c49ad72e7b1)   
 [Elegir página de ubicación del elemento &#40;Administrador de informes&#41;](http://msdn.microsoft.com/library/4a53a1a8-d1e1-47ef-b1fc-63352ece7d3c)   
 [Página de propiedades generales, informes &#40;Administrador de informes&#41;](http://msdn.microsoft.com/library/66c99d28-ab41-45f0-bf02-ed560293595d)   
 [Conceptos de Reporting Services &#40;SSRS&#41;](../../reporting-services/reporting-services-concepts-ssrs.md)   
 [Administrador de informes &#40;Modo nativo de SSRS&#41;](http://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)  
  
  
