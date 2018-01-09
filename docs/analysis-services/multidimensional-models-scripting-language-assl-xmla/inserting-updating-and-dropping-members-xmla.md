---
title: Insertar, actualizar y quitar miembros (XMLA) | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- inserting dimension members
- XML for Analysis, members
- removing dimension members
- dropping dimension members
- write-enabled dimensions [Analysis Services]
- XMLA, members
- deleting dimension members
- dimensions [Analysis Services], XML for Analysis
ms.assetid: bba922b5-8b88-4051-9506-ff055248182a
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 17c8d0a3fddeb0cfd9d8a6ef69eac11bc9b2c34a
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="inserting-updating-and-dropping-members-xmla"></a>Insertar, actualizar y quitar miembros (XMLA)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Puede usar el [insertar](../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md), [actualizar](../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md), y [Drop](../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md) comandos de XML for Analysis (XMLA) para respectivamente Insertar, actualizar o eliminar los miembros de una dimensión habilitada para escritura. Para obtener más información acerca de las dimensiones habilitadas para escritura, consulte [dimensiones habilitadas para escritura](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions.md).  
  
## <a name="inserting-new-members"></a>Insertar nuevos miembros  
 El **insertar** comando inserta nuevos miembros en atributos especificados en una dimensión habilitada para escritura.  
  
 Antes de construir el **insertar** comando, debe tener disponible para los nuevos miembros que se va a insertar la siguiente información:  
  
-   La dimensión donde se van a insertar los nuevos miembros.  
  
-   El atributo de la dimensión donde se van a insertar los nuevos miembros.  
  
-   Los nombres de los nuevos miembros, incluida cualquier traducción aplicable del nombre.  
  
-   Las claves de los nuevos miembros. Si un atributo utiliza una clave compuesta, la clave puede requerir varios valores.  
  
-   Los valores de cualquier propiedad de atributo aplicable que no se implemente como otros atributos en la dimensión. Entre estas propiedades de atributo se incluyen operaciones unarias, traducciones, resúmenes personalizados, propiedades de resúmenes personalizados y niveles omitidos.  
  
 El **insertar** comando solamente acepta dos propiedades:  
  
-   El [objeto](../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md) propiedad, que contiene una referencia de objeto para la dimensión en la que los miembros se va a insertar. La referencia de objeto contiene el identificador de la base de datos, el identificador del cubo y el identificador de dimensión para la dimensión.  
  
-   El [atributos](../../analysis-services/xmla/xml-elements-properties/attributes-element-xmla.md) propiedad, que contiene uno o varios [atributo](../../analysis-services/xmla/xml-elements-properties/attribute-element-xmla.md) elementos para identificar los atributos que se va a insertar los miembros. Cada **atributo** elemento identifica un atributo y proporciona el nombre, valor, traducciones, operador unario, resúmenes personalizados, propiedades de resúmenes personalizados y niveles omitidos para un solo miembro va a agregar al atributo identificado.  
  
    > [!NOTE]  
    >  Todas las propiedades de la **atributo** elemento debe incluirse. De lo contrario, puede producirse un error.  
  
## <a name="updating-existing-members"></a>Actualizar los miembros existentes  
 El **actualización** comando actualiza los miembros existentes en atributos especificados, en función de las relaciones con otros miembros de otros atributos, en una dimensión habilitada para escritura. El **actualización** comando puede mover miembros a otros niveles de jerarquías incluidos en la dimensión y pueden usarse para reestructurar las jerarquías de elementos primarios y secundarios definidas por atributos primarios.  
  
 Antes de construir el **actualización** comando, debe tener disponible para los miembros que se va a actualizar la siguiente información:  
  
-   La dimensión donde se van a actualizar los miembros existentes.  
  
-   Los atributos de la dimensión donde se van a actualizar los miembros existentes.  
  
-   Las claves de los miembros existentes. Si un atributo utiliza una clave compuesta, la clave puede requerir varios valores.  
  
-   Los valores de cualquier propiedad de atributo aplicable que no se implemente como otros atributos en la dimensión. Entre estas propiedades de atributo se incluyen operaciones unarias, traducciones, resúmenes personalizados, propiedades de resúmenes personalizados y niveles omitidos.  
  
 El **actualización** comando toma solo tres propiedades obligatorias:  
  
-   El **objeto** propiedad, que contiene una referencia de objeto para la dimensión en la que los miembros se van a actualizarse. La referencia de objeto contiene el identificador de la base de datos, el identificador del cubo y el identificador de dimensión para la dimensión.  
  
-   El **atributos** propiedad, que contiene uno o varios **atributo** elementos para identificar los atributos en el que los miembros se van a actualizarse. El **atributo** elemento identifica un atributo y proporciona el nombre, valor, traducciones, operador unario, resúmenes personalizados, propiedades de resúmenes personalizados y niveles omitidos para un miembro único actualizado para el atributo identificado.  
  
    > [!NOTE]  
    >  Todas las propiedades de la **atributo** elemento debe incluirse. De lo contrario, puede producirse un error.  
  
