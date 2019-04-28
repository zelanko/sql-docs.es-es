---
title: Objetos (Analysis Services - datos multidimensionales) de dimensiones | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- dimensions [Analysis Services], objects
ms.assetid: 7f3d55c7-cccb-4ad0-b6cb-3a2c9992dd68
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c0c64f95b0c366453e1099c80d8e40b217fb7801
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62702461"
---
# <a name="dimension-objects-analysis-services---multidimensional-data"></a>Objetos de dimensión (Analysis Services - Datos multidimensionales)
  Un objeto <xref:Microsoft.AnalysisServices.Dimension> simple se compone de la información básica, atributos y jerarquías. La información básica incluye el nombre de la dimensión, el tipo de la dimensión, el origen de datos, el modo de almacenamiento y otros aspectos. Los atributos definen los datos reales de la dimensión. Los atributos no pertenecen necesariamente a una jerarquía, pero éstas se generan a partir de los atributos. La jerarquía crea listas ordenadas de niveles y define las maneras en que un usuario puede explorar la dimensión.  
  
## <a name="in-this-section"></a>En esta sección  
 Los temas siguientes proporcionan más información acerca del diseño y la implementación de objetos de dimensión.  
  
|Tema|Descripción|  
|-----------|-----------------|  
|[Dimensiones &#40;Analysis Services - Datos multidimensionales&#41;](dimensions-analysis-services-multidimensional-data.md)|En [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], las dimensiones son un componente fundamental de los cubos. Las dimensiones organizan los datos en función de un área de interés para los usuarios, por ejemplo clientes, almacenes o empleados.|  
|[Atributos y jerarquías de atributos](attributes-and-attribute-hierarchies.md)|Las dimensiones son colecciones de atributos que están enlazados a una o varias columnas de una tabla o vista de la vista del origen de datos.|  
|[Relaciones de atributo](attribute-relationships.md)|En [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], atributos dentro de una dimensión siempre se relacionan con directa o indirectamente con el atributo clave. Al definir una dimensión basada en un esquema en estrella, donde todos los atributos de la dimensión se derivan de la misma tabla relacional, se define automáticamente una relación de atributo entre el atributo clave y cada atributo no clave de la dimensión. Al definir una dimensión basada en un esquema de copo de nieve, donde los atributos de la dimensión se derivan de varias tablas relacionadas, se define automáticamente una relación de atributo del modo siguiente:<br /><br /> -Entre el atributo clave y que no son clave cada atributo enlazado a columnas de la tabla de dimensiones principal.<br />-Entre el atributo clave y el atributo enlazado a la clave externa en la tabla secundaria que vincula las tablas de dimensiones subyacente.<br />-Entre el atributo clave está enlazado a externa en la tabla secundaria y cada atributo no clave enlazado a columnas de la tabla secundaria.|  
  
  
