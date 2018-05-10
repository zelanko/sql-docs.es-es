---
title: Relaciones | Documentos de Microsoft
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tabular-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: bb047cdd332861f6cfbff16dda6a536544369c1c
ms.sourcegitcommit: 1aedef909f91dc88dc741748f36eabce3a04b2b1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/08/2018
---
# <a name="relationships"></a>Relaciones 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  En los modelos tabulares, una relación es una conexión entre dos tablas de datos. La relación establece cómo se deben relacionar los datos de las dos tablas. Por ejemplo, una tabla de clientes y una tabla de pedidos se pueden relacionar para mostrar el nombre del cliente que está asociado a cada pedido.  
  
 Cuando use el Asistente para la importación de tablas para importar desde el mismo origen de datos, las relaciones que ya existan en las tablas (en el origen de datos) que elija importar se volverán a crear en el modelo. Si desea ver las relaciones detectadas que se han vuelto a crear automáticamente, use la vista de diagrama del diseñador de modelos o el cuadro de diálogo Administrar relaciones. También puede crear manualmente nuevas relaciones entre las tablas usando la vista de diagrama del diseñador de modelos o mediante los cuadros de diálogo Crear relación o Administrar relaciones.  
  
 Después de definir las relaciones entre las tablas (automáticamente durante la importación o creándolas manualmente), es posible filtrar los datos usando las columnas relacionadas y buscar valores en las tablas relacionadas.  
  
> [!TIP]  
>  Si el modelo contiene varias relaciones, la vista de diagrama le permitirá visualizar y crear relaciones entre las tablas con más claridad.  
  
  
##  <a name="what"></a> Ventajas  
 Una relación es una conexión entre dos tablas de datos, basada en una o más columnas de cada tabla. Para ver por qué son útiles las relaciones, imagine que realiza el seguimiento de los datos de los pedidos de los clientes de su negocio. Podría realizar el seguimiento de todos los datos en una sola tabla que tiene una estructura como la siguiente:  
  
|CustomerID|Nombre|EMail|DiscountRate|OrderID|OrderDate|Product|Cantidad|  
|----------------|----------|-----------|------------------|-------------|---------------|-------------|--------------|  
|1|Ashton|chris.ashton@contoso.com|.05|256|2010-01-07|Compact Digital|11|  
|1|Ashton|chris.ashton@contoso.com|.05|255|2010-01-03|SLR Camera|15|  
|2|Jaworski|michal.jaworski@contoso.com|.10|254|2010-01-03|Budget Movie-Maker|27|  
  
 Este enfoque puede funcionar, pero implica almacenar muchos datos redundantes, como la dirección de correo electrónico del cliente para cada pedido. El almacenamiento es barato, pero tiene que asegurarse de que actualiza cada fila para ese cliente si la dirección de correo electrónico cambia. Una solución a este problema es dividir los datos en varias tablas y definir relaciones entre esas tablas. Este es el enfoque usado en *bases de datos relacionales* como SQL Server. Por ejemplo, una base de datos importada en un modelo podría representar los datos de los pedidos usando tres tablas relacionadas:  
  
### <a name="customers"></a>Clientes  
  
|[CustomerID]|Nombre|EMail|  
|--------------------|----------|-----------|  
|1|Ashton|chris.ashton@contoso.com|  
|2|Jaworski|michal.jaworski@contoso.com|  
  
### <a name="customerdiscounts"></a>CustomerDiscounts  
  
|[CustomerID]|DiscountRate|  
|--------------------|------------------|  
|1|.05|  
|2|.10|  
  
### <a name="orders"></a>Orders  
  
