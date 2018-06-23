---
title: Definir el comportamiento de suma parcial (Asistente de Business Intelligence) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.asvs.biwizard.semiadditivememberdetection.f1
ms.assetid: e57080ba-ce96-40f8-bca7-6701d1725b3c
caps.latest.revision: 24
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 79ee4ffdb89c4ee8ccb13f4a4985f6d545f573ad
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36107776"
---
# <a name="define-semiadditive-behavior-business-intelligence-wizard"></a>Definir el comportamiento de suma parcial (Asistente de Business Intelligence)
  Use la página **Definir el comportamiento de suma parcial** para habilitar o deshabilitar el comportamiento de suma parcial en medidas. Este comportamiento determina cómo se agregan a una dimensión de tiempo las medidas que contiene un cubo.  
  
> [!NOTE]  
>  Excepto LastChild, que está disponible en la edición Standard, los comportamientos de suma parcial solo están disponibles en las ediciones Business Intelligence o Enterprise. Además, como el comportamiento de suma parcial solo se define en medidas y no en dimensiones, no verá esta página del Asistente de Business Intelligence si se ha iniciado desde el Diseñador de dimensiones o haciendo clic con el botón derecho en una dimensión en el Explorador de soluciones de [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
## <a name="options"></a>Opciones  
 **Desactivar el comportamiento de suma parcial**  
 Deshabilita el comportamiento de suma parcial en todas las medidas del cubo.  
  
 **El asistente ha detectado el \<nombre de la dimensión > dimensión de cuenta, que contiene miembros de suma parcial. El servidor agregará a los miembros de esta dimensión de acuerdo con el comportamiento de suma parcial especificado para cada tipo de cuenta.**  
 Habilita el comportamiento de suma parcial para las dimensiones de cuentas que contienen miembros de suma parcial. Al seleccionar esta opción establece la función de agregación de todas las medidas en grupos de medida que hacen referencia a la dimensión de cuenta para `ByAccount`.  
  
 Para más información sobre las dimensiones de cuenta, vea [Crear una cuenta financiera de una dimensión de tipo primario-secundario](multidimensional-models/database-dimensions-finance-account-of-parent-child-type.md).  
  
 **Definir el comportamiento de suma parcial para medidas individuales**  
 Habilita el comportamiento de suma parcial y especifica la función de agregación de suma parcial para medidas específicas. La función de agregación se aplica a todas las dimensiones a las que se hace referencia en el grupo de medida que contiene la medida.  
  
 **Medidas**  
 Muestra el nombre de la medida que contiene el cubo.  
  
 **Función de suma parcial**  
 Seleccione la función de agregación para la medida seleccionada. En la tabla siguiente se enumeran las funciones de agregación disponibles.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**AverageOfChildren**|Se agrega devolviendo el promedio de los miembros secundarios de la medida.|  
|`ByAccount`|Se agrega mediante la función de agregación asociada con el tipo de cuenta especificado de un atributo en una dimensión de cuentas.|  
|`Count`|Se agrega mediante la función `Count`.|  
|`DistinctCount`|Se agrega mediante la función `DistinctCount`.|  
|**FirstChild**|Se agrega devolviendo el primer miembro secundario de la medida en una dimensión de tiempo.|  
|**FirstNonEmpty**|Se agrega devolviendo el primer miembro no vacío de la medida en una dimensión de tiempo.|  
|**LastChild**|Se agrega devolviendo el último miembro secundario de la medida en una dimensión de tiempo.|  
|**LastNonEmpty**|Se agrega devolviendo el último miembro no vacío de la medida en una dimensión de tiempo.|  
|`Max`|Se agrega mediante la función `Max`.|  
|`Min`|Se agrega mediante la función `Min`.|  
|**Ninguno**|No se realiza ningún tipo de agregación.|  
|`Sum`|Se agrega mediante la función `Sum`.|  
  
> [!NOTE]  
>  Las selecciones realizadas para esta opción solo se aplican si se ha seleccionado **Define semiadditive behavior for individual members (Definir el comportamiento de suma parcial para miembros individuales)** .  
  
## <a name="see-also"></a>Vea también  
 [Ayuda de F1 de Asistente de Business Intelligence](business-intelligence-wizard-f1-help.md)   
 [Diseñador de cubos &#40;Analysis Services - datos multidimensionales&#41;](cube-designer-analysis-services-multidimensional-data.md)   
 [Diseñador de dimensiones &#40;Analysis Services - datos multidimensionales&#41;](dimension-designer-analysis-services-multidimensional-data.md)  
  
  