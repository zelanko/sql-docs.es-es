---
title: Implementar soluciones de modelo mediante el Asistente para la implementación | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Analysis Services Deployment Wizard
- deploying [Analysis Services], Analysis Services Deployment Wizard
- Analysis Services deployments, Analysis Services Deployment Wizard
- Analysis Services Deployment Wizard, about Analysis Services Deployment Wizard
ms.assetid: ff711e8e-971c-43ba-b479-effc034af4a4
author: minewiskan
ms.author: owend
ms.openlocfilehash: 6e3dfd0b727fd917c37aa44aa8fd1d29326aaaa1
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/09/2020
ms.locfileid: "84546901"
---
# <a name="deploy-model-solutions-using-the-deployment-wizard"></a>Implementar soluciones con el Asistente para la implementación
  El [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Asistente para la implementación de utiliza los archivos de salida XML generados a partir de un [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] proyecto de como archivos de entrada. Estos archivos de entrada se pueden modificar fácilmente para personalizar la implementación de un proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . El script de implementación generado puede ejecutarse inmediatamente o guardarse para su implementación posterior.  
  
 Puede realizar la implementación con el asistente según lo explicado aquí. También puede automatizarla o utilizar la capacidad Sincronizar. Si la base de datos implementada es grande, considere la posibilidad de utilizar particiones en los sistemas de destino. También puede automatizar la creación y el llenado de particiones mediante los Objetos de administración de análisis (AMO).  
  
> [!IMPORTANT]  
>  Ni los archivos de salida XML ni el script de implementación contendrán el Id. de usuario o la contraseña si dicha información se ha especificado en la cadena de conexión para un origen de datos o por motivos de suplantación. Puesto que en este escenario se requieren para el procesamiento, deberá agregar manualmente esta información. Si la implementación no incluye el procesamiento, puede agregar esta información de conexión y suplantación cuando lo desee después de la implementación. Si la implementación incluye el procesamiento, puede agregar esta información en el asistente o en el script de implementación una vez guardado.  
  
## <a name="in-this-section"></a>En esta sección  
 Los siguientes temas describen cómo trabajar con el Asistente para la implementación de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , los archivos de entrada y el script de implementación:  
  
|Tema|Descripción|  
|-----------|-----------------|  
|[Ejecutar el Asistente para la implementación de Analysis Services](running-the-analysis-services-deployment-wizard.md)|Describe los diversos modos en los que se puede ejecutar el Asistente para la implementación de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|[Comprender los archivos de entrada utilizados para crear el script de implementación](deployment-script-files-input-used-to-create-deployment-script.md)|Describe qué archivos utiliza el Asistente para la implementación de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] como valores de entrada, cuáles de esos archivos contiene, y proporciona vínculos con los temas que describen cómo modificar los valores de cada uno de los archivos de entrada.|  
|[Descripción del script de implementación de Analysis Services](understanding-the-analysis-services-deployment-script.md)|Describe lo que contiene el script de implementación y cómo se ejecuta este.|  
  
## <a name="see-also"></a>Consulte también  
 [Implementar soluciones de modelo mediante XMLA](deploy-model-solutions-using-xmla.md)   
 [Sincronizar bases de datos de Analysis Services](synchronize-analysis-services-databases.md)   
 [Descripción de los archivos de entrada utilizados para crear el script de implementación](deployment-script-files-input-used-to-create-deployment-script.md)   
 [Implementar soluciones de modelos con la utilidad de implementación](deploy-model-solutions-with-the-deployment-utility.md)  
  
  
