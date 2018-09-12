---
title: Anular la supresión de las advertencias de Ejecutar informe personalizado | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Management Studio [SQL Server], custom reports
ms.assetid: 0deed900-c910-4d12-aac0-6ab9e39eb068
caps.latest.revision: 15
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0829c079945c765efd836b25f30a54777c324a2a
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2018
ms.locfileid: "43814381"
---
# <a name="unsuppress-run-custom-report-warnings"></a>Anular la supresión de las advertencias de Ejecutar informe personalizado
  Para los informes personalizados existen dos cuadros de diálogo de advertencia. En este tema se describe cómo anular la supresión de la presentación de estos cuadros en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 De forma predeterminada, el cuadro de diálogo **Ejecutar informe personalizado** aparece antes de la ejecución de un informe personalizado. Si activa la casilla **No volver a mostrar esta advertencia** , el cuadro de diálogo ya no aparecerá más. De forma predeterminada, el cuadro de diálogo **Ejecutar informe personalizado** también aparece cuando se abre un informe personalizado y, a continuación, se hace clic en un vínculo para abrir otro informe personalizado. Este cuadro de diálogo muestra la ruta completa al archivo de informe detallado personalizado. Si activa la casilla **No volver a mostrar esta advertencia** , el cuadro de diálogo ya no aparecerá más.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-unsuppress-the-main-custom-report-warning-dialog-box"></a>Para anular la supresión del cuadro de diálogo de advertencia principal del informe personalizado  
  
1.  Conectarse a \< *Server*>\\<*Share*>|\<*unidad*> \ Documents and Settings\\< UserProfile\>\Application Data\Microsoft\Microsoft SQL Server\120\Tools\Shell\reports.xml.  
  
2.  Haga clic en `reports.xml`y, a continuación, haga clic en **editar**.  
  
3.  Cambio**\<SuppressWarning > true\</suppresswarning > a \<SuppressWarning > false\</suppresswarning >**.  
  
4.  Reinicie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
#### <a name="to-unsuppress-the-drill-through-custom-report-warning-dialog-box"></a>Para anular la supresión del cuadro de diálogo de advertencia del informe de obtención de detalles personalizado  
  
1.  Conectarse a \< *Server*>\\<*Share*>|\<*unidad*> \ Documents and Settings\\< UserProfile\>\Application Data\Microsoft\Microsoft SQL Server\120\Tools\Shell\reports.xml.  
  
2.  Haga clic en `reports.xml`y haga clic en **editar**.  
  
3.  Cambio  **\<SuppressDrillthroughWarning > true\</SuppressDrillthroughWarning > a \<SuppressDrillthroughWarning > false\</SuppressDrillthroughWarning >**.  
  
4.  Reinicie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
## <a name="see-also"></a>Vea también  
 [Informes personalizados en Management Studio](custom-reports-in-management-studio.md)   
 [Agregar un informe personalizado a Management Studio](add-a-custom-report-to-management-studio.md)   
 [Usar informes personalizados con las propiedades de nodo del Explorador de objetos](use-custom-reports-with-object-explorer-node-properties.md)  
  
  
