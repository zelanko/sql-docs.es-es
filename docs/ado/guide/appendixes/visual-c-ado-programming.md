---
title: Programación ADO en Visual C++ | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- ADO, Visual C++
- Visual C++ [ADO]
ms.assetid: 11233b96-e05c-4221-9aed-5f20944b0f1c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e1b34c2b88c8e1906438f706143fcf6ec966026d
ms.sourcegitcommit: fa2f85b6deeceadc0f32aa7f5f4e2b6e4d99541c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/03/2019
ms.locfileid: "53997597"
---
# <a name="visual-c-ado-programming"></a>Programación ADO en Visual C++
La referencia de API de ADO describe la funcionalidad de la interfaz de programación de aplicaciones (API) de ADO mediante una sintaxis similar a Microsoft Visual Basic. Aunque el público objetivo son todos los usuarios, los programadores de ADO emplean diversos lenguajes como Visual Basic, Visual C++ (con y sin la **#import** directiva) y Visual J ++ (con el paquete de clase ADO y WFC).  

> [!NOTE]
> Microsoft terminó de soporte técnico para Visual J ++ en 2004.

 Para dar cabida a esta diversidad, el [ADO para índices de sintaxis de Visual C++](../../../ado/guide/appendixes/using-ado-with-microsoft-visual-c.md) proporcionar vínculos a descripciones comunes de funcionalidad, parámetros, comportamientos excepcionales y así sucesivamente, en la API de sintaxis específica del lenguaje de Visual C++ Referencia.  
  
 ADO se implementa con interfaces COM (Component Object Model). Sin embargo, resulta más fácil para los programadores trabajar con COM en algunos lenguajes de programación que otras. Por ejemplo, casi todos los detalles de uso de COM se tratan implícitamente para programadores de Visual Basic, mientras que los programadores de Visual C++ deben ocuparse de esos detalles.  
  
 Las siguientes secciones resumen la información para programadores de C y C++ con ADO y el **#import** directiva. Se centra en los tipos de datos específicos de COM (**Variant**, **BSTR**, y **SafeArray**) y control de errores (_com_error).  
  
## <a name="using-the-import-compiler-directive"></a>Usar la directiva de compilador #import  
 El **#import** directiva de compilador de Visual C++ simplifica el trabajo con las propiedades y métodos de ADO. La directiva toma el nombre de un archivo que contenga una biblioteca de tipos, por ejemplo, la DLL de ADO (Msado15.dll) y genera archivos de encabezado que contienen declaraciones typedef, punteros inteligentes para las interfaces y constantes enumeradas. Cada interfaz está encapsulado o encapsulado en una clase.  
  
 Para cada operación dentro de una clase (es decir, una llamada de método o propiedad), hay una declaración para llamar a la operación directamente (es decir, la forma "sin procesar" de la operación) y una declaración para llamar a la operación sin procesar y generar un error de COM si la operación no se puede ejecutar succ essfully. Si la operación es una propiedad, suele haber una directiva de compilador que crea una sintaxis alternativa para la operación que tiene una sintaxis similar a Visual Basic.  
  
 Las operaciones que recuperan el valor de una propiedad tienen nombres de la forma **obtener**_propiedad_. Las operaciones que establecen el valor de una propiedad tienen nombres de la forma, **colocar**_propiedad_. Las operaciones que establecen el valor de una propiedad con un puntero a un objeto ADO tienen nombres de la forma, **PutRef**_propiedad_.  
  
 Puede obtener o establecer una propiedad con llamadas de estas formas:  
  
```cpp
variable = objectPtr->GetProperty(); // get property value   
objectPtr->PutProperty(value);       // set property value  
objectPtr->PutRefProperty(&value);   // set property with object pointer  
```
  
## <a name="using-property-directives"></a>Propiedad directivas using  
 El **__declspec(property...)**  directiva de compilador es una extensión del lenguaje C específicas de Microsoft que declara una función utilizada como una propiedad que tenga una sintaxis alternativa. Como resultado, puede establecer u obtener valores de una propiedad de una manera similar a Visual Basic. Por ejemplo, puede establecer y obtener una propiedad de este modo:  
  
```cpp
objectPtr->property = value;        // set property value  
variable = objectPtr->property;     // get property value  
```
  
 Tenga en cuenta que no es necesario código:  
  
```cpp
objectPtr->PutProperty(value);      // set property value  
variable = objectPtr->GetProperty;  // get property value  
```
  
 El compilador generará adecuado **obtener**_-_, **colocar**-, o **PutRef**_propiedad_ llamada según la sintaxis alternativa declarada y si se va la propiedad de lectura o escritura.  
  
 El **__declspec(property...)**  solo puede declarar la directiva de compilador **obtener**, **colocar**, o **obtener** y **colocar** sintaxis alternativa para una función. Operaciones de solo lectura, solo tienen un **obtener** declaración; las operaciones de solo escritura solo tiene un **colocar** declaración; las operaciones que son ambos leen y escriben tienen ambos **obtener** y **colocar** declaraciones.  
  
 Solo dos declaraciones son posibles con esta directiva. Sin embargo, cada propiedad tiene tres funciones: **Obtener**_propiedad_, **colocar**_propiedad_, y **PutRef**_propiedad_. En ese caso, solo dos formas de la propiedad tienen la sintaxis alternativa.  
  
 Por ejemplo, el **comando** objeto **ActiveConnection** propiedad se declara con una sintaxis alternativa para **obtener**_ActiveConnection_y **PutRef**_ActiveConnection_. El **PutRef**-sintaxis es una buena elección porque en la práctica, normalmente desea colocar una apertura **conexión** objeto (es decir, un **conexión** puntero de objeto) en este propiedad. Por otro lado, el **Recordset** objeto tiene **obtener**-, **colocar**-, y **PutRef**_ActiveConnection_las operaciones, pero sin sintaxis alternativa.  
  
## <a name="collections-the-getitem-method-and-the-item-property"></a>Colecciones, GetItem (método) y la propiedad del elemento  
 ADO define varias colecciones, incluidas **campos**, **parámetros**, **propiedades**, y **errores**. En Visual C++, el **GetItem (_índice_)** método devuelve un miembro de la colección. *Índice* es un **Variant**, cuyo valor es un índice numérico del miembro de la colección, o una cadena que contiene el nombre del miembro.  
  
 El **__declspec(property...)**  directiva de compilador declara el **elemento** fundamental de la propiedad como una sintaxis alternativa para cada colección **GetItem()** método. La sintaxis alternativa utiliza corchetes y es similar a una referencia de la matriz. En general, los dos formularios de aspecto similar al siguiente:  
  
```cpp
  
      collectionPtr->GetItem(index);  
collectionPtr->Item[index];  
```
  
 Por ejemplo, asignar un valor a un campo de un **Recordset** objeto, denominado  **_rs_**, derivada de la **autores** tabla de la **pubs** base de datos. Use la **Item()** propiedad para tener acceso a la tercera **campo** de la **Recordset** objeto **campos** colección (las colecciones se indizan de cero; Suponga que el tercer campo se denomina  **_au\_fname_**). A continuación, llame a la **Value()** método en el **campo** objeto para asignar un valor de cadena.  
  
 Esto se puede expresar en Visual Basic en los siguientes cuatro maneras (los dos últimos formularios son exclusivos de Visual Basic; otros lenguajes no tienen equivalentes):  
  
```cpp
rs.Fields.Item(2).Value = "value"  
rs.Fields.Item("au_fname").Value = "value"  
rs(2) = "value"  
rs!au_fname = "value"  
```
  
 Es el equivalente en Visual C++ para los dos primeros formularios anteriores:  
  
```cpp
rs->Fields->GetItem(long(2))->PutValue("value");   
rs->Fields->GetItem("au_fname")->PutValue("value");  
```
  
 -o bien - (la sintaxis alternativa para el **valor** también se muestra la propiedad)  
  
```cpp
rs->Fields->Item[long(2)]->Value = "value";  
rs->Fields->Item["au_fname"]->Value = "value";  
```
  
 Para obtener ejemplos de cómo recorrer en iteración una colección, consulte la sección "Colecciones de ADO" de "Referencia de ADO".  
  
## <a name="com-specific-data-types"></a>Tipos de datos específicos de COM  
 En general, cualquier tipo de datos de Visual Basic que se encuentre en la referencia de API de ADO tiene un equivalente en Visual C++. Éstos incluyen tipos de datos estándar, como **unsigned char** para Visual Basic **bytes**, **corto** para **entero**, y  **Long** para **largo**. Buscar en la sintaxis de Indexesto ver exactamente lo que se requiere para los operandos de un determinado método o propiedad.  
  
 Las excepciones a esta regla son los tipos de datos específicos de COM: **Variant**, **BSTR**, y **SafeArray**.  
  
### <a name="variant"></a>Variant  
 Un **Variant** es un tipo de datos estructurado que contiene un miembro de valor y un miembro de tipo de datos. Un **Variant** puede contener una amplia gama de otros tipos de datos incluidos otra variante, BSTR, Boolean, IDispatch o IUnknown puntero, moneda, fecha y así sucesivamente. COM también proporciona métodos que facilitan para conversión a un tipo de datos a otro.  
  
 El **_variant_t** clase encapsula y gestiona la **Variant** tipo de datos.  
  
 Cuando la referencia de API de ADO indica que un método o el operando de la propiedad toma un valor, generalmente significa el valor se pasa en un **_variant_t**.  
  
 Esta regla es true de forma explícita cuando la **parámetros** sección en los temas de la referencia de API de ADO indica que un operando es un **Variant**. Una excepción es cuando la documentación indica explícitamente el operando toma un tipo de datos estándar, tales como **largo** o **bytes**, o una enumeración. Otra excepción es cuando el operando toma un **cadena**.  
  
### <a name="bstr"></a>BSTR  
 Un **BSTR** (**B**asic **STR**ing) es un tipo de datos estructurado que contiene una cadena de caracteres y la longitud de cadena. COM proporciona métodos para asignar, manipular y liberar un **BSTR**.  
  
 El **_bstr_t** clase encapsula y gestiona la **BSTR** tipo de datos.  
  
 Cuando la referencia de API de ADO indica que un método o propiedad toma un **cadena** valor, significa que el valor es en forma de un **_bstr_t**.  
  
### <a name="casting-variantt-and-bstrt-classes"></a>Clases de conversión _variant_t y _bstr_t  
 A menudo no es necesario código explícitamente un **_variant_t** o **_bstr_t** en un argumento para una operación. Si el **_variant_t** o **_bstr_t** clase tiene un constructor que coincida con el tipo de datos del argumento, el compilador generará adecuado **_variant_t** o **_bstr_t**.  
  
 Sin embargo, si el argumento es ambiguo, es decir, el tipo del argumento datos coincide con más de un constructor, debe convertir el argumento con el tipo de datos adecuado para invocar el constructor correcto.  
  
 Por ejemplo, la declaración para el **Recordset:: Open** método es:  
  
```cpp
    HRESULT Open (  
        const _variant_t & Source,  
        const _variant_t & ActiveConnection,  
        enum CursorTypeEnum CursorType,  
        enum LockTypeEnum LockType,  
        long Options );  
```
  
 El `ActiveConnection` argumento acepta una referencia a un **_variant_t**, que se puede codificar como una cadena de conexión o un puntero a una apertura **conexión** objeto.  
  
 El valor correcto **_variant_t** se construirá implícitamente si se pasa una cadena como "`DSN=pubs;uid=MyUserName;pwd=MyPassword;`", o un puntero, como "`(IDispatch *) pConn`".  
  
> [!NOTE]
>  Si se conecta a un proveedor de origen de datos que admite la autenticación de Windows, debe especificar **Trusted_Connection = yes** o **Integrated Security = SSPI** en lugar de Id. de usuario y contraseña información de la cadena de conexión.  
  
 O bien puede codificar explícitamente un **_variant_t** que contiene un puntero, como "`_variant_t((IDispatch *) pConn, true)`". La conversión, `(IDispatch *)`, resuelve la ambigüedad con otro constructor que toma un puntero a una interfaz IUnknown.  
  
 Es crucial, aunque rara vez se ha mencionado hechos, que ADO es una interfaz IDispatch. Cada vez que se debe pasar un puntero a un objeto ADO como un **Variant**, debe convertir explícitamente ese puntero como un puntero a una interfaz IDispatch.  
  
 El último caso codifica explícitamente el segundo argumento booleano del constructor con su valor predeterminado opcional, `true`. Este argumento hace que el **Variant** constructor llame a su **AddRef**(método) (), que compensa a ADO automáticamente una llamada a la **_variant_t:: Release**método) Cuando se completa la llamada al método o propiedad de ADO.  
  
