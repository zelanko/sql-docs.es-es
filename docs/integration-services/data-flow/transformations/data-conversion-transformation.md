---
title: Transformación Conversión de datos | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.dataconversiontrans.f1
- sql13.dts.designer.dataconversiontransformation.f1
helpviewer_keywords:
- converting data types [Integration Services]
- Data Conversion transformation
- data types [Integration Services], converting
ms.assetid: fd515bbc-6f49-4d0c-ae7f-6ea3c3f24a1c
caps.latest.revision: 53
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: f76181a1bfaaf249fda54916fc1e7f0f17b315a4
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/12/2018
ms.locfileid: "35404817"
---
# <a name="data-conversion-transformation"></a>Conversión de datos, transformación
  La transformación Conversión de datos convierte los datos de una columna de entrada a otro tipo de datos diferente y después los copia a una nueva columna de salida. Por ejemplo, un paquete puede extraer los datos de diferentes orígenes y después usar esta transformación para convertir las columnas al tipo de datos necesario para el almacén de datos de destino. Puede aplicar múltiples conversiones a una sola columna de entrada.  
  
 Un paquete puede utilizar esta transformación para realizar las siguientes conversiones de tipos de datos:  
  
-   Cambiar el tipo de datos. Para obtener más información, vea [Integration Services Data Types](../../../integration-services/data-flow/integration-services-data-types.md).  
  
    > [!NOTE]  
    >  Si va a convertir datos a un tipo de datos de fecha o de fecha y hora, la fecha de la columna de salida tiene el formato ISO, aunque las preferencias de la configuración regional especifiquen un formato diferente.  
  
-   Establecer la longitud de la columna de los datos de cadena así como la precisión y la escala de los datos numéricos. Para más información, vea [Precisión, escala y longitud &#40;Transact-SQL&#41;](../../../t-sql/data-types/precision-scale-and-length-transact-sql.md).  
  
-   Especificar una página de códigos. Para más información, consulte [Comparing String Data](../../../integration-services/data-flow/comparing-string-data.md).  
  
    > [!NOTE]  
    >  Al copiar datos entre columnas con un tipo de datos de cadena, las dos columnas deben usar la misma página de códigos.  
  
 Si la longitud de una columna de salida de datos de tipo cadena es menor que la longitud de la columna de entrada correspondiente, se truncarán los datos de salida. Para más información, vea [Control de errores en los datos](../../../integration-services/data-flow/error-handling-in-data.md).  
  
 Esta transformación tiene una entrada, una salida y una salida de error.  
  
## <a name="related-tasks"></a>Related Tasks  
 Puede establecer propiedades a través del Diseñador [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o mediante programación. Para obtener más información sobre cómo usar la transformación Conversión de datos en el Diseñador SSIS, vea [Convertir datos en un tipo de datos diferente mediante la transformación Conversión de datos](../../../integration-services/data-flow/transformations/convert-data-type-by-using-data-conversion-transformation.md). Para más información sobre cómo establecer las propiedades de esta transformación mediante programación, vea [Propiedades comunes](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796) y [Propiedades personalizadas de transformación](../../../integration-services/data-flow/transformations/transformation-custom-properties.md).  
  
## <a name="related-content"></a>Contenido relacionado  
 Entrada de blog, sobre la [comparación de rendimiento entre las técnicas de conversión de tipos de datos en SSIS 2008](http://go.microsoft.com/fwlink/?LinkId=220823), en blogs.msdn.com.  
  
## <a name="data-conversion-transformation-editor"></a>Editor de transformación Conversión de datos
  Use el cuadro de diálogo **Editor de transformación Conversión de datos** para seleccionar las columnas que desea convertir, seleccione el tipo de datos al que desea convertir la columna y establezca los atributos de conversión.  
  
> [!NOTE]  
>  La propiedad **FastParse** de las columnas de salida de transformación Conversión de datos no está disponible en el **Editor de transformación Conversión de datos**, pero puede establecerse mediante el **Editor avanzado**. Para obtener más información acerca de esta propiedad, vea la sección sobre la transformación Conversión de datos en [Transformation Custom Properties](../../../integration-services/data-flow/transformations/transformation-custom-properties.md).  
  
### <a name="options"></a>Opciones  
 **Columnas de entrada disponibles**  
 Seleccione, mediante las casillas, las columnas que desea convertir. Las selecciones agregan columnas de entrada a la tabla que aparece debajo.  
  
 **Columna de entrada**  
 Seleccione las columnas que desea convertir en la lista de columnas de entrada disponibles. Su selección se refleja en las selecciones de las anteriores casillas.  
  
 **Alias de salida**  
 Escriba un alias para cada columna nueva. El valor predeterminado es **Copy of** seguido del nombre de la columna de entrada; no obstante, puede elegir un nombre descriptivo exclusivo.  
  
 **Tipo de datos**  
 Seleccione en la lista un tipo de datos disponible. Para obtener más información, vea [Integration Services Data Types](../../../integration-services/data-flow/integration-services-data-types.md).  
  
 **Longitud**  
 Establezca la longitud de la columna para los datos de cadena.  
  
 **Precisión**  
 Establezca la precisión para los datos numéricos.  
  
 **Escala**  
 Establezca la escala para los datos numéricos.  
  
 **Página de códigos**  
 Seleccione la página de códigos adecuada para las columnas de tipo DT_STR.  
  
 **Configurar la salida de errores**  
 Especifique cómo controlar los errores de nivel de fila con el cuadro de diálogo [Configurar la salida de errores](http://msdn.microsoft.com/library/5f8da390-fab5-44f8-b268-d8fa313ce4b9) .  
  
## <a name="see-also"></a>Ver también  
 [Análisis rápido](http://msdn.microsoft.com/library/6688707d-3c5b-404e-aa2f-e13092ac8d95)   
 [Flujo de datos](../../../integration-services/data-flow/data-flow.md)   
 [Transformaciones de Integration Services](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  
