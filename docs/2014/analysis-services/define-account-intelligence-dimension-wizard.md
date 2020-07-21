---
title: Definir la inteligencia de cuentas (Asistente para dimensiones) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dimensionwizard.accountintelligencetypemapping.f1
ms.assetid: cbcff072-3a7e-4e98-858f-1b4265461561
author: minewiskan
ms.author: owend
ms.openlocfilehash: 0b218c10826253bc63985e2eb970a4102873e699
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/08/2020
ms.locfileid: "84528861"
---
# <a name="define-account-intelligence-dimension-wizard"></a>Definir la inteligencia de cuentas (Asistente para dimensiones)
  Use la página **Definir la inteligencia de cuentas** para asignar tipos de cuenta definidos en la instancia de [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] a los tipos de cuenta definidos en el atributo de la dimensión asociado al tipo de atributo **Tipo de cuenta** de la dimensión.  
  
> [!NOTE]  
>   Esta página solo se muestra si ha seleccionado **Dimensión estándar** en la página **Seleccionar el tipo de dimensión** y si ha asignado un atributo de dimensión al tipo de atributo **Tipo de cuenta** en la página **Especificar tipo de dimensión** .  
  
## <a name="options"></a>Opciones  
 **Tipos de cuenta de tabla de origen**  
 Muestra los valores incluidos en el atributo de dimensión asignado al tipo de atributo **Tipo de cuenta** en la página **Especificar clave y tipo de dimensión** .  
  
 **Tipos de cuenta integrados**  
 Seleccione el tipo de cuenta definido en la instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] que está asignado a los tipos de cuenta de la tabla de origen.  
  
 En la tabla siguiente se enumeran los tipos de cuenta definidos en una instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
|Value|Descripción|  
|-----------|-----------------|  
|**Recurso**|Valor de cosas en propiedad en un momento dado.|  
|**Saldo**|Cuenta de algo en un momento dado.|  
|**Expense**|Valor de cosas consumidas.|  
|**Flujo**|Cuenta incremental de cosas.|  
|**Income**|Valor de las cosas recibidas.|  
|**Liability**|Valor de cosas debidas en un momento dado.|  
|**Estadística**|Proporción calculada de algo o cuenta de algo que no se agrega.|  
  
## <a name="see-also"></a>Consulte también  
 [Asistente para dimensiones (ayuda F1)](dimension-wizard-f1-help.md)   
 [Dimensiones &#40;Analysis Services de datos multidimensionales&#41;](multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)   
 [Dimensiones en modelos multidimensionales](multidimensional-models/dimensions-in-multidimensional-models.md)  
  
  
