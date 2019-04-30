---
title: Trabajar con conjuntos de registros | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Recordset object [ADO]
ms.assetid: bdf9a56a-de4a-44de-9111-2f11ab7b16ea
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2378d438c575ad54a89f09c4c9ddcb157c246ffd
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63184827"
---
# <a name="working-with-recordsets"></a>Trabajar con conjuntos de registros
El **Recordset** objeto tiene características integradas que permiten reorganizar el orden de los datos en el conjunto de resultados para buscar un registro específico en función de criterios que suministran e incluso a optimizar estas operaciones de búsqueda mediante índices. Si estas características están disponibles para su uso depende del proveedor y en algunos casos - como los de la [índice](../../../ado/reference/ado-api/index-property.md) propiedad - la estructura del origen de datos propia.  
  
## <a name="arranging-data"></a>Organizar datos  
 Con frecuencia, la manera más eficaz para ordenar los datos en su **Recordset** consiste en especificar una cláusula ORDER BY en el comando SQL utilizado para devolver los resultados. Sin embargo, es posible que deba cambiar el orden de los datos en un **Recordset** que ya se ha creado. Puede usar el **ordenación** propiedad para establecer el orden en que las filas de una **Recordset** se recorren. Además, el **filtro** propiedad determina qué filas son puede obtenerse al recorrer las filas.  
  
 El **ordenación** propiedad establece o devuelve un **cadena** valor que indica el campo de nombres en el **conjunto de registros** en el que se va a ordenar. Cada nombre está separado por una coma y está seguido opcionalmente por un espacio y la palabra clave **ASC** (que ordena el campo en orden ascendente) o **DESC** (que ordena el campo en orden descendente). De forma predeterminada, si no se especifica ninguna palabra clave, el campo se ordena en orden ascendente.  
  
 La operación de ordenación es eficaz porque los datos no se reorganizan físicamente, pero se tiene acceso en el orden especificado por un índice.  
  
 El **ordenación** propiedad requiere la [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) propiedad se establece en **adUseClient**. Se creará un índice temporal para cada campo especificado en el **ordenación** propiedad si no existe.  
  
 Establecer el **ordenación** restablecerá las filas a su orden original y eliminar índices temporales propiedad en una cadena vacía. No se eliminarán los índices existentes.  
  
 Supongamos que un **Recordset** contiene tres campos denominados *firstName*, *middleInitial*, y *lastName*. Establecer el **ordenación** propiedad a la cadena "`lastName DESC, firstName ASC`", que ordenará los **Recordset** por apellido en orden descendente y, a continuación, por nombre en orden ascendente. Se omite la inicial del segundo nombre.  
  
 Ningún campo al que hace referencia en una cadena de criterios de ordenación puede denominarse "ASC" o "DESC" porque esos nombres en conflicto con las palabras clave **ASC** y **DESC**. Asigne a un campo que tiene un alias de un nombre en conflicto mediante la **AS** palabra clave en la consulta que devuelve el **Recordset**.  
  
 Para obtener más información acerca de **Recordset** filtrado, consulte "Filtrado de resultados de la" más adelante en este tema.  
  
## <a name="finding-a-specific-record"></a>Buscar un registro específico  
 ADO proporciona el [buscar](../../../ado/reference/ado-api/find-method-ado.md) y [Seek](../../../ado/reference/ado-api/seek-method.md) métodos para buscar un registro determinado en un **Recordset**. El **buscar** método es compatible con una variedad de proveedores, pero se limita a un criterio de búsqueda único. El **Seek** método permite realizar búsquedas en varios criterios, pero no es compatible con muchos proveedores.  
  
 Los índices de campos pueden mejorar considerablemente el rendimiento de la **buscar** método y **ordenación** y **filtro** propiedades de la **Recordset** objeto. Puede crear un índice interno para un **campo** objeto estableciendo sus dinámicos [optimizar](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md) propiedad. Esta propiedad se agrega a la **propiedades** colección de la **campo** objeto cuando se establece la [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) propiedad **adUseClient**. Recuerde que este índice es interno a ADO: no se puede obtener acceso a él o utilizarlo para ningún otro propósito. Además, este índice es distinta de la [índice](../../../ado/reference/ado-api/index-property.md) propiedad de la **Recordset** objeto.  
  
 El **buscar** método busca rápidamente un valor dentro de una columna (campo) de un **Recordset**. Con frecuencia puede mejorar la velocidad de la **buscar** método en una columna mediante el **optimizar** propiedad para crear un índice en ella.  
  
 El **buscar** método limita la búsqueda al contenido de un campo. El **Seek** método requiere un índice y tiene también otras limitaciones. Si debe buscar en varios campos que no son la base de un índice, o si el proveedor no admite índices, puede limitar los resultados mediante el uso de la **filtro** propiedad de la **Recordset** objeto.  
  
