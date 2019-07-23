---
title: Propiedades personalizadas de ADO NET | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: e062a9ab-1e6b-4061-845a-4f8a0552b09d
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 923ff84b7f5e6616083f0d965f917cd1ecc21b6c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68045558"
---
# <a name="ado-net-custom-properties"></a>Propiedades personalizadas de ADO NET

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  **Propiedades personalizadas de origen**  
  
 El origen de ADO NET tiene propiedades personalizadas y propiedades comunes a todos los componentes de flujo de datos.  
  
 En la tabla siguiente se describen las propiedades personalizadas del origen de ADO NET. Todas las propiedades son de lectura y escritura.  
  
|Nombre de propiedad|Tipo de datos|Descripción|  
|-------------------|---------------|-----------------|  
|CommandTimeout|String|Valor que especifica el número de segundos que transcurren antes de agotarse el tiempo de espera del comando SQL. El valor 0 indica que el comando no agota nunca el tiempo de espera.|  
|SqlCommand|String|Instrucción SQL que el origen de ADO NET usa para extraer datos.<br /><br /> Cuando el paquete se carga, puede actualizar dinámicamente esta propiedad con la instrucción SQL que el origen de ADO NET utilizará. Para más información, vea [Expresiones de Integration Services &#40;SSIS&#41;](../../integration-services/expressions/integration-services-ssis-expressions.md) y [Usar expresiones de propiedad en paquetes](../../integration-services/expressions/use-property-expressions-in-packages.md).|  
|AllowImplicitStringConversion|Boolean|Valor que indica si ocurre lo siguiente:<br /><br /> -No se genera un error de validación si hay una desigualdad entre los tipos de los metadatos externos y los tipos de las columnas de salida que son cadenas (DT_WSTR o DT_NTEXT).<br /><br /> -La conversión implícita de los tipos de los metadatos externos al tipo de datos de cadena que la columna de resultados utiliza.<br /><br /> <br /><br /> El valor predeterminado es TRUE.<br /><br /> Para más información, consulte [ADO NET Source](../../integration-services/data-flow/ado-net-source.md).|  
  
 La salida y las columnas de salida del origen de ADO NET no tienen ninguna propiedad personalizada.  
  
 Para más información, consulte [ADO NET Source](../../integration-services/data-flow/ado-net-source.md).  
  
 **Propiedades personalizadas de los destinos**  
  
 El destino de [!INCLUDE[vstecado](../../includes/vstecado-md.md)] tiene propiedades personalizadas y propiedades comunes a todos los componentes de flujo de datos.  
  
 En la tabla siguiente se describen las propiedades personalizadas del destino [!INCLUDE[vstecado](../../includes/vstecado-md.md)] . Todas las propiedades son de lectura y escritura. Estas propiedades no están disponibles en el **Editor de destinos ADO NET**, pero se pueden establecer con el **Editor avanzado**.  
  
|Propiedad|Tipo de datos|Descripción|  
|--------------|---------------|-----------------|  
|BatchSize|Integer|Número de filas de un lote que se envía al servidor. El valor **0** indica que el tamaño del lote coincide con el tamaño del búfer interno. El valor predeterminado de esta propiedad es **0**.|  
|CommandTimeOut|Integer|Número máximo de segundos que el comando SQL se puede ejecutar antes de superar el tiempo de espera. Si el valor es **0** , indica un tiempo infinito. El valor predeterminado de esta propiedad es **0**.|  
|TableOrViewName|String|Nombre de la tabla o vista de destino.|  
  
 Para más información, consulte [ADO NET Destination](../../integration-services/data-flow/ado-net-destination.md).  
  
## <a name="see-also"></a>Consulte también  
 [Common Properties](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
  
