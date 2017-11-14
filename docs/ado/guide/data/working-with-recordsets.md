---
title: Trabajar con conjuntos de registros | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Recordset object [ADO]
ms.assetid: bdf9a56a-de4a-44de-9111-2f11ab7b16ea
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 368e3b3a793bce6b6182ba262493d9a8ed1ac1bd
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="working-with-recordsets"></a>Trabajar con conjuntos de registros
El **Recordset** objeto tiene características integradas que permiten reorganizar el orden de los datos en el conjunto de resultados, para buscar un registro específico en función de criterios que suministre e incluso a optimizar las operaciones de búsqueda con índices. Si estas características están disponibles para su uso depende del proveedor y en algunos casos, como el de la [índice](../../../ado/reference/ado-api/index-property.md) propiedad: la estructura del propio origen de datos.  
  
## <a name="arranging-data"></a>Organizar datos  
 Con frecuencia, la manera más eficaz para ordenar los datos de su **Recordset** consiste en especificar una cláusula ORDER BY en el comando SQL utilizado para devolver los resultados. Sin embargo, tendrá que cambiar el orden de los datos en un **Recordset** que ya se ha creado. Puede usar el **ordenación** propiedad para establecer el orden de las filas de un **Recordset** se recorren. Además, el **filtro** propiedad determina qué filas son accesibles cuando atraviesa filas.  
  
 El **ordenación** propiedad establece o devuelve un **cadena** los nombres de valor que indica el campo de la **Recordset** en el que se va a ordenar. Cada nombre está separado por una coma y, seguido opcionalmente de un espacio y la palabra clave **ASC** (que ordena el campo en orden ascendente) o **DESC** (que ordena el campo en orden descendente). De forma predeterminada, si no se especifica ninguna palabra clave, el campo se ordena en orden ascendente.  
  
 La operación de ordenación es eficaz porque los datos no se reorganizan físicamente, pero se tiene acceso en el orden especificado por un índice.  
  
 El **ordenación** propiedad requiere la [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) propiedad se establezca en **adUseClient**. Se creará un índice temporal para cada campo especificado en el **ordenación** propiedad si todavía no existe un índice.  
  
 Establecer el **ordenación** propiedad en una cadena vacía se restablecerá todas las filas a su orden original y se eliminarán los índices temporales. No se eliminarán los índices existentes.  
  
 Suponga que un **Recordset** contiene tres campos denominados *firstName*, *middleInitial*, y *lastName*. Establecer el **ordenación** propiedad a la cadena "`lastName DESC, firstName ASC`", que ordenará el **Recordset** por apellido en orden descendente y, a continuación, por nombre en orden ascendente. Se omite la inicial del segundo nombre.  
  
 Ningún campo al que hace referencia en una cadena de criterios de ordenación puede denominarse "ASC" o "DESC" porque esos nombres en conflicto con las palabras clave **ASC** y **DESC**. Tener un campo que tiene un alias de un nombre en conflicto mediante la **AS** palabra clave en la consulta que devuelve el **conjunto de registros**.  
  
 Para obtener más información acerca de **Recordset** filtrado, vea "Filtrar resultados de la" más adelante en este tema.  
  
## <a name="finding-a-specific-record"></a>Buscar un registro específico  
 ADO proporciona el [buscar](../../../ado/reference/ado-api/find-method-ado.md) y [Seek](../../../ado/reference/ado-api/seek-method.md) métodos para buscar un registro determinado en un **conjunto de registros**. El **buscar** método es compatible con una variedad de proveedores, pero se limita a un criterio de búsqueda sencillo. El **Seek** método permite la búsqueda con varios criterios, pero no es compatible con muchos proveedores.  
  
 Los índices de campos pueden mejorar mucho el rendimiento de la **buscar** método y **ordenación** y **filtro** propiedades de la **conjunto de registros** objeto. Puede crear un índice interno para un **campo** objeto estableciendo sus dinámicos [optimizar](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md) propiedad. Esta propiedad dinámica se agrega a la **propiedades** colección de la **campo** objeto cuando se establece la [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) propiedad **adUseClient**. Recuerde que este índice es interno a ADO: no se puede obtener acceso a él o utilizarlo para otros fines. Además, este índice es distinto de la [índice](../../../ado/reference/ado-api/index-property.md) propiedad de la **Recordset** objeto.  
  
 El **buscar** método busca rápidamente un valor dentro de una columna (campo) de un **conjunto de registros**. Con frecuencia puede mejorar la velocidad de la **buscar** método en una columna mediante el **optimizar** propiedad que se va a crear un índice en ella.  
  
 El **buscar** método limita la búsqueda al contenido de un campo. El **Seek** método requiere un índice y tiene también otras limitaciones. Si debe buscar en varios campos que no son la base de un índice, o si el proveedor no admite índices, puede limitar los resultados mediante el **filtro** propiedad de la **Recordset** objeto.  
  
