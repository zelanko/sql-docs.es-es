---
title: Propiedades (SSAS Tabular) de la tabla | Documentos de Microsoft
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.custom: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.asvs.bidtoolset.tableprop.f1
ms.assetid: 16d3347b-7e43-4a6b-9956-fdd6ede092e6
caps.latest.revision: "10"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: d94c318d63f68b3fe23d903526bad398fff438e5
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/08/2017
---
# <a name="table-properties-ssas-tabular"></a>Propiedades de la tabla (SSAS tabular)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]Este tema describen las propiedades de tabla de modelo tabular. Las propiedades que se describen aquí son diferentes de las del cuadro de diálogo Editar propiedades de tabla, que definen qué columnas del origen se importan.  
  
 Secciones de este tema:  
  
-   [Propiedades de tabla](#bkmk_properties)  
  
-   [Configuración de propiedades de tabla](#bkmk_config_prop)  
  
##  <a name="bkmk_properties"></a> Propiedades de tabla  
 **Básico**  
  
|Propiedad|Valor predeterminado|Description|  
|--------------|---------------------|-----------------|  
|**Nombre de conexión**|\<nombre de conexión >|Nombre de la conexión con el origen de datos de la tabla.<br /><br /> Para modificar la conexión, haga clic en el botón.|  
|**Oculto**|False|Especifica si la tabla se oculta en las listas de campos del cliente de informes.|  
|**Particiones**||Las particiones de la tabla no se muestran en la ventana **Propiedades** . Para ver, crear o modificar las particiones, haga clic en el botón para abrir el Administrador de particiones.|  
|**Datos de origen**||El origen de datos de la tabla no se pueden mostrar en la ventana **Propiedades** . Para ver o modificar los datos de origen, haga clic en el botón para abrir el cuadro de diálogo Editar propiedades de tabla.|  
|**Descripción de tabla**||Descripción de la tabla.<br /><br /> En [!INCLUDE[ssGeminiClient](../../includes/ssgeminiclient-md.md)], si un usuario final coloca el cursor sobre esta tabla en la lista de campos, aparece la descripción como una información sobre herramientas.|  
|**Nombre de tabla**|\<nombre descriptivo >|Especifica el nombre descriptivo de la tabla. El nombre de tabla puede especificar cuándo se importa una tabla con el Asistente para la importación de tablas o en cualquier momento después de la importación. El nombre de tabla en el modelo puede ser diferente de la tabla asociada en el origen. El nombre descriptivo de la tabla aparece en la lista de campos de la aplicación cliente de informes como en la base de datos modelo en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].|  
  
 **Propiedades de informes**  
  
 Para obtener descripciones detalladas e información sobre la configuración de propiedades de informes, vea [Propiedades de informes de Vista avanzada &#40;SSAS tabular&#41;](../../analysis-services/tabular-models/power-view-reporting-properties-ssas-tabular.md).  
  
|Propiedad|Valor predeterminado|Description|  
|--------------|---------------------|-----------------|  
|**Conjunto de campos predeterminado**|||  
|Comportamiento de tabla|||  
  
##  <a name="bkmk_config_prop"></a> Configuración de propiedades de tabla  
  
1.  En el diseñador de modelos, en la vista de datos, haga clic en una tabla (pestaña), o bien, en la vista de diagramas, haga clic en un encabezado de tabla.  
  
2.  En la ventana **Propiedades** , haga clic en una propiedad y, a continuación, escriba un valor o haga clic en el botón de opciones de configuración adicionales.  
  
  
