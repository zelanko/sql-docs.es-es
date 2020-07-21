---
title: Relaciones de dimensión | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- relationships [Analysis Services]
- member groups [Analysis Services]
- regular dimensions [Analysis Services]
- many-to-many relationships [Analysis Services]
- cubes [Analysis Services], relationships
- reference dimensions
- dimensions [Analysis Services], relationships
- fact dimensions [Analysis Services]
- relationships [Analysis Services], dimensions
ms.assetid: de54c059-cb0f-4f66-bd70-8605af05ec4f
author: minewiskan
ms.author: owend
ms.openlocfilehash: 2334c1a97bb4172fff70550dbece5376eb1cb9d7
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/09/2020
ms.locfileid: "84545304"
---
# <a name="dimension-relationships"></a>Relaciones de dimensión
  El uso de la dimensión define las relaciones entre una dimensión de cubo y los grupos de medida de un cubo. Una dimensión de cubo es una instancia de una dimensión de base de datos que se utiliza en un cubo específico. Un cubo puede y suele tener dimensiones de cubo que no están directamente relacionadas con un grupo de medida, pero que podrían estar indirectamente relacionadas con el grupo de medida a través de otra dimensión o grupo de medida. Cuando se agrega una dimensión de base de datos o un grupo de medida a un cubo, [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] intenta determinar el uso de la dimensión mediante el examen de las relaciones entre las tablas de dimensiones y las tablas de hechos en la vista del origen de datos del cubo, y mediante el examen de las relaciones entre los atributos de las dimensiones. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] establece automáticamente la configuración del uso de la dimensión para las relaciones que puede detectar.  
  
 Una relación entre una dimensión y un grupo de medida consta de las tablas de dimensiones y hechos que participan en la relación y un atributo de granularidad que especifica la granularidad de la dimensión del grupo de medida concreto.  
  
## <a name="regular-dimension-relationships"></a>Relaciones de dimensión normales  
 Hay una relación de dimensión normal entre una dimensión de cubo y un grupo de medida cuando la columna de clave de la dimensión se combina directamente con la tabla de hechos. Esta relación directa se basa en una relación de clave principal y clave externa en la base de datos relacional subyacente, pero también podría basarse en una relación lógica definida en la vista del origen de datos. Una relación de dimensión normal representa la relación entre tablas de dimensiones y una tabla de hechos en un diseño de esquema en estrella tradicional. Para obtener más información sobre las relaciones normales, vea [definir una relación normal y propiedades de relación normal](../multidimensional-models/define-a-regular-relationship-and-regular-relationship-properties.md).  
  
## <a name="reference-dimension-relationships"></a>Relaciones de dimensión de referencia  
 Hay una relación de dimensión de referencia entre una dimensión de cubo y un grupo de medida cuando la columna de clave de la dimensión se combina indirectamente con la tabla de hechos mediante una clave de otra tabla de dimensiones, como se muestra en la siguiente ilustración.  
  
 ![Diagrama lógico: relación de dimensiones a las que se hace referencia](../../analysis-services/dev-guide/media/as-refdimension1.gif "Diagrama lógico: relación de dimensiones a las que se hace referencia")  
  
 Una relación de dimensión de referencia representa la relación entre tablas de dimensiones y una tabla de hechos en un diseño de esquema de copo de nieve. Cuando las tablas de dimensiones se conectan en un esquema de copo de nieve, es posible definir una única dimensión mediante columnas de varias tablas, o bien, definir dimensiones independientes basadas en las tablas de dimensiones independientes y, a continuación, definir un vínculo entre ellas mediante la configuración de la relación de dimensión de referencia. En la ilustración siguiente se muestra una tabla de hechos denominada **InternetSales**y dos tablas de dimensiones denominadas **Customer** y **Geography**, en un esquema de copo de nieve.  
  
 ![Esquema lógico: relación de dimensiones a las que se hace referencia](../../analysis-services/dev-guide/media/as-refdim-schema1.gif "Esquema lógico: relación de dimensiones a las que se hace referencia")  
  
 Puede crear una dimensión con la tabla **Customer** como la tabla principal de dimensiones y la tabla **Geography** incluida como una tabla relacionada. Entonces se define una relación normal entre la dimensión y el grupo de medida InternetSales.  
  
 Como alternativa, puede crear dos dimensiones relacionadas con el grupo de medida InternetSales: una dimensión basada en la tabla **Customer** y una dimensión basada en la tabla **Geography** . A continuación, puede relacionar la dimensión geográfica con el grupo de medida InternetSales mediante una relación de dimensión de referencia por medio de la dimensión de cliente. En este caso, cuando los hechos del grupo de medida InternetSales están influenciados por la dimensión geográfica, los hechos están influenciados por Customer y Geography. Si el cubo contiene un segundo grupo de medida denominado Reseller Sales, no podrá dimensionar los hechos del grupo de medida Reseller Sales por Geography, dado que no existiría relación entre Reseller Sales y Geography.  
  
 No hay ningún límite con respecto al número de dimensiones de referencia que se pueden encadenar, como se muestra en la siguiente ilustración.  
  
 ![Diagrama lógico: relación de dimensiones a las que se hace referencia](../../analysis-services/dev-guide/media/as-refdimension2.gif "Diagrama lógico: relación de dimensiones a las que se hace referencia")  
  
 Para obtener más información sobre las relaciones referenciadas, vea [definir una relación referenciada y propiedades de la relación referenciadas](../multidimensional-models/define-a-referenced-relationship-and-referenced-relationship-properties.md).  
  
