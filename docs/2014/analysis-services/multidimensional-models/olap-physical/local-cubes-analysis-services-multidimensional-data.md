---
title: Cubos locales (Analysis Services de datos multidimensionales) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- cubes [Analysis Services], local
ms.assetid: e52e1515-35a7-4dc3-9bbf-736d176ba0c7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8c67150d5345b95b025e4005642ebccac63f86f2
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/09/2019
ms.locfileid: "68889497"
---
# <a name="local-cubes-analysis-services---multidimensional-data"></a>Cubos locales (Analysis Services - Datos multidimensionales)
  Para crear, actualizar o eliminar los cubos locales, debe escribir y ejecutar un script ASSL o un programa AMO.  
  
 Los cubos locales y los modelos de minería de datos locales permiten el análisis en una estación de trabajo cliente aunque esté desconectada de la red. Por ejemplo, una aplicación cliente puede llamar al proveedor OLE DB para OLAP 9.0 (MSOLAP.3), que carga el motor de cubos locales para crear y consultar los cubos locales, tal como se muestra en la siguiente ilustración:  
  
 ![Arquitectura de cliente para modelos y cubos locales](https://docs.microsoft.com/analysis-services/analysis-services/dev-guide/media/as-localcubearch9.gif "Arquitectura de cliente para modelos y cubos locales")  
  
 ADMOD.NET y los objetos de administración de análisis (AMO) también cargan el motor de cubo local cuando interactúan con los cubos locales. Solo un proceso puede obtener acceso al archivo de cubo local porque el motor de cubo local bloquea exclusivamente un archivo de cubo local cuando establece una conexión al cubo local. En un proceso se permiten hasta cinco conexiones simultáneas.  
  
 Un archivo .cub puede contener más de un cubo o modelo de minería de datos. Las consultas a los cubos locales y modelos de minería de datos se controlan mediante el motor de cubos locales y no necesitan ninguna conexión con una instancia de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
> [!NOTE]  
>  El uso de [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] y de [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] para administrar cubos locales no está admitido.  
  
## <a name="local-cubes"></a>Cubos locales  
 Un cubo local se puede crear y rellenar a partir de un cubo [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] existente en una instancia o desde un origen de datos relacional.  
  
|Origen de los datos del cubo local|Método de creación|  
|------------------------------------|---------------------|  
|Cubo basado en servidor|Puede usar la instrucción CREATE global Cube o un [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] script de lenguaje de scripting de (ASSL) para crear y rellenar un cubo a partir de un cubo basado en servidor. Para obtener más información, vea [Create global Cube &#40;Statement&#41; MDX](/sql/mdx/mdx-data-definition-create-global-cube) o [Analysis Services scripting &#40;Language&#41; ASSL Reference](https://docs.microsoft.com/bi-reference/assl/analysis-services-scripting-language-assl-for-xmla).|  
|Origen de datos relacionales|Puede usar un script ASSL para crear y rellenar una base de datos relacional OLE DB. Para crear un cubo local mediante ASSL, conéctese a un archivo de cubo local (*.cub) y ejecute el script ASSL de la misma forma que ejecuta un script ASSL en una instancia de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] para crear un cubo de servidor. Para obtener más información, vea [Analysis Services referencia de &#40;ASSL&#41; de lenguaje](https://docs.microsoft.com/bi-reference/assl/analysis-services-scripting-language-assl-for-xmla)de scripting.|  
  
 Use la instrucción REFRESH CUBE  para volver a generar un cubo local y actualizar sus datos. Para obtener más información, vea [Actualizar instrucción &#40;de&#41;cubo MDX](/sql/mdx/mdx-data-definition-refresh-cube).  
  
### <a name="local-cubes-created-from-server-based-cubes"></a>Cubos locales creados desde cubos basados en servidor  
 Al crear cubos locales creados a partir de cubos basados en servidor, debe tener en cuenta las siguientes consideraciones:  
  
-   Las medidas de recuento distintivas no están admitidas.  
  
-   Cuando agrega una medida, también debe incluir como mínimo una dimensión relacionada con la medida que se agrega. Para obtener más información sobre las relaciones de dimensión con los grupos de medida, vea [relaciones de dimensión](../../multidimensional-models-olap-logical-cube-objects/dimension-relationships.md).  
  
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
 Para que un usuario pueda crear un cubo local a partir de un cubo del servidor, se debe conceder al usuario permisos de **obtención de detalles y cubo local** en el cubo del servidor. Para obtener más información, vea [conceder permisos &#40;para cubos o modelos Analysis Services&#41;](../../multidimensional-models/grant-cube-or-model-permissions-analysis-services.md).  
  
 Los cubos locales no se protegen mediante roles como los cubos de servidor. Cualquier usuario con acceso de nivel de archivo a un archivo de cubo local puede realizar consultas en los cubos que allí residen. Puede usar la propiedad de conexión `Encryption Password` en un archivo de cubo local para establecer una contraseña en el archivo de cubo local. Al establecer una contraseña en un archivo de cubo local es preciso que todas las conexiones futuras al archivo de cubo local usen esta contraseña para consultar el archivo.  
  
## <a name="see-also"></a>Vea también  
 [Instrucción &#40;Create global Cube MDX&#41;](/sql/mdx/mdx-data-definition-create-global-cube)   
 [Desarrollar aplicaciones con Analysis Services Scripting Language &#40;ASSL&#41;](../scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)   
 [Instrucción &#40;Refresh Cube MDX&#41;](/sql/mdx/mdx-data-definition-refresh-cube)  
  
  
