---
title: Consulta y filtro (pestaña explorador, diseñador de cubos) (Analysis Services-datos multidimensionales) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.browsecube.filterpane.f1
ms.assetid: f5cf0bb1-3afb-4856-a2ef-614deb4e7e49
author: minewiskan
ms.author: owend
ms.openlocfilehash: aa501e2a5b23f32fbd10d244788b1e6e938e938b
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/09/2020
ms.locfileid: "84539737"
---
# <a name="query-and-filter-browser-tab-cube-designer-analysis-services---multidimensional-data"></a>Consulta y filtro (pestaña Explorador del Diseñador de cubos) (Analysis Services - Datos multidimensionales)
  Este área de la pestaña **Explorador** en el Diseñador de cubos contiene un área de consulta y de filtro para ayudar a elegir datos del cubo y utilizarlos en procesos de examen o en consultas. Puede agregar todos los objetos de cubo que desee y luego ver los resultados en el área de datos, o exportar los resultados en un informe utilizando Analizar en Excel para visualizar cómo verían los datos los usuarios finales.  
  
> [!WARNING]  
>  Cuando se trabaja con datos en este área, el **Explorador** utiliza el modo de diseño gráfico de forma predeterminada. Sin embargo, puede editar la consulta directamente mediante MDX, haciendo clic en el botón de alternancia **Modo de diseño** . Cuando realiza esta acción, el panel que permite diseñar filtros en dimensiones desaparece. Si desea agregar un filtro, puede volver al modo de diseño gráfico.  
  
 De forma predeterminada, para conectarse al origen de datos cuando se ejecuta una consulta se utilizan las credenciales del usuario actual, no las credenciales especificadas en la página **Información de suplantación** . Sin embargo, también puede cambiar el contexto de usuario para la consulta o el informe haciendo clic en **Cambiar usuario** en la **Barra de herramientas**.  
  
## <a name="options"></a>Opciones  
 **Dimensión**  
 Seleccione la dimensión en la que segmentar el subcubo.  
  
 **Hierarchy**  
 Seleccione la jerarquía en la que segmentar el subcubo.  
  
 **Operador**  
 Seleccione el operador que define cómo se aplica la expresión de **Expresión de filtro** en la jerarquía seleccionada. En la tabla siguiente se describen los operadores disponibles.  
  
|Value|Descripción|  
|-----------|-----------------|  
|**Igual**|Los resultados están restringidos al conjunto definido en **Expresión de filtro**.|  
|**No es igual**|Los resultados están restringidos a los miembros excluidos por el conjunto definido en **Expresión de filtro**.|  
|**En**|Los resultados están restringidos al conjunto con nombre seleccionado en **Expresión de filtro**.|  
|**No en el**|Los resultados están restringidos a los miembros excluidos por el conjunto con nombre seleccionado en **Expresión de filtro**.|  
|**Contiene**|El resultado se restringe a los miembros cuyos nombres contienen la cadena de **Expresión de filtro**.|  
|**Comienza por**|El resultado se restringe a los miembros cuyos nombres comienzan con la cadena de **Expresión de filtro**.|  
|**Intervalo (Inclusivo)**|El resultado se restringe al intervalo elegido en **Expresión de filtro**.|  
|**Intervalo (Exclusivo)**|El resultado se restringe a los miembros excluidos por el intervalo elegido en **Expresión de filtro**.|  
|**MDX**|El resultado se restringe a la expresión MDX (Expresiones multidimensionales) establecida en **Expresión de filtro**.|  
  
 **Expresión de filtro**  
 Escriba la expresión que debe evaluar el **Operador**, que restringe los resultados que se van a examinar.  
  
> [!NOTE]  
>  Este campo es un elemento de entrada de datos dinámico que cambia el aspecto para reflejar los tipos de datos necesarios para el operador seleccionado.  
  
## <a name="see-also"></a>Consulte también  
 [Diseñador de cubos &#40;Analysis Services de datos multidimensionales&#41;](cube-designer-analysis-services-multidimensional-data.md)   
 [Explorador de cubos &#40;&#41; &#40;Analysis Services de datos multidimensionales&#41;](browser-cube-designer-analysis-services-multidimensional-data.md)   
 [Barra de herramientas &#40;pestaña explorador, diseñador de cubos&#41; &#40;Analysis Services-datos multidimensionales&#41;](toolbar-browser-tab-cube-designer-analysis-services-multidimensional-data.md)   
 [Analizar en Excel &#40;pestaña explorador, diseñador de cubos&#41; &#40;Analysis Services de datos multidimensionales&#41;](analyze-in-excel-browser-cube-designer-analysis-services-multidimensional-data.md)   
 [Metadatos &#40;pestaña explorador, diseñador de cubos&#41; &#40;Analysis Services-datos multidimensionales&#41;](metadata-browser-tab-cube-designer-analysis-services-multidimensional-data.md)  
  
  
