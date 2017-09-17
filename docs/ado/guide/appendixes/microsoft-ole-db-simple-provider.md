---
title: Un proveedor sencillo de Microsoft OLE DB | Documentos de Microsoft
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
- simple provider [ADO]
- providers [ADO], OLE DB simple provider
- OLE DB simple provider [ADO]
ms.assetid: 1e7dc6f0-482c-4103-8187-f890865e40fc
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b81dae92dcb8f6493fd6d6c74515750d4e4a0f66
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="microsoft-ole-db-simple-provider-overview"></a>Información general de un proveedor sencillo de OLE DB de Microsoft
El Microsoft OLE DB sencillo proveedor (OSP) permite que ADO tener acceso a los datos para el que un proveedor se ha escrito utilizando la [Kit de herramientas de OLE DB Simple proveedor (OSP)](http://msdn.microsoft.com/en-us/6e7b7931-9e4a-4151-ae51-672abd3f84a6). Simples proveedores están diseñados para tener acceso a orígenes de datos que requieren un soporte OLE DB solo fundamental, como matrices en memoria o documentos XML.

## <a name="connection-string-parameters"></a>Parámetros de cadena de conexión
 Para conectarse a la OLE DB simples DLL del proveedor, establezca el *proveedor* argumento pasado a la [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) propiedad:

```
MSDAOSP
```

 Este valor también se puede establecer o leer utilizando el [proveedor](../../../ado/reference/ado-api/provider-property-ado.md) propiedad.

 Puede conectar con proveedores de simples que se han registrado como proveedores de OLE DB completos mediante el nombre de proveedor registrado, determinado por el sistema de escritura de proveedor.

## <a name="typical-connection-string"></a>Cadena de conexión típica
 Una cadena de conexión típica para este proveedor es:

```
"Provider=MSDAOSP;Data Source=serverName"
```

 La cadena consta de estas palabras clave:

|Palabra clave|Description|
|-------------|-----------------|
|**Proveedor**|Especifica el proveedor OLE DB para SQL Server.|
|**Origen de datos**|Especifica el nombre de un servidor.|

## <a name="xml-document-example"></a>Ejemplo de documento XML
 El OLE DB Simple proveedor (OSP) de MDAC 2.7 o posterior y Windows Data Access Components (Windows DAC) se ha mejorado para admitir la apertura de ADO jerárquica **conjuntos de registros** en archivos XML arbitrarios. Estos archivos XML pueden contener el esquema de persistencia XML de ADO, pero no es necesario. Esto se ha implementado mediante la conexión la OSP a la **MSXML2.DLL**; por lo tanto, **MSXML2.DLL** o posterior es necesario.

 El **portfolio.xml** archivo usado en el ejemplo siguiente contiene el siguiente árbol:

```
Portfolio
   Stock
      Shares
      Symbol
      Price
      Info
         Company Name
         WebSite
```

 El XML utiliza heurística integrada para convertir los nodos de un árbol XML a los capítulos jerárquica **conjunto de registros**.

 Mediante estos métodos heurísticos integradas, el árbol XML se convierte en un nivel dos jerárquico **Recordset** de la forma siguiente:

```
Parent Recordset
Shares, Symbol, Price, $Text
   Child Recordset
      Company Name, WebSite, $Text
```

 Tenga en cuenta que las etiquetas de cartera e información no se representan en el jerárquica **conjunto de registros**. Para obtener una explicación de cómo el DSO XML convierte árboles XML en jerárquica **conjuntos de registros**, vea las siguientes reglas. La columna $Text se describe en la sección siguiente.

## <a name="rules-for-assigning-xml-elements-and-attributes-to-columns-and-rows"></a>Reglas para asignar elementos y atributos XML a las columnas y filas
 DSO XML sigue un procedimiento para asignar elementos y atributos para columnas y filas en aplicaciones enlazadas a datos. XML se modela como un árbol con una etiqueta que contiene toda la jerarquía. Por ejemplo, una descripción XML de un libro podría contener etiquetas de capítulo, etiquetas de figura y etiquetas de sección. En el nivel más alto sería la etiqueta del libro, que contiene el capítulo de subelementos, la figura y la sección. Cuando el DSO XML asigna elementos XML en filas y columnas, se convierten los subelementos no complejos, no el elemento de nivel superior.

 El XML utiliza este procedimiento para convertir los subelementos no complejos:

-   Cada subelemento y el atributo corresponde a una columna en algunos **Recordset** en la jerarquía.

-   El nombre de la columna es el mismo que el nombre del subelemento o atributo, a menos que el elemento primario tiene un atributo y un elemento secundario con el mismo nombre, en cuyo caso un "!" se antepone al nombre de columna del subelemento.

-   Cada columna sea un *simple* columna que contiene valores escalares (normalmente cadenas) o un **Recordset** columna que contiene el elemento secundario **conjuntos de registros**.

-   Las columnas correspondientes a los atributos son siempre simples.

-   Las columnas correspondientes a los subelementos están **Recordset** columnas si el subelemento tiene sus propio subelementos o atributos (o ambos), o elemento primario del subelemento tiene más de una instancia del subelemento como un elemento secundario. En caso contrario, la columna es simple.

-   Cuando hay varias instancias de un subelemento (en diferentes objetos primarios), la columna es una **Recordset** columna si *cualquier* de las instancias implica un **Recordset** columna; su columna es sencilla solo si *todos los* instancias implican una columna simple.

-   Todos los **conjuntos de registros** tiene una columna adicional denominada $Text.

 El código que se necesita para construir un **Recordset** es como sigue:

```
Dim adoConn as ADODB.Connection
Dim adoRS as ADODB.Recordset

Set adoRS = New ADODB.Connection
Set adoRS = New ADODB.Recordset

adoConn.Open "Provider=MSDAOSP; Data Source=MSXML2.DSOControl.2.6;"
adoRS.Open "http://WebServer/VRoot/portfolio.xml, adoConn
```

> [!NOTE]
>  La ruta de acceso del archivo de datos se puede especificar utilizando cuatro distintas convenciones de nomenclaturas.

```
'HTTP://
adoRS.Open "http://WebServer/VRoot/portfolio.xml", adoConn
'FILE://
adoRS.Open "file:/// C:\\Directory\\portfolio.xml", adoConn
'UNC Path
adoRS.Open "\\ComputerName\ShareName\portfolio.xml", adoConn
'Full DOS Path
adoRS.Open "C:\Directory\portfolio.xml", adoConn
```

 Tan pronto como el **Recordset** se ha abierto, el ADO habitual **Recordset** se pueden usar comandos de navegación.

 **Conjuntos de registros** generados por la OSP tienen algunas limitaciones:

-   Los cursores del cliente (**adUseClient**) no se admiten.

-   Jerárquica **conjuntos de registros** crea sobre arbitrario XML no puede ser persistentes con **Recordset.Save**.

-   **Conjuntos de registros** creado con la OSP son de solo lectura.

-   El XMLDSO agrega una columna adicional de datos ($Text) a cada uno **Recordset** en la jerarquía.

 Para obtener más información sobre el proveedor OLE DB simples, consulte [crear un proveedor Simple](http://msdn.microsoft.com/en-us/b31a6cba-58ae-4ee8-9039-700973d354d6).

## <a name="code-example"></a>Ejemplo de código
 El siguiente código de Visual Basic, se muestra cómo abrir un archivo XML arbitrario, construir jerárquica **Recordset**y escribir cada registro de cada uno de ellos de forma recursiva **Recordset** a la ventana de depuración.

 Este es un archivo XML simple que contiene cotizaciones. El código siguiente usa este archivo para construir un jerárquica de dos niveles **conjunto de registros**.

```
<portfolio>
   <stock>
      <shares>100</shares>
      <symbol>MSFT</symbol>
      <price>$70.00</price>
      <info>
         <companyname>Microsoft Corporation</companyname>
         <website>http://www.microsoft.com</website>
      </info>
   </stock>
   <stock>
      <shares>100</shares>
      <symbol>AAPL</symbol>
      <price>$107.00</price>
      <info>
         <companyname>Apple Computer, Inc.</companyname>
         <website>http://www.apple.com</website>
      </info>
   </stock>
   <stock>
      <shares>100</shares>
      <symbol>DELL</symbol>
      <price>$50.00</price>
      <info>
         <companyname>Dell Corporation</companyname>
         <website>http://www.dell.com</website>
      </info>
    </stock>
    <stock>
       <shares>100</shares>
       <symbol>INTC</symbol>
       <price>$115.00</price>
       <info>
          <companyname>Intel Corporation</companyname>
          <website>http://www.intel.com</website>
       </info>
   </stock>
</portfolio>
```

 Los siguientes son dos procedimientos sub en Visual Basic. El primero se crea el **Recordset** y lo pasa a la *WalkHier* sub procedimiento, qué recursiva hacia abajo en la jerarquía, escribir cada **campo** en cada registro de cada uno **Recordset** a la ventana de depuración.

```
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
    adoRS.Open "http://bwillett3/Kowalski/portfolio.xml", adoConn

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

