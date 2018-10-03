---
title: Definir la inteligencia de cuentas (Asistente de Business Intelligence) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.biwizard.acctintelligence.mapaccounttype.f1
ms.assetid: fe4c204b-1031-4ac4-9916-8052ce2301cc
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0afc9be649d3d9eb23a9c0e4b1b601b772cd16fc
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48209405"
---
# <a name="define-account-intelligence-business-intelligence-wizard"></a>Definir la inteligencia de cuentas (Asistente de Business Intelligence)
  Use la página **Definir la inteligencia de cuentas** para asignar tipos de cuenta definidos en la instancia de [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] a tipos de cuenta definidos por una tabla de origen en el origen de datos que proporciona datos para la dimensión de cuenta.  
  
> [!NOTE]  
>  Esta página aparecerá si se ha asignado un atributo de dimensión al tipo de atributo **Tipo de cuenta** en la página **Configurar los atributos de dimensión** .  
  
## <a name="options"></a>Opciones  
 **Tipos de cuenta de tabla de origen**  
 Muestra los valores que contiene el atributo de dimensión asignado al tipo de atributo **Tipo de cuenta** de la página **Configurar los atributos de dimensión** .  
  
 **Tipos de cuenta integrados**  
 Seleccione el tipo de cuenta definido en la instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] que está asignado a los tipos de cuenta de la tabla de origen.  
  
 En la tabla siguiente se enumeran los tipos de cuenta definidos en una instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**Asset**|Valor de cosas en propiedad en un momento dado.|  
|**Equilibrio**|Cuenta de algo en un momento dado.|  
|**Expense**|Valor de cosas consumidas.|  
|**Flow**|Cuenta incremental de cosas.|  
|**Income**|Valor de las cosas recibidas.|  
|**Liability**|Valor de cosas debidas en un momento dado.|  
|**Estadísticas**|Proporción calculada de algo o cuenta de algo que no se agrega.|  
  
## <a name="see-also"></a>Vea también  
 [Asistente de Business Intelligence F1 Ayuda](business-intelligence-wizard-f1-help.md)   
 [Diseñador de cubos &#40;Analysis Services - datos multidimensionales&#41;](cube-designer-analysis-services-multidimensional-data.md)   
 [Diseñador de dimensiones &#40;Analysis Services - datos multidimensionales&#41;](dimension-designer-analysis-services-multidimensional-data.md)  
  
  
