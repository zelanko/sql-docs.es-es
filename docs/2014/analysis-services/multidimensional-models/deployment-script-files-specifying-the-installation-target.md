---
title: Especificar el destino de instalación | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- input files [Analysis Services]
- installation targets [Analysis Services]
- Analysis Services deployments, installation targets
- Analysis Services Deployment Wizard, installation targets
- deploying [Analysis Services], installation targets
- modifying installation targets
ms.assetid: cb706817-6f63-4771-92c3-b70030bbce3d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f5a46dc4c6130bb49d973ffc0025388c563c080f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66075218"
---
# <a name="specifying-the-installation-target"></a>Especificar el destino de instalación
  El [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Asistente para implementación de lee la información del destino de instalación la \< *nombre del proyecto*> .deploymenttargets archivo. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] crea este archivo cuando se genera el proyecto de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] usa la base de datos y servidor especificados en el **implementación** página de la  *\<nombre del proyecto >* **las páginas de propiedades** cuadro de diálogo para crear el \< *nombre del proyecto*> archivo .targets.  
  
## <a name="modifying-the-installation-target-for-deployment"></a>Modificar el destino de instalación para la implementación  
 En algunas situaciones, puede que necesite implementar un proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en una base de datos o en una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que sea diferente a la especificada en la página **Implementación** . Por ejemplo, puede que desee implementar el proyecto en un servidor para realizar pruebas antes de la implementación y, a continuación, implementarlo en un servidor de producción. Puede que también desee implementar un proyecto finalizado y probado en varios servidores de producción de un clúster de equilibrio de carga de red (NLB), o en un servidor de ensayo y un servidor de producción.  
  
 Para implementar un proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en una base de datos o una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] diferentes, puede cambiar el destino de instalación del archivo de entrada mediante uno de los métodos descritos en el siguiente procedimiento.  
  
#### <a name="to-change-the-installation-target-after-the-input-files-have-been-generated"></a>Para cambiar el destino de instalación después de haber generado los archivos de entrada  
  
-   Ejecute el Asistente para la implementación de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] de forma interactiva. En la página **Destino de instalación** , especifique un nuevo destino para la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] y la base de datos.  
  
     -o bien-  
  
-   Ejecute el Asistente para la implementación de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en el símbolo del sistema y ajuste el asistente de manera que se ejecute en modo de archivo de respuesta. Para obtener más información acerca del modo de archivo de respuesta, vea [Running the Analysis Services Deployment Wizard](running-the-analysis-services-deployment-wizard.md).  
  
     -o bien-  
  
-   Modificar el \< *nombre del proyecto*> archivo .deploymenttargets usando cualquier editor de texto.  
  
## <a name="see-also"></a>Vea también  
 [Especificar opciones de implementación de roles y particiones](deployment-script-files-partition-and-role-deployment-options.md)   
 [Especificar la configuración para la implementación de soluciones](deployment-script-files-solution-deployment-config-settings.md)   
 [Especificar opciones de procesamiento](deployment-script-files-specifying-processing-options.md)  
  
  
