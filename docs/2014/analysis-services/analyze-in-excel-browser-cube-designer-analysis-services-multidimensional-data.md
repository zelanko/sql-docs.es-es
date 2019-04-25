---
title: Analizar en Excel (pestaña explorador, Diseñador de cubos) (Analysis Services - datos multidimensionales) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.browsecube.datapane.f1
- sql12.asvs.ssms.analyzeinexcel.f1
ms.assetid: 890ed457-137e-44ac-9b2c-83344a1b8fc9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: cdd0c98a00b5643c73b1536b7449c855a444aea8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62643520"
---
# <a name="analyze-in-excel-browser-tab-cube-designer-analysis-services---multidimensional-data"></a>Analizar en Excel (pestaña Explorador de cubo del Diseñador de cubos) (Analysis Services - Datos multidimensionales)
  **Analizar en Excel** proporciona al desarrollador de cubos un mecanismo para ver rápidamente cómo se mostraría un proyecto al usuario final. La característica **Analizar en Excel** abre Microsoft Excel, crea una conexión de origen de datos con la base de datos del área de trabajo y agrega automáticamente una tabla dinámica a la hoja de cálculo. Esta característica reemplaza al control Web de Office que, en versiones anteriores, proporcionaba una tabla dinámica incrustada en la pestaña Explorador.  
  
 **Para ver los datos del cubo:**  
  
1.  En [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], en el Explorador de soluciones, haga doble clic en un cubo para abrirlo en el Diseñador de cubos.  
  
2.  Haga clic en la pestaña **Explorador** .  
  
3.  Haga clic en **Volver a conectar** para validar la conexión.  
  
4.  Haga clic en el icono de Excel de la barra de menús.  
  
5.  Cuando le pidan que habilite las conexiones de datos, haga clic en **Habilitar**. Excel se abre a través la conexión de datos actual y agrega una tabla dinámica a la hoja de cálculo para que pueda empezar a examinar los datos.  
  
 Ahora puede generar una tabla dinámica de forma interactiva arrastrando medidas desde la tabla de hechos hasta el área de valores y agregando atributos de dimensión a las áreas de fila y de columna. Si tiene jerarquías, agréguelas a las áreas de fila o de columna. Puede recorrer la jerarquía hacia arriba o hacia abajo para examinar los datos de hechos en diferentes niveles.  
  
 Los objetos y los datos se ven en el contexto del usuario o el rol vigente y de la perspectiva. Con Excel, para conectarse al origen de datos cuando se ejecuta una consulta, se usan las credenciales del usuario actual, no las credenciales especificadas en la página **Información de suplantación** .  
  
> [!NOTE]  
>  Para usar la característica Analizar en Excel, Excel debe estar instalado en el mismo equipo que [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Si Excel no está instalado en el mismo equipo, puede usar Excel en otro equipo y conectarse al cubo como origen de datos. A continuación, podrá agregar manualmente una tabla dinámica a la hoja de cálculo. Los objetos del modelo (tablas, columnas, medidas y KPI) se incluyen como campos en la lista de campos de la tabla dinámica.  
  
 Para obtener más información acerca de la característica **Analizar en Excel** , vea estos recursos:  
  
 [Analizar en Excel &#40;SSAS tabular&#41;](tabular-models/analyze-in-excel-ssas-tabular.md)  
  
 [Analizar un modelo tabular en Excel &#40;SSAS tabular&#41;](tabular-models/analyze-a-tabular-model-in-excel-ssas-tabular.md)  
  
 [Examinar los datos y metadatos de un cubo](multidimensional-models/browse-data-and-metadata-in-cube.md)  
  
## <a name="see-also"></a>Vea también  
 [Explorador &#40;Diseñador de cubos&#41; &#40;Analysis Services - datos multidimensionales&#41;](browser-cube-designer-analysis-services-multidimensional-data.md)   
 [Barra de herramientas &#40;pestaña del explorador, Diseñador de cubos&#41; &#40;Analysis Services - datos multidimensionales&#41;](toolbar-browser-tab-cube-designer-analysis-services-multidimensional-data.md)   
 [Metadatos &#40;pestaña del explorador, Diseñador de cubos&#41; &#40;Analysis Services - datos multidimensionales&#41;](metadata-browser-tab-cube-designer-analysis-services-multidimensional-data.md)   
 [Consulta y filtro &#40;pestaña del explorador, Diseñador de cubos&#41; &#40;Analysis Services - datos multidimensionales&#41;](query-filter-browser-cube-designer-analysis-services-multidimensional-data.md)  
  
  
