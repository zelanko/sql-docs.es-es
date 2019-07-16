---
title: Propiedad Filter | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 03/20/2018
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::Filter
helpviewer_keywords:
- Filter property
ms.assetid: 80263a7a-5d21-45d1-84fc-34b7a9be4c22
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ff06bc27e765945d1cca74b5f8401e0caadf6b17
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67918636"
---
# <a name="filter-property"></a>Propiedad Filter
Indica un filtro para los datos en un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos

Establece o devuelve un **Variant** valor, que puede contener uno de los siguientes elementos:  
  
-   **Cadena de criterios:** Una cadena formada por uno o más cláusulas concatenadas con **AND** o **OR** operadores.  
  
-   **Matriz de marcadores:** Matriz de marcador único valores que señalan a los registros en el **Recordset** objeto.  
  
-   Un [FilterGroupEnum](../../../ado/reference/ado-api/filtergroupenum.md) valor.  
  
## <a name="remarks"></a>Comentarios

Use la **filtro** propiedad para ocultar selectivamente los registros en un **Recordset** objeto. El filtrado **Recordset** se convierte en el cursor actual. Otras propiedades que devuelven valores según actual **cursor** se ven afectados, como [propiedad AbsolutePosition (ADO)](../../../ado/reference/ado-api/absoluteposition-property-ado.md), [propiedad AbsolutePage (ADO)](../../../ado/reference/ado-api/absolutepage-property-ado.md), [ Propiedad RecordCount (ADO)](../../../ado/reference/ado-api/recordcount-property-ado.md), y [PageCount (propiedad, ADO)](../../../ado/reference/ado-api/pagecount-property-ado.md). Establecer el **filtro** propiedad en un valor específico de nuevo el registro actual mueve al primer registro que satisface el nuevo valor.
  
La cadena de criterios se compone de las cláusulas en el formulario *NombreCampo-Operador-valor* (por ejemplo, `"LastName = 'Smith'"`). Puede crear cláusulas compuestas concatenando cláusulas individuales con **AND** (por ejemplo, `"LastName = 'Smith' AND FirstName = 'John'"`) o **OR** (por ejemplo, `"LastName = 'Smith' OR LastName = 'Jones'"`). Para las cadenas de criterios, Use las siguientes directrices:

-   *FieldName* debe ser un nombre de campo válido de la **Recordset**. Si el nombre del campo contiene espacios, debe incluir el nombre entre corchetes.  
  
-   Operador debe ser uno de los siguientes: \<, >, \<=, > =, <>, =, o **como**.  
  
