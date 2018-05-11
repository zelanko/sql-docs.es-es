---
title: Dimensión objetos (Analysis Services - datos multidimensionales) | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: olap
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6f90b07683e227b140bc33e194b76fe346990dbe
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="dimension-objects-analysis-services---multidimensional-data"></a>Objetos de dimensión (Analysis Services - Datos multidimensionales)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Un objeto <xref:Microsoft.AnalysisServices.Dimension> simple se compone de la información básica, atributos y jerarquías. La información básica incluye el nombre de la dimensión, el tipo de la dimensión, el origen de datos, el modo de almacenamiento y otros aspectos. Los atributos definen los datos reales de la dimensión. Los atributos no pertenecen necesariamente a una jerarquía, pero éstas se generan a partir de los atributos. La jerarquía crea listas ordenadas de niveles y define las maneras en que un usuario puede explorar la dimensión.  
  
## <a name="in-this-section"></a>En esta sección  
 Los temas siguientes proporcionan más información acerca del diseño y la implementación de objetos de dimensión.  
  
|Tema|Description|  
|-----------|-----------------|  
|[Dimensiones & #40; Analysis Services - datos multidimensionales & #41;](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)|En [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], las dimensiones son un componente fundamental de los cubos. Las dimensiones organizan los datos en función de un área de interés para los usuarios, por ejemplo clientes, almacenes o empleados.|  
|[Atributos y jerarquías de atributo](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)|Las dimensiones son colecciones de atributos que están enlazados a una o varias columnas de una tabla o vista de la vista del origen de datos.|  
|[Relaciones de atributo](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md)|En [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], atributos dentro de una dimensión siempre se relacionan directa o indirectamente con el atributo clave. Al definir una dimensión basada en un esquema en estrella, donde todos los atributos de la dimensión se derivan de la misma tabla relacional, se define automáticamente una relación de atributo entre el atributo clave y cada atributo no clave de la dimensión. Al definir una dimensión basada en un esquema de copo de nieve, donde los atributos de la dimensión se derivan de varias tablas relacionadas, se define automáticamente una relación de atributo del modo siguiente:<br /><br /> Entre el atributo clave y cada atributo sin clave enlazado a columnas de la tabla principal de dimensiones.<br /><br /> Entre el atributo clave y el atributo enlazado a la clave externa de la tabla secundaria que vincula las tablas de dimensiones subyacentes.<br /><br /> Entre el atributo enlazado a la clave externa de la tabla secundaria y cada atributo no clave enlazado a las columnas de la tabla secundaria.|  
  
  
