---
title: Agrupar miembros de atributo (discretización) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- NameColumn property
- discretization [Analysis Services]
- member groups [Analysis Services]
- grouping members
- DiscretizationNumber property
- sort orders [Analysis Services]
- DiscretizationMethod property
- adding members to member group
- number of member groups
- members [Analysis Services], groups
- names [Analysis Services], member groups
ms.assetid: 5cf2f407-accc-4baf-b54f-7703af338325
caps.latest.revision: 34
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8e07f85d5a6162bed15393d8c255a55cf01b903c
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37251457"
---
# <a name="group-attribute-members-discretization"></a>Agrupar miembros de atributos (discretización)
  Un grupo de miembros es una colección de miembros de dimensión consecutivos generada por el sistema. En [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], los miembros de un atributo pueden agruparse en varios grupos de miembros mediante un proceso denominado discretización. Un nivel de una jerarquía contiene miembros o grupos de miembro, pero no los dos. Cuando los usuarios corporativos examinan un nivel que contiene grupos de miembros, ven los nombres y valores de celdas de estos grupos. Los miembros que genera [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para admitir grupos de miembros se denominan miembros de agrupación y son similares a los miembros normales.  
  
 La propiedad `DiscretizationMethod` de un atributo controla cómo se agrupan los miembros.  
  
|Configuración de `DiscretizationMethod`|Descripción|  
|--------------------------------------|-----------------|  
|`None`|Muestra los miembros.|  
|`Automatic`|Selecciona el método que mejor represente los datos: ya sea el `EqualAreas` método o la `Clusters` método.|  
|`EqualAreas`|Intenta dividir los miembros del atributo en grupos que contengan el mismo número de miembros.|  
|`Clusters`|Intenta dividir los miembros del atributo en grupos mediante el muestreo de los datos de entrenamiento, la inicialización en un número de puntos aleatorios y la ejecución de varias iteraciones del algoritmo de clústeres Expectation-Maximization (EM).<br /><br /> Este método resulta útil porque funciona en cualquier curva de distribución, pero requiere más tiempo de procesamiento.|  
  
 La propiedad `DiscretizationNumber` de los atributos especifica el número de grupos que se van a mostrar. Si esta propiedad se establece con el valor predeterminado, 0, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] determina el número de grupos mediante el muestreo o la lectura de los datos (según la configuración de `DiscretizationMethod`).  
  
 El criterio de ordenación de los miembros de los grupos de miembros se controla mediante el `OrderBy` propiedad del atributo. Según este criterio de ordenación, los miembros de un grupo de miembros se ordenan consecutivamente.  
  
 El uso normal de los grupos de miembros consiste en obtener detalles de un nivel con pocos miembros en otro con muchos miembros. Para permitir al usuario obtener detalles de un nivel en otro, cambie la propiedad `DiscretizationMethod` del atributo en el nivel que contiene muchos miembros de `None` a uno de los métodos de discretización que se describen en la tabla anterior. Por ejemplo, una dimensión Client contiene una jerarquía de atributo Client Name con 500.000 miembros. Puede cambiar el nombre de atributo Client Groups y establecer el `DiscretizationMethod` propiedad `Automatic` para mostrar los grupos de miembros en el nivel de miembro de jerarquía de atributo.  
  
 Para obtener detalles de clientes concretos de cada grupo, puede crear otra jerarquía de atributos Client Name enlazada a la misma columna de la tabla. A continuación, cree una nueva jerarquía de usuario basada en los dos atributos. El nivel superior se basa en el atributo Client Groups y el nivel inferior se basa en el atributo Client Name. El valor de la propiedad `IsAggregatable` es `True` en ambos atributos. El usuario puede expandir el nivel (All) de la jerarquía para ver los miembros del grupo y expandirlos para ver los miembros hoja de la jerarquía. Para ocultar un nivel de grupo o cliente, puede establecer la propiedad `AttributeHierarchyVisible` en `False` en el atributo correspondiente.  
  
