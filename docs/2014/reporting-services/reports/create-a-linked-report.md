---
title: Crear un informe vinculado | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- linked reports [Reporting Services], creating
ms.assetid: 12be8341-cb57-45e8-a421-2bf66b50234d
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 36abfdc4ea1be04b45c834fde91762c035e0b9c9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63288511"
---
# <a name="create-a-linked-report"></a>Crear un informe vinculado
  Un informe vinculado es un elemento del servidor de informes que proporciona un punto de acceso a un informe existente. Conceptualmente, es similar a los accesos directos a programa que se usan para ejecutar un programa o abrir un archivo.  
  
 Un informe vinculado se deriva de otro informe existente y conserva la definición de informe original. El informe vinculado siempre hereda el diseño de informe y las propiedades del origen de datos del informe original. El resto de propiedades y parámetros pueden ser distintos de los del informe original, incluyendo la seguridad, los parámetros, la ubicación, las suscripciones y las programaciones.  
  
 Se puede crear un informe vinculado cuando se desean crear versiones adicionales de un informe existente. Por ejemplo, se podría usar un único informe de ventas regional para crear informes específicos de regiones para todos los territorios de ventas.  
  
 Si bien los informes vinculados se basan normalmente en informes con parámetros, no es necesario disponer de este tipo de informe. Puede crear informes vinculados siempre que desee implementar un informe existente con diferentes parámetros.  
  
### <a name="to-create-a-linked-report"></a>Crear un informe vinculado  
  
1.  En el Administrador de informes, navegue hasta la carpeta que contiene el informe al que desea vincular y, a continuación, abra el menú de opciones para hacer clic en **Crear informe vinculado**.  
  
2.  Escriba un nombre para el nuevo informe vinculado. Si lo desea, escriba una descripción.  
  
3.  Para guardar el informe en una carpeta diferente, haga clic en **Cambiar ubicación**. Haga clic en la carpeta que desee utilizar o escriba el nombre de la carpeta en el cuadro **Ubicación** . [!INCLUDE[clickOK](../../../includes/clickok-md.md)] Si no selecciona una carpeta distinta, el informe vinculado se creará en la carpeta actual (donde está almacenado el informe en que se basa).  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)] Se abre el informe vinculado.  
  
     El icono de un informe vinculado es distinto de otros elementos administrados por un servidor de informes. El siguiente icono distingue los informes vinculados:  
  
     ![Icono de informe vinculado](../media/hlp-16linked.gif "Icono de informe vinculado")  
  
## <a name="see-also"></a>Vea también  
 [Abrir y cerrar un informe &#40;Administrador de informes&#41;](../reports/open-and-close-a-report-report-manager.md)   
 [Nuevo informe vinculado &#40;página del Administrador de informes&#41;](../new-linked-report-page-report-manager.md)   
 [Elegir página de ubicación del elemento &#40;Administrador de informes&#41;](../choose-item-location-page-report-manager.md)   
 [Página de propiedades generales, informes &#40;Administrador de informes&#41;](../general-properties-page-reports-report-manager.md)   
 [Conceptos de Reporting Services &#40;SSRS&#41;](../reporting-services-concepts-ssrs.md)   
 [Administrador de informes &#40;Modo nativo de SSRS&#41;](../report-manager-ssrs-native-mode.md)  
  
  
