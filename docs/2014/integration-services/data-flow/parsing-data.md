---
title: Analizar datos | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- parsing [Integration Services]
- data parsing [Integration Services]
ms.assetid: 8893ea9d-634c-4309-b52c-6337222dcb39
caps.latest.revision: 37
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 7517819f2cf6909cd95d76043519f78b06699b6c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36201404"
---
# <a name="parsing-data"></a>Analizar datos
  Los flujos de datos de paquetes extraen y cargan datos entre almacenes de datos heterogéneos, que pueden usar diversos tipos de datos estándar y personalizados. En un flujo de datos, los orígenes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] realizan el trabajo de extraer datos, analizar datos de cadenas y convertir datos en un tipo de datos de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Las transformaciones posteriores pueden analizar datos para convertirlos en un tipo de datos diferentes, o bien crear copias de columnas con diferentes tipos de datos. Las expresiones usadas en los componentes también pueden convertir argumentos y operandos en diferentes tipos de datos. Finalmente, cuando se cargan los datos en un almacén de datos, el destino puede analizar los datos para convertirlos en un tipo de datos que usa el destino. Para más información, consulte [Integration Services Data Types](integration-services-data-types.md).  
  
## <a name="types-of-parsing"></a>Tipos de análisis  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] proporciona dos tipos de análisis para convertir los datos: el análisis rápido y el análisis estándar.  
  
-   El análisis rápido es un conjunto rápido y simple de rutinas de análisis que no admite conversiones de tipos de datos específicos de la configuración regional sino solo los formatos de fecha y hora usados con mayor frecuencia. Para más información, consulte [Fast Parse](../fast-parse.md).  
  
-   El análisis estándar es un conjunto completo de rutinas de análisis que admite todas las conversiones de tipos de datos proporcionadas por las API de conversión de tipo de datos de automatización disponibles en Oleaut32.dll y Ole2dsip.dll. Para más información, consulte [Standard Parse](../standard-parse.md).  
  
  