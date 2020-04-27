---
title: Propiedades del servidor (página Registro) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.swb.reportserver.serverproperties.logging.f1
ms.assetid: b338deab-4868-4951-9f22-0605add2fc95
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 2a04c27fd790a1ad5c4ba453b43af5983a6440e3
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66099528"
---
# <a name="server-properties-logging-page"></a>Propiedades del servidor (página Registro)
  Utilice esta página para establecer límites en los datos de ejecución de informes que recoge un servidor de informes. Los datos de ejecución se almacenan internamente en la base de datos del servidor de informes. Puede realizar el seguimiento de la actividad de informe para el servidor de informes que se ejecuta en modo nativo o en modo integrado con SharePoint. Si el servidor de informes forma parte de una implementación escalada, el registro de ejecución de informes mantiene un registro de toda la actividad de informe para la implementación completa en un archivo de registro único.  
  
 Para abrir esta página, inicie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conéctese a un servidor de informes, haga clic con el botón secundario en el nombre del servidor de informes y seleccione **Propiedades**. Haga clic en **Registro** para abrir esta página.  
  
## <a name="options"></a>Opciones  
 **Habilitar el registro de la ejecución de informes**  
 Haga clic para crear y almacenar información sobre la actividad de informe en el servidor. Si esta opción está habilitada, el servidor de informes realizará un seguimiento sobre qué informes se usan, la frecuencia del procesamiento de informes, el tipo de operación de informe que se realizó, el formato de salida y quién ejecutó el informe. Para obtener más información sobre los puntos de datos adicionales que se capturan en el registro, vea [registro de ejecución del servidor de informes y la vista ExecutionLog3](../report-server/report-server-executionlog-and-the-executionlog3-view.md).  
  
 **Quitar entradas de registro anteriores a este número de días**  
 Permite especificar el número de días después del cual se eliminarán las entradas de registro del registro de la ejecución de informes. El valor predeterminado es 60 días.  
  
## <a name="see-also"></a>Consulte también  
 [Establecer las propiedades del servidor de informes &#40;Management Studio&#41;](set-report-server-properties-management-studio.md)   
 [Conectarse a un servidor de informes en Management Studio](connect-to-a-report-server-in-management-studio.md)   
 [Archivos de registro y orígenes de Reporting Services](../report-server/reporting-services-log-files-and-sources.md)   
 [Servidor de informes en Management Studio ayuda de F1](report-server-in-management-studio-f1-help.md)   
 [Registro de ejecución del servidor de informes y la vista ExecutionLog3](../report-server/report-server-executionlog-and-the-executionlog3-view.md)  
  
  