-   Valor es el valor con el que se compararán los valores de campo (por ejemplo, "Smith", 24/8/95 #, 12.345 o 50,00 dólares). Use comillas simples con cadenas y símbolos de libra esterlina (#) con fechas. Puede usar para números, puntos decimales, signos de dólar y notación científica. Si es operador **como**, valor puede usar caracteres comodín. Solo el asterisco (*) y el signo de porcentaje (%) se permiten caracteres comodín y deben ser el último carácter de la cadena. el valor no puede ser Null.  
  
> [!NOTE]
>  Para incluir las comillas simples (') en el valor de filtro, utilice dos comillas simples para representar una. Por ejemplo, debe ser la cadena de criterios para filtrar por o ' Malley, `"col1 = 'O''Malley'"`. Para incluir las comillas simples al principio y al final del valor de filtro, escriba la cadena con signos de número (#). Por ejemplo, para filtrar por '1', debe ser la cadena de criterios `"col1 = #'1'#"`.  
  
-   No hay ninguna preferencia entre AND y o. Las cláusulas se pueden agrupar entre paréntesis. Sin embargo, no se puede agrupar cláusulas unidas mediante OR y, a continuación, unir el grupo a otra cláusula mediante AND, como se muestra en el siguiente fragmento de código:  
 `(LastName = 'Smith' OR LastName = 'Jones') AND FirstName = 'John'`  
  
-   En su lugar, se crea este filtro como  
 `(LastName = 'Smith' AND FirstName = 'John') OR (LastName = 'Jones' AND FirstName = 'John')`  
  
-   En un **como** cláusula, puede usar un carácter comodín al principio y al final del patrón. Por ejemplo, puede usar `LastName Like '*mit*'`. O con **como** puede usar un carácter comodín solo al final del patrón. Por ejemplo: `LastName Like 'Smit*'`.  
  
 Las constantes de filtro que sea más fácil resolver conflictos de registros individuales durante el modo de actualización por lotes, ya que permite ver, por ejemplo, los registros que se vieron afectados durante la última [método UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) llamada al método.  
  
Establecer el **filtro** propia propiedad puede producir un error debido a un conflicto con los datos subyacentes. Por ejemplo, este error puede ocurrir cuando otro usuario ya se ha eliminado un registro. En tal caso, el proveedor devuelve advertencias a la [colección de errores (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md) colección, pero no detiene la ejecución del programa. Se produce un error en tiempo de ejecución solo si hay conflictos en todos los registros solicitados. Use la [propiedad Status (ADO Recordset)](../../../ado/reference/ado-api/status-property-ado-recordset.md) propiedad para localizar los registros con conflictos.  
  
Establecer el **filtro** propiedad en una cadena de longitud cero ("") tiene el mismo efecto que usar el **adFilterNone** constante.
  
Cada vez que el **filtro** propiedad está establecida, la posición actual del registro se mueve al primer registro en el subconjunto filtrado de registros en el **Recordset**. De forma similar, cuando el **filtro** propiedad está desactivada, la posición actual del registro se mueve al primer registro en el **Recordset**.

Suponga que un **Recordset** se filtra en función de un campo de algún tipo de variante, como el tipo sql_variant. Un error (DISP_E_TYPEMISMATCH o 80020005) se produce cuando no coinciden con los subtipos de los valores de campo y el filtro utilizados en la cadena de criterios. Por ejemplo, supongamos que:

- Un **Recordset** objeto (rs) contiene una columna (C) del tipo sql_variant.
- Y un campo de esta columna se ha asignado un valor de 1 del tipo I4. Se establece la cadena de criterios en `rs.Filter = "C='A'"` en el campo.

Esta configuración produce el error durante el tiempo de ejecución. Sin embargo, `rs.Filter = "C=2"` aplicado en el mismo campo no producirá ningún error. Y el campo se filtra en el conjunto de registros actual.

Consulte la [propiedad marcador (ADO)](../../../ado/reference/ado-api/bookmark-property-ado.md) propiedad para obtener una explicación de los valores de marcador desde la que puede crear una matriz que se usará con la propiedad de filtro.

Solo los filtros en forma de cadenas de criterios afectan al contenido de un persistente **Recordset**. Un ejemplo de una cadena de criterios es `OrderDate > '12/31/1999'`. Los filtros creados con una matriz de marcadores o mediante un valor de la **FilterGroupEnum**, no afectan al contenido de conservados **Recordset**. Estas reglas se aplican a los conjuntos de registros creados con cursores del lado cliente o servidor.
  
> [!NOTE]
>  Al aplicar la marca adFilterPendingRecords a un filtrado y modificar **Recordset** en el modo de actualización por lotes, el resultante **Recordset** está vacío si el filtrado se basa en el campo de clave de un tabla única clave y la modificación se ha realizado en los valores de campo de clave. El resultante **Recordset** estará vacío si se cumple una de las instrucciones siguientes:  
  
-   El filtrado se basaba en los campos que no son de clave en una tabla única clave.  
  
-   El filtrado se basaba en todos los campos de una tabla con varias claves.  
  
-   Se han realizado modificaciones en los campos que no son de clave en una tabla única clave.  
  
-   Se han realizado modificaciones en los campos de una tabla con varias claves.  
  
En la tabla siguiente se resume los efectos de **adFilterPendingRecords** diferentes combinaciones de filtrado y modificaciones. La columna izquierda muestra las posibles modificaciones. Se pueden realizar modificaciones en cualquiera de los campos no clave, en el campo de clave en una tabla con una clave única o en cualquiera de los campos de clave en una tabla con varias claves. La fila superior muestra el criterio de filtrado. El filtrado puede basarse en cualquiera de los campos no clave, el campo de clave en una tabla con una clave única, o cualquiera de los campos de clave en una tabla con varias claves. Las celdas de intersección muestran los resultados. Un **+** signo significa que se aplica **adFilterPendingRecords** da como resultado un valor no vacío **Recordset**. Un **-** vacío significa que el signo menos **Recordset**.  
  
||No son claves|Clave única|Varias claves|
|-|--------------|----------------|-------------------|
|**No son claves**|+|+|+|
|**Clave única**|+|-|N/D|
|**Varias claves**|+|N/D|+|
|||||
  
## <a name="applies-to"></a>Se aplica a

[Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vea también

[Ejemplo Filter y RecordCount propiedades (VB)](../../../ado/reference/ado-api/filter-and-recordcount-properties-example-vb.md)
[ejemplo Filter y RecordCount propiedades (VC ++)](../../../ado/reference/ado-api/filter-and-recordcount-properties-example-vc.md)
[Clear (método) (ADO)](../../../ado/reference/ado-api/clear-method-ado.md) 
 [(ADO) de propiedad dinámica optimize](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)