## <a name="fact-dimension-relationships"></a>Relaciones de dimensión de hechos  
 Las dimensiones de hechos, más conocidas como dimensiones degeneradas, son dimensiones estándar que se crean a partir de columnas de atributos de tablas de hechos en lugar de columnas de atributos de tablas de dimensiones. Los datos útiles de dimensiones algunas veces se almacenan en una tabla de hechos para reducir la duplicación. Por ejemplo, en el diagrama siguiente se muestra la tabla de hechos **FactResellerSales** de la [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] base de datos de ejemplo.  
  
 ![Las columnas de la tabla de hechos son compatibles con las dimensiones](../../analysis-services/dev-guide/media/as-factdim.gif "Las columnas de la tabla de hechos son compatibles con las dimensiones")  
  
 La tabla contiene información sobre atributos no solo para cada línea de un pedido emitido por un distribuidor, sino sobre el propio pedido. Los atributos rodeados por un círculo en el diagrama anterior identifican la información de la tabla **FactResellerSales** que podría usarse como atributos en una dimensión. En este caso, dos piezas adicionales de información, el número de seguimiento del transportista y el número de orden de compra emitido por el distribuidor están representados por las columnas de atributo CarrierTrackingNumber y CustomerPONumber. Esta información es interesante; por ejemplo, los usuarios deberían estar interesados en ver la información agregada, como el costo total del producto, para todos los pedidos que se envían con un solo número de seguimiento. Sin embargo, sin una dimensión no se pueden organizar ni agregar datos para estos dos atributos.  
  
 En teoría, se podría crear una tabla de dimensiones que utilizara la misma información de clave que la tabla FactResellerSales y mover las otras dos columnas de atributos, CarrierTrackingNumber y CustomerPONumber, a esa tabla de dimensiones. Sin embargo, así se duplicaría una parte significativa de los datos y se agregaría una complejidad innecesaria al almacenamiento de datos para poder representar solo dos atributos como una dimensión independiente.  
  
> [!NOTE]  
>  Las dimensiones de hechos se suelen utilizar para permitir acciones de obtención de detalles. Para más información sobre las acciones, vea [Acciones &#40;Analysis Services - Datos multidimensionales&#41;](../multidimensional-models/actions-analysis-services-multidimensional-data.md).  
  
> [!NOTE]  
>  Las dimensiones de hechos deben actualizarse incrementalmente después de cada actualización al grupo de medida al que hace referencia la relación de hechos. Si la dimensión de hechos es una dimensión ROLAP, el motor de procesamiento de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] elimina todas las cachés y procesa incrementalmente el grupo de medida.  
  
 Para obtener más información sobre las relaciones de hechos, vea [definir las propiedades de una relación de hechos y de una relación](../multidimensional-models/define-a-fact-relationship-and-fact-relationship-properties.md)de hechos.  
  
## <a name="many-to-many-dimension-relationships"></a>Relaciones de dimensión varios a varios  
 En la mayoría de dimensiones, cada hecho se combina con un solo miembro de la dimensión y un único miembro de la dimensión puede asociarse a varios hechos. En terminología de bases de datos relacionales, esto se conoce como relación de uno a varios. No obstante, suele resultar útil combinar un único hecho con varios miembros de dimensión. Por ejemplo, un cliente de un banco podría tener varias cuentas (cuenta corriente, libreta de ahorro, tarjetas de crédito y cuentas de inversión) y una cuenta también puede tener varios propietarios. La dimensión de cliente creada a partir de estas relaciones tendrá varios miembros relacionados con una única transacción de cuenta.  
  
 ![Esquema lógico: relación de dimensiones varios a varios](../../analysis-services/dev-guide/media/as-many-dimension1.gif "Esquema lógico: relación de dimensiones varios a varios")  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]permite definir una relación de varios a varios entre una dimensión y una tabla de hechos.  
  
> [!NOTE]  
>  Para admitir una relación de dimensión de varios a varios, la vista del origen de datos debe haber establecido una relación de clave externa entre todas las tablas implicadas, tal y como se muestra en el diagrama anterior. De lo contrario, no podrá seleccionar el grupo de medida intermedio correcto cuando establezca la relación en la pestaña **uso de dimensiones** del diseñador de dimensiones.  
  
 Para obtener más información sobre las relaciones de varios a varios, vea [definir una relación de varios a varios y propiedades de la relación de varios a varios](../multidimensional-models/define-a-many-to-many-relationship-and-many-to-many-relationship-properties.md).  
  
## <a name="see-also"></a>Consulte también  
 [Dimensiones &#40;Analysis Services - Datos multidimensionales&#41;](../multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)  
  
  
