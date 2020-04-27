---
title: Especificar tipo de dimensión (Asistente para dimensiones) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dimensionwizard.bidimensionproperties.f1
ms.assetid: 3215282a-532d-4ff2-b721-286f088967fc
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6de1b056942673d358cec4768c6854a6966d139e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66068372"
---
# <a name="specify-dimension-type-dimension-wizard"></a>Especificar tipo de dimensión (Asistente para dimensiones)
  Use la página **Especificar tipo de dimensión** para definir el tipo de dimensión y agregar a la dimensión tipos de atributo especiales asociados con el tipo de dimensión seleccionado.  
  
> [!NOTE]  
>  Esta página solo se muestra si se ha seleccionado **Dimensión estándar** en la página **Seleccionar el tipo de dimensión** .  
  
## <a name="options"></a>Opciones  
 **Tipo de dimensión**  
 Seleccione el tipo de dimensión para la dimensión. En la tabla siguiente se enumeran los tipos de dimensión disponibles.  
  
|Value|Descripción|  
|-----------|-----------------|  
|**Cuentas**|Las dimensiones de cuenta contienen datos y metadatos que representan una lista de cuentas.<br /><br /> Para más información sobre las dimensiones de cuenta, vea [Crear una cuenta financiera de una dimensión de tipo primario-secundario](multidimensional-models/database-dimensions-finance-account-of-parent-child-type.md).|  
|**Lista de materiales**|Las dimensiones de lista de materiales (o BOM) son dimensiones normales en las que los datos y los metadatos representan información de inventario o fabricación, como listas de piezas para productos.<br /><br /> Para más información sobre las dimensiones normales, vea [Tipos de dimensiones](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md).|  
|**Channel**|Las dimensiones de canal son dimensiones normales en las que los datos y los metadatos representan información de canales.<br /><br /> Para más información sobre las dimensiones normales, vea [Tipos de dimensiones](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md).|  
|**Moneda**|Las dimensiones de moneda contienen datos y metadatos que representan información de monedas.<br /><br /> Para más información sobre las dimensiones de moneda, vea [Crear una dimensión de tipo moneda](multidimensional-models/database-dimensions-create-a-currency-type-dimension.md).|  
|**Compradores**|Las dimensiones de cliente son dimensiones normales en las que los datos y los metadatos representan información de clientes o contactos.<br /><br /> Para más información sobre las dimensiones normales, vea [Tipos de dimensiones](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md).|  
|**Geografía**|Las dimensiones de geografía son dimensiones normales en las que los datos y los metadatos representan información geográfica, como ciudades o códigos postales.<br /><br /> Para más información sobre las dimensiones normales, vea [Tipos de dimensiones](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md).|  
|**Organización**|Las dimensiones de organización son dimensiones normales en las que los datos y los metadatos representan información organizativa, como empleados o subsidiarias.<br /><br /> Para más información sobre las dimensiones normales, vea [Tipos de dimensiones](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md).|  
|**Productos**|Las dimensiones de producto son dimensiones normales en las que los datos y los metadatos representan información de productos.<br /><br /> Para más información sobre las dimensiones normales, vea [Tipos de dimensiones](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md).|  
|**Promoción**|Las dimensiones de promoción son dimensiones normales en las que los datos y los metadatos representan información de promociones de mercadotecnia.<br /><br /> Para más información sobre las dimensiones normales, vea [Tipos de dimensiones](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md).|  
|**Cuantitativo**|Las dimensiones cuantitativas son dimensiones normales en las que los datos y los metadatos representan información cuantitativa.<br /><br /> Para más información sobre las dimensiones normales, vea [Tipos de dimensiones](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md).|  
|**Tarifas**|Las dimensiones de tarifa son dimensiones normales en las que los datos y los metadatos representan información de tasa de cambio y conversión de monedas.|  
|**Normal**|Las dimensiones normales son el tipo de dimensión más común [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]que se usa en.<br /><br /> Para más información sobre las dimensiones normales, vea [Tipos de dimensiones](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md).|  
|**Escenario**|Las dimensiones de escenario son dimensiones normales en las que los datos y los metadatos representan información de análisis estratégico y de planes.<br /><br /> Para más información sobre las dimensiones normales, vea [Tipos de dimensiones](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md).|  
|**Time**|Las dimensiones de tiempo contienen datos y metadatos orientados al tiempo.<br /><br /> Para más información sobre las dimensiones de tiempo, vea [Crear una dimensión de tipo Date](multidimensional-models/database-dimensions-create-a-date-type-dimension.md).|  
|**Utilidad**|Las dimensiones de utilidad son dimensiones normales en las que los datos y los metadatos representan información que no encaja en otro tipo de dimensión.<br /><br /> Para más información sobre las dimensiones normales, vea [Tipos de dimensiones](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md).|  
  
## <a name="dimension-attributes-options"></a>Opciones de atributos de dimensión  
  
> [!NOTE]  
>  Las opciones de esta sección están disponibles solo si el **Tipo de dimensión** seleccionado tiene tipos de atributo especiales asociados. No todas las dimensiones tienen tipos de atributo especiales asociados.  
  
 **Inclui**  
 Seleccione esta opción para incluir el tipo de atributo en la dimensión.  
  
 **Tipo de atributo**  
 Muestra el tipo de atributo asociado con el tipo de dimensión seleccionado en **Tipo de dimensión**. Para más información sobre tipos de atributo, vea [Elemento Type &#40;DimensionAttribute&#41; &#40;ASSL&#41;](https://docs.microsoft.com/bi-reference/assl/properties/type-element-dimensionattribute-assl).  
  
 **Atributo de dimensión**  
 Seleccione el atributo de dimensión al que el Asistente para dimensiones asignará el tipo de atributo especial que se muestra en **Tipo de atributo**.  
  
## <a name="see-also"></a>Consulte también  
 [Asistente para dimensiones (ayuda F1)](dimension-wizard-f1-help.md)   
 [Dimensiones &#40;Analysis Services de datos multidimensionales&#41;](multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)   
 [Dimensiones en modelos multidimensionales](multidimensional-models/dimensions-in-multidimensional-models.md)  
  
  