### <a name="safearray"></a>SafeArray  
 Un **SafeArray** es un tipo de datos estructurado que contiene una matriz de otros tipos de datos. Un **SafeArray** se denomina *seguro* porque contiene información sobre los límites de cada dimensión de matriz y limita el acceso a elementos de la matriz dentro de esos límites.  
  
 Cuando la referencia de API de ADO indica que un método o propiedad acepte o devuelva una matriz, significa que el método o propiedad acepte o devuelva un **SafeArray**, no es una matriz de C o C++ nativa.  
  
 Por ejemplo, el segundo parámetro de la **conexión** objeto **OpenSchema** método requiere una matriz de **Variant** valores. Los **Variant** valores se deben pasar como elementos de un **SafeArray**y que **SafeArray** debe establecerse como el valor de otro **Variant** . Resulta que otros **Variant** que se pasa como segundo argumento de **OpenSchema**.  
  
 Como aún más ejemplos, el primer argumento de la **buscar** método es un **Variant** cuyo valor es unidimensional **SafeArray**; cada de los argumentos opcionales de la primeros y segundo de **AddNew** es unidimensional **SafeArray**; y el valor devuelto de la **GetRows** método es un **Variant** cuyo valor es un bidimensional **SafeArray**.  
  
## <a name="missing-and-default-parameters"></a>Parámetros predeterminados y ausentes  
 Visual Basic permite faltan parámetros en métodos. Por ejemplo, el **Recordset** objeto **abierto** método tiene cinco parámetros, pero se puede omitir parámetros intermedios y no incluir parámetros finales. Valor predeterminado es **BSTR** o **Variant** se sustituirá según el tipo de datos del operando que faltan.  
  
 En C/C ++, se deben especificar todos los operandos. Si desea especificar un parámetro que falta cuyo tipo de datos es una cadena, especifique un **_bstr_t** que contiene una cadena nula. Si desea especificar un parámetro que falta cuyo tipo de datos es un **Variant**, especifique un **_variant_t** con un valor DISP_E_PARAMNOTFOUND y un tipo VT_ERROR. Como alternativa, especifique el equivalente **_variant_t** constante, **vtMissing**, que suministra el **#import** directiva.  
  
 Tres métodos son excepciones para el uso típico de **vtMissing**. Estos son los **Execute** métodos de la **conexión** y **comando** objetos y el **NextRecordset** método de la **Recordset** objeto. Estas son sus firmas:  
  
