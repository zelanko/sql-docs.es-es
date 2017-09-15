---
title: "Obtener acceso a filas de un conjunto de registros jerárquico | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: H1Hack27Feb2017
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- hierarchical Recordsets [ADO]
- data shaping [ADO], hierarchical Recordsets
ms.assetid: 25f1d2a1-6d5e-4457-aa07-5db5c75dee18
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1107c5c4aafb0a2e661bbc1307f9aea71b278270
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="accessing-rows-in-a-hierarchical-recordset-example"></a>Acceso a las filas en un conjunto de registros jerárquico (ejemplo)
En el ejemplo siguiente se muestra los pasos necesarios para el acceso a filas en una jerárquica [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md):

1.  **Conjunto de registros** objetos desde la **autores** y **titleauthor** tablas están relacionadas por identificador de autor.

2.  El bucle externo muestra el nombre y apellido de cada autor, estado e identificación.

3.  Anexa **Recordset** para cada fila se recupera de la [campos](../../../ado/reference/ado-api/fields-collection-ado.md) colección y se asigna a *rstTitleAuthor*.

4.  El bucle interno muestra cuatro campos de cada fila en anexa **conjunto de registros**.

 El [StayInSync](../../../ado/reference/ado-api/stayinsync-property.md) propiedad está establecida en **false** a efectos de ilustración, para que puedan ver el capítulo cambiar explícitamente en cada iteración del bucle externo. Para hacer que el ejemplo de código más eficaz, puede mover la asignación en el paso 3 antes de la primera línea en el paso 2, para que la asignación se realiza solo una vez. A continuación, establezca el [StayInSync](../../../ado/reference/ado-api/stayinsync-property.md) propiedad **true**, de modo que *rstTitleAuthor* cambie implícita y automáticamente al capítulo correspondiente siempre que *rst* se mueve a una nueva fila.

## <a name="example"></a>Ejemplo

```
Sub datashape()
   Dim cnn As New ADODB.Connection
   Dim rst As New ADODB.Recordset
   Dim rstTitleAuthor As New ADODB.Recordset

   cnn.Provider = "MSDataShape"
   cnn.Open    "Data Provider=MSDASQL;" & _
               "Data Source=SRV;Integrated Security=SSPI;Database=Pubs"
' STEP 1
   rst.StayInSync = FALSE
   rst.Open    "SHAPE  {select * from authors} "  & _
               "APPEND ({select * from titleauthor} " & _
               "RELATE au_id TO au_id) AS chapTitleAuthor", _
               cnn
' STEP 2
   While Not rst.EOF
      Debug.Print    rst("au_fname"), rst("au_lname"), _
                     rst("state"), rst("au_id")
' STEP 3
      Set rstTitleAuthor = rst("chapTitleAuthor").Value
' STEP 4
      While Not rstTitleAuthor.EOF
         Debug.Print rstTitleAuthor(0), rstTitleAuthor(1), _
                     rstTitleAuthor(2), rstTitleAuthor(3)
         rstTitleAuthor.MoveNext
      Wend
      rst.MoveNext
   Wend
End Sub
```

## <a name="see-also"></a>Vea también
 [Información general sobre la forma de datos](../../../ado/guide/data/data-shaping-overview.md) [objeto Field](../../../ado/reference/ado-api/field-object.md) [(ADO) de la colección de campos](../../../ado/reference/ado-api/fields-collection-ado.md) [gramática Formal forma](../../../ado/guide/data/formal-shape-grammar.md) [para dar forma al servicio de datos de Microsoft OLE DB (proveedor de servicios ADO)](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) [objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md) [proveedores necesarios para dar forma a datos](../../../ado/guide/data/required-providers-for-data-shaping.md) [cláusula APPEND de forma](../../../ado/guide/data/shape-append-clause.md) [Forma comandos en General](../../../ado/guide/data/shape-commands-in-general.md) [cláusula COMPUTE de forma](../../../ado/guide/data/shape-compute-clause.md) [de Visual Basic para las funciones de aplicaciones](../../../ado/guide/data/visual-basic-for-applications-functions.md)

