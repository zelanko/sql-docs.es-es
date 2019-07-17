---
title: La colección Fields | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Field object [ADO], fields collection
- Fields collection [ADO]
ms.assetid: 574cf36e-e5f5-403b-983c-749ef93c108f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 197a57b8a9b9ea2927a057733992a02c731a335a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67923932"
---
# <a name="the-fields-collection"></a>Fields (colección)
El **campos** colección es una de las colecciones de ADO intrínsecas. Una colección es un conjunto ordenado de elementos que se puede hacer referencia como una unidad. Para obtener más información acerca de las colecciones de ADO, vea [el modelo de objetos ADO](../../../ado/guide/data/ado-objects-and-collections.md).  
  
 El **campos** colección contiene un **campo** de objeto para cada campo (columna) en el **Recordset**. Al igual que todas las colecciones de ADO, tiene **recuento** y **elemento** propiedades, así como **Append** y **actualizar** métodos. También tiene **CancelUpdate**, **eliminar**, **Resync**, y **actualización** métodos, que no están disponibles para otras colecciones de ADO.  
  
## <a name="examining-the-fields-collection"></a>Examen de la colección de campos  
 Tenga en cuenta la **campos** colección del ejemplo **Recordset** introducidas en esta sección. El ejemplo **Recordset** se derivó de la instrucción SQL  
  
```  
SELECT ProductID, ProductName, UnitPrice FROM Products WHERE CategoryID = 7  
```  
  
 Por lo tanto, debe buscar el **Recordset Fields** conjunto contiene tres campos.  
  
```  
'BeginWalkFields  
    Dim objFields As ADODB.Fields  
    Dim intLoop As Integer  
  
    objRs.Open strSQL, strConnStr, adOpenForwardOnly, adLockReadOnly, adCmdText  
  
    Set objFields = objRs.Fields  
  
    For intLoop = 0 To (objFields.Count - 1)  
        Debug.Print objFields.Item(intLoop).Name  
    Next  
'EndWalkFields  
```  
  
 Este código simplemente determina el número de **campo** objetos en el **campos** colección utilizando el **recuento** propiedad y recorre la colección y devuelve el valor de el **nombre** propiedad para cada **campo** objeto. Puede usar muchos más **campo** propiedades para obtener información acerca de un campo. Para obtener más información sobre cómo consultar un **campo**, consulte [el objeto de campo](../../../ado/guide/data/the-field-object.md).  
  
## <a name="counting-columns"></a>Recuento de columnas  
 Como cabría esperar, el **recuento** propiedad devuelve el número real de **campo** objetos en el **campos** colección. Dado que la numeración de los miembros de una colección comienza con cero, siempre se deben codificar bucles empezando por el miembro cero y terminando con el valor de la **recuento** propiedad menos 1. Si está utilizando Microsoft Visual Basic y desea recorrer los miembros de una colección sin comprobar en el **recuento** propiedad, utilice el **For Each... Siguiente** comando.  
  
 Si el **recuento** propiedad es cero, no hay ningún objeto en la colección.  
  
## <a name="getting-to-the-field"></a>Introducción al campo  
 Al igual que con cualquier colección de ADO, la **elemento** propiedad es la propiedad predeterminada de la colección. Devuelve el individuo **campo** objeto especificado por el nombre o índice que se pasa a él. Por lo tanto, las instrucciones siguientes son equivalentes para el ejemplo **Recordset**:  
  
```  
objField = objRecordset.Fields.Item("ProductID")  
objField = objRecordset.Fields("ProductID")  
objField = objRecordset.Fields.Item(0)  
objField = objRecordset.Fields(0)  
```  
  
 ¿Si estos métodos son equivalentes, que es mejor? Depende. Usar un índice para recuperar un **campo** de la colección es más rápido porque tiene acceso a la **campo** directamente sin tener que realizar una búsqueda de cadena. Por otro lado, el orden de **campos** debe conocerse dentro de la colección, y si se cambia el orden, la referencia a la **del campo** índice tendrán que cambiarse siempre que aparece. Aunque un poco más lento, con el nombre de la **campo** es más flexible porque no depende en el orden de los **campos** en la colección.  
  
## <a name="using-the-refresh-method"></a>Mediante el método de actualización  
 A diferencia de otras colecciones de ADO, utilizando el **actualizar** método en el **campos** colección no tiene ningún efecto visible. Para recuperar los cambios de la estructura subyacente de la base de datos, debe usar el **Requery** método, o si el **Recordset** objeto no admite marcadores, el **MoveFirst**método, lo que hará que el comando se ejecute en el proveedor de nuevo.  
  
## <a name="adding-fields-to-a-recordset"></a>Agregar campos a un conjunto de registros  
 El **Append** método se utiliza para agregar campos a un **Recordset**.  
  
 Puede usar el **Append** método para crear un **Recordset** mediante programación sin tener que abrir una conexión a un origen de datos. Se producirá un error de tiempo de ejecución si el **Append** se llama al método en el **campos** colección de una abierta **Recordset** o en un **Recordset** donde el **ActiveConnection** se estableció la propiedad. Se pueden anexar campos solo a un **Recordset** que no está abierto y aún no se ha conectado a un origen de datos. Sin embargo, para especificar valores para los recién anexados **campos**, el **Recordset** primero deben estar abiertos.  
  
 Los desarrolladores suelen necesitan un lugar para almacenar algunos datos temporalmente o desea algunos datos para que actúe como si provinieran de un servidor por lo que ésta pueda participar en el enlace de datos en una interfaz de usuario. ADO (junto con el [servicio de cursores de Microsoft para OLE DB](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)) permite al programador crear vacío **Recordset** objeto especificando la información de columna y llamando a **abrir**. En el ejemplo siguiente, se anexan tres nuevos campos a un nuevo **Recordset** objeto. El **Recordset** se abre, dos nuevos registros se agregan y el **Recordset** se almacenan en un archivo. (Para obtener más información acerca de **Recordset** persistencia, consulte [actualizar y conservar datos](../../../ado/guide/data/updating-and-persisting-data.md).)  
  
```  
'BeginFabricate  
    Dim objRs As ADODB.Recordset  
    Set objRs = New ADODB.Recordset  
  
    With objRs.Fields  
        .Append "StudentID", adChar, 11, adFldUpdatable  
        .Append "FullName", adVarChar, 50, adFldUpdatable  
        .Append "PhoneNmbr", adVarChar, 20, adFldUpdatable  
    End With  
  
    With objRs  
        .Open  
  
        .AddNew  
        .Fields(0) = "123-45-6789"  
        .Fields(1) = "John Doe"  
        .Fields(2) = "(425) 555-5555"  
        .Update  
  
        .AddNew  
        .Fields(0) = "123-45-6780"  
        .Fields(1) = "Jane Doe"  
        .Fields(2) = "(615) 555-1212"  
        .Update  
    End With  
  
    objRs.Save App.Path & "FabriTest.adtg", adPersistADTG  
  
    objRs.Close  
'EndFabricate  
```  
  
 El uso de la **anexar campos** método difiere entre el **Recordset** objeto y el **registro** objeto. Para obtener más información sobre la **registro** de objetos, consulte [registros y secuencias](../../../ado/guide/data/records-and-streams.md).  
  
## <a name="see-also"></a>Vea también  
 [Fabricación de conjuntos de registros jerárquicos](../../../ado/guide/data/fabricating-hierarchical-recordsets.md)
