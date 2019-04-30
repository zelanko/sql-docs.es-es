---
title: Insertar, actualizar y quitar miembros (XMLA) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3a409e21e925b3912aee5ec751747f61bce05276
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63138587"
---
# <a name="inserting-updating-and-dropping-members-xmla"></a>Insertar, actualizar y quitar miembros (XMLA)
  Puede usar el [insertar](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/insert-element-xmla), [actualizar](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/update-element-xmla), y [Drop](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/drop-element-xmla) los comandos de XML for Analysis (XMLA) para insertar respectivamente, actualizar o eliminar miembros de una dimensión habilitada para escritura. Para obtener más información acerca de las dimensiones habilitadas para escritura, consulte [dimensiones habilitadas para escritura](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions.md).  
  
## <a name="inserting-new-members"></a>Insertar nuevos miembros  
 El **insertar** comando inserta nuevos miembros en atributos especificados en una dimensión habilitada para escritura.  
  
 Antes de construir el **insertar** comando, debe tener disponible para los miembros nuevos que se va a insertar la información siguiente:  
  
-   La dimensión donde se van a insertar los nuevos miembros.  
  
-   El atributo de la dimensión donde se van a insertar los nuevos miembros.  
  
-   Los nombres de los nuevos miembros, incluida cualquier traducción aplicable del nombre.  
  
-   Las claves de los nuevos miembros. Si un atributo utiliza una clave compuesta, la clave puede requerir varios valores.  
  
-   Los valores de cualquier propiedad de atributo aplicable que no se implemente como otros atributos en la dimensión. Entre estas propiedades de atributo se incluyen operaciones unarias, traducciones, resúmenes personalizados, propiedades de resúmenes personalizados y niveles omitidos.  
  
 El **insertar** comando solamente acepta dos propiedades:  
  
-   El [objeto](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla) propiedad, que contiene una referencia de objeto para la dimensión que se va a insertar los miembros. La referencia de objeto contiene el identificador de la base de datos, el identificador del cubo y el identificador de dimensión para la dimensión.  
  
-   El [atributos](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/attributes-element-xmla) propiedad, que contiene uno o varios [atributo](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/attribute-element-xmla) elementos para identificar los atributos que se va a insertar los miembros. Cada **atributo** elemento identifica un atributo y proporciona el nombre, valor, traducciones, operador unario, resúmenes personalizados, propiedades de resúmenes personalizados y los niveles omitidos para un solo miembro a agregarse al atributo identificado.  
  
    > [!NOTE]  
    >  Todas las propiedades para el **atributo** elemento debe incluirse. De lo contrario, puede producirse un error.  
  
## <a name="updating-existing-members"></a>Actualizar los miembros existentes  
 El **actualización** comando actualiza los miembros existentes en los atributos especificados, en función de las relaciones con otros miembros de otros atributos, en una dimensión habilitada para escritura. El **actualización** comando puede mover miembros a otros niveles de jerarquías incluidos en la dimensión y pueden usarse para reestructurar las jerarquías de elementos primarios y secundarios definidas por atributos primarios.  
  
 Antes de construir el **actualización** comando, debe tener disponible para los miembros que se puede actualizar la siguiente información:  
  
-   La dimensión donde se van a actualizar los miembros existentes.  
  
-   Los atributos de la dimensión donde se van a actualizar los miembros existentes.  
  
-   Las claves de los miembros existentes. Si un atributo utiliza una clave compuesta, la clave puede requerir varios valores.  
  
-   Los valores de cualquier propiedad de atributo aplicable que no se implemente como otros atributos en la dimensión. Entre estas propiedades de atributo se incluyen operaciones unarias, traducciones, resúmenes personalizados, propiedades de resúmenes personalizados y niveles omitidos.  
  
 El **actualización** comando toma solo tres propiedades obligatorias:  
  
-   El **objeto** propiedad, que contiene una referencia de objeto para la dimensión en el que los miembros se van a actualizarse. La referencia de objeto contiene el identificador de la base de datos, el identificador del cubo y el identificador de dimensión para la dimensión.  
  
-   El **atributos** propiedad, que contiene uno o varios **atributo** elementos para identificar los atributos en el que los miembros se van a actualizarse. El **atributo** elemento identifica un atributo y proporciona el nombre, valor, traducciones, operador unario, resúmenes personalizados, propiedades de resúmenes personalizados y los niveles omitidos para un miembro único actualizado para el atributo identificado.  
  
    > [!NOTE]  
    >  Todas las propiedades para el **atributo** elemento debe incluirse. De lo contrario, puede producirse un error.  
  
