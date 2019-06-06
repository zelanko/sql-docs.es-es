---
title: Un proveedor sencillo de OLE DB de Microsoft | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- simple provider [ADO]
- providers [ADO], OLE DB simple provider
- OLE DB simple provider [ADO]
ms.assetid: 1e7dc6f0-482c-4103-8187-f890865e40fc
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: bc17df7bad00205803b33cb4af17cb3c6ddaac56
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2019
ms.locfileid: "66701287"
---
# <a name="microsoft-ole-db-simple-provider-overview"></a>Información general de un proveedor sencillo de OLE DB de Microsoft
Permite que Microsoft OLE DB simples proveedor (OSP) ADO tener acceso a los datos para el que un proveedor se ha escrito utilizando el [Kit de herramientas de OLE DB simples proveedor (OSP)](https://msdn.microsoft.com/6e7b7931-9e4a-4151-ae51-672abd3f84a6). Simple proveedores están diseñados para tener acceso a orígenes de datos que requieren la compatibilidad de OLE DB solo fundamental, como matrices en memoria o documentos XML.

## <a name="connection-string-parameters"></a>Parámetros de cadena de conexión
 Para conectarse a la OLE DB simples DLL del proveedor, establezca el *proveedor* argumento para el [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) propiedad:

```vb
MSDAOSP
```

 Este valor también se puede establecer o leer utilizando el [proveedor](../../../ado/reference/ado-api/provider-property-ado.md) propiedad.

 Puede conectarse a los proveedores de simple que se han registrado con el nombre del proveedor registrado, determinado por el escritor de proveedores como proveedores de OLE DB completos.

## <a name="typical-connection-string"></a>Cadena de conexión típica
 Una cadena de conexión típica para este proveedor es:

```vb
"Provider=MSDAOSP;Data Source=serverName"
```

 La cadena consta de estas palabras clave:

|Palabra clave|Descripción|
|-------------|-----------------|
|**Proveedor**|Especifica el proveedor OLE DB para SQL Server.|
|**Origen de datos**|Especifica el nombre de un servidor.|

## <a name="xml-document-example"></a>Ejemplo de documento XML
 Se ha mejorado la OLE DB simples proveedor (OSP) en MDAC 2.7 o posterior y Windows Data Access Components (Windows DAC) para admitir la apertura ADO jerárquica **conjuntos de registros** a través de los archivos XML arbitrarios. Estos archivos XML pueden contener el esquema de persistencia de XML de ADO, pero no es necesario. Esto se ha implementado mediante la conexión de la OSP a la **MSXML2.DLL**; por lo tanto **MSXML2.DLL** o posterior es necesario.

 El **portfolio.xml** archivo usado en el ejemplo siguiente contiene el árbol de la siguiente:

```console
Portfolio
   Stock
      Shares
      Symbol
      Price
      Info
         Company Name
         WebSite
```

 DSO XML utiliza la heurística integrada para convertir los nodos de un árbol XML a los capítulos jerárquica **Recordset**.

 Con estas heurísticas integradas, el árbol XML se convierte en un nivel dos jerárquico **Recordset** de la forma siguiente:

```console
Parent Recordset
Shares, Symbol, Price, $Text
   Child Recordset
      Company Name, WebSite, $Text
```

 Tenga en cuenta que las etiquetas de cartera y la información no se representan en el jerárquica **Recordset**. Para obtener una explicación de cómo los DSO XML convierte árboles XML a jerárquica **conjuntos de registros**, vea las siguientes reglas. La columna $Text se describe en la sección siguiente.

## <a name="rules-for-assigning-xml-elements-and-attributes-to-columns-and-rows"></a>Reglas de asignación de elementos y atributos XML en columnas y filas
 DSO XML sigue un procedimiento para asignar los elementos y atributos para columnas y filas en las aplicaciones enlazadas a datos. XML se modela como un árbol con una etiqueta que contiene toda la jerarquía. Por ejemplo, una descripción XML de un libro podría contener etiquetas del capítulo, figura etiquetas y las etiquetas de sección. En el nivel más alto sería la etiqueta del libro, que contiene la figura, la sección y el capítulo de subelementos. Cuando los DSO XML asigna los elementos XML en filas y columnas, se convierten los subelementos, no el elemento de nivel superior.

 El XML de DSO utiliza este procedimiento para convertir los subelementos:

-   Cada subelemento y un atributo corresponde a una columna en algunos **Recordset** en la jerarquía.

-   El nombre de la columna es el mismo que el nombre del subelemento o atributo, a menos que el elemento primario tiene un atributo y un subelemento con el mismo nombre, en cuyo caso un "!" se antepone al nombre de columna del subelemento.

-   Cada columna sea un *simple* columna que contiene valores escalares (normalmente las cadenas) o un **Recordset** columna que contiene el elemento secundario **conjuntos de registros**.

-   Las columnas correspondientes a los atributos son siempre simples.

-   Son las columnas correspondientes a los subelementos **Recordset** columnas si el subelemento tiene su propio subelementos o atributos (o ambos), o elemento primario del subelemento tiene más de una instancia del subelemento como elemento secundario. En caso contrario, la columna es sencilla.

-   Cuando hay varias instancias de un subelemento (de primarios diferentes), la columna es una **Recordset** columna si *cualquier* de las instancias implica un **Recordset** columna; su es sencilla columna solo si *todas* instancias implican una columna simple.

-   Todos los **conjuntos de registros** tiene una columna adicional denominada $Text.

 El código que se necesita para construir un **Recordset** es como sigue:

```vb
Dim adoConn as ADODB.Connection
Dim adoRS as ADODB.Recordset

Set adoRS = New ADODB.Connection
Set adoRS = New ADODB.Recordset

adoConn.Open "Provider=MSDAOSP; Data Source=MSXML2.DSOControl.2.6;"
adoRS.Open "https://WebServer/VRoot/portfolio.xml, adoConn
```

> [!NOTE]
>  La ruta de acceso del archivo de datos se puede especificar con cuatro distintas convenciones de nomenclatura.

```vb
'HTTP://
adoRS.Open "https://WebServer/VRoot/portfolio.xml", adoConn
'FILE://
adoRS.Open "file:/// C:\\Directory\\portfolio.xml", adoConn
'UNC Path
adoRS.Open "\\ComputerName\ShareName\portfolio.xml", adoConn
'Full DOS Path
adoRS.Open "C:\Directory\portfolio.xml", adoConn
```

 Tan pronto como el **Recordset** se ha abierto, el ADO habitual **Recordset** se pueden usar comandos de navegación.

 **Conjuntos de registros** generados por la OSP tiene algunas limitaciones:

-   Los cursores del cliente (**adUseClient**) no se admiten.

-   Jerárquica **conjuntos de registros** creado sobre arbitrario XML no puede ser persistente mediante **Recordset.Save**.

-   **Conjuntos de registros** creado con la OSP son de solo lectura.

-   El XMLDSO agrega una columna de datos ($Text) adicional a cada **Recordset** en la jerarquía.

 Para obtener más información sobre el proveedor OLE DB simples, consulte [creación de un proveedor Simple](https://msdn.microsoft.com/b31a6cba-58ae-4ee8-9039-700973d354d6).

## <a name="code-example"></a>Ejemplo de código
 El siguiente código de Visual Basic muestra cómo abrir un archivo XML arbitrario, construir jerárquica **Recordset**y escribir cada registro de cada uno de forma recursiva **Recordset** a la ventana de depuración.

 Este es un archivo XML simple que contiene las cotizaciones de acciones. El siguiente código usa este archivo para construir un nivel dos jerárquico **Recordset**.

```xml
<portfolio>
   <stock>
      <shares>100</shares>
      <symbol>MSFT</symbol>
      <price>$70.00</price>
      <info>
         <companyname>Microsoft Corporation</companyname>
         <website>https://www.microsoft.com</website>
      </info>
   </stock>
   <stock>
      <shares>100</shares>
      <symbol>AAPL</symbol>
      <price>$107.00</price>
      <info>
         <companyname>Apple Computer, Inc.</companyname>
         <website>https://www.apple.com</website>
      </info>
   </stock>
   <stock>
      <shares>100</shares>
      <symbol>DELL</symbol>
      <price>$50.00</price>
      <info>
         <companyname>Dell Corporation</companyname>
         <website>https://www.dell.com</website>
      </info>
    </stock>
    <stock>
       <shares>100</shares>
       <symbol>INTC</symbol>
       <price>$115.00</price>
       <info>
          <companyname>Intel Corporation</companyname>
          <website>https://www.intel.com</website>
       </info>
   </stock>
</portfolio>
```

 Los siguientes son dos procedimientos sub en Visual Basic. Crea la primera la **Recordset** y lo pasa a la *WalkHier* sub procedimiento, qué recursiva inferiores de la jerarquía, cada escritura **campo** en cada registro de cada uno **Recordset** a la ventana de depuración.

```vb
Private Sub BrowseHierRecordset()
' Add ADO 2.7 or later to Project/References
' No need to add MSXML2, ADO just passes the ProgID through to the OSP.

    Dim adoConn As ADODB.Connection
    Dim adoRS As ADODB.Recordset
    Dim adoChildRS As ADODB.Recordset

    Set adoConn = New ADODB.Connection
    Set adoRS = New ADODB.Recordset
    Set adoChildRS = ADODB.Recordset

    adoConn.Open "Provider=MSDAOSP; Data Source=MSXML2.DSOControl.2.6;"
    adoRS.Open "https://bwillett3/Kowalski/portfolio.xml", adoConn

    Dim iLevel As Integer
    iLevel = 0
    WalkHier iLevel, adoRS

End Sub

Sub WalkHier(ByVal iLevel As Integer, ByVal adoRS As ADODB.Recordset)
    iLevel = iLevel + 1
    PriorLevel = iLevel
    While Not adoRS.EOF
        For ndx = 0 To adoRS.Fields.Count - 1
            If adoRS.Fields(ndx).Name <> "$Text" Then
                If adoRS.Fields(ndx).Type = adChapter Then
                    Set adoChildRS = adoRS.Fields(ndx).Value
                    WalkHier iLevel, adoChildRS
                Else
                    Debug.Print iLevel & ": adoRS.Fields(" & ndx & _
                       ") = " & adoRS.Fields(ndx).Name & " = " & _
                       adoRS.Fields(ndx).Value
                End If
            End If
        Next ndx
        adoRS.MoveNext
    Wend
    iLevel = PriorLevel
End Sub
```
