---
title: Cuadro de diálogo Propiedades del ensamblado (Analysis Services - datos multidimensionales) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.sqlserverstudio.assemblyproperties.f1
ms.assetid: da1174d6-d82b-4337-ac19-7368dbd95a84
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b21230ddff5a3db043b533a4f921a30b02da739b
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66062294"
---
# <a name="assembly-properties-dialog-box-analysis-services---multidimensional-data"></a>Cuadro de diálogo Propiedades del ensamblado (Analysis Services - Datos multidimensionales)
  Use el cuadro de diálogo **Propiedades del ensamblado** en [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] para establecer las propiedades de una referencia de ensamblado en una base de datos [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . Para mostrar el cuadro de diálogo **Propiedades del ensamblado** , haga clic con el botón derecho en **Explorador de objetos** y seleccione **Propiedades**.  
  
## <a name="options"></a>Opciones  
  
|Término|Definición|  
|----------|----------------|  
|**Name**|Escriba para cambiar el nombre de la referencia de ensamblado.<br /><br /> Nota: Si cambia este valor no cambia el nombre del ensamblado al que hace referencia la referencia de ensamblado, sino que se cambia el nombre usado el mediante el [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] instancia o base de datos al que hace referencia a la referencia de ensamblado.|  
|**ID**|Muestra el identificador del ensamblado al que se refiere la referencia de ensamblado.|  
|**Descripción**|Escriba para cambiar la descripción de la referencia de ensamblado.|  
|**Marca de tiempo de creación**|Muestra la fecha y la hora de creación de la referencia de ensamblado.|  
|**Última actualización de esquema**|Muestra la fecha y la hora de la última actualización de los metadatos de la referencia de ensamblado.|  
|**Tipo**|Muestra el tipo de referencia de ensamblado. Se muestran las siguientes opciones:<br /><br /> **Ensamblado .NET**: La referencia de ensamblado se refiere a un ensamblado de [!INCLUDE[msCoName](../includes/msconame-md.md)] .NET Framework.<br /><br /> **COM DLL**: La referencia de ensamblado se refiere a una biblioteca COM.|  
|**Source**|Muestra el origen de la referencia de ensamblado. Esta propiedad normalmente contiene la ruta completa y el nombre de archivo del ensamblado al que se refiere la referencia de ensamblado.|  
|**Conjunto de permisos**|Seleccione el conjunto de permisos utilizado para determinar el acceso a la referencia de ensamblado. Para obtener más información acerca de los valores disponibles para esta propiedad, vea <xref:Microsoft.AnalysisServices.ClrAssembly.PermissionSet%2A>.|  
|**Información de suplantación**|Seleccione la información de suplantación que se utilizará al obtener acceso a la referencia de ensamblado. Para más información sobre los valores disponibles para esta propiedad, vea [Elemento ImpersonationInfo &#40;ASSL&#41;](https://docs.microsoft.com/bi-reference/assl/properties/impersonationinfo-element-assl).|  
  
## <a name="see-also"></a>Vea también  
 [Diseñadores y cuadros de diálogo de Analysis Services &#40;datos multidimensionales&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [Administración de ensamblados de modelos multidimensionales](multidimensional-models/multidimensional-model-assemblies-management.md)  
  
  