### <a name="find"></a>Buscar  
 El **buscar** método busca un **conjunto de registros** para la fila que cumple un criterio especificado. Si lo desea, se puede especificar la dirección de la búsqueda, la fila inicial y el desplazamiento desde la fila inicial. Si se cumple el criterio, la posición de fila actual se establece en el registro encontrado; en caso contrario, se establece la posición al final (o inicio) de la **Recordset**, en función de la dirección de la búsqueda.  
  
 Solo un nombre de columna única puede especificarse para el criterio. En otras palabras, este método no admite búsquedas de varias columnas.  
  
 El operador de comparación del criterio puede ser"**>**"(mayor que),"**\<**" (menor que), "=" (igual), "> =" (mayor o igual que), "< =" (menor o igual que), " <> "(no igual) o"LIKE"(coincidencia de modelos).  
  
 El valor del criterio puede ser una cadena, un número de punto flotante o una fecha. Valores de cadena se delimitan con comillas simples o marcas "#" (signo de número) (por ejemplo, "estado = 'WA'" o "estado = WA #"). Los valores de fecha se delimitan con marcas de "#" (signo de número) (por ejemplo, "fecha_inicial > #7/22/&#97;").  
  
 Si el operador de comparación es "like", el valor de cadena puede contener un asterisco (*) para buscar una o más apariciones de cualquier carácter o una subcadena. Por ejemplo, "state like'm\*'" encuentra Maine y Massachusetts. También puede utilizar asteriscos iniciales y finales para buscar una subcadena que se encuentra dentro de los valores. Por ejemplo, "estado como '\*como\*'" encuentra Alaska, Arkansas y Massachusetts.  
  
 Asteriscos pueden usarse solo al final de una cadena de criterios o juntos al principio y al final de una cadena de criterios, como se muestra anteriormente. No se puede usar el asterisco como carácter comodín inicial ('* str') o incrustar indicado anteriormente\*r'). Esto producirá un error.  
  
### <a name="seek-and-index"></a>Buscar e índice  
 Use la **Seek** método junto con el **índice** propiedad si el proveedor subyacente admite índices en el **Recordset** objeto. Use la [admite](../../../ado/reference/ado-api/supports-method.md)**(adSeek)** método para determinar si el proveedor subyacente admite **Seek**y el **Supports** método para determinar si el proveedor admite índices. (Por ejemplo, el [proveedor OLE DB para Microsoft Jet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-jet.md) admite **Seek** y **índice**.)  
  
 Si **Seek** hace que no se encontró la fila deseada, ningún error se produce y la fila se coloca al final de la **conjunto de registros**. Establecer el **índice** propiedad en el índice deseado antes de ejecutar este método.  
  
 Este método es compatible sólo con cursores de servidor. Seek no se admite cuando la [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) valor de propiedad de la **Recordset** objeto es **adUseClient**.  
  
 Este método se puede utilizar solo cuando la **Recordset** objeto se ha abierto con un [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) valo **adCmdTableDirect**.  
  
