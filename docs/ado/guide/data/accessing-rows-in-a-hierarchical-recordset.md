---
title: Obtener acceso a las filas de un conjunto de registros jerárquico | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- hierarchical Recordsets [ADO]
- data shaping [ADO], hierarchical Recordsets
ms.assetid: 25f1d2a1-6d5e-4457-aa07-5db5c75dee18
author: rothja
ms.author: jroth
ms.openlocfilehash: 2eacfa8122589dbf594040f3279d466ef9c113cd
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2020
ms.locfileid: "82761493"
---
# <a name="accessing-rows-in-a-hierarchical-recordset-example"></a>Obtener acceso a las filas de un conjunto de registros jerárquico (ejemplo)
En el ejemplo siguiente se muestran los pasos necesarios para tener acceso a las filas de un [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md)jerárquico:

1.  Los objetos de **conjunto de registros** de las tablas **authors** y **TITLEAUTHOR** están relacionados con el identificador de autor.

2.  El bucle exterior muestra el nombre y el apellido de cada autor, el estado y la identificación.

3.  El conjunto de **registros** anexado para cada fila se recupera de la colección [Fields](../../../ado/reference/ado-api/fields-collection-ado.md) y se asigna a *rstTitleAuthor*.

4.  El bucle interno muestra cuatro campos de cada fila del **conjunto de registros**anexado.

 La propiedad [StayInSync](../../../ado/reference/ado-api/stayinsync-property.md) está establecida en **false** para fines ilustrativos, de modo que puede ver el cambio de capítulo explícitamente en cada iteración del bucle exterior. Para que el ejemplo de código sea más eficaz, puede pasar la asignación en el paso 3 antes de la primera línea del paso 2, de modo que la asignación se realice solo una vez. A continuación, establezca la propiedad [StayInSync](../../../ado/reference/ado-api/stayinsync-property.md) en **true**para que *rstTitleAuthor* cambie implícita y automáticamente al capítulo correspondiente siempre que *RST* se mueva a una nueva fila.

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

## <a name="see-also"></a>Consulte también
 [Información general sobre](../../../ado/guide/data/data-shaping-overview.md) la forma de datos colección de campos de [objeto de campo](../../../ado/reference/ado-api/field-object.md) [(ADO)](../../../ado/reference/ado-api/fields-collection-ado.md) [gramática de forma Formal](../../../ado/guide/data/formal-shape-grammar.md) [servicio de forma de datos de OLE DB (proveedor de servicios ADO)](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) [objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md) [proveedores necesarios para la forma de datos](../../../ado/guide/data/required-providers-for-data-shaping.md) los comandos de forma de la [cláusula Append](../../../ado/guide/data/shape-append-clause.md) [de forma general en](../../../ado/guide/data/shape-commands-in-general.md) [las funciones](../../../ado/guide/data/visual-basic-for-applications-functions.md) de la [cláusula COMPUTE de Shape](../../../ado/guide/data/shape-compute-clause.md) Visual Basic para aplicaciones