|[CustomerID]|OrderID|OrderDate|Product|Cantidad|  
|--------------------|-------------|---------------|-------------|--------------|  
|1|256|2010-01-07|Compact Digital|11|  
|1|255|2010-01-03|SLR Camera|15|  
|2|254|2010-01-03|Budget Movie-Maker|27|  
  
 Si importa estas tablas desde la misma base de datos, el Asistente para la importación de tablas puede detectar las relaciones entre las tablas en función de las columnas que están entre [corchetes] y puede reproducirlas en el diseñador de modelos. Para obtener más información, vea [Detección automática e inferencia de las relaciones](#detection) en este tema. Si importa tablas de varios orígenes, puede crear manualmente las relaciones tal y como se describe en [crear una relación entre dos tablas](../../analysis-services/tabular-models/create-a-relationship-between-two-tables-ssas-tabular.md).  
  
### <a name="columns-and-keys"></a>Claves y columnas  
 Las relaciones se basan en las columnas de cada tabla que contienen los mismos datos. Por ejemplo, las tablas Customer y Orders se pueden estar relacionadas entre sí porque ambas contienen una columna que almacena un identificador de cliente. En el ejemplo, los nombres de columna son los mismos, pero no es obligatorio. Uno podría ser CustomerID y otro CustomerNumber, siempre que todas las filas de la tabla Orders contengan un identificador que también esté almacenado en la tabla Customers.  
  
 En una base de datos relacional, hay varios tipos de *claves*, que normalmente son solo columnas con propiedades especiales. Los cuatro tipos siguientes de claves se pueden usar en bases de datos relacionales:  
  
-   *Clave principal*: identifica de forma única una fila en una tabla, como CustomerID en la tabla Customers.  
  
-   *Clave alternativa* (o *clave candidata*): columna distinta de la clave principal que es única. Por ejemplo, una tabla Employees podría almacenar un identificador de empleado y un número de la seguridad social, ambos números únicos.  
  
-   *Clave externa*: columna que hace referencia a una columna única de otra tabla, como CustomerID en la tabla Orders, que hace referencia a CustomerID en la tabla Customers.  
  
-   *Clave compuesta*: una clave compuesta de más de una columna. Las claves compuestas no se admiten en los modelos tabulares. Para obtener más información, vea "Claves compuestas y columnas de búsqueda" en este tema.  
  
 En los modelos tabulares, la clave principal o la clave alternativa se conocen como la *columna de búsqueda relacionada*, o simplemente *columna de búsqueda*. Si una tabla tiene una clave principal y una clave alternativa, puede usar cualquiera de ellas como columna de búsqueda. La clave externa se conoce como la *columna de origen* o simplemente *columna*. En nuestro ejemplo, una relación se definiría entre CustomerID en la tabla Orders (la columna) y CustomerID (la columna de búsqueda) en la tabla Customers. Si importa los datos desde una base de datos relacional, de forma predeterminada el diseñador de modelos elige la clave externa de una tabla y la clave principal correspondiente de la otra. Sin embargo, puede utilizar cualquier columna que tenga valores únicos para la columna de búsqueda.  
  
### <a name="types-of-relationships"></a>Tipos de relaciones  
 La relación entre Customers y Orders es una *relación de uno a varios*. Cada cliente puede tener varios pedidos, pero un pedido no puede tener varios clientes. Los otros tipos de relaciones son de *uno a uno* y *varios a varios*. La tabla CustomerDiscounts, que define una tarifa reducida única para cada cliente, tiene una relación de uno a uno con la tabla Customers. Un ejemplo de relación de varios a varios es una relación directa entre Products y Customers, en la que un cliente puede comprar varios productos y el mismo producto puede ser comprado por varios clientes. El diseñador de modelos no admite relaciones de varios a varios en la interfaz de usuario. Para obtener más información, vea "[Relaciones varios a varios](#bkmk_many_to_many)" en este tema.  
  
 En la siguiente tabla se muestran las relaciones entre las tres tablas:  
  
|Relación|Tipo|columna de búsqueda|columna|  
|------------------|----------|-------------------|------------|  
|Customers-CustomerDiscounts|uno a uno|Customers.CustomerID|CustomerDiscounts.CustomerID|  
|Customers-Orders|uno a varios|Customers.CustomerID|Orders.CustomerID|  
  
### <a name="relationships-and-performance"></a>Relaciones y rendimiento  
 Una vez creada una relación, el diseñador de modelos normalmente debe recalcular las fórmulas en que se usen columnas de las tablas de la relación recién creada. El proceso puede tardar algún tiempo, en función de la cantidad de datos y la complejidad de las relaciones.  
  
##  <a name="requirements"></a> Requirements for relationships  
 El diseñador de modelos tiene varios requisitos que se deben seguir al crear relaciones:  
  
### <a name="single-active-relationship-between-tables"></a>Relación única activa entre tablas  
 Varias relaciones podrían producir dependencias ambiguas entre las tablas. Para crear cálculos precisos, se necesita una única ruta de una tabla a la tabla siguiente. Por lo tanto, puede haber solo una relación activa entre cada par de tablas. Por ejemplo, en AdventureWorks DW 2012, la tabla DimDate contiene una columna DateKey que está relacionada con tres columnas diferentes de la tabla FactInternetSales: OrderDate, DueDate y ShipDate. Si intenta importar estas tablas, la primera relación se creará correctamente, pero recibirá el error siguiente en las relaciones sucesivas en las que participe la misma columna:  
  
 \* Relación: tabla [columna 1] -> tabla [columna 2] - estado: error - motivo: no se puede crear una relación entre tablas \<tabla 1 > y \<tabla 2 >. Entre dos tablas solo puede existir una relación directa o indirecta.  
  
 Si tiene dos tablas y varias relaciones entre ellas, entonces deberá importar varias copias de la tabla que contenga la columna de búsqueda y crear una relación entre cada par de tablas.  
  
 Puede haber varias relaciones inactivas entre las tablas. La ruta de acceso que se va a usar entre las tablas se especifica mediante el cliente de informes en el momento de la consulta.  
  
### <a name="one-relationship-for-each-source-column"></a>Una relación para cada columna de origen  
 Una columna de origen no puede participar en varias relaciones. Si ya ha usado una columna como columna de origen en una relación, pero desea usar esa columna para conectar con otra columna de búsqueda relacionada en una tabla diferente, puede crear una copia de la columna y emplearla para la nueva relación.  
  
 Es fácil crear una copia de una columna que tiene los mismos valores exactos usando una fórmula de DAX en una columna calculada. Para obtener más información, consulte [crear una columna calculada](../../analysis-services/tabular-models/ssas-calculated-columns-create-a-calculated-column.md).  
  
### <a name="unique-identifier-for-each-table"></a>Identificador único para cada tabla  
 Cada tabla debe tener una única columna que identifique de forma única cada fila de esa tabla. A menudo se hace referencia a esta columna como la clave principal.  
  
### <a name="unique-lookup-columns"></a>Columnas de búsqueda única  
 Los valores de datos de la columna de búsqueda deben ser únicos. En otras palabras, la columna no puede contener duplicados. En los modelos tabulares, las cadenas NULL y vacías equivalen a un valor en blanco, que es un valor de datos distinto. Esto significa que no puede tener varios valores nulos en la columna de búsqueda.  
  
### <a name="compatible-data-types"></a>Tipos de datos compatibles  
 Los tipos de datos de la columna de origen y de la columna de búsqueda deben ser compatibles. Para obtener más información acerca de los tipos de datos, vea [tipos de datos compatibles](../../analysis-services/tabular-models/data-types-supported-ssas-tabular.md).  
  
### <a name="composite-keys-and-lookup-columns"></a>Claves compuestas y columnas de búsqueda  
 Las claves compuestas no se pueden usar en un modelo tabular; siempre debe tener una columna que identifique de forma única cada fila de la tabla. Si intenta importar tablas que tienen una relación existente basada en una clave compuesta, el Asistente para la importación de tablas omitirá esa relación porque no se puede crear en el modelo tabular.  
  
 Si desea crear una relación entre dos tablas en el diseñador de modelos, y hay varias columnas que definen las claves principales y las claves externas, debe combinar los valores para crear una columna de clave única antes de crear la relación. Puede hacerlo antes de importar los datos, o hacerlo en el diseñador de modelos creando una columna calculada.  
  
###  <a name="bkmk_many_to_many"></a> Many-to-Many relationships  
 Los modelos tabulares no admiten las relaciones de varios a varios, y no se pueden agregar *tablas de unión* en el diseñador de modelos. Sin embargo, puede usar funciones de DAX para modelar las relaciones de varios a varios.  
  
 También puede intentar configurar un filtro cruzado bidireccional para ver si logra el mismo propósito. A veces se puede satisfacer el requisito de relación de varios a varios mediante filtros cruzados que perduran un contexto de filtro entre varias relaciones de tabla. Vea [Filtros cruzados bidireccionales para modelos tabulares en SQL Server 2016 Analysis Services](../../analysis-services/tabular-models/bi-directional-cross-filters-tabular-models-analysis-services.md) para obtener más información.  
  
### <a name="self-joins-and-loops"></a>Autocombinaciones y bucles  
 Las autocombinaciones no se permiten en las tablas de modelos tabulares. Una autocombinación es una relación recursiva entre una tabla y ella misma. Las autocombinaciones se utilizan a menudo para definir las jerarquías de elementos primarios y secundarios. Por ejemplo, podría unir una tabla de empleados a sí misma para generar una jerarquía que muestre la cadena de dirección en un negocio.  
  
 El diseñador de modelos no permite crear bucles entre las relaciones de un modelo. En otras palabras, se prohíbe el conjunto siguiente de relaciones.  
  
 Tabla 1, columna a a Tabla 2, columna f  
  
 Tabla 2, columna f a Tabla 3, columna n  
  
 Tabla 3, columna n a Tabla 1, columna a  
  
 Si intenta crear una relación que crearía un bucle, se generará un error.  
  
##  <a name="detection"></a> Inference of relationships  
 En algunos casos, las relaciones entre las tablas se encadenan automáticamente. Por ejemplo, si crea una relación entre los dos primeros conjuntos de tablas del ejemplo siguiente, se deduce que existe una relación entre las otras dos tablas y se establece una relación automáticamente.  
  
 Productos y categorías: creadas manualmente  
  
 Categoría y subcategoría: creadas manualmente  
  
 Productos y subcategoría: se deduce la relación  
  
 Para que las relaciones se encadenen automáticamente, las relaciones deben ir en una dirección, como se mostró antes. Si las relaciones iniciales fueran entre, por ejemplo, ventas y productos, y ventas y clientes, no se deduciría una relación. Esto se debe a que la relación entre los productos y los clientes es una relación de varios a varios.  
  
##  <a name="bkmk_detection"></a> Detection of relationships when importing data  
 Al importar de una tabla relacional de origen de datos, el Asistente para la importación de tablas detecta las relaciones existentes en las tablas de origen según los datos del esquema de origen. Si se importan las tablas relacionadas, esas relaciones se duplicarán en el modelo.  
  
##  <a name="bkmk_manually_create"></a> Manually create relationships  
 Aunque la mayoría de las relaciones entre las tablas de un único origen de datos relacional se detectarán automáticamente y se crearán en el modelo tabular, hay también muchos casos en los que debe crear manualmente las relaciones entre las tablas del modelo.  
  
 Si su modelo contiene datos de varios orígenes, probablemente tendrá que crear las relaciones manualmente. Por ejemplo, puede importar las tablas Customers, CustomerDiscounts, y Orders de un origen de datos relacional. Las relaciones que existen entre esas tablas en el origen se crean automáticamente en el modelo. A continuación, puede agregar otra tabla de un origen diferente, por ejemplo, importar datos de la región de una tabla geográfica en un libro de Microsoft Excel. Después, puede crear manualmente una relación entre una columna de la tabla Clientes y una columna de la tabla Geografía.  
  
 Para crear manualmente las relaciones en un modelo tabular, puede usar la vista de diagrama del diseñador de modelos o el cuadro de diálogo Administrar relaciones. La vista de diagrama muestra las tablas, con las relaciones entre ellas, en un formato gráfico. Puede hacer clic en una columna de una tabla y arrastrar el cursor a otra tabla para crear fácilmente una relación, en el orden correcto, entre las tablas. El cuadro de diálogo Administrar relaciones muestra las relaciones entre las tablas en un formato de tabla simple. Para obtener información sobre cómo crear manualmente las relaciones, vea [crear una relación entre dos tablas](../../analysis-services/tabular-models/create-a-relationship-between-two-tables-ssas-tabular.md).  
  
##  <a name="bkmk_dupl_errors"></a> Duplicate values and other errors  
 Si elige una columna que no se puede usar en la relación, aparece una X roja al lado de la columna. Puede pausar el cursor sobre el icono de error para ver un mensaje con más información sobre el problema. Entre los problemas que pueden impedir crear una relación entre las columnas seleccionadas están:  
  
|Problema o mensaje|Solución|  
|------------------------|----------------|  
|No se puede crear la relación porque las dos columnas seleccionadas contienen valores duplicados.|Para crear una relación válida, al menos una de las columnas del par seleccionado debe contener solo valores únicos.<br /><br /> Puede modificar las columnas para quitar los valores duplicados o revertir el orden de las columnas de manera que la columna que contiene valores únicos se use como **columna de búsqueda relacionada**.|  
|La columna contiene un valor nulo o vacío.|Las columnas de datos no se pueden unir entre sí por un valor nulo. Para cada fila, debe haber un valor en las dos columnas que se usan en una relación.|  
  
##  <a name="bkmk_related_tasks"></a> Related tasks  
  
|Tema|Description|  
|-----------|-----------------|  
|[Crear una relación entre dos tablas](../../analysis-services/tabular-models/create-a-relationship-between-two-tables-ssas-tabular.md)|Describe cómo crear manualmente una relación entre dos tablas.|  
|[Eliminar relaciones](../../analysis-services/tabular-models/delete-relationships-ssas-tabular.md)|Describe cómo eliminar una relación y las consecuencias de la eliminación de relaciones.|  
|[Filtros cruzados bidireccionales para modelos tabulares en SQL Server 2016 Analysis Services](../../analysis-services/tabular-models/bi-directional-cross-filters-tabular-models-analysis-services.md)|Describe el filtrado cruzado bidireccional para tablas relacionadas. Un contexto de filtro de una relación de tabla se puede utilizar al consultar a través de una segunda relación de tabla si las tablas están relacionadas y se definen filtros cruzados bidireccionales.|  
  
## <a name="see-also"></a>Vea también  
 [Tablas y columnas](../../analysis-services/tabular-models/tables-and-columns-ssas-tabular.md)   
 [Importar datos](http://msdn.microsoft.com/library/6617b2a2-9f69-433e-89e0-4c5dc92982cf)  
  
  
