---
title: Formatos de datos numéricos | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- integer data types [Integration Services]
- numeric data formats for fast parse
- locale-sensitive parsing [Integration Services]
- fast parse [Integration Services]
ms.assetid: fa3975ce-9d21-408a-857d-f85e30af27b0
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d0f48c3a6cebe079d93601f53698afafb350587e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66057386"
---
# <a name="numeric-data-formats"></a>Formatos de datos numéricos
  El análisis rápido ofrece un conjunto rápido y simple de rutinas, que no distinguen la configuración regional, para analizar datos. El análisis rápido admite solo un conjunto limitado de formatos para tipos de datos enteros.  
  
## <a name="integer-data-types"></a>Tipos de datos enteros  
 Los tipos de datos enteros que proporciona [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] son DT_I1, DT_UI1, DT_I2, DT_UI2, DT_I4, DT_UI4, DT_I8 y DT_UI8. Para obtener más información, vea [Integration Services tipos de datos](data-flow/integration-services-data-types.md).  
  
 El análisis rápido admite los siguientes formatos para tipos de datos enteros:  
  
-   Espacios iniciales y finales de cero o superiores o tabulaciones. Por ejemplo, el valor " 123  " es válido. El valor que todo él es espacios equivale a cero.  
  
-   Un signo más o menos inicial, o ningún signo inicial. Por ejemplo, los valores +123, -123 y 123 son válidos.  
  
-   Uno o más numerales indo-árabes (0-9). Por ejemplo, el valor 345 es válido. No se admiten numerales de otros idiomas.  
  
 Entre los formatos de datos no admitidos se incluyen los siguientes:  
  
-   Caracteres especiales. Por ejemplo, el carácter de moneda $ no se admite y el valor $20 no puede analizarse.  
  
-   Los caracteres de espacios en blanco como avance de línea, retorno de carro y espacios de no separación. Por ejemplo, el valor " 123" no puede analizarse.  
  
-   Representaciones hexadecimales de números enteros. Por ejemplo, el valor 2EE no puede analizarse.  
  
-   Representaciones en notación científica de números enteros. Por ejemplo, el valor 1E+10 no puede analizarse.  
  
 Los siguientes formatos son datos de salida para números enteros:  
  
-   Un signo menos para números negativos y nada para números positivos.  
  
-   Ningún espacio en blanco.  
  
-   Uno o más numerales indo-árabes (0-9).  
  
  
