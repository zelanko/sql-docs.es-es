---
title: Configuración de un servidor para ejecutar la directiva Desactivado de forma predeterminada | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 41c3022d-ab13-443e-ac64-ba1d64584f79
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 8beb6998d78ad9a113ce18323133de7ed39ead56
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66090641"
---
# <a name="configure-a-server-to-run-the-off-by-default-policy"></a>Configurar un servidor para ejecutar la directiva Desactivado de forma predeterminada
  Ahora hay una directiva denominada Desactivado de forma predeterminada. En esta tarea, comprobará si el servidor cumple los requisitos de la directiva Desactivado de forma predeterminada.  
  
### <a name="to-run-the-off-by-default-policy"></a>Para ejecutar la directiva Desactivado de forma predeterminada  
  
1.  En el Explorador de objetos, haga clic con el botón derecho en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], seleccione **Directivas**y haga clic en **Evaluar**.  
  
2.  En el cuadro de diálogo **Evaluar directivas** puede seleccionar las directivas de otra instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o de un archivo. Para este paso, deje **Origen** establecido en su instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
3.  En la sección **Directivas** , seleccione la directiva **Desactivado de forma predeterminada** .  
  
4.  Para ver si el servidor cumple la directiva, haga clic en **Evaluar**.  
  
5.  En el área **Resultados** , verá un círculo verde con una marca de verificación si el [!INCLUDE[ssDE](../../includes/ssde-md.md)] cumple la directiva. Verá un círculo rojo con una X si el [!INCLUDE[ssDE](../../includes/ssde-md.md)] no cumple la directiva.  
  
6.  En el área **Detalles del destino** , verá información adicional en la columna **Mensaje** si se produce un error. En la columna **Mensaje** , haga clic en **Ver** para ver un informe que contiene los resultados de la comprobación de cada propiedad de faceta que se comprobó.  
  
7.  La descripción de la directiva se muestra en la parte inferior de la página y la sección **Ayuda adicional** muestra el hipervínculo que ha configurado para la directiva. Haga clic en el hipervínculo de mensaje para abrir la página web que especificó al crear la directiva.  
  
8.  Cierre el explorador y, después, cierre el cuadro de diálogo **Vista detallada de resultados** .  
  
9. Si el servidor no cumple la directiva y quiere deshabilitar Correo electrónico de base de datos, haga clic en **Aplicar** en la página **Resultados de la evaluación** .  
  
10. Cierre los cuadros de diálogo **Vista detallada de resultados** y **Evaluar directivas** .  
  
## <a name="next-lesson"></a>Lección siguiente  
 [Lección 2: Crear y aplicar una directiva de normas de denominación](lesson-2-create-and-apply-a-naming-standards-policy.md)  
  
  
