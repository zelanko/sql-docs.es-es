---
title: "Editor de transformaci&#243;n Mapa de caracteres | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.charactermaptransformation.f1"
helpviewer_keywords: 
  - "Editor de transformación Mapa de caracteres"
ms.assetid: 3f1dbcf9-9cca-4606-bdcc-7ea6ad48cdf3
caps.latest.revision: 26
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 26
---
# Editor de transformaci&#243;n Mapa de caracteres
  Use el cuadro de diálogo **Editor de transformación Mapa de caracteres** para seleccionar las funciones de cadena que se van a aplicar a datos de columna y para especificar si la asignación es una modificación en contexto o se agrega como una columna nueva.  
  
 Para obtener más información acerca de la transformación Mapa de caracteres, vea [Character Map Transformation](../../../integration-services/data-flow/transformations/character-map-transformation.md).  
  
## Opciones  
 **Columnas de entrada disponibles**  
 Use las casillas para seleccionar las columnas que se van a transformar con las funciones de cadena. Las selecciones aparecen en la siguiente tabla.  
  
 **Columna de entrada**  
 Muestra las columnas de entrada seleccionadas de la tabla anterior. También puede cambiar o quitar una selección utilizando la lista de columnas de entrada disponibles.  
  
 **Destino**  
 Especifique si se guardan los resultados de las operaciones de cadena en contexto, utilizando la columna existente, o se guardan los datos modificados como una columna nueva.  
  
|Value|Description|  
|-----------|-----------------|  
|Nueva columna|Guardar los datos en una columna nueva. Asigne el nombre de columna en **Alias de salida**.|  
|Modificación en contexto|Guardar los datos modificados en la columna existente.|  
  
 **Operación**  
 Seleccione de la lista las funciones de cadena que se aplicarán a los datos de la columna.  
  
|Value|Description|  
|-----------|-----------------|  
|Minúsculas|Convertir en minúsculas.|  
|Mayúsculas|Convertir en mayúsculas.|  
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
 Use el cuadro de diálogo [Configurar la salida de errores](../Topic/Configure%20Error%20Output.md) para especificar las opciones de control de errores de esta transformación.  
  
## Vea también  
 [Referencia de errores y mensajes de Integration Services](../../../integration-services/integration-services-error-and-message-reference.md)  
  
  