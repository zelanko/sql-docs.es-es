---
title: Editor de transformación conversión de datos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.dataconversiontransformation.f1
helpviewer_keywords:
- Data Conversion Transformation Editor
ms.assetid: 7b4e4873-e8fe-4549-a965-65bebdb270bc
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 5346c808c7d724ae630bb3dd25016a9977af363e
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66060052"
---
# <a name="data-conversion-transformation-editor"></a>Editor de transformación Conversión de datos
  Use el cuadro de diálogo **Editor de transformación Conversión de datos** para seleccionar las columnas que desea convertir, seleccione el tipo de datos al que desea convertir la columna y establezca los atributos de conversión.  
  
> [!NOTE]  
>  El `FastParse` propiedad de las columnas de salida de la transformación conversión de datos no está disponible en el **Editor de transformación conversión de datos**, pero se puede establecer utilizando la **Editor avanzado**. Para obtener más información acerca de esta propiedad, vea la sección sobre la transformación Conversión de datos en [Transformation Custom Properties](data-flow/transformations/transformation-custom-properties.md).  
  
 Para obtener más información acerca de la transformación Conversión de datos, vea [Data Conversion Transformation](data-flow/transformations/data-conversion-transformation.md).  
  
## <a name="options"></a>Opciones  
 **Columnas de entrada disponibles**  
 Seleccione, mediante las casillas, las columnas que desea convertir. Las selecciones agregan columnas de entrada a la tabla que aparece debajo.  
  
 **Columna de entrada**  
 Seleccione las columnas que desea convertir en la lista de columnas de entrada disponibles. Su selección se refleja en las selecciones de las anteriores casillas.  
  
 **Alias de salida**  
 Escriba un alias para cada columna nueva. El valor predeterminado es `Copy of` seguido del nombre de la columna de entrada; no obstante, puede elegir un nombre descriptivo exclusivo.  
  
 **Tipo de datos**  
 Seleccione en la lista un tipo de datos disponible. Para obtener más información, vea [Integration Services Data Types](data-flow/integration-services-data-types.md).  
  
 **Longitud**  
 Establezca la longitud de la columna para los datos de cadena.  
  
 **Precisión**  
 Establezca la precisión para los datos numéricos.  
  
 **Escala**  
 Establezca la escala para los datos numéricos.  
  
 **Página de códigos**  
 Seleccione la página de códigos adecuada para las columnas de tipo DT_STR.  
  
 **Configurar la salida de errores**  
 Especifique cómo controlar los errores de nivel de fila con el cuadro de diálogo [Configurar la salida de errores](../../2014/integration-services/configure-error-output.md) .  
  
## <a name="see-also"></a>Vea también  
 [Referencia de errores y mensajes de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Convertir datos en un tipo de datos diferente mediante la transformación Conversión de datos](data-flow/transformations/convert-data-type-by-using-data-conversion-transformation.md)  
  
  
