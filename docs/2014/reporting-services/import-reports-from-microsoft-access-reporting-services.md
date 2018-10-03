---
title: Importar informes desde Microsoft Access (Reporting Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Access reports [Reporting Services]
- importing reports
ms.assetid: 4f29d5b8-b77d-4714-a84a-05523df55646
author: maggiesmsft
ms.author: douglasl
manager: craigg
ms.openlocfilehash: dc63daf4095238f948be6bde22bf190aa4d1977a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48086517"
---
# <a name="import-reports-from-microsoft-access-reporting-services"></a>Importar informes desde Microsoft Access (Reporting Services)
  En el Diseñador de informes, puede importar informes desde un [!INCLUDE[msCoName](../includes/msconame-md.md)] base de datos o proyecto. Deberá instalar Access 2002 o una versión posterior en el mismo equipo en el que está instalado el Diseñador de informes.  
  
 Cuando se usa la característica de importación, se importan todos los informes de la base de datos o del archivo de proyecto. Si el archivo de Access contiene muchos informes, es recomendable crear un proyecto de informes diferente para importarlos y, después, abrir los archivos RDL individuales en el proyecto de informes principal. Puede modificar los informes después de importarlos al Diseñador de informes.  
  
> [!NOTE]  
>  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] no admite todos los objetos de informe de Access. Se muestran los elementos que no se convierten en el **lista de tareas** ventana. Para obtener más información, consulte [admite características de informes de Access &#40;SSRS&#41;](../../2014/reporting-services/supported-access-report-features-ssrs.md).  
  
### <a name="to-import-reports-from-microsoft-access"></a>Para importar informes desde Microsoft Access  
  
1.  Abra o cree el proyecto al que desea importar los informes.  
  
2.  En el **proyecto** menú, elija **importar informes**y, a continuación, haga clic en **Microsoft Access**. Como alternativa, haga clic en el proyecto en el Explorador de soluciones, seleccione **importar informes**y, a continuación, haga clic en **Microsoft Access**.  
  
3.  En el **abierto** cuadro de diálogo, seleccione la base de datos de Access (.mdb, .accdb) o un proyecto (.adp) que contiene los informes y, a continuación, haga clic en **abierto**. Todos los informes existentes en el archivo de base de datos o de proyecto se importan y se especifican en la carpeta de informes en el Explorador de soluciones.  
  
4.  Compruebe el **lista de tareas** ventana para errores de compilación. Para ver el **lista de tareas** ventana, abra el **vista** menú, elija **Other Windows**y, a continuación, haga clic en **lista de tareas**.  
  
## <a name="see-also"></a>Vea también  
 [Diseñar informes con el Diseñador de informes &#40;SSRS&#41;](tools/design-reporting-services-paginated-reports-with-report-designer-ssrs.md)  
  
  