```cpp
_RecordsetPtr <A HREF="mdmthcnnexecute.htm">Execute</A>( _bstr_t CommandText, VARIANT * RecordsAffected,   
        long Options );  // Connection  
_RecordsetPtr <A HREF="mdmthcmdexecute.htm">Execute</A>( VARIANT * RecordsAffected, VARIANT * Parameters,   
        long Options );  // Command  
_RecordsetPtr <A HREF="mdmthnextrec.htm">NextRecordset</A>( VARIANT * RecordsAffected );  // Recordset  
```
  
 Los parámetros, *RecordsAffected* y *parámetros*, son punteros a un **Variant**. *Parámetros* es un parámetro de entrada que especifica la dirección de un **Variant** que contiene un solo parámetro, o matriz de parámetros, que modificará el comando que se está ejecutando. *RecordsAffected* es un parámetro de salida que especifica la dirección de un **Variant**, donde se devuelve el número de filas afectadas por el método.  
  
 En el **comando** objeto **Execute** método, puede indicar que no se especifica ningún parámetro estableciendo *parámetros* como `&vtMissing` (que se recomienda) o a el puntero null (es decir, **NULL** o cero (0)). Si *parámetros* se establece al puntero nulo, el método sustituye internamente el equivalente de **vtMissing**y, a continuación, completa la operación.  
  
 En todos los métodos, indique que no se debe devolver el número de registros afectados estableciendo *RecordsAffected* al puntero nulo. En este caso, el puntero null no es tanto un parámetro que falta como un valor que indica que el método debería descartar el número de registros afectados.  
  
 Por lo tanto, para estos tres métodos, es válida para algo de código, como:  
  
