---
title: rrRenderingError - Error de Reporting Services | Microsoft Docs
description: 'En esta página de referencia de error, obtenga información sobre el identificador de evento "rrRenderingError": Error durante la representación del informe.'
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: troubleshooting
ms.topic: conceptual
helpviewer_keywords:
- rrRenderingError
ms.assetid: 0751efc3-b81b-44ee-8aac-8560f86ca322
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 67e43301ac1582bd3cfc085a9ad6412724d4ec92
ms.sourcegitcommit: df1f0f2dfb9452f16471e740273cd1478ff3100c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/29/2020
ms.locfileid: "87395293"
---
# <a name="rrrenderingerror---reporting-services-error"></a>rrRenderingError - Error de Reporting Services
    
## <a name="details"></a>Detalles  
  
|Category|Value|  
|-|-|  
|Nombre de producto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|Id. de evento|rrRenderingError|  
|Origen de eventos|Microsoft.ReportingServices.Diagnostics.Utilities.ErrorStrings.resources.Strings|  
|Componente|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|  
|Texto del mensaje|Error durante la representación del informe. (rrRenderingError) %1|  
  
## <a name="explanation"></a>Explicación  
 Se devuelve este mensaje cuando [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no puede representar ni exportar el informe.  
  
 Un mensaje que indique que no se admite el tamaño se suele producir cuando el tamaño de página RDL especificado no es válido. Especifique un tamaño de página RDL válido y, a continuación, vuelva a intentarlo.  
  
 Un mensaje que indique que no se admite la medida de tamaño RDL se suele producir cuando se especifica un tipo de unidad no admitido. Los tipos de unidad válidos son cm, pda, mm, pc y pt. Especifique un tipo de unidad válido y vuelva a intentarlo.  
  
 Un mensaje que indique que no se admite un tamaño negativo se suele producir cuando se especifica una medida negativa para el tamaño de página, por ejemplo -5 cm. Especifique un número positivo para el tamaño de página y, a continuación, vuelva a intentarlo.  
  
 Un mensaje que indique que se ha especificado un tamaño RDL fuera del intervalo se suele producir cuando una medida para el tamaño de página está fuera del tamaño de margen de página válido. Especifique una medida para el tamaño de página que esté dentro de los tamaños de margen de página válidos.  
  
 Un mensaje que indica que no se admite un color especificado se suele producir cuando el color especificado en el RDL no es válido. Elija un color admitido por RDL y, a continuación, vuelva a intentarlo.  
  
 Un mensaje que indique que la etiqueta de acción solo es opcional cuando se use una acción única y que si se agregan varias acciones se necesitan etiquetas para cada acción se suele producir cuando se especifica una etiqueta de acción y no es válida. Especifique una etiqueta de acción válida para cada acción.  
  
 Un mensaje que indique que el argumento de estilo debe ser de un tipo específico se suele producir cuando el valor de estilo es incorrecto para el tipo de datos especificado. La especificación RDL identifica los tipos válidos que puede utilizar en los valores de estilo de los distintos elementos RDL. Por ejemplo, un valor de estilo incorrecto para el color de fondo es "2pt" y un valor incorrecto para el alto es "true". Especifique un valor correcto y, a continuación, vuelva a intentarlo.  
  
 Un mensaje que indique que no se admite el estilo de borde se suele producir cuando el estilo de borde especificado no es válido. Especifique un estilo de borde admitido y, a continuación, vuelva a intentarlo.  
  
 Un mensaje que indique que no se admite el tipo MIME de imagen se suele producir cuando el tipo MIME especificado para un elemento de informe de imagen no es válido. Especifique un tipo MIME admitido para el elemento de informe y, a continuación, vuelva a intentarlo.  
  
 Un mensaje que indique que el número de filas supera el número máximo posible de filas por hoja se suele producir cuando se supera el número de filas de una hoja de cálculo de Excel. Excel admite un máximo de 65.000 filas.  
  
 Un mensaje que indique que el número de columnas supera el número máximo posible de columnas por hoja se suele producir cuando se supera el número de columnas de una hoja de cálculo de Excel.  
  
## <a name="user-action"></a>Acción del usuario  
  
## <a name="internal-only"></a>Solo para uso interno  
  
