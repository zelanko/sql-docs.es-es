---
title: EntityType, elemento (CSDLBI) | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: 372e2c13-ec38-4bb1-981c-50758d59a1da
caps.latest.revision: 16
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: bf36253ccc373fb260538fdbc3d78764ce5548f9
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="entitytype-element-csdlbi"></a>EntityType, elemento (CSDLBI)
  El elemento **EntityType** es un tipo complejo que representa la estructura de una entidad de nivel superior, como un cliente o un pedido, en un modelo de datos. El elemento **bi:EntityType** extiende la definición del [EntityType](http://msdn.microsoft.com/library/bb399206.aspx) utilizado en [Entity Data Framework](http://msdn.microsoft.com/library/bb399567.aspx).  
  
 Se debe especificar un elemento EntityType para cada una de las entidades incluidas en el modelo de datos. Los subelementos de EntityType describen las columnas y medidas de la tabla. Las relaciones entre las tablas se incluyen en el elemento **EntityContainer**.  
  
## <a name="elements-and-attributes"></a>Atributos y elementos  
 En la tabla siguiente se enumeran los elementos y atributos que definen el elemento **EntityType** . Vea también los atributos aplicables al elemento [EntityType](http://msdn.microsoft.com/library/bb399206.aspx) .  
  
|Nombre|Es obligatorio|Descripción|  
|----------|-----------------|-----------------|  
|Contenido|No|Cadena que contiene los posibles tipos de datos de una columna. El valor se deriva del valor de DimensionAttributeTypeEnumType en el modelo de datos.<br /><br /> Si el valor de DimensionAttributeTypeEnumType es “ExtendedType”, el valor de Contents se deriva del elemento ExtendedType de DimensionAttribute. No es necesario que el cliente responda a estos valores.|  
|DefaultDetails|No|Lista de referencias de propiedad que representan el conjunto de columnas de la tabla.<br /><br /> Vea [DefaultDetails, elemento &#40; CSDLBI &#41; ](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/defaultdetails-element-csdlbi.md).|  
|DefaultImage|No|Referencia a una columna que contiene la imagen que ilustra la entidad.<br /><br /> En los modelos multidimensionales, este elemento corresponde a un atributo binario en el atributo de dimensión. Si este atributo está presente, el elemento debe contener exactamente un elemento MemberRef.<br /><br /> Vea [MemberRef, elemento &#40; CSDLBI &#41; ](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/memberref-element-csdlbi.md).|  
|DefaultMeasure|No|Referencia a una medida de la entidad que se debe utilizar como valor predeterminado al realizar cálculos en dicha entidad. Si no se especifica, el valor predeterminado es SUM.<br /><br /> Vea [MemberRef, elemento &#40; CSDLBI &#41; ](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/memberref-element-csdlbi.md).|  
|DisplayKey|No|Lista de referencias a columnas o a extremos de rol que constituye un identificador seguro que identifica de forma exclusiva una instancia de entidad.<br /><br /> Vea [DisplayKey, elemento &#40; CSDLBI &#41; ](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/displaykey-element-csdlbi.md).|  
|Jerarquía|No|Lista de jerarquías del modelo.<br /><br /> Vea [Hierarchy, elemento &#40; CSDLBI &#41; ](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/hierarchy-element-csdlbi.md).|  
|ReferenceName|Sí|Identificador que se puede utilizar para hacer referencia a esta entidad en una consulta de expresiones de análisis de datos (DAX).<br /><br /> Si este atributo no está presente, se utiliza el nombre de campo completo de la entidad.|  
|SortMembers|No|Lista de propiedades según las que se ordena. El atributo SortDirection indica si el orden es ascendente o descendente.|  
  
## <a name="contents-element"></a>Elemento Contents  
 El elemento **Contents** es un tipo simple que describe el tipo de datos de la entidad.  
  
 El contenido de la entidad (columna) pueden ser cualquiera de los valores siguientes:  
  
|Valor|Description|  
|-----------|-----------------|  
|Regular|No se define de otro modo.|  
|Time|Los atributos representan periodos de tiempo, como años, semestres, trimestres, meses o días.|  
|Geografía|Los atributos representan información geográfica, como ciudades o códigos postales.|  
|Organización|Los atributos representan información organizativa, como empleados o subsidiarias.|  
|Lista de materiales|Los atributos representan información de inventario o de fabricación, como listas de piezas para productos.|  
|Cuentas|Los atributos representan un gráfico de cuentas para informes financieros.|  
|Clientes|Los atributos representan información de clientes o de contacto.|  
|Productos|Los atributos representan información de productos.|  
|Escenario|Los atributos representan información de planeación o análisis estratégico.|  
|Cuantitativa|Los atributos representan información cuantitativa.|  
|Utilidad|Los atributos representan información diversa.|  
|Moneda|Contiene datos y metadatos de moneda.|  
|Tarifas|Los atributos representan información de tasa de cambio.|  
|Canal|Los atributos representan información de canal.|  
|Promoción|Los atributos representan información de promociones de marketing.|  
  
## <a name="example"></a>Ejemplo  
 **Tabular**  
  
 En el ejemplo siguiente se muestra parte de la representación de la versión 1.1 de CSDLBI de la tabla Geography utilizada en el modelo tabular AdventureWorks. La columna RowNumber es una columna oculta generada automáticamente como identificador de fila en los modelos tabulares, por lo que tiene el atributo Contents, **RowNumber**.  
  
```  
  
<EntityType   
     Name="DimGeography">  
     <Key>  
        <PropertyRef Name="RowNumber" />  
     </Key>  
     <Property   
        Name="RowNumber"   
        Type="Int64" Nullable="false">  
     <bi:Property   
        Hidden="true"   
        Contents="RowNumber"   
        Stability="RowNumber" />  
     </Property>  
....  
  
```  
  
## <a name="example"></a>Ejemplo  
 **Multidimensional**  
  
 En el ejemplo siguiente se muestran los elementos EntityType de la versión 1.1 de CSDLBI que representan una parte de una dimensión de tiempo del cubo de operaciones de Contoso.  
  
```  
<EntityType   
       Name="CalendarQuarter">  
    <Key>  
       <PropertyRef Name="RowNumber" />  
    </Key>  
  
    <Property Name="RowNumber"   
       Type="Int64"   
       Nullable="false">  
    <bi:Property   
       Hidden="true"   
       Contents="RowNumber"   
       Stability="RowNumber"   
    />  
    </Property>  
  
    <Property Name="CalendarQuarter2"   
       Type="String"   
       MaxLength="Max"   
       Unicode="true"   
       FixedLength="false"   
       Nullable="false">  
    <bi:Property   
       Caption="CalendarQuarter"   
       ReferenceName="CalendarQuarter"   
    />  
    </Property>  
   <bi:EntityType />  
</EntityType>  
```  
  
## <a name="see-also"></a>Vea también  
 [Referencia técnica de anotaciones de BI para CSDL](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/technical-reference-for-bi-annotations-to-csdl.md)  
  
  

