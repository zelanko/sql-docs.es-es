---
title: Expresiones (DMX) | Documentos de Microsoft
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- DMX
helpviewer_keywords:
- Data Mining Extensions [Analysis Services], expressions
- DMX [Analysis Services], expressions
- expressions [DMX]
ms.assetid: 00579552-19c8-4e9d-a790-f88df3e1aeea
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: c04c55fc461d4429d55d32a776f5bea8eca345e8
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="expressions-dmx"></a>Expresiones (DMX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  En las extensiones de minería de datos (DMX), una expresión es una combinación de identificadores, valores y operadores que [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] puede evaluar para obtener un resultado.  
  
 Una expresión DMX puede ser sencilla o compleja. Una expresión sencilla puede ser una de las siguientes:  
  
 Constante  
 Una constante es un símbolo que representa un único valor específico. Una constante puede ser una cadena, o un valor numérico o de fecha. Debe usar comillas simples (') para delimitar constantes de cadena y de fecha.  
  
 Función escalar  
 Las funciones escalares devuelven un valor único.  
  
 Función no escalar  
 Las funciones no escalares devuelven una tabla.  
  
 Identificador de objeto  
 Los identificadores de objeto se consideran como expresiones sencillas en DMX.  
  
 Para generar expresiones complejas, puede usar operadores para combinar las expresiones. Para obtener más información acerca de los operadores, vea [extensiones de minería de datos &#40; DMX &#41; Referencia de operadores](../dmx/data-mining-extensions-dmx-operator-reference.md).  
  
## <a name="see-also"></a>Vea también  
 [Extensiones de minería de datos &#40; DMX &#41; Referencia](../dmx/data-mining-extensions-dmx-reference.md)   
 [Extensiones de minería de datos &#40; DMX &#41; Referencia de funciones](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Extensiones de minería de datos &#40; DMX &#41; Referencia de instrucciones](../dmx/data-mining-extensions-dmx-statements.md)   
 [Extensiones de minería de datos &#40; DMX &#41; Convenciones de sintaxis](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Extensiones de minería de datos &#40; DMX &#41; Elementos de sintaxis](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Funciones de predicción generales &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md)   
 [Estructura y el uso de consultas de predicción DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Descripción de la instrucción Select de DMX](../dmx/understanding-the-dmx-select-statement.md)  
  
  