```cpp
pConnection->Execute("commandText", NULL, adCmdText);   
pCommand->Execute(NULL, NULL, adCmdText);  
pRecordset->NextRecordset(NULL);  
```
  
## <a name="error-handling"></a>Tratamiento de errores  
 En COM, la mayoría de las operaciones devuelve un código de retorno HRESULT que indica si una función se completó correctamente. El **#import** directiva genera código de contenedor en torno a cada método de "raw" o una propiedad y comprueba el HRESULT devuelto. Si el valor HRESULT indica un error, el código de contenedor genera un error de COM que realiza la llamada _com_issue_errorex () con el código de retorno HRESULT como argumento. Objetos de error COM se pueden capturar en un **intente**-**catch** bloque. (Para una mayor eficacia, detecte una referencia a un **_com_error** objeto.)  
  
 Recuerde, éstas son errores de ADO: son el resultado de la operación de ADO. Los errores devueltos por el proveedor subyacente aparecen como **Error** objetos en el **conexión** objeto **errores** colección.  
  
 El **#import** directiva sólo crea errores rutinas de manipulación para los métodos y propiedades declarados en la DLL de ADO. Sin embargo, puede aprovechar este mismo mecanismo de control escribiendo su propia función alineado o macro de comprobación de errores de error. Vea el tema [extensiones de Visual C++](../../../ado/guide/appendixes/visual-c-extensions-for-ado.md), o el código en las secciones siguientes para obtener ejemplos.  
  
