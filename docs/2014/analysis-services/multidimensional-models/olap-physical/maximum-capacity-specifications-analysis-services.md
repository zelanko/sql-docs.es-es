---
title: Especificaciones de capacidad máxima (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- objects [Analysis Services], maximum number
- objects [Analysis Services], maximum size
ms.assetid: 49fe1673-b908-4c7a-88ff-415efd294d27
author: minewiskan
ms.author: owend
ms.openlocfilehash: d0495ed563585a5b7427655428a257174673fc02
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/09/2020
ms.locfileid: "84545922"
---
# <a name="maximum-capacity-specifications-analysis-services"></a>Especificaciones de capacidad máxima (Analysis Services)
  En las siguientes tablas se especifican el tamaño y la cantidad máximos de diversos objetos definidos en los componentes de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] en distintos modos de implementación de servidor.  
  
 Este tema contiene las siguientes secciones:  
  
 [Multidimensional y de minería de datos (DeploymentMode=0)](#bkmk_OLAP)  
  
 [SharePoint (DeploymentMode=1)](#bkmk_sharepoint)  
  
 [Tabular (DeploymentMode=2)](#bkmk_vertipaq)  
  
##  <a name="multidimensional-and-data-mining-deploymentmode0"></a><a name="bkmk_OLAP"></a>Multidimensional y minería de datos (DeploymentMode = 0)  
 El modo de almacenamiento MOLAP, que almacena datos y metadatos, tiene límites físicos adicionales en el tamaño de los archivos. Los archivos de cadenas tienen un tamaño máximo de 4 GB de forma predeterminada. Si necesita archivos mayores para los almacenes de cadenas, puede especificar otro arquitectura de almacenamiento de cadenas. Para obtener más información, vea [configurar el almacenamiento de cadenas para dimensiones y particiones](../configure-string-storage-for-dimensions-and-partitions.md).  
  
|Object|Tamaños/números máximos|  
|------------|----------------------------|  
|Bases de datos en una instancia|2^31-1 = 2 147 483 647|  
|Dimensiones de una base de datos|2^31-1 = 2 147 483 647|  
|Atributos de una dimensión|2^31-1 = 2 147 483 647|  
|Miembros de un atributo de dimensión|2^31-1 = 2 147 483 647|  
|Jerarquías definidas por el usuario en una dimensión|2^31-1 = 2 147 483 647|  
|Niveles en una jerarquía definida por el usuario|2^31-1 = 2 147 483 647|  
|Cubos de una base de datos|2^31-1 = 2 147 483 647|  
|Grupos de medida de un cubo|2^31-1 = 2 147 483 647|  
|Medidas de un grupo de medida|2^31-1 = 2 147 483 647|  
|Cálculos de un cubo|2^31-1 = 2 147 483 647|  
|KPI de un cubo|2^31-1 = 2 147 483 647|  
|Acciones de un cubo|2^31-1 = 2 147 483 647|  
|Particiones de un cubo|2^31-1 = 2 147 483 647|  
|Traducciones de un cubo|2^31-1 = 2 147 483 647|  
|Agregaciones de una partición|2^31-1 = 2 147 483 647|  
|Celdas devueltas por una consulta|2^31-1 = 2 147 483 647|  
|Tamaño del registro de la consulta de origen|64 K|  
|Longitud de nombres de objeto|100 caracteres|  
|Número máximo de estados distintos de una columna de atributo de modelo de minería de datos|2^31-1 = 2 147 483 647|  
|Número máximo de atributos considerados (selección de características)|2^31-1 = 2 147 483 647|  
  
 Para obtener más información sobre las directrices de nomenclatura de objetos, vea [objetos y características](../scripting-language-assl/assl-objects-and-object-characteristics.md)de objetos de ASSL.  
  
 Para obtener más información sobre las limitaciones de los orígenes de datos para el procesamiento analítico en línea (OLAP) y la minería de datos, vea [orígenes de datos compatibles &#40;SSAS multidimensional&#41;](../supported-data-sources-ssas-multidimensional.md), [orígenes de datos compatibles &#40;ssas multidimensional&#41;](../supported-data-sources-ssas-multidimensional.md)y [objetos ASSL y características de objetos](../scripting-language-assl/assl-objects-and-object-characteristics.md).  
  
##  <a name="sharepoint-deploymentmode1"></a><a name="bkmk_sharepoint"></a>SharePoint (DeploymentMode = 1)  
  
|Object|Tamaños/números máximos|  
|------------|----------------------------|  
|Bases de datos en una instancia|2^31-1 = 2 147 483 647|  
|Tablas de una base de datos|2^31-1 = 2 147 483 647|  
|Columnas de una tabla|2 ^ 31-1 = **advertencia 2.147.483.647:** el número total de columnas de una tabla depende del número total de medidas y columnas calculadas asociadas a la misma tabla. El número máximo de 'Columnas + Medidas + Columnas calculadas' de una tabla es 2^31-1 = 2.147.483.647|  
|Filas de una tabla|**ADVERTENCIA ilimitada:** con la restricción de que ninguna columna única puede contener más de 1.999.999.997 valores distintos.|  
|Jerarquías de una tabla|2^31-1 = 2 147 483 647|  
|Niveles de una jerarquía|2^31-1 = 2 147 483 647|  
|Relaciones|2^31-1 = 2 147 483 647|  
|Columnas de clave de una tabla|2^31-1 = 2 147 483 647|  
|Medidas de una tabla|2 ^ 31-1 = **advertencia 2.147.483.647:** el número total de medidas de una tabla depende del número total de columnas y columnas calculadas asociadas a la misma tabla. El número máximo de 'Columnas + Medidas + Columnas calculadas' de una tabla es 2^31-1 = 2.147.483.647|  
|Columnas calculadas de una tabla|2 ^ 31-1 = **advertencia 2.147.483.647:** el número total de columnas calculadas de una tabla depende del número total de columnas y medidas asociadas a la misma tabla. El número máximo de 'Columnas + Medidas + Columnas calculadas' de una tabla es 2^31-1 = 2.147.483.647|  
|Celdas devueltas por una consulta|2^31-1 = 2 147 483 647|  
|Tamaño del registro de la consulta de origen|64 K|  
|Longitud de nombres de objeto|100 caracteres|  
  
##  <a name="tabular-deploymentmode2"></a><a name="bkmk_vertipaq"></a>Tabular (DeploymentMode = 2)  
  
|Object|Tamaños/números máximos|  
|------------|----------------------------|  
|Bases de datos en una instancia|2^31-1 = 2 147 483 647|  
|Tablas de una base de datos|2^31-1 = 2 147 483 647|  
|Columnas de una tabla|2 ^ 31-1 = **advertencia 2.147.483.647:** el número total de columnas de una tabla depende del número total de medidas y columnas calculadas asociadas a la misma tabla. El número máximo de 'Columnas + Medidas + Columnas calculadas' de una tabla es 2^31-1 = 2.147.483.647|  
|Filas de una tabla|**ADVERTENCIA ilimitada:** con la restricción de que ninguna columna individual de la tabla puede tener más de 1.999.999.997 valores distintos.|  
|Jerarquías de una tabla|2^31-1 = 2 147 483 647|  
|Niveles de una jerarquía|2^31-1 = 2 147 483 647|  
|Relaciones|2^31-1 = 2 147 483 647|  
|Columnas de clave de una tabla|2^31-1 = 2 147 483 647|  
|Medidas de una tabla|2 ^ 31-1 = **advertencia 2.147.483.647:** el número total de medidas de una tabla depende del número total de columnas y columnas calculadas asociadas a la misma tabla. El número máximo de 'Columnas + Medidas + Columnas calculadas' de una tabla es 2^31-1 = 2.147.483.647|  
|Columnas calculadas de una tabla|2 ^ 31-1 = **advertencia 2.147.483.647:** el número total de columnas calculadas de una tabla depende del número total de columnas y medidas asociadas a la misma tabla. El número máximo de 'Columnas + Medidas + Columnas calculadas' de una tabla es 2^31-1 = 2.147.483.647|  
|Celdas devueltas por una consulta|2^31-1 = 2 147 483 647|  
|Tamaño del registro de la consulta de origen|64 K|  
|Longitud de nombres de objeto|100 caracteres|  
  
## <a name="see-also"></a>Consulte también  
 [Determinar el modo de servidor de una instancia de Analysis Services](../../instances/determine-the-server-mode-of-an-analysis-services-instance.md)   
 [Propiedades generales](../../server-properties/general-properties.md)  
  
  