### <a name="find"></a>Buscar  
 El **buscar** búsquedas de los métodos un **Recordset** para la fila que cumple un criterio especificado. Opcionalmente, se puede especificar la dirección de la búsqueda, la fila inicial y el desplazamiento desde la fila inicial. Si se cumple el criterio, la posición de fila actual se establece en el registro se encuentra; en caso contrario, se establece la posición al final (o inicio) de la **Recordset**, en función de la dirección de búsqueda.  
  
 Solo un nombre de columna única puede especificarse para el criterio. En otras palabras, este método no admite búsquedas de varias columnas.  
  
 Puede ser el operador de comparación para el criterio"**>**"(mayor que),"**\<**" (menor que), "=" (igual), "> =" (mayor o igual que), "< =" (menor o igual que), " <> "(no igual a), o"LIKE"(coincidencia).  
  
 El valor del criterio puede ser una cadena, número de punto flotante o fecha. Los valores de cadena están delimitados con comillas simples o marcas "#" (signo de número) (por ejemplo, "estado = 'WA'" o "estado = WA #"). Los valores de fecha se delimitan con marcas de "#" (signo de número) (por ejemplo, "start_date > #7/22/97 #").  
  
 Si el operador de comparación es "like", el valor de cadena puede contener un asterisco (*) para buscar una o más apariciones de cualquier carácter o subcadena. Por ejemplo, "state like'm\*'" encuentra Maine y Massachusetts. También puede utilizar asteriscos iniciales y finales para buscar una subcadena que se encuentra dentro de los valores. Por ejemplo, "estado como '\*como\*'" coincide con Alaska, Arkansas y Massachusetts.  
  
 Los asteriscos pueden usarse solo al final de una cadena de criterios o juntos al principio y al final de una cadena de criterios, como se mostró anteriormente. No se puede usar el asterisco como comodín inicial ('* str') o incrustados indicado anteriormente\*r'). Esto provocará un error.  
  
### <a name="seek-and-index"></a>Buscar e indizar  
 Use la **Seek** método junto con el **índice** propiedad si el proveedor subyacente admite índices en el **Recordset** objeto. Use la [admite](../../../ado/reference/ado-api/supports-method.md)**(adSeek)** método para determinar si el proveedor subyacente admite **Seek**y el **Supports** método para determinar si el proveedor admite los índices. (Por ejemplo, el [proveedor OLE DB para Microsoft Jet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-jet.md) admite **Seek** y **índice**.)  
  
 Si **Seek** hace que no se encontró la fila deseada, ningún error se produce y la fila se coloca al final de la **Recordset**. Establecer el **índice** propiedad en el índice deseado antes de ejecutar este método.  
  
 Este método solo se admite con cursores de servidor. Buscar no se admite cuando la [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) valor de propiedad de la **Recordset** objeto es **adUseClient**.  
  
 Este método puede usarse solo cuando la **Recordset** objeto se ha abierto con un [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) valor de **adCmdTableDirect**.  
  
## <a name="filtering-the-results"></a>Filtrar los resultados  
 El **buscar** método limita la búsqueda al contenido de un campo. El **Seek** método requiere un índice y tiene también otras limitaciones. Si debe buscar en varios campos que no son la base de un índice o si el proveedor no admite índices, puede limitar los resultados mediante el uso de la **filtro** propiedad de la **Recordset** objeto.  
  
 Use la **filtro** propiedad para ocultar selectivamente los registros en un **Recordset** objeto. El filtrado **Recordset** se convierte en el cursor actual, lo que significa que los registros que no cumple la **filtro** criterios no están disponibles en el **Recordset** hasta que el **Filtro** se quita. Otras propiedades que devuelven valores según el cursor actual se ven afectados, como **AbsolutePosition**, **AbsolutePage**, **RecordCount**, y  **PageCount**. Esto es porque si se establece la **filtro** propiedad en un valor específico moverá el registro actual en el primer registro que satisface el nuevo valor.  
  
 El **filtro** propiedad toma un argumento de tipo variant. Este valor representa uno de los tres métodos para usar el **filtro** propiedad: una cadena de criterios, un **FilterGroupEnum** constante o una matriz de marcadores. Para obtener más información, consulte el filtrado con una cadena de criterios, filtrar por una constante y filtrar por marcadores más adelante en este tema.  
  
> [!NOTE]
>  Cuando sepa los datos que desea seleccionar, es normalmente más eficaz para abrir un **Recordset** con una instrucción SQL que filtra el conjunto de resultados, en lugar de depender de eficazmente la **filtro** propiedad.  
  
 Para quitar un filtro en un **Recordset**, utilice el **adFilterNone** constante. Establecer el **filtro** propiedad en una cadena de longitud cero ("") tiene el mismo efecto que usar el **adFilterNone** constante.  
  
### <a name="filtering-with-a-criteria-string"></a>Con una cadena de criterios de filtrado  
 La cadena de criterios consta de las cláusulas en el formulario *NombreCampo Operador valor* (por ejemplo, `"LastName = 'Smith'"`). Puede crear cláusulas compuestas concatenando cláusulas individuales con **AND** (por ejemplo, `"LastName = 'Smith' AND FirstName = 'John'"`) y **o** (por ejemplo, `"LastName = 'Smith' OR LastName = 'Jones'"`). Utilice las siguientes directrices para las cadenas de criterios:  
  