## <a name="visual-c-equivalents-of-visual-basic-conventions"></a>Equivalentes de convenciones de Visual Basic en Visual C++  
 El siguiente es un resumen de diversas convenciones de la documentación de ADO, codificadas en Visual Basic, así como sus equivalentes en Visual C++.  
  
### <a name="declaring-an-ado-object"></a>Declarar un objeto ADO  
 En Visual Basic, una variable de objeto ADO (en este caso para un **Recordset** objeto) se declara como sigue:  
  
```vb
Dim rst As ADODB.Recordset  
```
  
 La cláusula "`ADODB.Recordset`", es el ProgID de la **Recordset** objeto tal como se define en el registro. Una nueva instancia de un **registro** objeto se declara como sigue:  
  
```vb
Dim rst As New ADODB.Recordset  
```
  
 -o bien-  
  
```vb
Dim rst As ADODB.Recordset  
Set rst = New ADODB.Recordset  
```
  
 En Visual C++, el **#import** directiva genera declaraciones de tipo puntero inteligente para todos los objetos ADO. Por ejemplo, una variable que señala a una **_Recordset** objeto es de tipo **_RecordsetPtr**y se declara como sigue:  
  
```cpp
_RecordsetPtr  rs;  
```
  
 Una variable que señala a una nueva instancia de un **_Recordset** objeto se declara como sigue:  
  
```cpp
_RecordsetPtr  rs("ADODB.Recordset");  
```
  
 -o bien-  
  
```cpp
_RecordsetPtr  rs;  
rs.CreateInstance("ADODB.Recordset");  
```
  
 -o bien-  
  
```cpp
_RecordsetPtr  rs;  
rs.CreateInstance(__uuidof(_Recordset));  
```
  
 Después de la **CreateInstance** se llama al método, la variable se puede utilizar como sigue:  
  
```cpp
rs->Open(...);  
```
  
 Tenga en cuenta que en un caso, el "`.`" operador se usa como si fuera de la variable de una instancia de una clase (`rs.CreateInstance`) y en otro caso, el "`->`" operador se usa como si fuera de la variable de puntero a una interfaz (`rs->Open`).  
  
 Una variable puede usarse de dos maneras porque el "`->`" se sobrecarga para permitir que una instancia de una clase comportarse como un puntero a una interfaz. Un miembro de clase privada de la variable de instancia contiene un puntero a la **_Recordset** interfaz; el "`->`" operador devuelve ese puntero; y el puntero devuelto tiene acceso a los miembros de la **_Recordset**  objeto.  
  
### <a name="coding-a-missing-parameter---string"></a>Codificar un parámetro que falta: cadena  
 Cuando necesite una falta de código **cadena** operando en Visual Basic, simplemente omita el operando. Debe especificar el operando en Visual C++. Código de un **_bstr_t** que tiene una cadena vacía como un valor.  
  
```cpp
_bstr_t strMissing(L"");  
```
  
### <a name="coding-a-missing-parameter---variant"></a>Codificar un parámetro que falta - Variant  
 Cuando necesite una falta de código **Variant** operando en Visual Basic, simplemente omita el operando. Debe especificar todos los operandos en Visual C++. Una falta de código **Variant** parámetro con un **_variant_t** establecido en el valor especial DISP_E_PARAMNOTFOUND y escriba VT_ERROR. Como alternativa, especifique **vtMissing**, que es una constante predefinida equivalente proporcionada por el **#import** directiva.  
  
```cpp
_variant_t  vtMissingYours(DISP_E_PARAMNOTFOUND, VT_ERROR);   
```
  
 -o bien use-  
  
```cpp
...vtMissing...;  
```
  
### <a name="declaring-a-variant"></a>Declarar un tipo Variant  
 En Visual Basic, un **Variant** se declara con el **Dim** instrucción como sigue:  
  
```vb
Dim VariableName As Variant  
```
  
 En Visual C++, declare una variable como tipo **_variant_t**. Esquema unos **_variant_t** declaraciones se muestran a continuación.  
  
> [!NOTE]
>  Estas declaraciones simplemente proporcionan una idea aproximada de lo que debe incluir el código en su propio programa. Para obtener más información, vea los ejemplos siguientes y la documentación Visual C ++.  
  
```cpp
_variant_t  VariableName(value);  
_variant_t  VariableName((data type cast) value);  
_variant_t  VariableName(value, VT_DATATYPE);  
_variant_t  VariableName(interface * value, bool fAddRef = true);  
```
  