## <a name="filtering-the-results"></a>Filtrar los resultados  
 El **buscar** método limita la búsqueda al contenido de un campo. El **Seek** método requiere un índice y tiene también otras limitaciones. Si debe buscar en varios campos que no son la base de un índice o si el proveedor no admite índices, puede limitar los resultados mediante el **filtro** propiedad de la **Recordset** objeto.  
  
 Use la **filtro** propiedad para ocultar selectivamente los registros de un **Recordset** objeto. El filtrado **Recordset** se convierte en el cursor actual, lo que significa que los registros que no cumple la **filtro** criterios no están disponibles en la **Recordset** hasta que el **Filtro** se quita. Otras propiedades que devuelven valores basados en el cursor actual se ven afectadas, como **AbsolutePosition**, **AbsolutePage**, **RecordCount**, y  **PageCount**. Esto es porque al establecer la **filtro** propiedad en un valor específico moverá el registro actual al primer registro que cumpla el nuevo valor.  
  
 El **filtro** propiedad toma un argumento de tipo variant. Este valor representa uno de los tres métodos para usar la **filtro** propiedad: una cadena de criterios, un **FilterGroupEnum** constante o una matriz de marcadores. Para obtener más información, vea Filtrar con una cadena de criterios, filtrar por una constante y filtrar por marcadores más adelante en este tema.  
  
> [!NOTE]
>  Cuando se conocen los datos que desea seleccionar, es normalmente más eficaz para abrir un **Recordset** con una instrucción SQL que filtra, de hecho el conjunto de resultados, en lugar de confiar en la **filtro** propiedad.  
  
 Para quitar un filtro de un **Recordset**, use la **adFilterNone** constante. Establecer el **filtro** propiedad en una cadena de longitud cero ("") tiene el mismo efecto que usar el **adFilterNone** constante.  
  
### <a name="filtering-with-a-criteria-string"></a>Filtrar con una cadena de criterios  
 La cadena de criterios se compone de cláusulas con el formato *NombreCampo Operador valor* (por ejemplo, `"LastName = 'Smith'"`). Puede crear cláusulas compuestas al concatenar cláusulas individuales mediante **AND** (por ejemplo, `"LastName = 'Smith' AND FirstName = 'John'"`) y **o** (por ejemplo, `"LastName = 'Smith' OR LastName = 'Jones'"`). Utilice las siguientes directrices para las cadenas de criterios:  
  
-   *FieldName* debe ser un nombre de campo válido de la **conjunto de registros**. Si el nombre del campo contiene espacios, debe incluir el nombre entre corchetes.  
  
-   *Operador* debe ser uno de los siguientes:  **\<** ,  **>** ,  **\< =** ,  **>=**  ,  **<>** ,  **=** , o **como**.  
  
