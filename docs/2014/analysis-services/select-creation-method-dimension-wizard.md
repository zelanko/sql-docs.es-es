---
title: Seleccionar método de creación (Asistente para dimensiones) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dimensionwizard.dimensiondefinition.f1
ms.assetid: 291b0b2d-a03a-4df6-82f7-90ad92d4d1cf
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d44afc5bb4c352a2cb5dfd39030a52db990e3a0b
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66069594"
---
# <a name="select-creation-method-dimension-wizard"></a>Seleccionar método de creación (Asistente para dimensiones)
  Use la página **Seleccionar método de creación** para seleccionar cómo se crea la dimensión.  
  
 **Para abrir el Asistente para dimensiones**  
  
-   En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], en el **Explorador de soluciones**, haga clic con el botón derecho en la carpeta **Dimensiones** para un proyecto de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] y, luego, haga clic en **Nueva dimensión**.  
  
## <a name="options"></a>Opciones  
 **Usar una tabla existente**  
 Cree una dimensión a partir de una o más tablas en un origen de datos. Los atributos que están disponibles para la dimensión dependerán de la estructura de los datos de la tabla.  
  
 Para más información, vea [Crear una dimensión usando una tabla existente](multidimensional-models/create-a-dimension-by-using-an-existing-table.md).  
  
 **Generar una tabla de tiempos en el origen de datos**  
 Cree una tabla de tiempos en el origen de datos subyacente y, a continuación, use dicha tabla para crear una dimensión de tiempo. Use esta opción cuando no existe dicha tabla y no desea usar un script para crear una. La nueva tabla de tiempos contendrá datos para el intervalo de fechas, atributos y calendarios que especifica en el asistente.  
  
> [!NOTE]  
>  Para usar esta opción, debe tener permiso para crear objetos en el origen de datos subyacente. Si no tiene permiso para crear objetos en el origen de datos, intente usar la opción **Generar una tabla de tiempos en el servidor** en su lugar  
  
 Para más información, vea [Crear una dimensión de tiempo generando una tabla de tiempos](multidimensional-models/create-a-time-dimension-by-generating-a-time-table.md).  
  
 **Generar una tabla de tiempos en el servidor**  
 Cree una tabla de tiempos directamente en el servidor y, a continuación, use dicha tabla para crear una dimensión de tiempos. Use esta opción si no tiene permiso para crear objetos en el origen de datos subyacente. La nueva dimensión de tiempos contendrá datos para el intervalo de fechas, atributos y calendarios que especifica en el asistente.  
  
 Para más información, vea [Crear una dimensión de tiempo generando una tabla de tiempos](multidimensional-models/create-a-time-dimension-by-generating-a-time-table.md).  
  
 **Generar una tabla que no sea de tiempos en el origen de datos**  
 Diseñe la dimensión sin un origen de datos relacional subyacente y, a continuación, genere el esquema necesario para el origen de datos. Este enfoque se conoce como modelado de arriba a abajo.  
  
> [!NOTE]  
>  Para usar esta opción, debe tener permiso para crear objetos en el origen de datos subyacente.  
  
 Puede generar la dimensión con o sin una plantilla. Para generar la dimensión con una plantilla, seleccione la plantilla en la lista **Plantilla** .  
  
 Para más información, vea [Crear una dimensión generando una tabla que no sea de tiempos en el origen de datos](multidimensional-models/create-a-dimension-by-generating-a-non-time-table-in-the-data-source.md).  
  
 **Plantilla**  
 Seleccione la plantilla que desea usar para crear la dimensión. Las plantillas proporcionan un completo conjunto de atributos y definiciones de jerarquías orientadas a un fin empresarial específico.  
  
> [!NOTE]  
>  Esta opción solo está disponible cuando se ha seleccionado la opción **Generar una tabla que no sea de tiempos en el origen de datos** .  
  
## <a name="see-also"></a>Consulte también  
 [Asistente para dimensiones (ayuda F1)](dimension-wizard-f1-help.md)   
 [Dimensiones &#40;Analysis Services de datos multidimensionales&#41;](multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)   
 [Dimensiones en modelos multidimensionales](multidimensional-models/dimensions-in-multidimensional-models.md)  
  
  
