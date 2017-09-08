---
title: "Dimensión objetos (Analysis Services - datos multidimensionales) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- dimensions [Analysis Services], objects
ms.assetid: 7f3d55c7-cccb-4ad0-b6cb-3a2c9992dd68
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 68fa5e37c0cc3620417f916ff35dcd6e3402d615
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="dimension-objects-analysis-services---multidimensional-data"></a>Objetos de dimensión (Analysis Services - Datos multidimensionales)
  Un objeto <xref:Microsoft.AnalysisServices.Dimension> simple se compone de la información básica, atributos y jerarquías. La información básica incluye el nombre de la dimensión, el tipo de la dimensión, el origen de datos, el modo de almacenamiento y otros aspectos. Los atributos definen los datos reales de la dimensión. Los atributos no pertenecen necesariamente a una jerarquía, pero éstas se generan a partir de los atributos. La jerarquía crea listas ordenadas de niveles y define las maneras en que un usuario puede explorar la dimensión.  
  
## <a name="in-this-section"></a>En esta sección  
 Los temas siguientes proporcionan más información acerca del diseño y la implementación de objetos de dimensión.  
  
|Tema|Description|  
|-----------|-----------------|  
|[Dimensiones &#40;Analysis Services - Datos multidimensionales&#41;](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)|En [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], las dimensiones son un componente fundamental de los cubos. Las dimensiones organizan los datos en función de un área de interés para los usuarios, por ejemplo clientes, almacenes o empleados.|  
|[Atributos y jerarquías de atributos](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)|Las dimensiones son colecciones de atributos que están enlazados a una o varias columnas de una tabla o vista de la vista del origen de datos.|  
|[Relación de los atributos](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md)|En [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], atributos dentro de una dimensión siempre se relacionan directa o indirectamente con el atributo clave. Al definir una dimensión basada en un esquema en estrella, donde todos los atributos de la dimensión se derivan de la misma tabla relacional, se define automáticamente una relación de atributo entre el atributo clave y cada atributo no clave de la dimensión. Al definir una dimensión basada en un esquema de copo de nieve, donde los atributos de la dimensión se derivan de varias tablas relacionadas, se define automáticamente una relación de atributo del modo siguiente:<br /><br /> Entre el atributo clave y cada atributo sin clave enlazado a columnas de la tabla principal de dimensiones.<br /><br /> Entre el atributo clave y el atributo enlazado a la clave externa de la tabla secundaria que vincula las tablas de dimensiones subyacentes.<br /><br /> Entre el atributo enlazado a la clave externa de la tabla secundaria y cada atributo no clave enlazado a las columnas de la tabla secundaria.|  
  
  
