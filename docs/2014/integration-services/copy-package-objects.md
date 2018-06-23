---
title: Copiar objetos de paquete | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- control flow [Integration Services], copying objects
- copying package objects [Integration Services]
- data flow [Integration Services], copying objects
- connection managers [Integration Services], copying
ms.assetid: 99b85e5c-d6bd-4e7c-afe4-51f6ce151c2f
caps.latest.revision: 13
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 17d8bf1d2297ac9ddbee9a4d393fa84cd3ee1236
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36199423"
---
# <a name="copy-package-objects"></a>Copiar objetos de paquete
  Este tema describe el modo de copiar elementos de flujo de control, elementos de flujo de datos y administradores de conexión dentro de un paquete o entre paquetes.  
  
### <a name="to-copy-control-and-data-flow-items"></a>Para copiar elementos de flujo de control y de datos  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contiene los paquetes con los que desea trabajar.  
  
2.  En el Explorador de soluciones, haga doble clic en los paquetes entre los que desea copiar.  
  
3.  En el Diseñador [!INCLUDE[ssIS](../includes/ssis-md.md)] , haga clic en la pestaña del paquete que contiene los elementos que desea copiar y haga clic en la pestaña **Flujo de control**, **Flujo de datos**o **Controladores de eventos** .  
  
4.  Seleccione los elementos del flujo de control o del flujo de datos que desee copiar. Puede seleccionar elementos de a uno por vez presionando la tecla Mayús y haciendo clic en el elemento, o puede seleccionar un grupo de elementos arrastrando el puntero a través de los elementos que desea seleccionar.  
  
    > [!IMPORTANT]  
    >  Las restricciones de precedencia y rutas de acceso que conectan elementos no se seleccionan automáticamente cuando selecciona los dos elementos que conectan. Para copiar un flujo de datos ordenado (un segmento del flujo de control o del flujo de datos), asegúrese también de copiar las restricciones de precedencia y las rutas de acceso.  
  
5.  Haga clic con el botón derecho en un elemento seleccionado y, después, haga clic en **Copiar**.  
  
6.  Si va a copiar elementos a un paquete diferente, haga clic en el paquete al que desea copiar y luego haga clic en la pestaña correspondiente para el tipo de elemento.  
  
    > [!IMPORTANT]  
    >  No puede copiar un flujo de datos a un paquete, a no ser que el paquete contenga al menos una tarea Flujo de datos.  
  
7.  Haga clic con el botón derecho y, luego, haga clic en **Pegar**.  
  
### <a name="to-copy-connection-managers"></a>Para copiar administradores de conexión  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contiene el paquete con el que desea trabajar.  
  
2.  En el Explorador de soluciones, haga doble clic en el paquete.  
  
3.  En el Diseñador [!INCLUDE[ssIS](../includes/ssis-md.md)] , haga clic en las pestañas **Flujo de control**, **Flujo de datos**o **Controlador de eventos** .  
  
4.  En el área **Administradores de conexiones** , haga clic con el botón derecho en el administrador de conexiones y, luego, haga clic en **Copiar**. Solo puede copiar un administrador de conexiones cada vez.  
  
5.  Si va a copiar elementos a un paquete diferente, haga clic en el paquete que desea copiar y, a continuación, en la pestaña **Flujo de control**, **Flujo de datos**o **Controlador de eventos** .  
  
6.  Haga clic con el botón derecho en el área **Administradores de conexiones** y, luego, haga clic en **Pegar**.  
  
## <a name="see-also"></a>Vea también  
 [Flujo de control](control-flow/control-flow.md)   
 [Flujo de datos](data-flow/data-flow.md)   
 [Conexiones de Integration Services &#40;SSIS&#41;](connection-manager/integration-services-ssis-connections.md)   
 [Copiar elementos de proyecto](../../2014/integration-services/copy-project-items.md)  
  
  