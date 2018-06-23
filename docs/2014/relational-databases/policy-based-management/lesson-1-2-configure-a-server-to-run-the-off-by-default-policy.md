---
title: Configuración de un servidor para ejecutar la directiva Desactivado de forma predeterminada | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 41c3022d-ab13-443e-ac64-ba1d64584f79
caps.latest.revision: 22
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 452514758526ae8d5183c614a16aa0a0c8ec3b14
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36196685"
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
  
  