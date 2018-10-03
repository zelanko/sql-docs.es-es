---
title: AddNew (método, ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::AddNew
- Recordset15::raw_AddNew
helpviewer_keywords:
- AddNew method [ADO]
ms.assetid: a9f54be9-5763-45d0-a6eb-09981b03bc08
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 911509c62c5ae93bc73ca94469ac776195d2a8b1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47605883"
---
# <a name="addnew-method-ado"></a>AddNew (método) (ADO)
Crea un nuevo registro para un actualizable [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
recordset.AddNew FieldList, Values  
```  
  
#### <a name="parameters"></a>Parámetros  
 *recordset*  
 Un **Recordset** objeto.  
  
 *FieldList*  
 Opcional. Un nombre único o una matriz de nombres o las posiciones ordinales de los campos en el nuevo registro.  
  
 *Valores*  
 Opcional. Un valor único o una matriz de valores para los campos en el nuevo registro. Si *Fieldlist* es una matriz, *valores* también debe ser una matriz con el mismo número de miembros; de lo contrario, se produce un error. El orden de los nombres de campo debe coincidir con el orden de los valores de campo en cada matriz.  
  
## <a name="remarks"></a>Comentarios  
 Use la **AddNew** método para crear e inicializar un nuevo registro. Use la [admite](../../../ado/reference/ado-api/supports-method.md) método con **adAddNew** (un [CursorOptionEnum](../../../ado/reference/ado-api/cursoroptionenum.md) valor) para comprobar si puede agregar registros a la actual **Recordset**objeto.  
  
 Después de llamar a la **AddNew** método, el nuevo registro se convierte en el registro actual y sigue siendo el actual después de llamar a la [actualización](../../../ado/reference/ado-api/update-method.md) método. Dado que el nuevo registro se anexa a la **Recordset**, una llamada a **MoveNext** tras la actualización moverá más allá del final de la **Recordset**, lo que permite **EOF**  True. Si el **Recordset** objeto no admite marcadores, es podrán que no pueda acceder al registro de nuevo cuando se mueva a otro registro. Dependiendo del tipo de cursor, es posible que deba llamar a la [Requery](../../../ado/reference/ado-api/requery-method.md) método para que sea accesible el nuevo registro.  
  
 Si se llama a **AddNew** mientras modifica el registro actual o agregar un nuevo registro, se llama ADO el **actualización** método para guardarlos cambios y, a continuación, crea el nuevo registro.  
  
 El comportamiento de la **AddNew** método depende del modo de actualización de la **Recordset** objeto y si se pasan los *Fieldlist* y *valores*argumentos.  
  
 En *modo de actualización inmediata* (en el que el proveedor escribe los cambios en el origen de datos subyacente cuando se llama el **actualizar** método), al llamar a la **AddNew** sin (método) conjuntos de argumentos del [EditMode](../../../ado/reference/ado-api/editmode-property.md) propiedad **adEditAdd** (un [EditModeEnum](../../../ado/reference/ado-api/editmodeenum.md) valor). El proveedor almacena en caché localmente los cambios de valor de campo. Una llamada a la **actualización** método envía el nuevo registro a la base de datos y se restablece el **EditMode** propiedad **adEditNone** (un **EditModeEnum**valor). Si se pasa el *Fieldlist* y *valores* argumentos, ADO envía inmediatamente el nuevo registro a la base de datos (no **actualización** es necesario llamar a); el **EditMode**  no cambia el valor de propiedad (**adEditNone**).  
  
 En *modo de actualización por lotes* (en el que el proveedor almacena en caché varios cambios y los escribe en el origen de datos subyacente únicamente cuando se llama el [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) método), al llamar a la **AddNew** método sin argumentos establece el **EditMode** propiedad **adEditAdd**. El proveedor almacena en caché localmente los cambios de valor de campo. Una llamada a la **actualización** método agrega el nuevo registro a la actual **Recordset**, pero el proveedor no envía los cambios a la base de datos subyacente, o restablecer el **EditMode** para **adEditNone**, hasta que llame a la **UpdateBatch** método. Si se pasa el *Fieldlist* y *valores* argumentos, ADO envía el nuevo registro en el proveedor de almacenamiento en una memoria caché y establece el **EditMode** a **adEditAdd** ; debe llamar a la **UpdateBatch** método para registrar el nuevo registro a la base de datos subyacente.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente muestra cómo usar el método AddNew con la lista de campos y la lista de valores incluidos, para ver cómo incluir la lista de campos y una lista de valores como matrices.  
  
```  
create table aa1 (intf int, charf char(10))  
insert into aa1 values (2, 'aa')  
  
Dim cn As New adodb.Connection  
Dim rs As New adodb.Recordset  
Dim cmd As New adodb.Command  
  
cn.ConnectionString = "Provider=SQLOLEDB;Data Source=alexverb2;uid=sa;pwd=foo$bar00;"  
  
cn.Open  
rs.Open "select * from xxx..aa1", cn, adOpenKeyset, adLockOptimistic  
  
Dim fieldsArray(1) As Variant  
fieldsArray(0) = "intf"  
fieldsArray(1) = "charf"  
Dim values(1) As Variant  
values(0) = 4  
values(1) = "as"  
rs.AddNew fieldsArray, values  
rs.Update  
```  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo del método AddNew (VB)](../../../ado/reference/ado-api/addnew-method-example-vb.md)   
 [Ejemplo del método AddNew (VBScript)](../../../ado/reference/ado-api/addnew-method-example-vbscript.md)   
 [Ejemplo del método AddNew (VC ++)](../../../ado/reference/ado-api/addnew-method-example-vc.md)   
 [Método CancelUpdate (ADO)](../../../ado/reference/ado-api/cancelupdate-method-ado.md)   
 [Propiedad EditMode](../../../ado/reference/ado-api/editmode-property.md)   
 [Requery (método)](../../../ado/reference/ado-api/requery-method.md)   
 [Método Supports](../../../ado/reference/ado-api/supports-method.md)   
 [Método de actualización](../../../ado/reference/ado-api/update-method.md)   
 [Método UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)
