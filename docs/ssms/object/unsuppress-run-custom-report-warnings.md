---
description: Anular la supresión de las advertencias de Ejecutar informe personalizado
title: Anular la supresión de las advertencias de Ejecutar informe personalizado
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Management Studio [SQL Server], custom reports
ms.assetid: 0deed900-c910-4d12-aac0-6ab9e39eb068
author: markingmyname
ms.author: maghan
ms.openlocfilehash: c6fd8adef633e50591088c8859fd8071c96da992
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88317051"
---
# <a name="unsuppress-run-custom-report-warnings"></a>Anular la supresión de las advertencias de Ejecutar informe personalizado
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
Para los informes personalizados existen dos cuadros de diálogo de advertencia. En este tema se describe cómo anular la supresión de la presentación de estos cuadros en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
De forma predeterminada, el cuadro de diálogo **Ejecutar informe personalizado** aparece antes de la ejecución de un informe personalizado. Si activa la casilla **No volver a mostrar esta advertencia** , el cuadro de diálogo ya no aparecerá más. De forma predeterminada, el cuadro de diálogo **Ejecutar informe personalizado** también aparece cuando se abre un informe personalizado y, a continuación, se hace clic en un vínculo para abrir otro informe personalizado. Este cuadro de diálogo muestra la ruta completa al archivo de informe detallado personalizado. Si activa la casilla **No volver a mostrar esta advertencia** , el cuadro de diálogo ya no aparecerá más.  
  
## <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a>Usar SQL Server Management Studio  
  
#### <a name="to-unsuppress-the-main-custom-report-warning-dialog-box"></a>Para anular la supresión del cuadro de diálogo de advertencia principal del informe personalizado  
  
1.  Conéctese a \<*Server*>\\<*Recurso compartido*>|\<*Drive*>\Documents and Settings\\<UserProfile>\Application Data\Microsoft\Microsoft SQL Server\130\Tools\Shell\reports.xml.  
  
2.  Haga clic con el botón derecho en **reports.xml**y, luego, haga clic en **Editar**.  
  
3.  Cambie **<SuppressWarning>true\<\/SuppressWarning> a <SuppressWarning>false\<\/SuppressWarning>** .  
  
4.  Reinicie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
#### <a name="to-unsuppress-the-drill-through-custom-report-warning-dialog-box"></a>Para anular la supresión del cuadro de diálogo de advertencia del informe de obtención de detalles personalizado  
  
1.  Conéctese a \<*Server*>\\<*Recurso compartido*>|\<*Drive*>\Documents and Settings\\<UserProfile>\Application Data\Microsoft\Microsoft SQL Server\130\Tools\Shell\reports.xml.  
  
2.  Haga clic con el botón derecho en **reports.xml**y, luego, haga clic en **Editar**.  
  
3.  Cambie **<SuppressDrillthroughWarning>true\<\/SuppressDrillthroughWarning>a <SuppressDrillthroughWarning>false\<\/SuppressDrillthroughWarning>** .  
  
4.  Reinicie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
## <a name="see-also"></a>Consulte también  
[Informes personalizados en Management Studio](../../ssms/object/custom-reports-in-management-studio.md)  
[agregar un informe personalizado a Management Studio](../../ssms/object/add-a-custom-report-to-management-studio.md)  
[Usar informes personalizados con las propiedades de nodo del Explorador de objetos](../../ssms/object/use-custom-reports-with-object-explorer-node-properties.md)  
  
