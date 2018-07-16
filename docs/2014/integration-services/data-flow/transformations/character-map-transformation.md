---
title: Transformación Mapa de caracteres | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.charactertrans.f1
helpviewer_keywords:
- mutually exclusive mapping [Integration Services]
- mapping data [Integration Services]
- string functions
- Character Map transformation [Integration Services]
ms.assetid: e0f50eb6-b893-400f-bb8c-fb3072cc2620
caps.latest.revision: 41
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 7b56b24150f5c1deb5897a1d64a6a7aae0a7d862
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37306035"
---
# <a name="character-map-transformation"></a>Transformación Mapa de caracteres
  La transformación Mapa de caracteres se aplica a funciones de cadena que operan sobre datos de caracteres, como la conversión de minúsculas a mayúsculas. Esta transformación solo opera en datos de columnas con un tipo de datos de cadena.  
  
 La transformación Mapa de caracteres puede convertir datos de columna in situ o agregar una columna a la salida de transformación y colocar los datos convertidos en la nueva columna. Puede aplicar distintos conjuntos de operaciones de asignación a la misma columna de entrada y colocar los resultados en columnas diferentes. Por ejemplo, puede convertir la misma columna a mayúsculas y minúsculas, y almacenar el resultado en dos columnas diferentes.  
  
 En algunas situaciones, la asignación puede provocar un truncamiento de datos. Por ejemplo, se puede producir un truncamiento cuando se asignan caracteres de un byte a caracteres representados con varios bytes. La transformación Mapa de caracteres incluye una salida de error que se puede usar para dirigir los datos truncados a otra salida distinta. Para obtener más información, vea [Control de errores en los datos](../error-handling-in-data.md).  
  
 Esta transformación tiene una entrada, una salida y una salida de error.  
  
## <a name="mapping-operations"></a>Operaciones de asignación  
 En la siguiente tabla se describen las operaciones de asignación admitidas por la transformación Mapa de caracteres.  
  
|Operación|Descripción|  
|---------------|-----------------|  
|Inversión de byte|Invierte el orden de los bytes.|  
|Formato completo|Asigna caracteres de formato medio a caracteres de formato completo.|  
|Formato medio|Asigna caracteres de formato completo a caracteres de formato medio.|  
|Hiragana|Asigna caracteres katakana a caracteres hiragana.|  
|Katakana|Asigna caracteres hiragana a caracteres katakana.|  
|Utilización lingüística de mayúsculas y minúsculas|Aplica la utilización lingüística de mayúsculas y minúsculas en lugar de las reglas del sistema. La utilización lingüística de mayúsculas y minúsculas se refiere a la funcionalidad ofrecida por la API de Win32 para la asignación de caracteres Unicode simples del turco y otras configuraciones regionales.|  
|Minúsculas|Conversión de caracteres a minúsculas.|  
|Chino simplificado|Asigna caracteres de chino tradicional a caracteres de chino simplificado.|  
|Chino tradicional|Asigna caracteres de chino simplificado a caracteres de chino tradicional.|  
|Mayúsculas|Conversión de caracteres a mayúsculas.|  
  
## <a name="mutually-exclusive-mapping-operations"></a>Operaciones de asignación mutuamente exclusivas  
 En una transformación pueden realizarse varias operaciones. Sin embargo, algunas operaciones son mutuamente exclusivas. La siguiente tabla enumera las restricciones que se aplican al usar varias operaciones sobre la misma columna. Las operaciones sobre las columnas Operación A y Operación B son mutuamente exclusivas.  
  
|Operación A|Operación B|  
|-----------------|-----------------|  
|Minúsculas|Mayúsculas|  
|Hiragana|Katakana|  
|Formato medio|Formato completo|  
|Chino tradicional|Chino simplificado|  
|Minúsculas|Hiragana, katakana, formato medio, formato completo|  
|Mayúsculas|Hiragana, katakana, formato medio, formato completo|  
  
## <a name="configuration-of-the-character-map-transformation"></a>Configuración de la transformación Mapa de caracteres  
 Puede configurar la transformación Mapa de caracteres de las maneras siguientes:  
  
-   Especificar las columnas que desea convertir.  
  
-   Especificar las operaciones que desea aplicar a cada columna.  
  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener más información acerca de las propiedades que puede establecer en el cuadro de diálogo **Editor de transformación Mapa de caracteres** , vea [Character Map Transformation Editor](../../character-map-transformation-editor.md).  
  
 El cuadro de diálogo **Editor avanzado** indica las propiedades que se pueden establecer mediante programación. Para obtener más información acerca de las propiedades que puede establecer a través del cuadro de diálogo **Editor avanzado** o mediante programación, haga clic en uno de los temas siguientes:  
  
-   [Propiedades comunes](../../common-properties.md)  
  
-   [Propiedades personalizadas de transformación](transformation-custom-properties.md)  
  
 Para obtener más información sobre cómo establecer valores de propiedades, haga clic en uno de los temas siguientes:  
  
-   [Establecer las propiedades de un componente de flujo de datos](../set-the-properties-of-a-data-flow-component.md)  
  
-   [Ordenación de datos para las transformaciones Mezclar y Combinación de mezcla](sort-data-for-the-merge-and-merge-join-transformations.md)  
  
  
