---
title: Objetos de ASSL y características de objeto | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- reference exceptions [Analysis Services Scripting Language]
- ASSL, objects
- inheritance [Analysis Services Scripting Language]
- localized names [Analysis Services Scripting Language]
- objects [Analysis Services Scripting Language]
- names [Analysis Services Scripting Language]
- Analysis Services Scripting Language, objects
- expansion [Analysis Services Scripting Language]
ms.assetid: 6e5c28b5-c0bc-4ccd-82e5-e174bbb71386
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: aee5e7b94aaaca2b35e34f8c4d49c2834189f114
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62736620"
---
# <a name="assl-objects-and-object-characteristics"></a>Objetos y características de objetos ASSL
  Los objetos en ASSL (Analysis Services Scripting Language) siguen instrucciones concretas con respecto a los grupos de objetos, herencia, nomenclatura, expansión y procesamiento.  
  
## <a name="object-groups"></a>Grupos de objetos  
 Todos [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] los objetos tienen una representación XML. Los objetos están divididos en dos grupos:  
  
 **Objetos principales**  
 Los objetos principales se pueden crear, modificar y eliminar de forma independiente. Los objetos principales incluyen:  
  
-   Servidores  
  
-   Bases de datos  
  
-   Dimensions  
  
-   Cubos  
  
-   Grupos de medida  
  
-   Particiones  
  
-   perspectivas  
  
-   Modelos de minería de datos  
  
-   Roles  
  
-   Comandos asociados a un servidor o base de datos  
  
-   Orígenes de datos  
  
 Los objetos principales cuentan con las siguientes propiedades para realizar el seguimiento de su historial y estado.  
  
-   `CreatedTimestamp`  
  
-   `LastSchemaUpdate`  
  
-   
  `LastProcessed` (donde corresponda)  
  
> [!NOTE]  
>  La clasificación de un objeto como un objeto principal afecta a la manera en que una instancia de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] trata ese objeto y la manera en que se trata ese objeto en el lenguaje de definición de objeto. Sin embargo, esta clasificación no garantiza que las herramientas de administración y desarrollo de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] permitirán la creación, modificación o eliminación independiente de estos objetos.  
  
 **Objetos secundarios**  
 Los objetos secundarios solo se pueden crear, modificar o eliminar como parte de la creación, modificación o eliminación del objeto principal primario. Los objetos secundarios incluyen:  
  
-   Jerarquías y niveles  
  
-   Atributos  
  
-   medidas  
  
-   Columnas de modelo de minería de datos  
  
-   Comandos asociados a un cubo  
  
-   Agregaciones  
  
## <a name="object-expansion"></a>Expansión de objetos  
 La restricción `ObjectExpansion` se puede usar para controlar el grado de expansión para XML de ASSL que devuelve el servidor. Esta restricción tiene las opciones que se muestran en la tabla siguiente.  
  
|Valor de enumeración|Permitido para \<Alter>|Descripción|  
|-----------------------|---------------------------|-----------------|  
|*ReferenceOnly*|no|Devuelve solamente el nombre, identificador y marca de tiempo para el objeto solicitado y para todos los objetos principales contenidos de forma recursiva.|  
|*ObjectProperties*|sí|Expande el objeto solicitado y los objetos secundarios contenidos, pero no devuelve los objetos principales contenidos.|  
|*ExpandObject*|no|Igual que *ObjectProperties*, pero también devuelve el nombre, identificador y marca de tiempo de los objetos principales contenidos.|  
|*ExpandFull*|sí|Expande totalmente el objeto solicitado y todos los objetos contenidos de forma recursiva.|  
  
 Esta sección de referencia de ASSL describe la representación *ExpandFull* . Todos los demás niveles `ObjectExpansion` se derivan de este nivel.  
  
## <a name="object-processing"></a>Procesamiento de objetos  
 ASSL incluye elementos o propiedades de solo lectura (por ejemplo, `LastProcessed`) que se pueden leer desde la instancia de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], pero que se omiten cuando los scripts de comando se envían a la instancia. 
  [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] omite los valores modificados de los elementos de solo lectura sin advertencias o errores.  
  
 
  [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] también omite las propiedades que no son adecuadas o que son irrelevantes sin provocar errores de validación. Por ejemplo, el elemento X únicamente debería estar presente cuando el elemento Y tiene un valor determinado. La instancia de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] omite el elemento X en lugar de validar ese elemento con el valor del elemento Y.  
  
  
