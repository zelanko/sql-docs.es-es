---
title: "Especificaciones de capacidad máxima (Analysis Services) | Documentos de Microsoft"
ms.custom: 
ms.date: 07/27/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- objects [Analysis Services], maximum number
- objects [Analysis Services], maximum size
ms.assetid: 49fe1673-b908-4c7a-88ff-415efd294d27
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 8e60e818b40d2aa7c266903a23d0fec908039b44
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/15/2018
---
# <a name="maximum-capacity-specifications-analysis-services"></a>Especificaciones de capacidad máxima (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
En las siguientes tablas se especifican el tamaño y la cantidad máximos de diversos objetos definidos en los componentes de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] en distintos modos de implementación de servidor.  
  
 Este tema contiene las siguientes secciones:  
  
 [Multidimensional y minería de datos (DeploymentMode = 0)](#bkmk_OLAP)  
  
 [SharePoint (DeploymentMode = 1)](#bkmk_sharepoint)  
  
 [Tabulares (DeploymentMode = 2)](#bkmk_vertipaq)  
  
##  <a name="bkmk_OLAP">Multidimensional y minería de datos (DeploymentMode = 0)</a>  
 El modo de almacenamiento MOLAP, que almacena datos y metadatos, tiene límites físicos adicionales en el tamaño de los archivos. Los archivos de cadenas tienen un tamaño máximo de 4 GB de forma predeterminada. Si necesita archivos mayores para los almacenes de cadenas, puede especificar otro arquitectura de almacenamiento de cadenas. Para obtener más información, consulte [configurar el almacenamiento de cadenas para dimensiones y particiones](../../../analysis-services/multidimensional-models/configure-string-storage-for-dimensions-and-partitions.md).  
  
|Object|Tamaños/números máximos|  
|------------|----------------------------|  
|Bases de datos en una instancia|2^31-1 = 2,147,483,647|  
|Dimensiones de una base de datos|2^31-1 = 2,147,483,647|  
|Atributos de una dimensión|2^31-1 = 2,147,483,647|  
|Miembros de un atributo de dimensión|2^31-1 = 2,147,483,647|  
|Jerarquías definidas por el usuario en una dimensión|2^31-1 = 2,147,483,647|  
|Niveles en una jerarquía definida por el usuario|2^31-1 = 2,147,483,647|  
|Cubos de una base de datos|2^31-1 = 2,147,483,647|  
|Grupos de medida de un cubo|2^31-1 = 2,147,483,647|  
|Medidas de un grupo de medida|2^31-1 = 2,147,483,647|  
|Cálculos de un cubo|2^31-1 = 2,147,483,647|  
|KPI de un cubo|2^31-1 = 2,147,483,647|  
|Acciones de un cubo|2^31-1 = 2,147,483,647|  
|Particiones de un cubo|2^31-1 = 2,147,483,647|  
|Traducciones de un cubo|2^31-1 = 2,147,483,647|  
|Agregaciones de una partición|2^31-1 = 2,147,483,647|  
|Celdas devueltas por una consulta|2^31-1 = 2,147,483,647|  
|Tamaño del registro de la consulta de origen|64K|  
|Longitud de nombres de objeto|100 caracteres|  
|Número máximo de estados distintos de una columna de atributo de modelo de minería de datos|2^31-1 = 2,147,483,647|  
|Número máximo de atributos considerados (selección de características)|2^31-1 = 2,147,483,647|  
  
 Para obtener más información acerca de las directrices de nomenclatura de objetos, consulte [ASSL y características de objetos](../../../analysis-services/multidimensional-models/scripting-language-assl/assl-objects-and-object-characteristics.md).  
  
 Para obtener más información acerca de las limitaciones de origen de datos de procesamiento analítico en línea (OLAP) y minería de datos, vea [admite orígenes de datos &#40; SSAS - Multidimensional &#41; ](../../../analysis-services/multidimensional-models/supported-data-sources-ssas-multidimensional.md), [Admite orígenes de datos &#40; SSAS - Multidimensional &#41; ](../../../analysis-services/multidimensional-models/supported-data-sources-ssas-multidimensional.md), y [ASSL y características de objetos](../../../analysis-services/multidimensional-models/scripting-language-assl/assl-objects-and-object-characteristics.md).  
  
##  <a name="bkmk_sharepoint">SharePoint (DeploymentMode = 1)</a>  
  
|Object|Tamaños/números máximos|  
|------------|----------------------------|  
|Bases de datos en una instancia|2^31-1 = 2,147,483,647|  
|Tablas de una base de datos|2^31-1 = 2,147,483,647|  
|Columnas de una tabla|2^31-1 = 2,147,483,647<br /><br /> **Advertencia:** número Total de columnas de una tabla depende del número total de medidas y columnas calculadas asociadas a la misma tabla.<br /><br /> El número máximo de 'Columnas + Medidas + Columnas calculadas' de una tabla es 2^31-1 = 2.147.483.647|  
|Filas de una tabla|Sin límite<br /><br /> **Advertencia:** con la restricción de que ninguna columna puede contener más de 1.999.999.997 valores distintos.|  
|Jerarquías de una tabla|2^31-1 = 2,147,483,647|  
|Niveles de una jerarquía|2^31-1 = 2,147,483,647|  
|Relaciones|2^31-1 = 2,147,483,647|  
|Columnas de clave de una tabla|2^31-1 = 2,147,483,647|  
|Medidas de una tabla|2^31-1 = 2,147,483,647<br /><br /> **Advertencia:** número Total de medidas en una tabla depende del número total de columnas y columnas calculadas asociadas a la misma tabla.<br /><br /> El número máximo de 'Columnas + Medidas + Columnas calculadas' de una tabla es 2^31-1 = 2.147.483.647|  
|Columnas calculadas de una tabla|2^31-1 = 2,147,483,647<br /><br /> **Advertencia:** número Total de columnas calculadas de una tabla depende del número total de columnas y las medidas asociadas a la misma tabla.<br /><br /> El número máximo de 'Columnas + Medidas + Columnas calculadas' de una tabla es 2^31-1 = 2.147.483.647|  
|Celdas devueltas por una consulta|2^31-1 = 2,147,483,647|  
|Tamaño del registro de la consulta de origen|64K|  
|Longitud de nombres de objeto|100 caracteres|  
  
##  <a name="bkmk_vertipaq">Tabulares (DeploymentMode = 2)</a>  
Los siguientes son límites teóricos. Rendimiento se verá reducido en los números más bajos.   

|Object|Tamaños/números máximos|  
|------------|----------------------------|  
|Bases de datos en una instancia|16,000|  
|Número combinado de tablas y columnas de una base de datos|16,000|  
|Filas de una tabla|Sin límite<br /><br /> **Advertencia:** con la restricción de que ninguna columna de la tabla puede tener más de 1.999.999.997 valores distintos.|  
|Jerarquías de una tabla|15,999|  
|Niveles de una jerarquía|15,999|  
|Relaciones|8,000|  
|Columnas de clave de tabla todos los|15,999|  
|Medidas en una de las tablas|2^31-1 = 2,147,483,647|  
|Celdas devueltas por una consulta|2^31-1 = 2,147,483,647|  
|Tamaño del registro de la consulta de origen|64K|  
|Longitud de nombres de objeto|512 caracteres|  
  
## <a name="see-also"></a>Vea también  
 [Determinar el modo de servidor de una instancia de Analysis Services](../../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)   
 [Propiedades generales](../../../analysis-services/server-properties/general-properties.md)  
  
  
