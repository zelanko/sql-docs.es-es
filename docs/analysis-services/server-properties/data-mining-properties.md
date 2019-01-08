---
title: Propiedades de minería de datos de Analysis Services | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: bd1440e5ce0649d31f0ae6c0577c61e9e081a800
ms.sourcegitcommit: 8a64c59c5d84150659a015e54f8937673cab87a0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/08/2018
ms.locfileid: "53072032"
---
# <a name="data-mining-properties"></a>Propiedades de minería de datos
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]

  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] admite las propiedades de servidor de minería de datos descritas en las siguientes tablas. Para obtener más información sobre otras propiedades de servidor y cómo establecerlas, vea [Configurar las propiedades de servidor en Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md).  
  
 **Se aplica a:** modo de servidor multidimensional  únicamente  
  
## <a name="non-specific-category"></a>Categoría no específica  
 **AllowSessionMiningModels**  
 Una propiedad booleana que indica si se pueden crear modelos de minería de datos de sesión.  
  
 El valor predeterminado para esta propiedad es False, que indica que no se pueden crear modelos de minería de datos de sesión.  
  
 **AllowAdHocOpenRowsetQueries**  
 Una propiedad booleana que indica si se permiten consultas ad hoc de conjuntos de filas abiertos.  
  
 El valor predeterminado para esta propiedad es False, que indica que las consultas de conjuntos de filas abiertos no están permitidas durante una sesión.  
  
 **AllowedProvidersInOpenRowset**  
 Una propiedad de cadena que identifica los proveedores que están permitidos en un conjunto de filas abierto; se compone de una lista separada por comas/puntos y coma de ProgID de proveedor, o en caso contrario [All].  
  
 **MaxConcurrentPredictionQueries**  
 Una propiedad de entero de 32 bits con signo que define el máximo de consultas de predicción simultáneas.  
  
## <a name="algorithms-category"></a>Categoría Algoritmos  
 **Microsoft_Association_Rules\ Enabled**  
 Una propiedad booleana que indica si el algoritmo Microsoft_Association_Rules está habilitado.  
  
 **Microsoft_Clustering\ Enabled**  
 Una propiedad booleana que indica si el algoritmo Microsoft_Clustering está habilitado.  
  
 **Microsoft_Decision_Trees\ Enabled**  
 Una propiedad booleana que indica si el algoritmo Microsoft_DecisionTrees está habilitado.  
  
 **Microsoft_Naive_Bayes\ Enabled**  
 Una propiedad booleana que indica si el algoritmo Microsoft_ Naive_Bayes está habilitado.  
  
 **Microsoft_Neural_Network\ Enabled**  
 Una propiedad booleana que indica si el algoritmo Microsoft_Neural_Network está habilitado.  
  
 **Microsoft_Sequence_Clustering\ Enabled**  
 Una propiedad booleana que indica si el algoritmo Microsoft_Sequence_Clustering está habilitado.  
  
 **Microsoft_Time_Series\ Enabled**  
 Una propiedad booleana que indica si el algoritmo Microsoft_Time_Series está habilitado.  
  
 **Microsoft_Linear_Regression\ Enabled**  
 Una propiedad booleana que indica si el algoritmo Microsoft_Linear_Regression está habilitado.  
  
 **Microsoft_Logistic_Regression\ Enabled**  
 Una propiedad booleana que indica si el algoritmo Microsoft_Logistic_Regression está habilitado.  
  
> [!NOTE]  
>  Además de las propiedades que definen los servicios de minería de datos disponibles en el servidor, existen propiedades de minería de datos que definen el comportamiento de algoritmos concretos. Estas propiedades se configuran al crear un modelo de minería de datos individual, no en el nivel de servidor. Para obtener más información, vea [Algoritmos de minería de datos &#40;Analysis Services: Minería de datos&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md).  
  
## <a name="see-also"></a>Vea también  
 [Arquitectura física &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/physical-architecture-analysis-services-data-mining.md)   
 [Configurar las propiedades de servidor en Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md)   
 [Determinar el modo de servidor de una instancia de Analysis Services](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  