## <a name="naming-template"></a>Plantilla de asignación de nombres  
 Los nombres de los grupos de miembro se generan automáticamente al crear grupos de miembro. A menos que especifique una plantilla de asignación de nombres, se utilizará la plantilla de asignación de nombres predeterminada. Para cambiar el método de asignación de nombres, especifique una plantilla de asignación de nombres en la opción `Format` para la propiedad `NameColumn` de un atributo. Pueden volver a definirse distintas plantillas de asignación de nombres para cada idioma especificado en la colección `Translations` del enlace de columna que se utiliza para la propiedad `NameColumn` del atributo.  
  
 La configuración `Format` utiliza la siguiente expresión de cadenas para definir la plantilla de asignación de nombres:  
  
 `<Naming template> ::= <First definition> [;<Intermediate definition>;<Last definition>]`  
  
 `<First definition> ::= <Name expression>`  
  
 `<Intermediate defintion> ::= <Name expression>`  
  
 `<Last definition> ::= <Name expression>`  
  
 El parámetro `<First definition>` solamente se aplica en el primer o único grupo de miembro generado por el método de discretización. Si no se proporcionan los parámetros opcionales `<Intermediate definition>` y `<Last definition>` , se utiliza el parámetro `<First definition>` para todos los grupos de medida generados para dicho atributo.  
  
 El parámetro `<Last definition>` solamente se aplica en el último grupo de miembro generado con el método de discretización.  
  
 El parámetro `<Intermediate bucket name>` se aplica a cada grupo de miembro distinto del primer o último grupo de miembro generado con el método de discretización. Si se generan dos o menos grupos de miembro, se omite este parámetro.  
  
 El parámetro `<Bucket name>` es una expresión de cadenas que puede incorporar un conjunto de variables para representar la información del miembro o grupo de miembro como parte del nombre del grupo de miembro:  
  
|Variable|Descripción|  
|--------------|-----------------|  
|%{First bucket member}|Nombre del primer miembro que se incluirá en el grupo de miembro actual.|  
|%{Last bucket member}|Nombre del último miembro que se incluirá en el grupo de miembro actual.|  
|%{Previous bucket last member}|Nombre del último miembro que se asignará al grupo de miembro anterior.|  
|%{Next bucket first member}|Nombre del primer miembro que se asignará al siguiente grupo de miembro.|  
|%{Bucket Min}|Valor mínimo de los miembros que se asignará al grupo de miembro actual.|  
|%{Bucket Max}|Valor máximo de los miembros que se asignará al grupo de miembro actual.|  
|%{Previous Bucket Max}|Valor máximo de los miembros que se asignará al grupo de miembro anterior.|  
|%{Next Bucket Min}|Valor mínimo de los miembros que se asignará al siguiente grupo de miembro.|  
  
 La plantilla de asignación de nombres predeterminada es `"%{First bucket member} - %{Last bucket member}"`y ofrece compatibilidad con versiones anteriores de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
> [!NOTE]  
>  Para incluir un punto y coma (;) como carácter literal en la plantilla de asignación de nombres, debe anteponer el carácter de símbolo de porcentaje (%).  
  
### <a name="example"></a>Ejemplo  
 La siguiente expresión de cadenas puede usarse para clasificar el atributo Yearly Income de la dimensión Customer de la base de datos de ejemplo [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , donde el atributo Yearly Income usa la agrupación de miembros:  
  
 "Less than %{Next Bucket Min};Between %{First bucket member} and %{Last bucket member};Greater than %{Previous Bucket Max}"  
  
## <a name="adding-new-members-to-existing-member-groups"></a>Agregar nuevos miembros a grupos de miembro existentes  
 Si se agregan nuevos miembros a la dimensión, se asignan a los grupos de miembro adecuados mediante la comparación del valor del miembro con el diseño del grupo de miembro actual.  
  
 Si se inserta un miembro entre el último miembro del grupo de miembro anterior y el primer miembro del siguiente grupo de miembro, el nuevo miembro se convertirá en el último miembro del anterior grupo de miembro.  
  
## <a name="updating-a-dimension-with-discretized-attributes"></a>Actualizar una dimensión con atributos de datos discretos  
 Al procesar una dimensión, un atributo de datos discretos se rediscretiza solamente con una actualización completa (ProcessFull). Para rediscretizar un atributo, debe realizar una actualización completa de la dimensión. Si la tabla de dimensiones de un atributo de datos discretos se actualiza y si se procesa la dimensión con una actualización incremental (ProcessAdd), el atributo de datos discretos no se rediscretiza. Los nombres y los elementos secundarios de los nuevos depósitos siguen siendo los mismos. Para más información sobre el procesamiento de dimensiones, vea [Procesar objetos de Analysis Services](processing-analysis-services-objects.md).  
  
## <a name="usage-limitations"></a>Limitaciones de uso  
  
-   No pueden crearse grupos de miembros en el nivel más alto o más bajo de una jerarquía. No obstante, si es necesario, puede agregar un nivel para que el nivel en donde desea crear grupos de miembros deje de ser el más alto o el más bajo. Puede ocultar el nivel agregado si establece su propiedad `Visible` en `False`.  
  
-   No se pueden crear grupos de miembro en dos niveles consecutivos de una jerarquía.  
  
-   No se admiten grupos de miembros en las dimensiones que utilizan el modo de almacenamiento ROLAP.  
  
-   Si se actualiza la tabla de dimensión de una dimensión que contiene grupos de miembro y la dimensión se procesa después, se genera un nuevo grupo de miembro. Los nombres y elementos secundarios de los nuevos grupos de miembro pueden ser diferentes de los grupos de miembro anteriores.  
  
## <a name="see-also"></a>Vea también  
 [Atributos y jerarquías de atributos](../multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)  
  
  
