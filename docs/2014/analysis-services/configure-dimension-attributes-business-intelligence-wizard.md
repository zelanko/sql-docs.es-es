---
title: Configurar los atributos de dimensión (Asistente de Business Intelligence) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.biwizard.acctintelligence.selectattributes.f1
ms.assetid: 3d046e63-bcb1-4ab1-9c37-652463fa68c3
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6992d667383539092f13602c277eec4ee2f7c7f8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48133695"
---
# <a name="configure-dimension-attributes-business-intelligence-wizard"></a>Configurar los atributos de dimensión (Asistente de Business Intelligence)
  Use la página **Configurar los atributos de dimensión** para asignar atributos de dimensión a los tipos de atributo que [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] usa para identificar atributos para dimensiones de cuentas.  
  
## <a name="options"></a>Opciones  
 **Tipo de dimensión**  
 Muestra el tipo de dimensión seleccionado.  
  
> [!NOTE]  
>  Esta opción no está disponible porque el `Type` propiedad de la dimensión no se puede cambiar a un valor distinto de *cuenta* para las dimensiones de cuenta.  
  
 **Atributos de dimensión**  
 Muestra los tipos de atributo válidos que se pueden asignar a los atributos de dimensión existentes en la dimensión.  
  
 **incluir**  
 Active una casilla para incluir el tipo de atributo correspondiente en la dimensión.  
  
 **Tipo de atributo**  
 Enumera los tipos de atributo que se pueden asignar a los atributos de dimensión existentes en la dimensión.  
  
 **Atributo de dimensión**  
 Active el atributo de dimensión que debe asignarse al tipo de atributo correspondiente.  
  
 **Establecer medidas en suma parcial en función de tipo de cuenta**  
 Seleccione esta opción para cambiar cada medida asociada con esta dimensión para que se agregue con el tipo de cuenta.  
  
> [!NOTE]  
>  Esta opción no aparece si se ha iniciado el Asistente de Business Intelligence desde el Diseñador de dimensiones o haciendo clic con el botón secundario en una dimensión del Explorador de soluciones de [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
## <a name="see-also"></a>Vea también  
 [Asistente de Business Intelligence F1 Ayuda](business-intelligence-wizard-f1-help.md)   
 [Diseñador de cubos &#40;Analysis Services - datos multidimensionales&#41;](cube-designer-analysis-services-multidimensional-data.md)   
 [Diseñador de dimensiones &#40;Analysis Services - datos multidimensionales&#41;](dimension-designer-analysis-services-multidimensional-data.md)  
  
  
