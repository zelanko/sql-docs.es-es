---
title: Perspectivas | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- ready-only cube view
- OLAP objects [Analysis Services], perspectives
- storing data [Analysis Services], perspectives
- perspectives [Analysis Services]
- cubes [Analysis Services], perspectives
- visibility [Analysis Services]
- storage [Analysis Services], perspectives
ms.assetid: b064171e-b1b4-4f32-95e5-59e1b831c4c9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2856bca26e8a49ffdb2ed5187479434c7762015b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62702627"
---
# <a name="perspectives"></a>perspectivas
  Una perspectiva es una definición que permite a los usuarios ver un cubo de una manera más fácil. Una perspectiva es un subconjunto de las características de un cubo. La perspectiva permite a los administradores crear vistas de un cubo, lo que ayuda a los usuarios a centrarse en los datos más pertinentes para ellos. Una perspectiva contiene subconjuntos de todos los objetos de un cubo. No puede incluir elementos que no están definidos en el cubo primario.  
  
 Un objeto <xref:Microsoft.AnalysisServices.Perspective> simple se compone de la información básica, dimensiones, grupos de medida, cálculos, KPI y acciones. La información básica incluye el nombre y la medida predeterminada de la perspectiva. Las dimensiones son un conjunto de las dimensiones del cubo. Los grupos de medida son un subconjunto de los grupos de medida del cubo. Los cálculos son un subconjunto de los cálculos del cubo. Los KPI son un subconjunto de los KPI del cubo. Las acciones son un subconjunto de las acciones del cubo.  
  
 Para usar la perspectiva, el cubo debe estar actualizado y haberse procesado.  
  
 Los cubos pueden ser objetos muy complejos para que los usuarios [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]los exploren. Un solo cubo puede representar el contenido de un almacenamiento de datos completo, con varios grupos de medida en un cubo que representan varias tablas de hechos y varias dimensiones basadas en varias tablas de dimensiones. Un cubo así puede ser muy complejo y eficaz, pero resultar desalentador para los usuarios que solo necesitan interactuar con una pequeña parte del cubo para satisfacer sus requisitos de informes y de Business Intelligence.  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] En [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], puede utilizar una perspectiva para reducir la complejidad percibida de un cubo en [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Una perspectiva define un subconjunto visible de un cubo que ofrece puntos de vista centrados en el cubo, específicos del negocio o la aplicación. La perspectiva controla la visibilidad de los objetos que contiene un cubo. Los siguientes objetos pueden mostrarse u ocultarse en una perspectiva:  
  
-   Dimensions  
  
-   Atributos  
  
-   Jerarquías  
  
-   Grupos de medida  
  
-   medidas  
  
-   Indicadores clave de rendimiento (KPI)  
  
-   Cálculos (miembros calculados, conjuntos con nombre y comandos de script)  
  
-   Acciones  
  
 Por ejemplo, el cubo **Adventure Works** de la [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] base [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] de datos de ejemplo contiene once grupos de medida y veinte dimensiones de cubo diferentes, que representan ventas, previsiones de ventas y datos financieros. Una aplicación cliente puede hacer referencia directa al cubo completo, pero esto puede resultar abrumador para un usuario que intenta extraer información básica de previsiones de ventas. En su lugar, el mismo usuario puede utilizar la perspectiva de **destinos de ventas** para limitar la vista del cubo de **Adventure Works** a solo los objetos relevantes para la previsión de ventas.  
  
 Se puede hacer referencia directa a los objetos de un cubo que no son visibles para el usuario en una perspectiva y recuperarlos mediante XML for Analysis (XMLA), MDX (Expresiones multidimensionales) o instrucciones de Extensiones de minería de datos (DMX). Las perspectivas no restringen el acceso a los objetos de un cubo y no deben usarse con este fin; en lugar de ello, se usan para proporcionar una mejor experiencia para el usuario al obtener acceso a un cubo.  
  
 Una perspectiva es una vista de solo lectura del cubo; no se pueden cambiar los nombres de los objetos ni los objetos del cubo en una perspectiva. De forma similar, el comportamiento o las características de un cubo, como el uso de totales visuales, no se puede cambiar en una perspectiva.  
  
## <a name="security"></a>Seguridad  
 Las perspectivas no están diseñadas para usarse como mecanismo de seguridad, sino como una herramienta para proporcionar una mejor experiencia para el usuario en las aplicaciones de Business Intelligence. Toda la seguridad de una determinada perspectiva se hereda del cubo subyacente. Por ejemplo, las perspectivas no pueden proporcionar acceso a objetos de un cubo al que el usuario no tiene acceso. - La seguridad del cubo se debe resolver para tener acceso a objetos del cubo mediante una perspectiva.  
  
  
