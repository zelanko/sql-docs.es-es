---
title: "Cuadro de diálogo CRI (generador de informes) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
f1_keywords:
- "10008"
helpviewer_keywords:
- CRI
- custom report items
ms.assetid: 2a3f2ac6-667e-4498-8b73-9c40beb993f5
caps.latest.revision: 18
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 37ba742708ded98cd5728a3051a2e7a76b9fa99f
ms.contentlocale: es-es
ms.lasthandoff: 06/13/2017

---
# <a name="convert-cri-dialog-box-report-builder"></a>Actualización de CRI (cuadro de diálogo del Generador de informes)
  Este informe contiene elementos de informe personalizados (CRI) con características no admitidas. Los CRI son extensiones del lenguaje RDL (Report Definition Language) que admiten objetos personalizados que muestran datos en un informe. Los CRI incluyen componentes de tiempo de diseño y de tiempo de ejecución proporcionados por otros fabricantes de software.  
  
> [!NOTE]  
>  La decisión de admitir elementos de informe personalizados en un servidor de informes debe tomarla el administrador del sistema. Para ver los CRI en un informe, los componentes CRI se deben instalar en el cliente de creación de informes para obtener una vista previa de un informe y se deben instalar en el servidor de informes para ver un informe publicado o cargado.  
  
 Algunos CRI se pueden convertir en elementos de informe en el nuevo formato de definición de informe. Al abrir el informe, se le pregunta si desea actualizar. Use la información siguiente para determinar si deben convertirse los CRI de este informe:  
  
-   **Sí** : elija **Sí** para convertir todos los CRI del informe, siempre que sea posible. Las características no admitidas de los CRI no se pueden actualizar y se quitan del archivo de definición de informe. Para obtener la lista de las características no admitidas, vea [Actualizar informes](../../reporting-services/install-windows/upgrade-reports.md). Al ver el informe, es posible que observe diferencias en la manera en que se muestran los CRI en el informe.  
  
-   **No** : elija **No** si no desea convertir los CRI del informe. El procesador de informes no puede mostrar la versión actual de estos CRI. Si el administrador del sistema tiene pensado instalar una nueva versión de los CRI de otros fabricantes de software que es compatible con el nuevo formato de definición de informe, debería elegir **No**. Hasta que estén disponibles las nuevas versiones, los CRI se muestran en el informe como un cuadro de texto vacío con una X roja.  
  
 En cualquier caso, el informe se actualiza al nuevo formato de definición de informe y se guarda una copia de seguridad del informe original como  *\<nombre del informe >* `-` Backup.rdl. Si guarda el informe en la herramienta de creación de informes, está guardando el informe actualizado en el nuevo formato de definición de informe. Si publica el informe, éste se guarda primero en su equipo y, a continuación, se publica en el servidor de informes. En realidad, está publicando la versión actualizada del informe en el servidor de informes.  
  
 Si no guarda el informe, el informe original no varía. Sin embargo, no podrá modificar este informe en una versión posterior de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] de [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] ni en un entorno de creación de informes que use este formato de definición de informe. Puede continuar ejecutando la versión original del informe cargándolo en un servidor de informes de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] o posterior de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] mediante el Administrador de informes. Para obtener más información, vea [Cargar un archivo o un informe &#40;Administrador de informes&#41;](../../reporting-services/reports/upload-a-file-or-report-report-manager.md).  
  
 En el caso de los informes cargados, no publicados, en un servidor de informes, el procesador de informes determina si se pueden actualizar al usarse por primera vez. Los informes que no se pueden actualizar se procesan en el modo de compatibilidad con versiones anteriores y siguen mostrándose igual que en la versión anterior de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Para más información, consulte [Upgrade Reports](../../reporting-services/install-windows/upgrade-reports.md).  
  
 Para identificar el formato de definición de informe actual de un informe, un servidor de informes o de un proyecto, o bien para el entorno de creación de informes, vea [Buscar la versión del esquema de definición de informe &#40;SSRS&#41;](../../reporting-services/reports/find-the-report-definition-schema-version-ssrs.md).  
  
## <a name="see-also"></a>Vea también  
 [Ayuda del Generador de informes para cuadros de diálogo, paneles y asistentes](http://msdn.microsoft.com/en-us/2da24891-0b6d-4d3c-8b18-81b98752642f)  
  
  
