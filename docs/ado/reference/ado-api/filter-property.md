---
title: Propiedad de filtro | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 03/20/2018
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: article
apitype: COM
f1_keywords:
- Recordset15::Filter
helpviewer_keywords:
- Filter property
ms.assetid: 80263a7a-5d21-45d1-84fc-34b7a9be4c22
caps.latest.revision: ''
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8c3b06134dcf65ead3a97577a6d08fd46ec2f52e
ms.sourcegitcommit: ccb05cb5a4cccaf7ffa9e85a4684fa583bab914e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/22/2018
---
# <a name="filter-property"></a>Propiedad de filtro
Indica un filtro para los datos en un [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos

Establece o devuelve un **Variant** valor, que puede contener uno de los siguientes elementos:  
  
-   **Cadena de criterios:** una cadena formada por uno o más cláusulas concatenadas con **AND** o **OR** operadores.  
  
-   **Matriz de marcadores:** que señalan a registros en los valores de una matriz de marcador único el **Recordset** objeto.  
  
-   A [FilterGroupEnum](../../../ado/reference/ado-api/filtergroupenum.md) valor.  
  
## <a name="remarks"></a>Comentarios

Use la **filtro** propiedad para ocultar selectivamente los registros de un **Recordset** objeto. El filtrado **Recordset** se convierte en el cursor actual. Otras propiedades que devuelven valores según la actual **cursor** se ven afectadas, como [propiedad AbsolutePosition (ADO)](../../../ado/reference/ado-api/absoluteposition-property-ado.md), [propiedad AbsolutePage (ADO)](../../../ado/reference/ado-api/absolutepage-property-ado.md), [ Propiedad RecordCount (ADO)](../../../ado/reference/ado-api/recordcount-property-ado.md), y [PageCount (propiedad, ADO)](../../../ado/reference/ado-api/pagecount-property-ado.md). Establecer el **filtro** propiedad a un nuevo valor específico, mueve el registro actual al primer registro que cumpla el nuevo valor.
  
La cadena de criterios se compone de cláusulas con el formato *NombreCampo-Operador-valor* (por ejemplo, `"LastName = 'Smith'"`). Puede crear cláusulas compuestas al concatenar cláusulas individuales mediante **AND** (por ejemplo, `"LastName = 'Smith' AND FirstName = 'John'"`) o **OR** (por ejemplo, `"LastName = 'Smith' OR LastName = 'Jones'"`). Para las cadenas de criterios, utilice las siguientes directrices:

-   *FieldName* debe ser un nombre de campo válido de la **conjunto de registros**. Si el nombre del campo contiene espacios, debe incluir el nombre entre corchetes.  
  
-   Operador debe ser uno de los siguientes valores: \<, >, \<=, > =, <>, =, o **como**.  
  
-   Valor es el valor con el que comparará los valores de campo (por ejemplo, 'Smith', #8/24/&#95;, 12.345 o 50,00 $). Use comillas simples con las cadenas y los signos de número (#) con las fechas. Para números, puede utilizar separadores decimales, signos de dólar y notación científica. Si el operador es **como**, valor puede utilizar caracteres comodín. Se permiten solo el asterisco (*) ni caracteres comodín de signo de porcentaje (%), y deben ser el último carácter de la cadena. el valor no puede ser Null.  
  
> [!NOTE]
>  Para incluir comillas simples (') en el valor de filtro, utilice dos comillas simples para representar una. Por ejemplo, para filtrar por o ' Malley, la cadena de criterios debe ser `"col1 = 'O''Malley'"`. Para incluir comillas simples al principio y al final del valor de filtro, encierre la cadena con un signo de almohadilla (#). Por ejemplo, para filtrar por '1', la cadena de criterios debe ser `"col1 = #'1'#"`.  
  
-   No hay ninguna preferencia entre AND y o. Las cláusulas se pueden agrupar entre paréntesis. Sin embargo, no se puede agrupar cláusulas combinadas mediante un operación OR y, a continuación, unir el grupo a otra cláusula mediante AND, como se muestra en el siguiente fragmento de código:  
 `(LastName = 'Smith' OR LastName = 'Jones') AND FirstName = 'John'`  
  
-   En su lugar, se crea este filtro como  
 `(LastName = 'Smith' AND FirstName = 'John') OR (LastName = 'Jones' AND FirstName = 'John')`  
  
-   En un **como** cláusula, puede usar un carácter comodín al principio y al final del patrón. Por ejemplo, puede usar `LastName Like '*mit*'`. O con **como** puede usar un carácter comodín solo al final del patrón. Por ejemplo, `LastName Like 'Smit*'`.  
  
 Las constantes de filtro que sea más fácil resolver conflictos de registros individuales durante el modo de actualización por lotes por lo que permite ver, por ejemplo, solo aquellos registros que se vieron afectados durante la última [método UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) llamada al método.  
  
Establecer el **filtro** propiedad en sí puede producir un error debido a un conflicto con los datos subyacentes. Por ejemplo, este error puede ocurrir cuando un registro se eliminó por otro usuario. En tal caso, el proveedor devuelve advertencias a la [colección de errores (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md) colección, pero no detiene la ejecución del programa. Se produce un error en tiempo de ejecución sólo si hay conflictos en todos los registros solicitados. Use la [propiedad Status (conjunto de registros ADO)](../../../ado/reference/ado-api/status-property-ado-recordset.md) propiedad para localizar los registros con conflictos.  
  
Establecer el **filtro** propiedad en una cadena de longitud cero ("") tiene el mismo efecto que usar el **adFilterNone** constante.
  
Cada vez que la **filtro** propiedad está establecida, la posición actual del registro se mueve al primer registro del subconjunto filtrado de registros en la **conjunto de registros**. De forma similar, cuando la **filtro** propiedad está desactivada, la posición actual del registro se mueve al primer registro en el **conjunto de registros**.

Suponga que un **Recordset** se filtra en función de un campo de algún tipo de variante, como el tipo sql_variant. Error (DISP_E_TYPEMISMATCH o 80020005) se produce cuando no coinciden con los subtipos de los valores de campo y filtro utilizados en la cadena de criterios. Por ejemplo, suponga que:

- A **Recordset** objeto (rs) contiene una columna (C) del tipo sql_variant.
- Y un campo de esta columna se ha asignado un valor de 1 del tipo I4. La cadena de criterios está establecida en `rs.Filter = "C='A'"` en el campo.

Esta configuración produce el error en tiempo de ejecución. Sin embargo, `rs.Filter = "C=2"` aplicado en el mismo campo no producirá ningún error. Y el campo se filtra el conjunto de registros actual.

Consulte la [propiedad marcador (ADO)](../../../ado/reference/ado-api/bookmark-property-ado.md) propiedad para obtener una explicación de los valores de marcador desde el que puede crear una matriz para utilizarla con la propiedad Filter.

Solo los filtros en el formato de las cadenas de criterios afectan al contenido de un persistente **conjunto de registros**. Un ejemplo de una cadena de criterios es `OrderDate > '12/31/1999'`. Los filtros creados con una matriz de marcadores o mediante un valor de la **FilterGroupEnum**, no afectan al contenido de conservados **conjunto de registros**. Estas reglas se aplican a los conjuntos de registros creados con cursores de cliente o servidor.
  
> [!NOTE]
>  Al aplicar la marca adFilterPendingRecords a un filtrado y modificar **Recordset** en el modo de actualización por lotes, los resultantes **Recordset** está vacío si el filtrado se basa en el campo clave de un tabla única clave y la modificación se ha realizado en los valores de campo de clave. El resultante **Recordset** será no está vacío si se cumple alguna de las instrucciones siguientes:  
  
-   El filtrado se basa en los campos sin clave en una tabla con una clave única.  
  
-   El filtrado se basa en los campos de una tabla con varias claves.  
  
-   Se realizaron modificaciones en los campos sin clave en una tabla con una clave única.  
  
-   Se realizaron modificaciones en los campos de una tabla con varias claves.  
  
En la tabla siguiente se resume los efectos de **adFilterPendingRecords** diferentes combinaciones de filtrado y modificaciones. La columna izquierda muestra las posibles modificaciones. Se pueden realizar modificaciones en cualquiera de los campos sin clave, en el campo de clave en una tabla con una clave única, o en cualquiera de los campos de clave en una tabla con varias claves. La fila superior muestra el criterio de filtrado. Filtrado puede basarse en cualquiera de los campos no clave, el campo de clave en una tabla con una clave única, o cualquiera de los campos de clave en una tabla con varias claves. Las celdas de intersección muestran los resultados. A  **+**  signo significa que aplicar **adFilterPendingRecords** da como resultado un valor no vacío **conjunto de registros**. A  **-**  signo significa vacío **conjunto de registros**.  
  
||No son claves|Clave única|Varias claves|
|-|--------------|----------------|-------------------|
|**No son claves**|+|+|+|
|**Clave única**|+|-|N/D|
|**Varias claves**|+|N/D|+|
|||||
  
## <a name="applies-to"></a>Se aplica a

[Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vea también

[Ejemplo de propiedades de RecordCount (VB) y filtro](../../../ado/reference/ado-api/filter-and-recordcount-properties-example-vb.md)
[filtro y ejemplo de las propiedades RecordCount (VC ++)](../../../ado/reference/ado-api/filter-and-recordcount-properties-example-vc.md)
[Clear (método) (ADO)](../../../ado/reference/ado-api/clear-method-ado.md) 
 [Optimizar propiedad dinámicos (ADO)](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)
