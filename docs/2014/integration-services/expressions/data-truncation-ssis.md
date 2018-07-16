---
title: Truncamiento de datos (SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- truncating data
- data truncation [Integration Services]
- expressions [Integration Services], data truncation
- truncate options [Integration Services]
ms.assetid: 02461e15-49ca-445b-abb3-5c369c283ec2
caps.latest.revision: 32
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 5f80a51df610040e18dbdae7b1552c56d81cb084
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37328097"
---
# <a name="data-truncation-ssis"></a>Truncamiento de datos (SSIS)
  Una expresión puede provocar accidentalmente un truncamiento de datos. El truncamiento puede producirse en las siguientes circunstancias:  
  
-   Cadenas. Por ejemplo, traducir datos de cadena con un tipo de datos DT_WSTR a una cadena de la misma longitud, medida en caracteres, con un tipo de datos DT_STR provoca una pérdida de datos si la cadena original contiene caracteres de doble byte.  
  
-   Dígitos significativos. Por ejemplo, la conversión de un entero con el tipo de datos DT_I4 a un tipo de datos DT_I2 o la conversión de un entero sin signo a un entero con signo.  
  
-   Dígitos no significativos. Por ejemplo, la conversión de un número real con el tipo de datos DT_R8 a DT_R4 o de un entero con el tipo de datos DT_I4 al tipo de datos DT_R4.  
  
 El evaluador de expresiones identifica las conversiones explícitas que pueden causar el truncamiento y emite una advertencia al analizar la expresión. Por ejemplo, el evaluador de expresiones emite una advertencia si se convierte una cadena de 30 caracteres en una cadena de 20 caracteres.  
  
> [!NOTE]  
>  El truncamiento no se comprueba en tiempo de ejecución; los datos se truncan sin advertencia. Sin embargo, la mayoría de los adaptadores y las transformaciones de datos admiten salidas de error que pueden controlar la disposición de las filas de error. Para obtener más información sobre cómo controlar el truncamiento de datos, vea [control de errores en datos](../data-flow/error-handling-in-data.md).  
  
  
