---
title: "Atributos CSDLBI para el diseño de informes | Documentos de Microsoft"
ms.custom: 
ms.date: 03/04/2017
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
ms.assetid: 61ba3a27-790e-43bc-b421-e01bf2fdbda6
caps.latest.revision: "9"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 4b2c46d037112cb79502e8d0ce56a5c9c319ec09
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="csdlbi-attributes-for-report-design"></a>Atributos CSDLBI para el diseño de informes
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]En esta sección se describe los atributos de las extensiones de CSDL para la creación de modelos tabulares que afectan a [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] diseño de consultas.  
  
## <a name="model-attributes"></a>Model Attributes  
 Estos atributos se definen en un subelemento de un elemento [EntityContainer](http://msdn.microsoft.com/library/bb399169.aspx) de CSDL.  
  
|Nombre del atributo|Tipo de datos|Description|  
|--------------------|---------------|-----------------|  
|Culture|Texto|Indica la referencia cultural usada para los formatos de moneda. Si se omite, se usa EN-US.|  
|IsRightToLeft|Boolean|Indica si los valores de los campos de texto se deben leer derecha a izquierda de forma predeterminada.|  
  
## <a name="entity-attributes"></a>Atributos de la entidad  
 Estos atributos se definen en un subelemento de un elemento EntitySet o EntityType de CSDL.  
  
|Nombre del atributo|Tipo de datos|Description|  
|--------------------|---------------|-----------------|  
|**ReferenceName**|Texto|El identificador usado para hacer referencia a esta entidad en una consulta de DAX. Si se omite, se usa el nombre.|  
|**Caption**|Texto|El nombre para mostrar de la entidad.|  
|**Documentación**|Texto|Texto descriptivo que se usa para ayudar a los usuarios empresariales a entender el significado de los datos.|  
|**Oculto**|Boolean|Indica si se debe mostrar la entidad. El valor predeterminado es **false**.|  
|**CollectionCaption**|Texto|Nombre plural para hacer referencia a un conjunto de instancias de la entidad. Si se omite, se usa el atributo Caption.|  
|**DisplayKey**|MemberRef[]|Lista ordenada de campos que se usa para identificar una instancia de la entidad para un usuario empresarial. Las referencias pueden incluir propiedades de instancia y de navegación. Cuando se hace referencia a una propiedad de navegación, se muestra el atributo **DisplayKey** de la entidad de destino. Si se omite el valor del atributo **DisplayKey** , se usa el campo Key.|  
|**Elemento DefaultImage**|MemberRef|Referencia al campo que contiene una imagen usada para identificar visualmente una instancia de la entidad a un usuario empresarial. Si se omite, se usa el primer campo de imagen en la entidad, si existe alguno.|  
|**DefaultDetails**|MemberRef[]|Lista ordenada de campos que representan el conjunto predeterminado de información detallada que se muestra a un usuario empresarial sobre una instancia de la entidad. Si se omite, se usan los cinco (5) primeros campos de la entidad, exceptuando aquellos a los que ya se ha hecho referencia mediante **Key**, **DisplayKey**o **DefaultImage**.|  
|**SortProperties**|MemberRef[]|Lista ordenada de campos por los cuales se suele ordenar la instancia de la entidad. Al ordenar según estos campos, se usa el atributo **SortDirection** especificado en cada campo. Si se omite, se usan los campos **DisplayKey** .|  
|**DefaultMeasure**|MemberRef|Referencia a una medida definida en el modelo, o a un campo numérico con una función de agregado predeterminada, para indicar que la medida o el campo se debe usar como la representación predeterminada para varias instancias de la entidad. Si se omite, se usa un recuento de las instancias de la entidad.|  
|**DefaultLocation**|MemberRef|Referencia a un campo cuyo valor representa la ubicación predeterminada asociada a una instancia de la entidad. Si se omite, se usa el primer campo de ubicación de la entidad, si existe alguno.|  
  
## <a name="field-attributes"></a>Atributos de los campos  
 Estos atributos se definen en un subelemento de un elemento Property de CSDL o en un elemento [NavigationProperty](http://msdn.microsoft.com/library/bb387104.aspx) .  
  
|Nombre del atributo|Tipo de datos|Description|  
|--------------------|---------------|-----------------|  
|**ReferenceName**|Texto|El identificador usado para hacer referencia a esta entidad en una consulta de DAX. Si se omite, se usa el nombre del campo.|  
|**Caption**|Texto|El nombre para mostrar de la entidad. Si se omite, se usa el campo **ReferenceName** .|  
|**Documentación**|Texto|Texto descriptivo que se usa para ayudar a los usuarios empresariales a entender el significado del campo.|  
|**Oculto**|Boolean|Indica si se debe mostrar el campo. El valor predeterminado es **false**, es decir, aparece el nombre del campo.|  
|**DisplayFolder**|Texto|El nombre (ruta de acceso completa) de la carpeta en la cual se muestra este campo. Si se omite, el campo se muestra en la raíz del modelo.|  
|**ContextualNameRule**|Enum|Valor que indica si se debe modificar el nombre de la propiedad basándose en el contexto en el que se usa, y cómo debe hacerse. Los valores posibles son:  **None**,  **Role**o  **Merge**.|  
|**Alignment**|Enum|Valor que indica cómo los valores del campo se deben alinear en una presentación tabular. Los valores posibles son: **Default**, **Center**, **Left**o **Right**. Si se omite, se determina la alineación basándose en el tipo de datos del campo de forma predeterminada.|  
|**FormatString**|Texto|Cadena de formato de .NET Framework que indica cómo se debe dar formato al valor del campo de forma predeterminada. Si se omite, se supone que se usa el formato siguiente:<br /><br /> Campos - fecha y hora: fecha corta regional o "d"<br /><br /> -Función de agregado campos punto flotante y campos enteros con un valor predeterminado: número regional o "n"<br /><br /> -Función de agregado de enteros no tiene ningún valor predeterminado: número decimal regional o "d"<br /><br /> Para todos los demás tipos de campos, no se aplica ninguna cadena de formato.|  
|**Unidades**|Texto|Símbolo que se aplica a los valores de los campos para expresar unidades. Si se omite, se supone que las unidades son desconocidas.|  
|**Width**|Integer|Anchura preferida en caracteres que debe reservar para mostrar los valores del campo en una presentación tabular. Si se omite, la anchura predeterminada se basa en el tipo de datos del campo.|  
|**SortDirection**|Enum|Valor que indica cómo se suelen ordenar los valores de los campos. Los valores posibles son: **Default**, **Ascending**o **Descending**. Si se omite, el valor predeterminado asigna una dirección de ordenación basándose en el tipo de datos del campo.|  
|**IsRightToLeft**|Boolean|Indica si el campo contiene texto que se debe leer de derecha a izquierda. Si se omite, se supone que se debe usar la configuración del modelo.|  
|**OrderBy**|MemberRef|Referencia a otro campo dentro del modelo que define la ordenación de los valores de este campo. Los valores de los dos campos deben tener una asignación 1:1, o la ordenación quedará indefinida. Si se omite, el campo se ordena basándose en su propio valor.|  
|**Contenido**|Enum|Enumeración que describe el subtipo o el contenido del campo. Si se omite, se supone que no es de ningún subtipo concreto, a menos que el tipo de datos del campo sea binario, en cuyo caso se supone que los datos son del subtipo Image. Para obtener una lista completa de los tipos de contenido admitidos, vea la documentación de AMO.|  
|**DefaultAggregateFunction**|Enum|Valor que indica la función predeterminada, si la hay, que se usa habitualmente para agregar este campo. Los valores posibles son: **None**, **Sum**, **Average**, **Count**, **Min**y **Max**. Si se omite, se supone que se debe usar **Sum** para los campos numéricos y **None** para todos los demás campos.|  
|**IsSimpleMeasure**|Boolean|Indica si una medida es únicamente un agregado simple de un campo numérico. Tales agregados se pueden definir fácilmente en la consulta según sea necesario y, por lo tanto, se deben omitir de la definición del modelo para mejorar el rendimiento. Si se omite, se supone que se debe usar el valor **false** .|  
|**KPI**<br /><br /> **KpiGoal**<br /><br /> **KpiStatus**|Subelemento|Indica que el elemento de medida debe usarse como un KPI. El subelemento KPI utiliza los elementos KpiGoal y KpiStatus para definir la imagen y los rangos de destino asociados.|  
  
  
