---
title: "Niveles de programación de modelo tabular de compatibilidad 1050 a través de 1103 | Documentos de Microsoft"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0ceb461e-12c1-44ea-97ac-b99bf308676b
caps.latest.revision: 16
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a125fb39f8cd8cf8f2024b18454dec30c1c15b97
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="tabular-model-programming-for-compatibility-levels-1050-through-1103"></a>Programación de modelo tabular para la compatibilidad 1050 1103 a través de niveles

[!INCLUDE[ssas-appliesto-sqlas-all](../../includes/ssas-appliesto-sqlas-all.md)]

  Los modelos tabulares utilizan estructuras relacionales para modelar los datos de Analysis Services utilizados por aplicaciones analíticas y de informes. Estos modelos se ejecutan en una instancia de Analysis Services configurada para el modo tabular, usando un motor de análisis en memoria para el almacenamiento y recorridos de tabla rápidos que agregan y calculan datos conforme se solicitan.  
  
 Si los requisitos de la solución personalizada de BI se satisfacen mejor mediante una base de datos de modelo tabular, puede usar cualquiera de las bibliotecas de cliente e interfaces de programación de Analysis Services para integrar la aplicación con modelos tabulares en una instancia de Analysis Services. Para consultar y calcular datos de modelo tabulares, puede utilizar DAX o MDX incrustado en el código.  
  
 Para los modelos tabulares creados en versiones anteriores de Analysis Services, en los modelos determinados en niveles de compatibilidad 1050 a través de 1103, los objetos que se trabaja mediante programación en AMO, ADOMD.NET, XMLA u OLE DB son fundamentalmente las mismas para ambos tabular y soluciones multidimensionales. En concreto, los metadatos del objeto definido para los modelos multidimensionales también sirve para los niveles de compatibilidad de modelo tabular 1050-1103.  
  
 A partir de SQL Server 2016, los modelos tabulares pueden ser creados o actualizados al nivel de compatibilidad de 1200 o superior, que usa metadatos tabulares para definir el modelo. Metadatos y la capacidad de programación son fundamentalmente diferentes en este nivel. Vea [Tabular modelo de programación para la compatibilidad de nivel 1200 y versiones posteriores](../../analysis-services/tabular-model-programming-compatibility-level-1200/tabular-model-programming-for-compatibility-level-1200.md) y [actualizar Analysis Services](../../database-engine/install-windows/upgrade-analysis-services.md) para obtener más información.  
  
## <a name="in-this-section"></a>En esta sección  
 [Anotaciones de CSDL para Business Intelligence &#40;CSDLBI&#41;](../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/csdl-annotations-for-business-intelligence-csdlbi.md)  
  
 [Descripción del modelo de objetos tabulares en compatibilidad 1050 1103 a través de niveles](../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/representation/understanding-tabular-object-model-at-levels-1050-through-1103.md)  
  
 [Referencia técnica de anotaciones de BI para CSDL](../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/technical-reference-for-bi-annotations-to-csdl.md)  
  

[Interfaz IMDEmbeddedData](../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/imdembeddeddata-interface.md)


  
  

