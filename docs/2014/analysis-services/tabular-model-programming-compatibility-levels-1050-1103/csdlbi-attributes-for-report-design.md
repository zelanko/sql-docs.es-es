---
title: Atributos CSDLBI para el diseño de informes | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
ms.assetid: 61ba3a27-790e-43bc-b421-e01bf2fdbda6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: dce0abecb352071a22e74cb820408fe5b8851fc3
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/13/2018
ms.locfileid: "53352532"
---
# <a name="csdlbi-attributes-for-report-design"></a>Atributos CSDLBI para el diseño de informes
  En esta sección se describen los atributos de las extensiones de CSDL para la creación de modelos tabulares que afectan al diseño de consultas de [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] .  
  
## <a name="model-attributes"></a>Model Attributes  
 Estos atributos se definen en un subelemento de un elemento [EntityContainer](https://msdn.microsoft.com/library/bb399169.aspx) de CSDL.  
  
|Nombre del atributo|Tipo de datos|Descripción|  
|--------------------|---------------|-----------------|  
|Culture|Texto|Indica la referencia cultural usada para los formatos de moneda. Si se omite, se usa EN-US.|  
|IsRightToLeft|Boolean|Indica si los valores de los campos de texto se deben leer derecha a izquierda de forma predeterminada.|  
  
## <a name="entity-attributes"></a>Atributos de la entidad  
 Estos atributos se definen en un subelemento de un elemento EntitySet o EntityType de CSDL.  
  
|Nombre del atributo|Tipo de datos|Descripción|  
|--------------------|---------------|-----------------|  
|`ReferenceName`|Texto|El identificador usado para hacer referencia a esta entidad en una consulta de DAX. Si se omite, se usa el nombre.|  
|`Caption`|Texto|El nombre para mostrar de la entidad.|  
|`Documentation`|Texto|Texto descriptivo que se usa para ayudar a los usuarios empresariales a entender el significado de los datos.|  
|`Hidden`|Boolean|Indica si se debe mostrar la entidad. De manera predeterminada, es `false`.|  
|`CollectionCaption`|Texto|Nombre plural para hacer referencia a un conjunto de instancias de la entidad. Si se omite, se usa el atributo Caption.|  
|`DisplayKey`|MemberRef[]|Lista ordenada de campos que se usa para identificar una instancia de la entidad para un usuario empresarial. Las referencias pueden incluir propiedades de instancia y de navegación. Cuando se hace referencia a una propiedad de navegación, se muestra el atributo `DisplayKey` de la entidad de destino. Si se omite el valor del atributo `DisplayKey`, se usa el campo Key.|  
|`DefaultImage`|MemberRef|Referencia al campo que contiene una imagen usada para identificar visualmente una instancia de la entidad a un usuario empresarial. Si se omite, se usa el primer campo de imagen en la entidad, si existe alguno.|  
|`DefaultDetails`|MemberRef[]|Lista ordenada de campos que representan el conjunto predeterminado de información detallada que se muestra a un usuario empresarial sobre una instancia de la entidad. Si se omite, se usan los cinco (5) primeros campos de la entidad, exceptuando aquellos a los que ya se ha hecho referencia mediante `Key`, `DisplayKey` o `DefaultImage`.|  
|`SortProperties`|MemberRef[]|Lista ordenada de campos por los cuales se suele ordenar la instancia de la entidad. Al ordenar según estos campos, se usa el atributo `SortDirection` especificado en cada campo. Si se omite, se usan los campos `DisplayKey`.|  
|`DefaultMeasure`|MemberRef|Referencia a una medida definida en el modelo, o a un campo numérico con una función de agregado predeterminada, para indicar que la medida o el campo se debe usar como la representación predeterminada para varias instancias de la entidad. Si se omite, se usa un recuento de las instancias de la entidad.|  
|`DefaultLocation`|MemberRef|Referencia a un campo cuyo valor representa la ubicación predeterminada asociada a una instancia de la entidad. Si se omite, se usa el primer campo de ubicación de la entidad, si existe alguno.|  
  
## <a name="field-attributes"></a>Atributos de los campos  
 Estos atributos se definen en un subelemento de un elemento Property de CSDL o en un elemento [NavigationProperty](https://msdn.microsoft.com/library/bb387104.aspx) .  
  
|Nombre del atributo|Tipo de datos|Descripción|  
|--------------------|---------------|-----------------|  
|`ReferenceName`|Texto|El identificador usado para hacer referencia a esta entidad en una consulta de DAX. Si se omite, se usa el nombre del campo.|  
|`Caption`|Texto|El nombre para mostrar de la entidad. Si se omite, el campo `ReferenceName` se utiliza.|  
|`Documentation`|Texto|Texto descriptivo que se usa para ayudar a los usuarios empresariales a entender el significado del campo.|  
|`Hidden`|Boolean|Indica si se debe mostrar el campo. El valor predeterminado es `false`, es decir, aparece el nombre del campo.|  
|`DisplayFolder`|Texto|El nombre (ruta de acceso completa) de la carpeta en la cual se muestra este campo. Si se omite, el campo se muestra en la raíz del modelo.|  
|`ContextualNameRule`|Enum|Valor que indica si se debe modificar el nombre de la propiedad basándose en el contexto en el que se usa, y cómo debe hacerse. Los valores posibles son: `None`, `Role` o `Merge`.|  
|`Alignment`|Enum|Valor que indica cómo los valores del campo se deben alinear en una presentación tabular. Los valores posibles son: `Default`, `Center`, `Left` o `Right`. Si se omite, el valor predeterminado determina la alineación basándose en el tipo de datos del campo.|  
|`FormatString`|Texto|Cadena de formato de .NET Framework que indica cómo debe aplicarse el valor del campo de forma predeterminada. Si se omite, se supone que se usa el formato siguiente:<br /><br /> -Los campos Datetime: formato de fecha corta o "d"<br />-Función de agregado campos punto flotante y campos enteros con un valor predeterminado: número regional o "n"<br />: Función de agregado de enteros no tiene ningún valor predeterminado: número decimal regional o "d"<br /><br /> Para todos los demás tipos de campos, no se aplica ninguna cadena de formato.|  
|`Units`|Texto|Símbolo que se aplica a los valores de los campos para expresar unidades. Si se omite, se supone que las unidades son desconocidas.|  
|`Width`|Integer|El ancho preferido de caracteres que se deben reservar para mostrar los valores del campo en una presentación tabular. Si se omite, un ancho predeterminado se basa en el tipo de datos del campo.|  
|`SortDirection`|Enum|Valor que indica cómo se suelen ordenar los valores de los campos. Los valores posibles son: `Default`, `Ascending` o `Descending`. Si se omite, escriba el valor predeterminado se asigna que una dirección de ordenación se basa en los datos del campo.|  
|`IsRightToLeft`|Boolean|Indica si el campo contiene texto que se debe leer de derecha a izquierda. Si se omite, se supone que se debe usar la configuración del modelo.|  
|`OrderBy`|MemberRef|Una referencia a otro campo dentro del modelo que define el criterio de ordenación para los valores de este campo. Los valores de los dos campos deben tener una asignación 1:1, o la ordenación quedará indefinida. Si se omite, el campo se ordena basándose en su propio valor.|  
|`Contents`|Enum|Enumeración que describe el subtipo o el contenido del campo. Si se omite, no determinado subtipo se supone que, a menos que el tipo de datos del campo es binario, en cuyo caso se supone imagen. Para obtener una lista completa de los tipos de contenido admitidos, vea la documentación de AMO.|  
|`DefaultAggregateFunction`|Enum|Valor que indica la función predeterminada, si la hay, que se usa habitualmente para agregar este campo. Los valores posibles son: `None`, `Sum`, `Average`, `Count`, `Min` y `Max`. Si se omite, se supone que se debe usar `Sum` para los campos numéricos y `None` para todos los demás campos.|  
|`IsSimpleMeasure`|Boolean|Indica si una medida es únicamente un agregado simple de un campo numérico. Tales agregados se pueden definir fácilmente en la consulta según sea necesario y, por lo tanto, se deben omitir de la definición del modelo para mejorar el rendimiento. Si se omite, se supone que se debe usar el valor `false`.|  
|`Kpi`<br /><br /> `KpiGoal`<br /><br /> `KpiStatus`|Subelemento|Indica que el elemento de medida debe usarse como un KPI. El subelemento KPI utiliza los elementos KpiGoal y KpiStatus para definir la imagen y los rangos de destino asociados.|  
  
  
