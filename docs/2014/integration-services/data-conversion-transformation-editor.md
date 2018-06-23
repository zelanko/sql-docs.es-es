---
title: Editor de transformación conversión de datos | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dts.designer.dataconversiontransformation.f1
helpviewer_keywords:
- Data Conversion Transformation Editor
ms.assetid: 7b4e4873-e8fe-4549-a965-65bebdb270bc
caps.latest.revision: 28
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 9c5157175181c7a43a2c8e3209c23905a4129d2d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36107009"
---
# <a name="data-conversion-transformation-editor"></a>Editor de transformación Conversión de datos
  Use el cuadro de diálogo **Editor de transformación Conversión de datos** para seleccionar las columnas que desea convertir, seleccione el tipo de datos al que desea convertir la columna y establezca los atributos de conversión.  
  
> [!NOTE]  
>  El `FastParse` propiedad de las columnas de salida de la transformación de conversión de datos no está disponible en la **Editor de transformación conversión de datos**, pero se puede establecer mediante el uso de la **Editor avanzado**. Para obtener más información acerca de esta propiedad, vea la sección sobre la transformación Conversión de datos en [Transformation Custom Properties](data-flow/transformations/transformation-custom-properties.md).  
  
 Para obtener más información acerca de la transformación Conversión de datos, vea [Data Conversion Transformation](data-flow/transformations/data-conversion-transformation.md).  
  
## <a name="options"></a>Opciones  
 **Columnas de entrada disponibles**  
 Seleccione, mediante las casillas, las columnas que desea convertir. Las selecciones agregan columnas de entrada a la tabla que aparece debajo.  
  
 **Columna de entrada**  
 Seleccione las columnas que desea convertir en la lista de columnas de entrada disponibles. Su selección se refleja en las selecciones de las anteriores casillas.  
  
 **Alias de salida**  
 Escriba un alias para cada columna nueva. El valor predeterminado es `Copy of` seguido del nombre de columna de entrada; sin embargo, puede elegir cualquier nombre único y descriptivo.  
  
 **Tipo de datos**  
 Seleccione en la lista un tipo de datos disponible. Para más información, consulte [Integration Services Data Types](data-flow/integration-services-data-types.md).  
  
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
 [Referencia de mensajes y Error de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Conversión de datos en un tipo de datos diferente con la transformación Conversión de datos](data-flow/transformations/convert-data-type-by-using-data-conversion-transformation.md)  
  
  