### <a name="using-arrays-of-variants"></a>Uso de matrices de variantes  
 En Visual Basic, las matrices de **variantes** se puede codificar con el **Dim** instrucción, o bien puede usar el **matriz** funcione, como se muestra en el ejemplo de código siguiente:  
  
```vb
Public Sub ArrayOfVariants  
Dim cn As ADODB.Connection  
Dim rs As ADODB.Recordset  
Dim fld As ADODB.Field  
  
    cn.Open "DSN=pubs"  
    rs = cn.OpenSchema(adSchemaColumns, _  
        Array(Empty, Empty, "authors", Empty))  
    For Each fld in rs.Fields  
        Debug.Print "Name = "; fld.Name  
    Next fld  
    rs.Close  
    cn.Close  
End Sub  
```
  
 El siguiente ejemplo de Visual C++, se muestra cómo utilizar un **SafeArray** usa con un **_variant_t**.  
  
#### <a name="notes"></a>Notas  
 Las notas siguientes corresponden a secciones comentadas en el ejemplo de código.  
  
1.  Una vez más, se define la función inline TESTHR() para aprovechar el mecanismo de control de errores existente.  
  
2.  Solo necesita una matriz unidimensional, por lo que puede usar **SafeArrayCreateVector**, en lugar de la finalidad general **SAFEARRAYBOUND** declaración y **SafeArrayCreate** función. El siguiente es lo que ese código tendría el aspecto similar al uso de **SafeArrayCreate**:  
  
    ```cpp
       SAFEARRAYBOUND   sabound[1];  
       sabound[0].lLbound = 0;  
       sabound[0].cElements = 4;  
       pSa = SafeArrayCreate(VT_VARIANT, 1, sabound);  
    ```
  
3.  El esquema identificado por la constante enumerada, **adSchemaColumns**, está asociado con cuatro columnas de restricción: TABLE_CATALOG, TABLE_SCHEMA, TABLE_NAME y COLUMN_NAME. Por lo tanto, una matriz de **Variant** se crean los valores con cuatro elementos. A continuación, se especifica un valor de restricción que corresponde a la tercera columna, TABLE_NAME.  
  
     El **Recordset** devuelto consta de varias columnas, un subconjunto de los cuales se las columnas de restricción. Los valores de las columnas de restricción para cada fila devuelta deben ser el mismo que los valores correspondientes de la restricción.  
  
4.  Aquellos que estén familiarizados con **SAFEARRAY** puede ser sorprende que **SafeArrayDestroy**() no se llama antes de la salida. De hecho, una llamada a **SafeArrayDestroy**() en este caso provocará una excepción en tiempo de ejecución. El motivo es que el destructor de `vtCriteria` llamará **VariantClear**() cuando el **_variant_t** sale del ámbito, que liberará el **SafeArray**. Una llamada a **SafeArrayDestroy**, sin borrar manualmente la **_variant_t**, provocará que el destructor intente borrar no es válido **SafeArray** puntero.  
  
     Si **SafeArrayDestroy** eran llama, el código tendría el aspecto siguiente:  
  
    ```cpp
          TESTHR(SafeArrayDestroy(pSa));  
       vtCriteria.vt = VT_EMPTY;  
          vtCriteria.parray = NULL;  
    ```
  
     Sin embargo, resulta mucho más sencillo permitir que el **_variant_t** administrar la **SafeArray**.  
  
```cpp
// Visual_CPP_ADO_Prog_1.cpp  
// compile with: /EHsc  
#import "msado15.dll" no_namespace rename("EOF", "EndOfFile")  
  
// Note 1  
inline void TESTHR( HRESULT _hr ) {   
   if FAILED(_hr)   
      _com_issue_error(_hr);   
}  
  
int main() {  
   CoInitialize(NULL);  
   try {  
      _RecordsetPtr pRs("ADODB.Recordset");  
      _ConnectionPtr pCn("ADODB.Connection");  
      _variant_t vtTableName("authors"), vtCriteria;  
      long ix[1];  
      SAFEARRAY *pSa = NULL;  
  
      pCn->Provider = "sqloledb";  
      pCn->Open("Data Source='(local)';Initial Catalog='pubs';Integrated Security=SSPI", "", "", adConnectUnspecified);  
      // Note 2, Note 3  
      pSa = SafeArrayCreateVector(VT_VARIANT, 1, 4);  
      if (!pSa)   
         _com_issue_error(E_OUTOFMEMORY);  
  
      // Specify TABLE_NAME in the third array element (index of 2).   
      ix[0] = 2;        
      TESTHR(SafeArrayPutElement(pSa, ix, &vtTableName));  
  
      // There is no Variant constructor for a SafeArray, so manually set the   
      // type (SafeArray of Variant) and value (pointer to a SafeArray).  
  
      vtCriteria.vt = VT_ARRAY | VT_VARIANT;  
      vtCriteria.parray = pSa;  
  
      pRs = pCn->OpenSchema(adSchemaColumns, vtCriteria, vtMissing);  
  
      long limit = pRs->GetFields()->Count;  
      for ( long x = 0 ; x < limit ; x++ )  
         printf( "%d: %s\n", x + 1, ((char*) pRs->GetFields()->Item[x]->Name) );  
      // Note 4  
      pRs->Close();  
      pCn->Close();  
   }  
   catch (_com_error &e) {  
      printf("Error:\n");  
      printf("Code = %08lx\n", e.Error());  
      printf("Code meaning = %s\n", (char*) e.ErrorMessage());  
      printf("Source = %s\n", (char*) e.Source());  
      printf("Description = %s\n", (char*) e.Description());  
   }  
   CoUninitialize();  
}  
```
  
