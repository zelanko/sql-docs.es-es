---
title: Configurar una alerta de base de datos de SQL Server (Windows) | Microsoft Docs
description: Obtenga información sobre cómo crear una alerta que se activará al alcanzar un valor de umbral de un contador del Monitor del sistema. En respuesta, el Monitor del sistema puede iniciar una aplicación.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- alerts [SQL Server], creating
ms.assetid: 65d2c5c1-921f-4eff-9ef7-149170ab61e8
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 982feaae1638250c80091778cdbacbfc21b0b3af
ms.sourcegitcommit: 9470c4d1fc8d2d9d08525c4f811282999d765e6e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/17/2020
ms.locfileid: "86458709"
---
# <a name="set-up-a-sql-server-database-alert-windows"></a>Configurar una alerta de base de datos de SQL Server (Windows)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  El Monitor del sistema permite crear una alerta que se activará al alcanzar un valor de umbral de un contador del Monitor del sistema. Como respuesta a la alerta, el Monitor del sistema puede iniciar una aplicación, como, por ejemplo, una aplicación personalizada creada para tratar la condición de alerta. Por ejemplo, puede crear una alerta que se active cuando el número de interbloqueos sea superior a un valor específico. 
  
 También se pueden definir alertas mediante Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] y el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para más información, consulte [Alertas](../../ssms/agent/alerts.md).  
  
## <a name="set-up-a-sql-server-database-alert"></a>Configurar una alerta de base de datos de SQL Server  
  
1. En el árbol de navegación de la ventana **Rendimiento**, expanda **Registros y alertas de rendimiento**.  
  
2. Haga clic con el botón derecho en **Alertas** y, después, seleccione **Nueva configuración de alerta**.
  
3. En el cuadro de diálogo **Nueva configuración de alerta**, escriba el nombre de la nueva alerta y, a continuación, seleccione **Aceptar**.  
  
4. En la pestaña **General** del cuadro de diálogo de la nueva alerta, agregue un **Comentario**. Seleccione **Agregar** para agregar un contador a la alerta.  
  
     Todas las alertas deben tener, como mínimo, un contador.  
  
5. En el cuadro de diálogo **Agregar contadores**, seleccione un objeto de SQL Server en la lista **Objeto de rendimiento**. Seleccione un contador en la lista **Seleccionar contadores de la lista**.  
  
6. Para agregar el contador a la alerta, seleccione **Agregar**. Puede continuar agregando contadores o seleccionar **Cerrar** para volver al cuadro de diálogo de la nueva alerta.  
  
7. En el cuadro de diálogo de la alerta nueva, seleccione **Superior a** o **Inferior a** en la lista **Alert when the value is** (Alertar cando el valor sea). A continuación, escriba un valor de umbral en **Límite**.  
  
     La alerta se genera cuando el valor del contador es superior o inferior al valor de umbral, dependiendo de si seleccionó **Superior a** o **Inferior a**.  
  
8. En los cuadros **Tomar datos de muestra cada** , establezca la frecuencia de muestreo.  
  
9. En la pestaña **Acción** , establezca las acciones que tendrán lugar cada vez que se desencadene la alerta.  
  
10. En la pestaña **Programación** , establezca el programa de inicio y fin de detección de alertas.  
  
## <a name="see-also"></a>Consulte también  
 [Crear una alerta de base de datos de SQL Server](../../relational-databases/performance-monitor/create-a-sql-server-database-alert.md)  
  
  
