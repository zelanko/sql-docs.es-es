---
title: Agregar un registro de contadores de rendimiento del flujo de datos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- performance counters [Integration Services]
- counters [Integration Services]
- logs [Integration Services], data flow counters
ms.assetid: b500d166-33ba-4b82-a92d-b0a333924e8d
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 9d22bbe58ac04786186a4b8cca7e51a61ea5b66e
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/22/2019
ms.locfileid: "58379123"
---
# <a name="add-a-log-for-data-flow-performance-counters"></a>Agregar un registro para los contadores de rendimiento del flujo de datos
  Este procedimiento describe cómo agregar un registro para los contadores de rendimiento que proporciona el motor de flujo de datos.  
  
> [!NOTE]  
>  Si instala [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] en un equipo que está ejecutando [!INCLUDE[winxpsvr](../includes/winxpsvr-md.md)]y, a continuación, actualiza el equipo a [!INCLUDE[firstref_longhorn](../includes/firstref-longhorn-md.md)], el proceso de actualización quita del equipo los contadores de rendimiento de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . Para restaurar en el equipo los contadores de rendimiento de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , ejecute el programa de instalación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en modo de reparación.  
  
### <a name="to-add-logging-of-performance-counters"></a>Para agregar un registro de contadores de rendimiento  
  
1.  En el **Panel de control**, si utiliza la Vista clásica, haga clic en **Herramientas administrativas**. Si utiliza la Vista por categorías, haga clic en **Rendimiento y mantenimiento** y, a continuación, en **Herramientas administrativas**.  
  
2.  Haga clic en **Rendimiento**.  
  
3.  En el cuadro de diálogo **Rendimiento** , expanda **Registros y alertas de rendimiento**, haga clic con el botón derecho en **Registros de contador**y, después, haga clic en **Nueva configuración de registro**. Escriba el nombre del registro. Por ejemplo, escriba **miRegistro**.  
  
4.  Haga clic en **Aceptar**.  
  
5.  En el cuadro de diálogo **miRegistro** , haga clic en **Agregar contadores**.  
  
6.  Haga clic en **Usar contadores del equipo local** para registrar los contadores de rendimiento en el equipo local o bien, haga clic en **Seleccionar contadores del equipo** y seleccione un equipo de la lista para registrar los contadores de rendimiento en el equipo especificado.  
  
7.  En el cuadro de diálogo **Agregar contadores** , seleccione **SQL Server:SSIS Pipeline** en la lista **Objeto de rendimiento** .  
  
8.  Para seleccionar los contadores de rendimiento, siga uno de estos procedimientos:  
  
    -   Seleccione **Todos los contadores** para registrar todos los contadores de rendimiento.  
  
    -   Elija **Seleccionar contadores de la lista** y seleccione los contadores de rendimiento que desee utilizar.  
  
9. Haga clic en **Agregar**.  
  
10. Haga clic en **Cerrar**.  
  
11. En el cuadro de diálogo **miRegistro** , revise la lista de contadores de rendimiento del registro en la lista **Contadores** .  
  
12. Para agregar más contadores, repita los pasos 5 a 10.  
  
13. Haga clic en **Aceptar**.  
  
    > [!NOTE]  
    >  Debe iniciar el servicio Registros y alertas de rendimiento con una cuenta local o de dominio que sea miembro del grupo Administradores.  
  
## <a name="see-also"></a>Vea también  
 [Performance Counters](performance/performance-counters.md)   
 [Ver entradas del registro en la ventana Registrar eventos](../../2014/integration-services/view-log-entries-in-the-log-events-window.md)  
  
  
