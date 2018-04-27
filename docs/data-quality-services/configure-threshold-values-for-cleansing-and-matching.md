---
title: Configurar los valores de umbral para la limpieza y la coincidencia | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.service: ''
ms.component: data-quality-services
ms.reviewer: ''
ms.suite: sql
ms.technology:
- data-quality-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.dqs.admin.config.general.f1
helpviewer_keywords:
- cleansing,threshold value
- cleansing threshold values
- matching,threshold value
ms.assetid: d2305409-7115-45a4-8f60-1213c0a47368
caps.latest.revision: 9
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5c6e3af5037c2a69d9ebea9dfda39a70fcc03b42
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="configure-threshold-values-for-cleansing-and-matching"></a>Configurar los valores de umbral para la limpieza y coincidencia

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  En este tema se describe cómo configurar los valores de umbral que se utilizarán durante las actividades de limpieza y búsqueda de coincidencias asistidas por PC en [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS).  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permissions  
 Para configurar estos valores de umbral, debe disponer del rol dqs_administrator en la base de datos DQS_MAIN.  
  
##  <a name="Configure"></a> Configurar los valores de umbral  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Ejecute la aplicación Data Quality Client](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  En la página de inicio de [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , haga clic en **Configuración**.  
  
3.  A continuación, haga clic en la pestaña **Configuración general** . Esta pestaña le permite especificar los valores de umbral para las actividades de limpieza y búsqueda de coincidencias.  
  
4.  Para establecer los valores de umbral para la actividad de limpieza, especifique los valores adecuados en los cuadros siguientes del área **Limpieza interactiva** :  
  
    -   **Puntuación mínima para sugerencias**: la puntuación mínima o el nivel de confianza que utilizará DQS para sugerir reemplazos para un valor durante el proceso de limpieza asistida por PC. Escriba un valor en la notación decimal del valor de porcentaje correspondiente. Por ejemplo, escriba 0,75 para un porcentaje del 75%. Este valor debe ser menor o igual que el valor especificado en el cuadro **Puntuación mínima de correcciones automáticas** . El valor predeterminado es 0,7.  
  
    -   **Puntuación mínima de correcciones automáticas**: la puntuación mínima o el nivel de confianza que utilizará DQS para corregir automáticamente un valor durante el proceso de limpieza asistida por PC. Escriba un valor en la notación decimal del valor de porcentaje correspondiente. Por ejemplo, escriba 0,9 para un porcentaje del 90%. El valor predeterminado es 0,8.  
  
5.  Para establecer el valor de umbral para la actividad de búsqueda de coincidencias, especifique un valor en el cuadro **Puntuación de registro mínima** en el área **Coincidencia** . Este valor indica la puntuación mínima necesaria para que un registro se considere como una coincidencia de otro. El valor predeterminado es 80 %.  
  
6.  Haga clic en **Cerrar**.  
  
  