### <a name="using-property-getputputref"></a>Uso de propiedad Get/Put/PutRef  
 En Visual Basic, el nombre de una propiedad no está calificado por si se recupera, asignado o asigna una referencia.  
  
```vb
Public Sub GetPutPutRef  
Dim rs As New ADODB.Recordset  
Dim cn As New ADODB.Connection  
Dim sz as Integer  
cn.Open "Provider=sqloledb;Data Source=yourserver;" & _  
         "Initial Catalog=pubs;Integrated Security=SSPI;"  
rs.PageSize = 10  
sz = rs.PageSize  
rs.ActiveConnection = cn  
rs.Open "authors",,adOpenStatic  
' ...  
rs.Close  
cn.Close  
End Sub  
```
  
 Este ejemplo de Visual C++ se muestra el **obtener**/**colocar**/**PutRef**_propiedad_.  
  
#### <a name="notes"></a>Notas  
 Las notas siguientes corresponden a secciones comentadas en el ejemplo de código.  
  
1.  En este ejemplo utiliza dos formas de un argumento de cadena que falta: una constante explícita, **strMissing**y una cadena que el compilador utilizará para crear un archivo temporal **_bstr_t** que existirá durante el ámbito de la  **Abra** método.  
  
2.  No es necesario convertir explícitamente el operando de `rs->PutRefActiveConnection(cn)` a `(IDispatch *)` porque el tipo del operando es ya `(IDispatch *)`.  
  
```cpp
// Visual_CPP_ado_prog_2.cpp  
// compile with: /EHsc  
#import "msado15.dll" no_namespace rename("EOF", "EndOfFile")  
  
int main() {  
   CoInitialize(NULL);  
   try {  
      _ConnectionPtr cn("ADODB.Connection");  
      _RecordsetPtr rs("ADODB.Recordset");  
      _bstr_t strMissing(L"");  
      long oldPgSz = 0, newPgSz = 5;  
  
      // Note 1  
      cn->Provider = "sqloledb";  
      cn->Open("Data Source='(local)';Initial Catalog=pubs;Integrated Security=SSPI;", strMissing, "", adConnectUnspecified);  
  
      oldPgSz = rs->GetPageSize();  
      // -or-  
      // oldPgSz = rs->PageSize;  
  
      rs->PutPageSize(newPgSz);  
      // -or-  
      // rs->PageSize = newPgSz;  
  
      // Note 2  
      rs->PutRefActiveConnection( cn );  
      rs->Open("authors", vtMissing, adOpenStatic, adLockReadOnly, adCmdTable);  
      printf("Original pagesize = %d, new pagesize = %d\n", oldPgSz, rs->GetPageSize());  
      rs->Close();  
      cn->Close();  
  
   }  
   catch (_com_error &e) {  
      printf("Description = %s\n", (char*) e.Description());  
   }  
   ::CoUninitialize();  
}  
```
  
### <a name="using-getitemx-and-itemx"></a>Uso de GetItem y elemento [x]  
 Este ejemplo de Visual Basic muestra la sintaxis estándar y alternativa para **elemento**().  
  
```vb
Public Sub GetItemItem  
Dim rs As New ADODB.Recordset  
Dim name as String  
rs = rs.Open "authors", "DSN=pubs;", adOpenDynamic, _  
         adLockBatchOptimistic, adTable  
name = rs(0)  
' -or-  
name = rs.Fields.Item(0)  
rs(0) = "Test"  
rs.UpdateBatch  
' Restore name  
rs(0) = name  
rs.UpdateBatch  
rs.Close  
End Sub  
```
  
 Se muestra en este ejemplo de Visual C++ **elemento**.  
  
