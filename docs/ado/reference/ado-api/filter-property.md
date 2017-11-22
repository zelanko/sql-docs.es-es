---
title: Propiedad de filtro | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: Recordset15::Filter
helpviewer_keywords: Filter property
ms.assetid: 80263a7a-5d21-45d1-84fc-34b7a9be4c22
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 22b1ee344246c2a21dc143822145ba6ca09060d0
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="filter-property"></a>Propiedad de filtro
Indica un filtro para los datos en un [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un **Variant** valor, que puede contener uno de los siguientes:  
  
-   **Cadena de criterios** ??? una cadena formada por uno o más cláusulas concatenadas con **AND** o **OR** operadores.  
  
-   **Matriz de marcadores** ??? una matriz de marcador único valores que señalan a registros en la **Recordset** objeto.  
  
-   A [FilterGroupEnum](../../../ado/reference/ado-api/filtergroupenum.md) valor.  
  
## <a name="remarks"></a>Comentarios  
 Use la **filtro** propiedad para ocultar selectivamente los registros de un **Recordset** objeto. El filtrado **Recordset** se convierte en el cursor actual. Otras propiedades que devuelven valores según la actual **cursor** se ven afectadas, como [propiedad AbsolutePosition (ADO)](../../../ado/reference/ado-api/absoluteposition-property-ado.md), [propiedad AbsolutePage (ADO)](../../../ado/reference/ado-api/absolutepage-property-ado.md), [ Propiedad RecordCount (ADO)](../../../ado/reference/ado-api/recordcount-property-ado.md), y [PageCount (propiedad, ADO)](../../../ado/reference/ado-api/pagecount-property-ado.md). Esto es porque al establecer la **filtro** propiedad en un valor específico moverá el registro actual al primer registro que cumpla el nuevo valor.  
  
 La cadena de criterios se compone de cláusulas con el formato *NombreCampo-Operador-valor* (por ejemplo, `"LastName = 'Smith'"`). Puede crear cláusulas compuestas al concatenar cláusulas individuales mediante **AND** (por ejemplo, `"LastName = 'Smith' AND FirstName = 'John'"`) o **OR** (por ejemplo, `"LastName = 'Smith' OR LastName = 'Jones'"`). Utilice las siguientes directrices para las cadenas de criterios:  
  
-   *FieldName* debe ser un nombre de campo válido de la **conjunto de registros**. Si el nombre del campo contiene espacios, debe incluir el nombre entre corchetes.  
  
-   Operador debe ser uno de los siguientes valores: \<, >, \<=, > =, <>, =, o **como**.  
  
-   Valor es el valor con el que comparará los valores de campo (por ejemplo, 'Smith', #8/24/&#95;, 12.345 o 50,00 $). Use comillas simples con las cadenas y los signos de número (#) con las fechas. Para números, puede utilizar separadores decimales, signos de dólar y notación científica. Si el operador es **como**, valor puede utilizar caracteres comodín. Se permiten solo el asterisco (*) ni caracteres comodín de signo de porcentaje (%), y deben ser el último carácter de la cadena. el valor no puede ser Null.  
  
> [!NOTE]
>  Para incluir comillas simples (') en el valor de filtro, utilice dos comillas simples para representar una. Por ejemplo, para filtrar por o ' Malley, la cadena de criterios debe ser "col1 = ' O'' Malley'". Para incluir comillas simples al principio y al final del valor de filtro, encierre la cadena con un signo de almohadilla (#). Por ejemplo, para filtrar por '1', la cadena de criterios debería ser "col1 = #' 1' #".  
  
-   No hay ninguna preferencia entre AND y o. Las cláusulas se pueden agrupar entre paréntesis. Sin embargo, no se puede agrupar cláusulas combinadas mediante un operación OR y, a continuación, unir el grupo a otra cláusula mediante AND, como se muestra esto:`(LastName = 'Smith' OR LastName = 'Jones') AND FirstName = 'John'`  
  
-   En su lugar, se crea este filtro como`(LastName = 'Smith' AND FirstName = 'John') OR (LastName = 'Jones' AND FirstName = 'John')`  
  
-   En un **como** cláusula, puede usar un carácter comodín al principio y al final del patrón (por ejemplo, LastName Like ' * mit\*'), o solo al final del patrón (por ejemplo, LastName Like ' Smit\*').  
  
 Las constantes de filtro que sea más fácil resolver conflictos de registros individuales durante el modo de actualización por lotes por lo que permite ver, por ejemplo, solo aquellos registros que se vieron afectados durante la última [método UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) llamada al método.  
  
 Establecer la propiedad de filtro propio puede producir un error debido a un conflicto con los datos subyacentes (por ejemplo, un registro ya se ha eliminado por otro usuario). En tal caso, el proveedor devuelve advertencias a la [colección de errores (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md) colección, pero no detiene la ejecución del programa. Se produce un error de tiempo de ejecución sólo si hay conflictos en todos los registros solicitados. Use la [propiedad Status (conjunto de registros ADO)](../../../ado/reference/ado-api/status-property-ado-recordset.md) propiedad para localizar los registros con conflictos.  
  
 Establecer el **filtro** propiedad en una cadena de longitud cero ("") tiene el mismo efecto que usar el **adFilterNone** constante.  
  
 Cada vez que la **filtro** propiedad está establecida, la posición actual del registro se mueve al primer registro del subconjunto filtrado de registros en la **conjunto de registros**. De forma similar, cuando la **filtro** propiedad está desactivada, la posición actual del registro se mueve al primer registro en el **conjunto de registros**.  
  
 Cuando un **Recordset** se filtra en función de un campo de un tipo variant (p. ej., sql_variant), un error (DISP_E_TYPEMISMATCH o 80020005) se producirá si no coinciden con los subtipos de los valores de campo y filtro utilizados en la cadena de criterios. Por ejemplo, si un **Recordset** objeto (rs) contiene una columna (C) del tipo sql_variant y un campo de esta columna se ha asignado un valor de 1 del tipo I4, establecer la cadena de criterios de rs. Filtro = "C = 'A'" en el campo se producirá el error en tiempo de ejecución. Sin embargo, rs. Filtro = "C = 2" aplicado en el mismo campo no producirá ningún error aunque el campo se filtrarán fuera del conjunto de registros actual.  
  
 Consulte la [propiedad marcador (ADO)](../../../ado/reference/ado-api/bookmark-property-ado.md) propiedad para obtener una explicación de los valores de marcador desde el que puede crear una matriz para utilizarla con la propiedad Filter.  
  
 Sólo los filtros con el formato de las cadenas de criterios (por ejemplo, OrderDate > ' 12/31/1999 ') afectan al contenido de un persistente **conjunto de registros**. Los filtros crean con una matriz de marcadores o mediante un valor de FilterGroupEnum no afectarán al contenido de conservados **conjunto de registros**. Estas reglas se aplican a los conjuntos de registros creados con cursores de cliente o servidor.  
  
> [!NOTE]
>  Al aplicar la marca adFilterPendingRecords a un filtrado y modificar **Recordset** en el modo de actualización por lotes, los resultantes **Recordset** está vacío si el filtrado se basa en el campo clave de un tabla única clave y la modificación se ha realizado en los valores de campo de clave. El resultante **Recordset** será no está vacío si se cumple alguna de las siguientes acciones:  
  
-   El filtrado se basa en los campos sin clave en una tabla con una clave única.  
  
-   El filtrado se basa en los campos de una tabla con varias claves.  
  
-   Se realizaron modificaciones en los campos sin clave en una tabla con una clave única.  
  
-   Se realizaron modificaciones en los campos de una tabla con varias claves.  
  
 En la tabla siguiente se resume los efectos de **adFilterPendingRecords** diferentes combinaciones de filtrado y modificaciones. La columna izquierda muestra las posibles modificaciones; se pueden realizar modificaciones en cualquiera de los campos sin clave, en el campo de clave en una tabla con una clave única, o en cualquiera de los campos de clave en una tabla con varias claves. La fila superior muestra el criterio de filtrado; filtrado puede basarse en cualquiera de los campos no clave, el campo de clave en una tabla con una clave única, o cualquiera de los campos de clave en una tabla con varias claves. Las celdas de intersección muestran los resultados: + significa que aplicar **adFilterPendingRecords** da como resultado un valor no vacío **Recordset**; - significa vacío **conjunto de registros**.  
  
||No son claves|Clave única|Varias claves|  
|-|--------------|----------------|-------------------|  
|**No son claves**|+|+|+|  
|**Clave única**|+|-|N/D|  
|**Varias claves**|+|N/D|+|  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Filtro y ejemplo de las propiedades RecordCount (VB)](../../../ado/reference/ado-api/filter-and-recordcount-properties-example-vb.md)   
 [Filtro y ejemplo de las propiedades RecordCount (VC ++)](../../../ado/reference/ado-api/filter-and-recordcount-properties-example-vc.md)   
 [Clear (método) (ADO)](../../../ado/reference/ado-api/clear-method-ado.md)   
 [Propiedad dinámica Optimize (ADO)](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)
