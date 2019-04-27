---
title: Propiedades (SSAS Tabular) del proyecto | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.depservconfig.f1
- sql12.asvs.bidtoolset.semmodelprojprop.f1
ms.assetid: 333c1fc0-361c-415a-bd68-4e057f67bcb7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 31a335797ad7a40fda7002b910127bb139af3f1b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62756794"
---
# <a name="project-properties-ssas-tabular"></a>Propiedades del proyecto (SSAS tabular)
  En este tema se describen las propiedades del proyecto de modelos. Todos los proyectos de modelos tabulares tienen propiedades de opciones de implementación y de servidor de implementación que especifican cómo se implementan el proyecto y el modelo. Por ejemplo, el servidor en el que se implementará el modelo y el nombre de la base de datos de modelo implementada. Estos valores son diferentes de las propiedades del modelo, que afectan a la base de datos del área de trabajo del modelo. Las propiedades del proyecto descritas a continuación se muestran en cuadro de diálogo de propiedades de modo, que es diferente de la ventana de propiedades utilizada para mostrar otros tipos de propiedades. Para ver las propiedades del proyecto modal, en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], en el **Explorador de soluciones**, haga clic con el botón secundario en el proyecto y, a continuación, haga clic en **Propiedades**.  
  
 Secciones de este tema:  
  
-   [Propiedades de proyecto](#bkmk_proj_properties)  
  
-   [Para configurar las opciones de implementación y servidor de implementación de propiedades](#bkmk_conf_proj_settings)  
  
##  <a name="bkmk_proj_properties"></a> Propiedades del proyecto  
 **Opciones de implementación**  
  
|Property|Valor predeterminado|Descripción|  
|--------------|---------------------|-----------------|  
|**Opción de procesamiento**|**Default**|De manera predeterminada, Analysis Services determinará el tipo de procesamiento necesario cuando se implementen los cambios en los objetos. Eso se suele traducir en el tiempo de implementación más breve. Sin embargo, también puede elegir un procesamiento completo o ningún procesamiento durante cada implementación.|  
|**Implementación transaccional**|**False**|Especifica si la implementación del modelo es o no transaccional. De manera predeterminada, la implementación de todos los objetos modificados no es transaccional con el procesamiento de dichos objetos implementados. La implementación puede ser correcta y persistir aunque se produzca un error de procesamiento. Puede cambiar este comportamiento para incluir la implementación y el procesamiento en una sola transacción.|  
|**Modo de consulta**|**In-Memory**|Especifica el origen desde el que se devuelven los resultados de la consulta. Para más información, vea [Modo DirectQuery &#40;SSAS tabular&#41;](directquery-mode-ssas-tabular.md).|  
  
 **Servidor de implementación**  
  
|Propiedad|Valor predeterminado|Descripción|  
|--------------|---------------------|-----------------|  
|**Server**|**localhost**|Especifica una instancia de Analysis Services. De forma predeterminada, los modelos se implementan en la instancia predeterminada de Analysis Services del equipo local. Puede cambiar este valor para especificar una instancia con nombre del equipo local o cualquier instancia de cualquier equipo remoto en que tenga permiso para crear objetos de Analysis Services. Normalmente, serán permisos de administrador.<br /><br /> El valor predeterminado de esta propiedad se puede modificar mediante la propiedad Servidor de implementación predeterminado de la página Implementación de la configuración de Analysis Server en el cuadro de diálogo Herramientas\Opciones. Para más información, vea [Configurar las propiedades predeterminadas de modelado de datos y de implementación &#40;SSAS tabular&#41;](properties-ssas-tabular.md).|  
|**Edición**|**Desarrollador**|Especifica la edición del servidor de Analysis Services en la que se implementará el modelo. La edición del servidor define varias características que se pueden incorporar al proyecto.|  
|**Base de datos**|**Modelo**|Especifica el nombre de la base de datos de Analysis Services en la que se crearán instancias de los objetos de modelo durante la implementación. Este nombre se especificará en una conexión de datos o en un archivo de conexión de datos .rsds. Se recomienda que el nombre refleje el tipo de análisis que se realizará usando el modelo, por ejemplo, AdventureWorksSalesModel.<br /><br /> **\*\* Importante \* \***  para evitar que los nombres duplicados en los modelos implementados, debería cambiar el **base de datos** configuración de nombre de propiedad para que refleje el propósito del modelo. Cuando los usuarios se conecten al modelo como origen de datos, este es el nombre que verán.|  
|**Nombre del cubo**|**Modelo**|Especifica el nombre del cubo de base de datos tal como se muestra en una conexión de datos del cliente de informes.|  
|**Versión**|**11.0**|Versión de la instancia de Analysis Services en la que se implementará el proyecto.|  
  
 **Opciones de DirectQuery**  
  
|Property|Valor predeterminado|Descripción|  
|--------------|---------------------|-----------------|  
|**Configuración de suplantación**|**Default**|Especifica las credenciales utilizadas para conectar a los orígenes de datos de un modelo que se ejecuta en el modo DirectQuery. Estas credenciales son diferentes de las credenciales de suplantación que se usan en el modo In-Memory predeterminado. Para más información, vea [Suplantación &#40;SSAS tabular&#41;](impersonation-ssas-tabular.md).|  
  
###  <a name="bkmk_conf_proj_settings"></a> Para configurar las opciones de implementación y servidor de implementación de propiedades  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], en el **Explorador de soluciones**, haga clic con el botón derecho en el proyecto y, luego, haga clic en **Propiedades**.  
  
2.  En la ventana **Propiedades** , haga clic en una propiedad y, a continuación, escriba un valor o haga clic en la flecha abajo para seleccionar una opción de configuración.  
  
## <a name="see-also"></a>Vea también  
 [Configurar las propiedades predeterminadas de modelado de datos y de implementación &#40;SSAS tabular&#41;](properties-ssas-tabular.md)   
 [Propiedades del modelo &#40;SSAS tabular&#41;](model-properties-ssas-tabular.md)   
 [Implementación de soluciones de modelos tabulares &#40;SSAS tabular&#41;](tabular-model-solution-deployment-ssas-tabular.md)  
  
  
