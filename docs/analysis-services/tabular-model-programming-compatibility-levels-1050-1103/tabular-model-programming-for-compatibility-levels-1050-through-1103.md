---
title: Programación de modelos tabulares para la compatibilidad de los niveles de 1050 a 1103 | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a1e14033255d45eaacda1d553c71224e11dfe964
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "38054703"
---
# <a name="tabular-model-programming-for-compatibility-levels-1050-through-1103"></a>Programación de modelos tabulares para la compatibilidad de los niveles de 1050 a 1103
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Los modelos tabulares utilizan estructuras relacionales para modelar los datos de Analysis Services utilizados por aplicaciones analíticas y de informes. Estos modelos se ejecutan en una instancia de Analysis Services configurada para el modo tabular, usando un motor de análisis en memoria para el almacenamiento y recorridos de tabla rápidos que agregan y calculan datos conforme se solicitan.  
  
 Si los requisitos de la solución personalizada de BI se satisfacen mejor mediante una base de datos de modelo tabular, puede usar cualquiera de las bibliotecas de cliente e interfaces de programación de Analysis Services para integrar la aplicación con modelos tabulares en una instancia de Analysis Services. Para consultar y calcular datos de modelo tabulares, puede utilizar DAX o MDX incrustado en el código.  
  
 Los objetos que se trabaja mediante programación en AMO, ADOMD.NET, XMLA u OLE DB para los modelos tabulares creados en versiones anteriores de Analysis Services, en los modelos determinados en los niveles de compatibilidad 1050 a 1103, son básicamente el mismo para ambos tabular y soluciones multidimensionales. En concreto, los metadatos del objeto definido para los modelos multidimensionales también se usan para los niveles de compatibilidad de modelo tabular 1050-1103.  
  
 A partir de SQL Server 2016, los modelos tabulares pueden ser creados o actualizados al nivel de compatibilidad 1200 o superior, que usa metadatos tabulares para definir el modelo. Los metadatos y la capacidad de programación son fundamentalmente distintas en este nivel. Consulte [programación de modelos tabulares de nivel de compatibilidad 1200 y superior](../../analysis-services/tabular-model-programming-compatibility-level-1200/tabular-model-programming-for-compatibility-level-1200.md) y [actualizar Analysis Services](../../database-engine/install-windows/upgrade-analysis-services.md) para obtener más información.  
  
## <a name="in-this-section"></a>En esta sección  
 [Anotaciones de CSDL para Business Intelligence &#40;CSDLBI&#41;](../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/csdl-annotations-for-business-intelligence-csdlbi.md)  
  
 [Descripción del modelo de objetos tabulares en la compatibilidad de los niveles de 1050 a 1103](../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/representation/understanding-tabular-object-model-at-levels-1050-through-1103.md)  
  
 [Referencia técnica para las anotaciones de Business Intelligence en CSDL](../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/technical-reference-for-bi-annotations-to-csdl.md)  
  

[Interfaz IMDEmbeddedData](../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/imdembeddeddata-interface.md)


  
  