-   El [donde](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/where-element-xmla) propiedad, que contiene uno o varios **atributo** elementos que restringen los atributos en el que los miembros se van a actualizarse. El **donde** propiedad es fundamental para limitar una **actualización** comando a instancias específicas de un miembro. Si el **donde** propiedad no se especifica, se actualizan todas las instancias de un miembro determinado. Por ejemplo, hay tres clientes para los que desea cambiar el nombre de ciudad de Redmond a Bellevue. Para cambiar el nombre de la ciudad, debe proporcionar un **donde** atributo de propiedad que identifica los tres miembros en el cliente para que se deben cambiar los miembros de atributo City. Si esto no proporciona **donde** propiedad, todos los clientes cuyo nombre de ciudad sea actualmente Redmond tendría el nombre de la ciudad de Bellevue después la **actualización** comando se ejecuta.  
  
    > [!NOTE]  
    >  A excepción de los nuevos miembros, el **actualizar** comando solo puede actualizar los valores de clave de atributo para atributos no incluidos en el **donde** cláusula. Por ejemplo, el nombre de ciudad no se puede actualizar cuando se actualiza un cliente; de lo contrario, dicho nombre se cambia para todos los clientes.  
  
### <a name="updating-members-in-parent-attributes"></a>Actualizar miembros de atributos primarios  
 Para admitir los atributos primarios, el **actualización** comando opcional [MoveWithDescendants](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/movewithdescendants-element-xmla)garantizar propiedades. Establecer el **MoveWithDescendants** propiedad en true indica que los descendientes del miembro primario también se deben mover con el miembro primario cuando cambia el identificador de dicho miembro primario. Si este valor se establece en false, al mover un miembro primario, los descendientes inmediatos de dicho miembro ascienden al nivel donde residía anteriormente el miembro primario.  
  
 Al actualizar los miembros de un atributo primario, el **actualizar** comando no puede actualizar los miembros de otros atributos.  
  
## <a name="dropping-existing-members"></a>Quitar miembros existentes  
 Antes de construir el **Drop** comando, debe tener disponible para los miembros que se quitará la siguiente información:  
  
-   La dimensión donde se van a quitar miembros existentes.  
  
-   Los atributos de la dimensión donde se van a quitar miembros existentes.  
  
-   Las claves de los miembros existentes que se van a quitar. Si un atributo utiliza una clave compuesta, la clave puede requerir varios valores.  
  
 El **Drop** comando acepta solo dos propiedades necesarias:  
  
-   El **objeto** propiedad, que contiene una referencia de objeto para la dimensión que se va a quitar los miembros. La referencia de objeto contiene el identificador de la base de datos, el identificador del cubo y el identificador de dimensión para la dimensión.  
  
-   El **donde** propiedad, que contiene uno o varios **atributo** elementos para restringir los atributos que se va a eliminar los miembros. El **donde** propiedad es fundamental para limitar una **Drop** comando a instancias específicas de un miembro. Si el **donde** comando no se especifica, se quitan todas las instancias de un miembro determinado. Por ejemplo, quiere quitar tres clientes de Redmond. Para quitar estos clientes, debe proporcionar un **donde** propiedad que identifica los tres miembros en el atributo Customer va a quitar y el miembro Redmond del atributo City desde el que los tres clientes son va a quitar. Si el **donde** propiedad especifica solo el miembro Redmond del atributo City, todos los clientes asociados a Redmond se quitarían la **Drop** comando. Si el **donde** propiedad solo especifica los tres miembros en el atributo Customer, los tres clientes se eliminarían por completo el **Drop** comando.  
  
    > [!NOTE]  
    >  El **atributo** elementos incluidos en un **Drop** comando debe contener solo el **AttributeName** y **claves** propiedades. De lo contrario, puede producirse un error.  
  
### <a name="dropping-members-in-parent-attributes"></a>Quitar miembros de atributos primarios  
 Establecer el [DeleteWithDescendants](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/deletewithdescendants-element-xmla) propiedad indica que deben eliminarse también los descendientes de un miembro primario con el miembro primario. Sin embargo, si este valor se establece en false, los descendientes inmediatos del miembro primario ascienden al nivel donde residía anteriormente el miembro primario.  
  
> [!IMPORTANT]  
>  Para eliminar el miembro primario y sus descendientes, un usuario solamente debe tener permisos de eliminación para el miembro primario. No es necesario que el usuario tenga permisos de eliminación para los descendientes.  
  
## <a name="see-also"></a>Vea también  
 [Elemento DROP &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/drop-element-xmla)   
 [Insertar elemento &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/insert-element-xmla)   
 [Actualizar elemento &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/update-element-xmla)   
 [Definir e identificar objetos &#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/defining-and-identifying-objects-xmla.md)   
 [Desarrollo con XMLA en Analysis Services](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
