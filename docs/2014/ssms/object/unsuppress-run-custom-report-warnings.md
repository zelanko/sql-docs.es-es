---
title: Anular la supresión de las advertencias de Ejecutar informe personalizado | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Management Studio [SQL Server], custom reports
ms.assetid: 0deed900-c910-4d12-aac0-6ab9e39eb068
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ed653b16fe524f364ba89f13e00715b725080033
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62824403"
---
# <a name="unsuppress-run-custom-report-warnings"></a>Anular la supresión de las advertencias de Ejecutar informe personalizado
  Para los informes personalizados existen dos cuadros de diálogo de advertencia. En este tema se describe cómo anular la supresión de la presentación de estos cuadros en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 De forma predeterminada, el cuadro de diálogo **Ejecutar informe personalizado** aparece antes de la ejecución de un informe personalizado. Si activa la casilla **No volver a mostrar esta advertencia** , el cuadro de diálogo ya no aparecerá más. De forma predeterminada, el cuadro de diálogo **Ejecutar informe personalizado** también aparece cuando se abre un informe personalizado y, a continuación, se hace clic en un vínculo para abrir otro informe personalizado. Este cuadro de diálogo muestra la ruta completa al archivo de informe detallado personalizado. Si activa la casilla **No volver a mostrar esta advertencia** , el cuadro de diálogo ya no aparecerá más.  
  
##  <a name="SSMSProcedure"></a> Uso de SQL Server Management Studio  
  
#### <a name="to-unsuppress-the-main-custom-report-warning-dialog-box"></a>Para anular la supresión del cuadro de diálogo de advertencia principal del informe personalizado  
  
1.  Conectar con \<la*unidad* de*recurso compartido*>|\<de *servidor*>\\<> \Documents\>and Settings\\<userprofile \Application Data\Microsoft\Microsoft SQL Server\120\Tools\Shell\reports.Xml.  
  
2.  Haga clic `reports.xml`con el botón secundario y, a continuación, haga clic en **Editar**.  
  
3.  Cambie**\<SuppressWarning>true\</SuppressWarning> a \<SuppressWarning>false\</SuppressWarning>**.  
  
4.  Reinicie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
#### <a name="to-unsuppress-the-drill-through-custom-report-warning-dialog-box"></a>Para anular la supresión del cuadro de diálogo de advertencia del informe de obtención de detalles personalizado  
  
1.  Conectar con \<la*unidad* de*recurso compartido*>|\<de *servidor*>\\<> \Documents\>and Settings\\<userprofile \Application Data\Microsoft\Microsoft SQL Server\120\Tools\Shell\reports.Xml.  
  
2.  Haga `reports.xml`clic con el botón secundario y haga clic en **Editar**.  
  
3.  Cambie ** \<SuppressDrillthroughWarning>true\</SuppressDrillthroughWarning>a \<SuppressDrillthroughWarning>false\</SuppressDrillthroughWarning>**.  
  
4.  Reinicie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
## <a name="see-also"></a>Consulte también  
 [Informes personalizados en Management Studio](custom-reports-in-management-studio.md)   
 [Agregar un informe personalizado a Management Studio](add-a-custom-report-to-management-studio.md)   
 [Usar informes personalizados con las propiedades de nodo del Explorador de objetos](use-custom-reports-with-object-explorer-node-properties.md)  
  
  