-   *FieldName* debe ser un nombre de campo válido de la **Recordset**. Si el nombre del campo contiene espacios, debe incluir el nombre entre corchetes.  
  
-   *Operador* debe ser uno de los siguientes: **\<**, **>**, **\< =**, **>=** , **<>**, **=**, o **como**.  
  
-   *Valor* es el valor con el que se compararán los valores de campo (por ejemplo, `'Smith'`, `#8/24/95#`, `12.345`, o `$50.00`). Utilice las comillas simples (') con las cadenas y signos de número (`#`) con fechas. Puede usar para números, puntos decimales, signos de dólar y notación científica. Si *operador* es **como**, *valor* puede usar caracteres comodín. Solo el asterisco (\*) y signo de porcentaje (%) se permiten caracteres comodín y deben ser el último carácter de la cadena. *Valor* no puede ser null.  
  
    > [!NOTE]
    >  Para incluir las comillas simples (') en el filtro *valor*, utilice dos comillas simples para representar una. Por ejemplo, para filtrar según *o ' Malley*, debe ser la cadena de criterios `"col1 = 'O''Malley'"`. Para incluir las comillas simples al principio y al final del valor de filtro, incluya la cadena de signos de número (#). Por ejemplo, para filtrar según *'1'*, debe ser la cadena de criterios `"col1 = #'1'#"`.  
  
 No hay ninguna preferencia entre **AND** y **o**. Las cláusulas se pueden agrupar entre paréntesis. Sin embargo, no se puede agrupar cláusulas combinadas por un **o** y, a continuación, unirse al grupo a otra cláusula mediante AND, como se indica a continuación.  
  
```  
(LastName = 'Smith' OR LastName = 'Jones') AND FirstName = 'John'  
```  
  
 En su lugar, debería crear el filtro como se indica a continuación.  
  
```  
(LastName = 'Smith' AND FirstName = 'John') OR (LastName = 'Jones' AND FirstName = 'John')  
```  
  
 En un **como** cláusula, puede usar un carácter comodín al principio y al final del patrón (por ejemplo, `LastName Like '*mit*'`) o solo al final del patrón (por ejemplo, `LastName Like 'Smit*'`).  
  
### <a name="filtering-with-a-constant"></a>Filtrar por una constante  
 Las constantes siguientes están disponibles para el filtrado **conjuntos de registros**.  
  
|Constante|Descripción|  
|--------------|-----------------|  
|**adFilterAffectedRecords**|Filtros para ver solo los registros afectados por la última **eliminar**, **Resync**, **UpdateBatch**, o **CancelBatch** llamar.|  
|**adFilterConflictingRecords**|Filtros para ver los registros que no se pudo la última actualización por lotes.|  
|**adFilterFetchedRecords**|Filtros para ver los registros en la memoria caché actual: es decir, los resultados de la última llamada para recuperar registros de la base de datos.|  
|**adFilterNone**|Quita el filtro actual y restaura todos los registros para su visualización.|  
|**adFilterPendingRecords**|Los filtros para ver solo los registros que han cambiado pero que no se han enviado al servidor. Solo es aplicable a modo de actualización por lotes.|  
  
 Las constantes de filtro que sea más fácil resolver conflictos de registros individuales durante el modo de actualización por lotes, ya que permite ver, por ejemplo, los registros que se vieron afectados durante la última **UpdateBatch** llamada al método, como se muestra en el ejemplo siguiente.  
  
 `Attribute VB_Name = "modExaminingData"`  
  
### <a name="filtering-with-bookmarks"></a>Filtrar por marcadores  
 Por último, puede pasar una matriz variant de marcadores para el **filtro** propiedad. El cursor resultante contendrá solo aquellos registros cuyo marcador se pasó a la propiedad. En el ejemplo de código siguiente se crea una matriz de los marcadores de los registros de un **Recordset** que tienen una "B" en el *ProductName* campo. A continuación, pasa la matriz a la **filtro** propiedad y muestra información sobre el resultado filtrado **Recordset**.  
  
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
 Use la **clon** duplicar el método para crear varios **Recordset** objetos, especialmente si desea mantener más de un registro actual en un determinado conjunto de registros. Mediante el **clon** es más eficaz que crear y abrir un nuevo método **Recordset** objeto con la misma definición que el original.  
  
 El registro actual de un clon recién creado se establece originalmente en el primer registro. El puntero de registro actual en un clonado **Recordset** no está sincronizada con el original, o viceversa. Puede navegar por separado en cada **Recordset**.  
  
 Cambios en uno **Recordset** objeto están visibles en todos sus clones, independientemente del tipo de cursor. Sin embargo, después de ejecutar [Requery](../../../ado/reference/ado-api/requery-method.md) en el original **Recordset**, los clones ya no se sincronizarán con el original.  
  
 Cierre el original **Recordset** no cierra sus copias, ni tampoco cerrar cierre una copia del original, o cualquiera de las demás copias.  
  
 Puede clonar un **Recordset** objeto sólo si admite marcadores. Los valores de marcador son intercambiables; es decir, una referencia de marcador de un **Recordset** objeto hace referencia en el mismo registro en cualquiera de sus clones.
