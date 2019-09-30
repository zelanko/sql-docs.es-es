---
title: Copiar objetos de paquete | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- control flow [Integration Services], copying objects
- copying package objects [Integration Services]
- data flow [Integration Services], copying objects
- connection managers [Integration Services], copying
ms.assetid: 99b85e5c-d6bd-4e7c-afe4-51f6ce151c2f
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 4636dde3123cc3742a7dde57fa2a468583e2f2bd
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/26/2019
ms.locfileid: "71293599"
---
# <a name="copy-package-objects"></a>Copiar objetos de paquete

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Este tema describe el modo de copiar elementos de flujo de control, elementos de flujo de datos y administradores de conexión dentro de un paquete o entre paquetes.  
  
### <a name="to-copy-control-and-data-flow-items"></a>Para copiar elementos de flujo de control y de datos  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contiene los paquetes con los que desea trabajar.  
  
2.  En el Explorador de soluciones, haga doble clic en los paquetes entre los que desea copiar.  
  
3.  En el Diseñador [!INCLUDE[ssIS](../includes/ssis-md.md)] , haga clic en la pestaña del paquete que contiene los elementos que desea copiar y haga clic en la pestaña **Flujo de control**, **Flujo de datos**o **Controladores de eventos** .  
  
4.  Seleccione los elementos del flujo de control o del flujo de datos que desee copiar. Puede seleccionar elementos de a uno por vez presionando la tecla Mayús y haciendo clic en el elemento, o puede seleccionar un grupo de elementos arrastrando el puntero a través de los elementos que desea seleccionar.  
  
    > [!IMPORTANT]  
    >  Las restricciones de precedencia y rutas de acceso que conectan elementos no se seleccionan automáticamente cuando selecciona los dos elementos que conectan. Para copiar un flujo de trabajo ordenado (un segmento del flujo de control o de flujo de datos), asegúrese también de copiar las restricciones de precedencia y las rutas de acceso.  
  
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
  
## <a name="see-also"></a>Consulte también  
 [Flujo de control](../integration-services/control-flow/control-flow.md)   
 [Flujo de datos](../integration-services/data-flow/data-flow.md)   
 [Conexiones de Integration Services &#40;SSIS&#41;](../integration-services/connection-manager/integration-services-ssis-connections.md)   
 [Copiar los elementos de proyectos](https://msdn.microsoft.com/library/1606c54d-20f9-49f3-a4ef-caad83a772aa)  
  
  