> [!NOTE]
>  La nota siguiente corresponde a secciones comentadas en el ejemplo de código:  Cuando se tiene acceso a la colección con **elemento**, el índice, **2**, deben convertirse a **largo** por lo que se va a invocar un constructor adecuado.  
  
```cpp
// Visual_CPP_ado_prog_3.cpp  
// compile with: /EHsc  
#import "msado15.dll" no_namespace rename("EOF", "EndOfFile")  
  
void main() {  
   CoInitialize(NULL);  
   try {  
      _ConnectionPtr cn("ADODB.Connection");  
      _RecordsetPtr rs("ADODB.Recordset");  
      _variant_t vtFirstName;  
  
      cn->Provider = "sqloledb";  
      cn->Open("Data Source='(local)';Initial Catalog=pubs;Integrated Security=SSPI;", "", "", adConnectUnspecified);  
  
      rs->PutRefActiveConnection( cn );  
      rs->Open("authors", vtMissing, adOpenStatic, adLockOptimistic, adCmdTable);  
      rs->MoveFirst();  
  
      // Note 1. Get a field.  
      vtFirstName = rs->Fields->GetItem((long)2)->GetValue();  
      // -or-  
      vtFirstName = rs->Fields->Item[(long)2]->Value;  
  
      printf( "First name = '%s'\n", (char*)( (_bstr_t)vtFirstName) );  
  
      rs->Fields->GetItem((long)2)->Value = L"TEST";  
      rs->Update(vtMissing, vtMissing);  
  
      // Restore name  
      rs->Fields->GetItem((long)2)->PutValue(vtFirstName);  
      // -or-  
      rs->Fields->GetItem((long)2)->Value = vtFirstName;  
      rs->Update(vtMissing, vtMissing);  
      rs->Close();  
   }  
   catch (_com_error &e) {  
      printf("Description = '%s'\n", (char*) e.Description());  
   }  
   ::CoUninitialize();  
}  
```
  
### <a name="casting-ado-object-pointers-with-idispatch-"></a>Convertir punteros a objetos ADO con (IDispatch *)  
 El siguiente ejemplo de Visual C++, se muestra cómo utilizar (IDispatch *) para punteros a objetos ADO cast.  
  
#### <a name="notes"></a>Notas  
 Las notas siguientes corresponden a secciones comentadas en el ejemplo de código.  
  
1.  Especifique una apertura **conexión** codificado explícitamente un objeto **Variant**. Convertirlo con (IDispatch \*) por lo que se invocará el constructor correcto. Además, establezca explícitamente la segunda **_variant_t** parámetro en el valor predeterminado de **true**, por lo que el recuento de referencias de objeto serán las correctas cuando el **Recordset:: Open** finaliza la operación.  
  
2.  La expresión, `(_bstr_t)`, no es una conversión, pero un **_variant_t** operador que extrae una **_bstr_t** cadena desde el **Variant** devuelto por **valor** .  
  
 La expresión, `(char*)`, no es una conversión, pero un **_bstr_t** operador que extrae un puntero a la cadena encapsulada en un **_bstr_t** objeto.  
  
 Esta sección de código muestra algunos de los comportamientos útiles de **_variant_t** y **_bstr_t** operadores.  
  
```cpp
// Visual_CPP_ado_prog_4.cpp  
// compile with: /EHsc  
#import "msado15.dll" no_namespace rename("EOF", "EndOfFile")  
  
int main() {  
   CoInitialize(NULL);  
   try {  
      _ConnectionPtr pConn("ADODB.Connection");  
      _RecordsetPtr pRst("ADODB.Recordset");  
  
      pConn->Provider = "sqloledb";  
      pConn->Open("Data Source='(local)';Initial Catalog='pubs';Integrated Security=SSPI", "", "", adConnectUnspecified);  
  
      // Note 1.  
      pRst->Open("authors", _variant_t((IDispatch *) pConn, true), adOpenStatic, adLockReadOnly, adCmdTable);  
      pRst->MoveLast();  
  
      // Note 2.  
      printf("Last name is '%s %s'\n",   
         (char*) ((_bstr_t) pRst->GetFields()->GetItem("au_fname")->GetValue()),  
         (char*) ((_bstr_t) pRst->Fields->Item["au_lname"]->Value));  
  
      pRst->Close();  
      pConn->Close();  
   }  
   catch (_com_error &e) {  
      printf("Description = '%s'\n", (char*) e.Description());  
   }     
   ::CoUninitialize();  
}  
```
