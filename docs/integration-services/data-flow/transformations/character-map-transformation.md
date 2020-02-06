---
title: Transformación Mapa de caracteres | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.charactertrans.f1
- sql13.dts.designer.charactermaptransformation.f1
helpviewer_keywords:
- mutually exclusive mapping [Integration Services]
- mapping data [Integration Services]
- string functions
- Character Map transformation [Integration Services]
ms.assetid: e0f50eb6-b893-400f-bb8c-fb3072cc2620
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 8211045a72ae56b04bb93b7be7e83f296f2467e5
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "71291664"
---
# <a name="character-map-transformation"></a>Transformación Mapa de caracteres

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  La transformación Mapa de caracteres se aplica a funciones de cadena que operan sobre datos de caracteres, como la conversión de minúsculas a mayúsculas. Esta transformación solo opera en datos de columnas con un tipo de datos de cadena.  
  
 La transformación Mapa de caracteres puede convertir datos de columna in situ o agregar una columna a la salida de transformación y colocar los datos convertidos en la nueva columna. Puede aplicar distintos conjuntos de operaciones de asignación a la misma columna de entrada y colocar los resultados en columnas diferentes. Por ejemplo, puede convertir la misma columna a mayúsculas y minúsculas, y almacenar el resultado en dos columnas diferentes.  
  
 En algunas situaciones, la asignación puede provocar un truncamiento de datos. Por ejemplo, se puede producir un truncamiento cuando se asignan caracteres de un byte a caracteres representados con varios bytes. La transformación Mapa de caracteres incluye una salida de error que se puede usar para dirigir los datos truncados a otra salida distinta. Para más información, vea [Control de errores en los datos](../../../integration-services/data-flow/error-handling-in-data.md).  
  
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
|Uppercase|Conversión de caracteres a mayúsculas.|  
  
## <a name="mutually-exclusive-mapping-operations"></a>Operaciones de asignación mutuamente exclusivas  
 En una transformación pueden realizarse varias operaciones. Sin embargo, algunas operaciones son mutuamente exclusivas. La siguiente tabla enumera las restricciones que se aplican al usar varias operaciones sobre la misma columna. Las operaciones sobre las columnas Operación A y Operación B son mutuamente exclusivas.  
  
|Operación A|Operación B|  
|-----------------|-----------------|  
|Minúsculas|Uppercase|  
|Hiragana|Katakana|  
|Formato medio|Formato completo|  
|Chino tradicional|Chino simplificado|  
|Minúsculas|Hiragana, katakana, formato medio, formato completo|  
|Uppercase|Hiragana, katakana, formato medio, formato completo|  
  
## <a name="configuration-of-the-character-map-transformation"></a>Configuración de la transformación Mapa de caracteres  
 Puede configurar la transformación Mapa de caracteres de las maneras siguientes:  
  
-   Especificar las columnas que desea convertir.  
  
-   Especificar las operaciones que desea aplicar a cada columna.  
  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o mediante programación.  
  
 El cuadro de diálogo **Editor avanzado** indica las propiedades que se pueden establecer mediante programación. Para obtener más información acerca de las propiedades que puede establecer a través del cuadro de diálogo **Editor avanzado** o mediante programación, haga clic en uno de los temas siguientes:  
  
-   [Common Properties](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Propiedades personalizadas de transformación](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 Para obtener más información sobre cómo establecer valores de propiedades, haga clic en uno de los temas siguientes:  
  
-   [Establecer las propiedades de un componente de flujo de datos](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
-   [Ordenación de datos para las transformaciones Mezclar y Combinación de mezcla](../../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)  
  
## <a name="character-map-transformation-editor"></a>Editor de transformación Mapa de caracteres
  Use el cuadro de diálogo **Editor de transformación Mapa de caracteres** para seleccionar las funciones de cadena que se van a aplicar a datos de columna y para especificar si la asignación es una modificación en contexto o se agrega como una columna nueva.  
  
### <a name="options"></a>Opciones  
 **Columnas de entrada disponibles**  
 Use las casillas para seleccionar las columnas que se van a transformar con las funciones de cadena. Las selecciones aparecen en la siguiente tabla.  
  
 **Columna de entrada**  
 Muestra las columnas de entrada seleccionadas de la tabla anterior. También puede cambiar o quitar una selección utilizando la lista de columnas de entrada disponibles.  
  
 **Destino**  
 Especifique si se guardan los resultados de las operaciones de cadena en contexto, utilizando la columna existente, o se guardan los datos modificados como una columna nueva.  
  
|Value|Descripción|  
|-----------|-----------------|  
|Nueva columna|Guardar los datos en una columna nueva. Asigne el nombre de columna en **Alias de salida**.|  
|Modificación en contexto|Guardar los datos modificados en la columna existente.|  
  
 **operación**  
 Seleccione de la lista las funciones de cadena que se aplicarán a los datos de la columna.  
  
|Value|Descripción|  
|-----------|-----------------|  
|Minúsculas|Convertir en minúsculas.|  
|Uppercase|Convertir en mayúsculas.|  
|Inversión de byte|Convertir invirtiendo el orden de los bytes.|  
|Hiragana|Convertir caracteres japoneses katakana en caracteres hiragana.|  
|Katakana|Convertir caracteres japoneses hiragana en caracteres katakana.|  
|Formato medio|Convertir caracteres de formato completo en formato medio.|  
|Formato completo|Convertir caracteres de formato medio en formato completo.|  
|Utilización lingüística de mayúsculas y minúsculas|Aplicar reglas lingüísticas de mayúsculas y minúsculas (asignación de caracteres Unicode simples del turco y otras configuraciones regionales) en vez de otras reglas del sistema.|  
|Chino simplificado|Convertir caracteres de chino tradicional en chino simplificado.|  
|Chino tradicional|Convertir caracteres de chino simplificado en chino tradicional.|  
  
 **Alias de salida**  
 Escriba un alias para cada columna de salida. El valor predeterminado es **Copy of** seguido del nombre de la columna de entrada; no obstante, puede elegir un nombre descriptivo exclusivo.  
  
 **Configurar la salida de errores**  
 Use el cuadro de diálogo [Configurar la salida de errores](https://msdn.microsoft.com/library/5f8da390-fab5-44f8-b268-d8fa313ce4b9) para especificar las opciones de control de errores de esta transformación.  
  
  
