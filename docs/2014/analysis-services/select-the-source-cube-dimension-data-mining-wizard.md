---
title: Seleccionar la dimensión de cubo de origen (Asistente para minería de datos) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.dmwizard.selectsourcecube.f1
ms.assetid: 556e216b-5e21-4160-967d-4c57591fbab4
author: minewiskan
ms.author: owend
ms.openlocfilehash: 98bc018ac9d95082a70334dc01f456a4b258b397
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84940786"
---
# <a name="select-the-source-cube-dimension-data-mining-wizard"></a>Seleccionar la dimensión de cubo de origen (Asistente para minería de datos)
  Utilice la página **Seleccionar la dimensión de cubo de origen** para seleccionar la dimensión desde el cubo que contiene los casos que desea analizar. Por ejemplo, si crea un modelo que analiza el comportamiento adquisitivo de los clientes basándose en los datos demográficos, seleccionaría la dimensión de cliente, que suele contener un registro único para cada cliente y diferentes atributos que representan datos demográficos, como el género, la ubicación o los ingresos. Más adelante en el asistente tendrá la oportunidad de agregar una tabla relacionada con esta tabla de casos: por ejemplo, puede agregar una tabla anidada que muestre los productos que ha comprado el cliente.  
  
> [!NOTE]  
>  Esta página aparecerá solo si ha seleccionado **A partir de un cubo existente** en la página **Seleccionar el método de definición** del asistente.  
  
## <a name="options"></a>Opciones  
 **Seleccione una dimensión de cubo de origen**  
 Seleccione la dimensión del cubo que proporcionará los datos de origen para su estructura de minería de datos.  
  
## <a name="choosing-a-dimension"></a>Elegir una dimensión  
 Dado que solamente puede seleccionar una dimensión para usar en el modelo, es importante comprender la estructura del cubo y seleccionar la dimensión que proporciona la mejor información para el modelo. Si no sabe qué dimensión debe usar, puede resultar útil examinar el cubo y revisar los campos y los datos incluidos en ellos mediante el Diseñador de dimensiones. Para más información, vea [Examinar los datos de dimensiones en el Diseñador de dimensiones](multidimensional-models/database-dimensions-browse-dimension-data-in-dimension-designer.md).  
  
 Si no conoce las dimensiones en general, vea [Introducción a las dimensiones &#40;Analysis Services - Datos multidimensionales&#41;](multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md).  
  
 Para obtener más información acerca del tipo de datos que suele incluir una sola dimensión, incluidos los atributos y las medidas que pueden resultar útiles para la minería de datos, vea [Dimension Relationships](multidimensional-models-olap-logical-cube-objects/dimension-relationships.md).  
  
 Si la dimensión que elige no contiene todos los atributos relacionados que necesita para crear el modelo de minería de datos, es posible que deba modificarla. Para más información, vea [Definir dimensiones de base de datos](multidimensional-models/define-database-dimensions.md).  
  
## <a name="see-also"></a>Consulte también  
 [Asistente para minería de datos (ayuda F1) &#40;Analysis Services: minería de datos&#41;](data-mining-wizard-f1-help-analysis-services-data-mining.md)   
 [Crear la estructura de minería de datos &#40;Asistente para minería de datos&#41;](create-the-data-mining-structure-data-mining-wizard.md)   
 [Seleccione la clave de caso &#40;Asistente para minería de datos&#41;](select-the-case-key-data-mining-wizard.md)  
  
  