-   *Valor* es el valor con el que comparará los valores de campo (por ejemplo, `'Smith'`, `#8/24/95#`, `12.345`, o `$50.00`). Utilice comillas simples (') con las cadenas y signos de número (`#`) con las fechas. Para números, puede utilizar separadores decimales, signos de dólar y notación científica. Si *operador* es **como**, *valor* puede usar caracteres comodín. Solo el asterisco (\*) y caracteres comodín (%) que se permiten caracteres de signo de porcentaje, y deben ser el último carácter de la cadena. *Valor* no puede ser nulo.  
  
    > [!NOTE]
    >  Debe incluir entre comillas simples (') en el filtro *valor*, utilice dos comillas simples para representar una. Por ejemplo, para filtrar según *o ' Malley*, la cadena de criterios debe ser `"col1 = 'O''Malley'"`. Para incluir comillas simples al principio y al final del valor de filtro, escriba la cadena de signos de número (#). Por ejemplo, para filtrar según *'1'*, la cadena de criterios debe ser `"col1 = #'1'#"`.  
  
 No hay ninguna preferencia entre **AND** y **o**. Las cláusulas se pueden agrupar entre paréntesis. Sin embargo, no se pueden agrupar cláusulas combinadas por un **o** y, a continuación, unir el grupo a otra cláusula mediante AND, como se indica a continuación.  
  
```  
(LastName = 'Smith' OR LastName = 'Jones') AND FirstName = 'John'  
```  
  
 En su lugar, debería crear el filtro como se indica a continuación.  
  
```  
(LastName = 'Smith' AND FirstName = 'John') OR (LastName = 'Jones' AND FirstName = 'John')  
```  
  
 En un **como** cláusula, puede usar un carácter comodín al principio y al final del patrón (por ejemplo, `LastName Like '*mit*'`) o solo al final del patrón (por ejemplo, `LastName Like 'Smit*'`).  
  
### <a name="filtering-with-a-constant"></a>Filtrar por una constante  
 Las constantes siguientes están disponibles para filtrar **conjuntos de registros**.  
  
|Constante|Description|  
|--------------|-----------------|  
|**adFilterAffectedRecords**|Filtros para ver solo los registros afectados por la última **eliminar**, **Resync**, **UpdateBatch**, o **CancelBatch** llamar.|  
|**adFilterConflictingRecords**|Filtros para ver los registros que no se pudo la última actualización por lotes.|  
|**adFilterFetchedRecords**|Filtros para ver los registros en la memoria caché actual, es decir, los resultados de la última llamada para recuperar registros de la base de datos.|  
|**adFilterNone**|Quita el filtro actual y restaura todos los registros para su visualización.|  
|**adFilterPendingRecords**|Filtros para ver solo los registros que han cambiado pero no se han enviado todavía al servidor. Se aplica solo a modo de actualización por lotes.|  
  
 Las constantes de filtro que sea más fácil resolver conflictos de registros individuales durante el modo de actualización por lotes por lo que permite ver, por ejemplo, solo aquellos registros que se vieron afectados durante la última **UpdateBatch** llamada al método, como se muestra en el ejemplo siguiente.  
  
 `Attribute VB_Name = "modExaminingData"`  
  
### <a name="filtering-with-bookmarks"></a>Filtrar con marcadores  
 Por último, puede pasar una matriz variant de marcadores para la **filtro** propiedad. El cursor resultante contendrá sólo aquellos registros cuyo marcador se pasó a la propiedad. En el ejemplo de código siguiente se crea una matriz de marcadores de los registros de un **Recordset** que tienen una "B" en la *ProductName* campo. A continuación, pasa la matriz a la **filtro** propiedad y muestra información sobre el filtrado de resultante **conjunto de registros**.  
  
```  
'BeginFilterBkmk  
Dim vBkmkArray() As Variant  
Dim i As Integer  
  
'Recordset created using "SELECT * FROM Products" as command.  
'So, we will check to see if ProductName has a capital B, and  
'if so, add to the array.  
i = 0  
Do While Not objRs.EOF  
    If InStr(1, objRs("ProductName"), "B") Then  
        ReDim Preserve vBkmkArray(i)  
        vBkmkArray(i) = objRs.Bookmark  
        i = i + 1  
        Debug.Print objRs("ProductName")  
    End If  
    objRs.MoveNext  
Loop  
  
'Filter using the array of bookmarks.  
objRs.Filter = vBkmkArray  
  
objRs.MoveFirst  
Do While Not objRs.EOF  
    Debug.Print objRs("ProductName")  
    objRs.MoveNext  
Loop  
'EndFilterBkmk  
```  
  
## <a name="creating-a-clone-of-a-recordset"></a>Crear un clon de un conjunto de registros  
 Use la **clon** duplicados de método para crear varios **Recordset** objetos, especialmente si desea mantener más de un registro actual en un determinado conjunto de registros. Mediante el **clon** método es más eficaz que crear y abrir un nuevo **Recordset** objeto con la misma definición que el original.  
  
 El registro actual de un clon recién creado se establece originalmente en el primer registro. El puntero del registro actual en un clonado **Recordset** no está sincronizada con el original ni viceversa. Es posible desplazarse independientemente en cada uno de ellos **conjunto de registros**.  
  
 Los cambios que realice a uno **Recordset** objeto están visibles en todos sus duplicados, independientemente del tipo de cursor. Sin embargo, después de ejecutar [Requery](../../../ado/reference/ado-api/requery-method.md) en el original **Recordset**, los clones ya no se sincronizarán con el original.  
  
 Cierre el original **Recordset** no se cierran sus copias, ni tampoco cerrar cerrar una copia del original o cualquiera de las demás copias.  
  
 Puede clonar un **Recordset** objeto sólo si admite marcadores. Los valores de marcador son intercambiables; es decir, una referencia de marcador de un **Recordset** objeto hace referencia al mismo registro en cualquiera de sus clones.