-   El [donde](../../analysis-services/xmla/xml-elements-properties/where-element-xmla.md) propiedad, que contiene uno o varios **atributo** elementos que restringen los atributos en el que los miembros se van a actualizarse. El **donde** propiedad es fundamental para limitar una **actualización** comando a instancias específicas de un miembro. Si el **donde** propiedad no se especifica, se actualizan todas las instancias de un miembro determinado. Por ejemplo, hay tres clientes para los que desea cambiar el nombre de ciudad de Redmond a Bellevue. Para cambiar el nombre de la ciudad, debe proporcionar un **donde** atributo de propiedad que identifica los tres miembros en el cliente para que se deben cambiar los miembros de atributo City. Si no se proporciona este **donde** propiedad, todos los clientes cuyo nombre de ciudad sea actualmente Redmond tendría el nombre de la ciudad de Bellevue después de la **actualización** ejecuciones de comandos.  
  
    > [!NOTE]  
    >  Con la excepción de los nuevos miembros, el **actualizar** comando solo puede actualizar los valores de clave de atributo para atributos no incluidos en el **donde** cláusula. Por ejemplo, el nombre de ciudad no se puede actualizar cuando se actualiza un cliente; de lo contrario, dicho nombre se cambia para todos los clientes.  
  
### <a name="updating-members-in-parent-attributes"></a>Actualizar miembros de atributos primarios  
 Para admitir los atributos primarios, el **actualización** comando opcional [MoveWithDescendants](../../analysis-services/xmla/xml-elements-properties/movewithdescendants-element-xmla.md)garantizar propiedades. Establecer el **MoveWithDescendants** propiedad en true indica que los descendientes del miembro primario deben moverse con el miembro primario cuando cambia el identificador de dicho miembro primario. Si este valor se establece en false, al mover un miembro primario, los descendientes inmediatos de dicho miembro ascienden al nivel donde residía anteriormente el miembro primario.  
  
 Al actualizar los miembros de un atributo primario, el **actualizar** comando no puede actualizar los miembros de otros atributos.  
  
## <a name="dropping-existing-members"></a>Quitar miembros existentes  
 Antes de construir el **Drop** comando, debe tener disponible para los miembros que se quitará la siguiente información:  
  
-   La dimensión donde se van a quitar miembros existentes.  
  
-   Los atributos de la dimensión donde se van a quitar miembros existentes.  
  
-   Las claves de los miembros existentes que se van a quitar. Si un atributo utiliza una clave compuesta, la clave puede requerir varios valores.  
  
 El **Drop** comando acepta solo dos propiedades necesarias:  
  
-   El **objeto** propiedad, que contiene una referencia de objeto para la dimensión en la que los miembros se va a quitar. La referencia de objeto contiene el identificador de la base de datos, el identificador del cubo y el identificador de dimensión para la dimensión.  
  
-   El **donde** propiedad, que contiene uno o varios **atributo** elementos para restringir los atributos que se va a eliminar los miembros. El **donde** propiedad es fundamental para limitar una **Drop** comando a instancias específicas de un miembro. Si el **donde** comando no se especifica, se quitan todas las instancias de un miembro determinado. Por ejemplo, quiere quitar tres clientes de Redmond. Para quitar estos clientes, debe proporcionar un **donde** propiedad que identifica los tres miembros en el atributo Customer va a quitar y el miembro Redmond del atributo City desde el que los tres clientes van a quitarse. Si el **donde** propiedad solo especifica el miembro Redmond del atributo City, todos los clientes asociados a Redmond se quitarían la **Drop** comando. Si el **donde** propiedad solo especifica los tres miembros en el atributo Customer, los tres clientes se eliminará por completo la **Drop** comando.  
  
    > [!NOTE]  
    >  El **atributo** elementos incluidos en un **Drop** comando debe contener solo el **AttributeName** y **claves** propiedades. De lo contrario, puede producirse un error.  
  
### <a name="dropping-members-in-parent-attributes"></a>Quitar miembros de atributos primarios  
 Establecer el [DeleteWithDescendants](../../analysis-services/xmla/xml-elements-properties/deletewithdescendants-element-xmla.md) propiedad indica que deben eliminarse también los descendientes de un miembro primario con el miembro primario. Sin embargo, si este valor se establece en false, los descendientes inmediatos del miembro primario ascienden al nivel donde residía anteriormente el miembro primario.  
  
> [!IMPORTANT]  
>  Para eliminar el miembro primario y sus descendientes, un usuario solamente debe tener permisos de eliminación para el miembro primario. No es necesario que el usuario tenga permisos de eliminación para los descendientes.  
  
## <a name="see-also"></a>Vea también  
 [Eliminar elemento &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md)   
 [Insertar elemento &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)   
 [Actualizar elemento &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)   
 [Definir e identificar objetos &#40; XMLA &#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/defining-and-identifying-objects-xmla.md)   
 [Desarrollo con XMLA en Analysis Services](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
