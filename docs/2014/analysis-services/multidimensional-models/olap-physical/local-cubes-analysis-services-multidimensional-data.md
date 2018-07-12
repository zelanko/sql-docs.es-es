---
title: Los cubos locales (Analysis Services - datos multidimensionales) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- cubes [Analysis Services], local
ms.assetid: e52e1515-35a7-4dc3-9bbf-736d176ba0c7
caps.latest.revision: 13
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3cc1e27115d898cc2ba839fb14d2f7edfa8c560f
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37149286"
---
# <a name="local-cubes-analysis-services---multidimensional-data"></a>Cubos locales (Analysis Services - Datos multidimensionales)
  Para crear, actualizar o eliminar los cubos locales, debe escribir y ejecutar un script ASSL o un programa AMO.  
  
 Los cubos locales y los modelos de minería de datos locales permiten el análisis en una estación de trabajo cliente aunque esté desconectada de la red. Por ejemplo, una aplicación cliente puede llamar al proveedor OLE DB para OLAP 9.0 (MSOLAP.3), que carga el motor de cubos locales para crear y consultar los cubos locales, tal como se muestra en la siguiente ilustración:  
  
 ![Arquitectura de cliente para los cubos locales y modelos](../../../analysis-services/dev-guide/media/as-localcubearch9.gif "arquitectura de cliente para los cubos locales y modelos")  
  
 ADMOD.NET y los objetos de administración de análisis (AMO) también cargan el motor de cubo local cuando interactúan con los cubos locales. Solo un proceso puede obtener acceso al archivo de cubo local porque el motor de cubo local bloquea exclusivamente un archivo de cubo local cuando establece una conexión al cubo local. En un proceso se permiten hasta cinco conexiones simultáneas.  
  
 Un archivo .cub puede contener más de un cubo o modelo de minería de datos. Las consultas a los cubos locales y modelos de minería de datos se controlan mediante el motor de cubos locales y no necesitan ninguna conexión con una instancia de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
> [!NOTE]  
>  El uso de [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] y de [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] para administrar cubos locales no está admitido.  
  
## <a name="local-cubes"></a>Cubos locales  
 Se puede crear un cubo local y rellena a partir de un cubo existente en un [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instancia o desde un origen de datos relacional.  
  
|Origen de los datos del cubo local|Método de creación|  
|------------------------------------|---------------------|  
|Cubo basado en servidor|Puede usar la instrucción CREATE GLOBAL CUBE o un [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] script Scripting Language (ASSL) para crear y rellenar un cubo a partir de un cubo basado en servidor. Para obtener más información, consulte [instrucción CREATE GLOBAL CUBE &#40;MDX&#41; ](/sql/mdx/mdx-data-definition-create-global-cube) o [Analysis Services Scripting Language &#40;ASSL&#41; referencia](../../scripting/analysis-services-scripting-language-assl-for-xmla.md).|  
|Origen de datos relacionales|Puede usar un script ASSL para crear y rellenar una base de datos relacional OLE DB. Para crear un cubo local mediante ASSL, conéctese a un archivo de cubo local (*.cub) y ejecute el script ASSL de la misma forma que ejecuta un script ASSL en una instancia de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] para crear un cubo de servidor. Para obtener más información, consulte [Analysis Services Scripting Language &#40;ASSL&#41; referencia](../../scripting/analysis-services-scripting-language-assl-for-xmla.md).|  
  
 Use la instrucción REFRESH CUBE  para volver a generar un cubo local y actualizar sus datos. Para obtener más información, consulte [REFRESH CUBE, instrucción &#40;MDX&#41;](/sql/mdx/mdx-data-definition-refresh-cube).  
  
### <a name="local-cubes-created-from-server-based-cubes"></a>Cubos locales creados desde cubos basados en servidor  
 Al crear cubos locales creados a partir de cubos basados en servidor, debe tener en cuenta las siguientes consideraciones:  
  
-   Las medidas de recuento distintivas no están admitidas.  
  
-   Cuando agrega una medida, también debe incluir como mínimo una dimensión relacionada con la medida que se agrega. Para obtener más información acerca de las relaciones de dimensión para grupos de medida, vea [relaciones de dimensión](../../multidimensional-models-olap-logical-cube-objects/dimension-relationships.md).  
  
-   Cuando agrega una jerarquía de elementos primarios y secundarios, los niveles y los filtros de la jerarquía de elementos primarios y secundarios se omiten y se incluye la totalidad de la jerarquía de elementos primarios y secundarios.  
  
-   Las propiedades de los miembros no se crean.  
  
-   Cuando incluye una medida de suma parcial, no se permiten segmentos en la dimensión de Cuenta o Tiempo.  
  
-   Las dimensiones de referencias siempre se materializan.  
  
-   Al incluir una dimensión de varios a varios, se aplican las siguientes reglas:  
  
    -   La dimensión varios a varios no se puede segmentar.  
  
    -   Se debe agregar una medida del grupo de medidas intermedio.  
  
    -   No se puede segmentar ninguna dimensión común a los dos grupos de mensajes implicados en la relación varios a varios.  
  
-   Solo los miembros calculados, los conjuntos con nombres y las asignaciones que dependen de medidas y dimensiones agregadas al cubo local se mostrarán en el cubo local. Los miembros calculados, los conjuntos con nombre y las asignaciones no válidos se excluirán automáticamente.  
  
### <a name="security"></a>Seguridad  
 Para que un usuario crear un cubo local desde un cubo de servidor, se debe conceder al usuario **obtención de detalles y cubo Local** permisos en el cubo del servidor. Para obtener más información, consulte [conceder permisos para cubos o modelos &#40;Analysis Services&#41;](../../multidimensional-models/grant-cube-or-model-permissions-analysis-services.md).  
  
 Los cubos locales no se protegen mediante roles como los cubos de servidor. Cualquier usuario con acceso de nivel de archivo a un archivo de cubo local puede realizar consultas en los cubos que allí residen. Puede usar la propiedad de conexión `Encryption Password` en un archivo de cubo local para establecer una contraseña en el archivo de cubo local. Al establecer una contraseña en un archivo de cubo local es preciso que todas las conexiones futuras al archivo de cubo local usen esta contraseña para consultar el archivo.  
  
## <a name="see-also"></a>Vea también  
 [Instrucción CREATE GLOBAL CUBE &#40;MDX&#41;](/sql/mdx/mdx-data-definition-create-global-cube)   
 [Desarrollar aplicaciones con Analysis Services Scripting Language &#40;ASSL&#41;](../scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)   
 [REFRESH CUBE, instrucción &#40;MDX&#41;](/sql/mdx/mdx-data-definition-refresh-cube)  
  
  
