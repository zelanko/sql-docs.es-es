---
title: Importar informes desde Microsoft Access (Reporting Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Access reports [Reporting Services]
- importing reports
ms.assetid: 4f29d5b8-b77d-4714-a84a-05523df55646
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 862d8b90f3c91dffda35971677db7fdc231c1b63
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66108929"
---
# <a name="import-reports-from-microsoft-access-reporting-services"></a>Importar informes desde Microsoft Access (Reporting Services)
  En Diseñador de informes, puede importar informes desde una base [!INCLUDE[msCoName](../includes/msconame-md.md)] de datos o un proyecto de Access. Deberá instalar Access 2002 o una versión posterior en el mismo equipo en el que está instalado el Diseñador de informes.  
  
 Cuando se usa la característica de importación, se importan todos los informes de la base de datos o del archivo de proyecto. Si el archivo de Access contiene muchos informes, es recomendable crear un proyecto de informes diferente para importarlos y, después, abrir los archivos RDL individuales en el proyecto de informes principal. Puede modificar los informes después de importarlos al Diseñador de informes.  
  
> [!NOTE]  
>  
  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] no admite todos los objetos de informe de Access. Los elementos que no se convierten se muestran en la ventana **lista de tareas** . Para obtener más información, vea [características de informes de Access admitidas &#40;SSRS&#41;](../../2014/reporting-services/supported-access-report-features-ssrs.md).  
  
### <a name="to-import-reports-from-microsoft-access"></a>Para importar informes desde Microsoft Access  
  
1.  Abra o cree el proyecto al que desea importar los informes.  
  
2.  En el menú **proyecto** , elija **importar informes**y, a continuación, haga clic en **Microsoft Access**. O bien, haga clic con el botón derecho en el proyecto en Explorador de soluciones, elija **importar informes**y, a continuación, haga clic en **Microsoft Access**.  
  
3.  En el cuadro de diálogo **abrir** , seleccione la base de datos de Access (. mdb,. accdb) o el proyecto (. ADP) que contiene los informes y, a continuación, haga clic en **abrir**. Todos los informes existentes en el archivo de base de datos o de proyecto se importan y se especifican en la carpeta de informes en el Explorador de soluciones.  
  
4.  Compruebe si hay errores de compilación en la ventana **lista de tareas** . Para ver la ventana de **lista de tareas** , abra el menú **Ver** , seleccione **otras ventanas**y, a continuación, haga clic en **lista de tareas**.  
  
## <a name="see-also"></a>Consulte también  
 [Diseñar informes con el Diseñador de informes &#40;SSRS&#41;](tools/design-reporting-services-paginated-reports-with-report-designer-ssrs.md)  
  
  
