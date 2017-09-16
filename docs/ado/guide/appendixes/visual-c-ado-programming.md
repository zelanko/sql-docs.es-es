---
title: "Programación ADO en Visual C++ | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 02/15/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- C++
helpviewer_keywords:
- ADO, Visual C++
- Visual C++ [ADO]
ms.assetid: 11233b96-e05c-4221-9aed-5f20944b0f1c
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9000f90f30c8761845305e75cf3d0ea7ea86927a
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="visual-c-ado-programming"></a>Programación ADO en Visual C++
La referencia de API de ADO describe la funcionalidad de la interfaz de programación de aplicaciones (API) de ADO mediante una sintaxis similar a Microsoft Visual Basic. Aunque dirigida a todos los usuarios, los programadores de ADO emplean diversos lenguajes como Visual Basic, Visual C++ (con y sin el **#import** directiva) y Visual J ++ (con el paquete de clases ADO/WFC).  

> [!NOTE]
> Microsoft ha finalizado de soporte técnico de Visual J ++ en 2004.

 Para dar cabida a esta diversidad, el [ADO para los índices de sintaxis de Visual C++](../../../ado/guide/appendixes/using-ado-with-microsoft-visual-c.md) proporcionan sintaxis específica del lenguaje de Visual C++ con vínculos a descripciones comunes de funcionalidad, parámetros, comportamientos excepcionales etc., en la API Referencia.  
  
 ADO se implementa con interfaces COM (Component Object Model). Sin embargo, resulta más fácil para los programadores trabajar con COM en algunos lenguajes de programación que otros. Por ejemplo, casi todos los detalles del uso de COM se manejan implícitamente para los programadores de Visual Basic, mientras que los programadores de Visual C++ deben asistir a esos detalles.  
  
 En las siguientes secciones resumen la información para programadores de C y C++ mediante ADO y el **#import** directiva. Se centra en tipos de datos específicos de COM (**Variant**, **BSTR**, y **SafeArray**) y control de errores (_com_error).  
  
## <a name="using-the-import-compiler-directive"></a>Uso de la directiva #import del compilador  
 El **#import** directiva de compilador de Visual C++ simplifica el trabajo con las propiedades y métodos de ADO. La directiva toma el nombre de un archivo que contenga una biblioteca de tipos, por ejemplo, la DLL de ADO (Msado15.dll) y genera archivos de encabezado que contienen declaraciones typedef, punteros inteligentes para las interfaces y las constantes enumeradas. Cada interfaz se encapsula o ajustada, en una clase.  
  
 Para cada operación dentro de una clase (es decir, una llamada de método o propiedad), hay una declaración para llamar a la operación directamente (es decir, la forma "sin formato" de la operación) y una declaración para llamar a la operación sin procesar y generar un error de COM si la operación no se puede ejecutar succ essfully. Si la operación es una propiedad, normalmente hay una directiva de compilador que crea una sintaxis alternativa para la operación que tiene una sintaxis similar a Visual Basic.  
  
 Las operaciones que se recuperan el valor de una propiedad tienen nombres de la forma, **obtener***propiedad*. Las operaciones que establecen el valor de una propiedad tienen nombres del formulario, **colocar***propiedad*. Las operaciones que establecen el valor de una propiedad con un puntero a un objeto ADO tienen nombres del formulario, **PutRef***propiedad*.  
  
 Puede obtener o establecer una propiedad con llamadas de estas formas:  
  
```  
variable = objectPtr->GetProperty(); // get property value   
objectPtr->PutProperty(value);       // set property value  
objectPtr->PutRefProperty(&value);   // set property with object pointer  
```  
  
## <a name="using-property-directives"></a>Utilizar directivas de propiedad  
 El **__declspec(property...) ** directiva de compilador es una extensión del lenguaje C específicas de Microsoft que declara una función utilizada como una propiedad que tenga una sintaxis alternativa. Como resultado, puede establecer u obtener valores de una propiedad de una manera similar a Visual Basic. Por ejemplo, puede establecer y obtener una propiedad de esta manera:  
  
```  
objectPtr->property = value;        // set property value  
variable = objectPtr->property;     // get property value  
```  
  
 Tenga en cuenta que no es necesario código:  
  
```  
objectPtr->PutProperty(value);      // set property value  
variable = objectPtr->GetProperty;  // get property value  
```  
  
 El compilador generará la correspondiente **obtener***-*, **colocar**-, o **PutRef***propiedad* llamada según la sintaxis alternativa declarada y si la propiedad se va a leer o escribir.  
  
 El **__declspec(property...) ** sólo puede declarar la directiva de compilador **obtener**, **colocar**, o **obtener** y **colocar** sintaxis alternativa para una función. Operaciones de solo lectura únicamente tienen un **obtener** declaración; las operaciones de solo escritura solo tiene un **colocar** declaración; las operaciones que son ambos leen y escriben tener **obtener** y **colocar** declaraciones.  
  
 Solo dos declaraciones son posibles con esta directiva; Sin embargo, cada propiedad tiene tres funciones de propiedad: **obtener***propiedad*, **colocar***propiedad*, y **PutRef ** *Propiedad*. En ese caso, solo dos formas de la propiedad tienen la sintaxis alternativa.  
  
 Por ejemplo, el **comando** objeto **ActiveConnection** propiedad se declara con una sintaxis alternativa para **obtener***ActiveConnection*y **PutRef***ActiveConnection*. El **PutRef**-sintaxis es una buena elección porque en la práctica, normalmente deberá colocar abierto **conexión** objeto (es decir, un **conexión** puntero de objeto) en este propiedad. Por otro lado, el **Recordset** objeto tiene **obtener**-, **colocar**-, y **PutRef***ActiveConnection*las operaciones, pero sin sintaxis alternativa.  
  
## <a name="collections-the-getitem-method-and-the-item-property"></a>Colecciones, el método GetItem y la propiedad del elemento  
 ADO define varias colecciones, incluidas **campos**, **parámetros**, **propiedades**, y **errores**. En Visual C++, el **GetItem (***índice***)** método devuelve un miembro de la colección. *Índice* es un **Variant**, el valor de los cuales es un índice numérico del miembro de la colección o una cadena que contiene el nombre del miembro.  
  
 El **__declspec(property...) ** directiva de compilador se declara el **elemento** de la propiedad como una sintaxis alternativa para cada colección fundamental **GetItem()** método. La sintaxis alternativa utiliza corchetes y es similar a una referencia a la matriz. En general, las dos formas de tener un aspecto similar al siguiente:  
  
```  
  
      collectionPtr->GetItem(index);  
collectionPtr->Item[index];  
```  
  
 Por ejemplo, asignar un valor a un campo de un **conjunto de registros** objeto, denominado ***rs***, derivado de la **autores** tabla de la **pubs** base de datos. Use la **Item()** propiedad para tener acceso a la tercera **campo** de la **Recordset** objeto **campos** colección (las colecciones se indizan de cero; Suponga que el tercer campo se denomina ***au_fname***). A continuación, llame a la **Value()** método en el **campo** objeto que se va a asignar un valor de cadena.  
  
 Esto se puede expresar en Visual Basic en los siguientes cuatro maneras (las últimas dos formas son exclusivas de Visual Basic; otros lenguajes no tienen equivalentes):  
  
```  
rs.Fields.Item(2).Value = "value"  
rs.Fields.Item("au_fname").Value = "value"  
rs(2) = "value"  
rs!au_fname = "value"  
```  
  
 Es el equivalente en Visual C++ para las dos primeras formas anteriores:  
  
```  
rs->Fields->GetItem(long(2))->PutValue("value");   
rs->Fields->GetItem("au_fname")->PutValue("value");  
```  
  
 - o bien - (la sintaxis alternativa para la **valor** también se muestra la propiedad)  
  
```  
rs->Fields->Item[long(2)]->Value = "value";  
rs->Fields->Item["au_fname"]->Value = "value";  
```  
  
 Para obtener ejemplos de cómo recorrer en iteración una colección, vea la sección "Colecciones de ADO" de "Referencia de ADO".  
  
## <a name="com-specific-data-types"></a>Tipos de datos específicos de COM  
 En general, cualquier tipo de datos de Visual Basic que encuentra en la referencia de API de ADO tiene un equivalente en Visual C++. Éstos incluyen tipos de datos estándar como **unsigned char** para un Visual Basic **bytes**, **corto** para **entero**, y ** Long** para **largo**. Buscar en la sintaxis Indexesto ver exactamente qué se requiere para los operandos de un determinado método o propiedad.  
  
 Las excepciones a esta regla son los tipos de datos específicos de COM: **Variant**, **BSTR**, y **SafeArray**.  
  
### <a name="variant"></a>Variant  
 A **Variant** es un tipo de datos estructurados que contiene un miembro de valor y un miembro de tipo de datos. A **Variant** puede contener una amplia variedad de otros tipos de datos, incluidos otro Variant, BSTR, Boolean, IDispatch, puntero a IUnknown, moneda, fecha etc. COM también proporciona métodos que facilitan la tarea para convierten a un tipo de datos a otro.  
  
 El **_variant_t** clase encapsula y administra el **Variant** tipo de datos.  
  
 Cuando la referencia de API de ADO indica que un método u operando de la propiedad toma un valor, suele significar se pasa el valor de un **_variant_t**.  
  
 Esta regla está explícitamente true cuando la **parámetros** sección en los temas de la referencia de API de ADO indica que un operando es un **Variant**. Una excepción es cuando la documentación indica explícitamente que el operando toma un tipo de datos estándar, como **largo** o **bytes**, o una enumeración. Otra excepción es cuando el operando toma un **cadena**.  
  
### <a name="bstr"></a>BSTR  
 A **BSTR** (**B**asic **STR**ing) es un tipo de datos estructurados que contiene una cadena de caracteres y la longitud de la cadena. COM proporciona métodos para asignar, manipular y liberar un **BSTR**.  
  
 El **_bstr_t** clase encapsula y administra el **BSTR** tipo de datos.  
  
 Cuando la referencia de API de ADO indica que un método o propiedad toma un **cadena** valor, significa que el valor existe en forma de un **_bstr_t**.  
  
### <a name="casting-variantt-and-bstrt-classes"></a>Clases de conversión _variant_t y _bstr_t  
 A menudo no es necesario código explícitamente un **_variant_t** o **_bstr_t** dentro de un argumento para una operación. Si el **_variant_t** o **_bstr_t** clase tiene un constructor que coincide con el tipo de datos del argumento, el compilador generará la correspondiente **_variant_t** o **_bstr_t**.  
  
 Sin embargo, si el argumento es ambiguo, es decir, tipo de datos del argumento coincide con más de un constructor, debe convertir el argumento con el tipo de datos adecuado para invocar el constructor correcto.  
  
 Por ejemplo, la declaración para el **Recordset:: Open** método es:  
  
```  
    HRESULT Open (  
        const _variant_t & Source,  
        const _variant_t & ActiveConnection,  
        enum CursorTypeEnum CursorType,  
        enum LockTypeEnum LockType,  
        long Options );  
```  
  
 El `ActiveConnection` argumento tiene una referencia a un **_variant_t**, que se puede codificar como una cadena de conexión o un puntero a un formato de archivo **conexión** objeto.  
  
 El valor correcto **_variant_t** se construirá implícitamente si se pasa una cadena como "`DSN=pubs;uid=MyUserName;pwd=MyPassword;`", o un puntero, como "`(IDispatch *) pConn`".  
  
> [!NOTE]
>  Si se conecta a un proveedor de origen de datos que admita la autenticación de Windows, debe especificar **Trusted_Connection = yes** o **Integrated Security = SSPI** en lugar de Id. de usuario y contraseña información de la cadena de conexión.  
  
 O bien, puede codificar explícitamente un **_variant_t** que contiene un puntero como "`_variant_t((IDispatch *) pConn, true)`". La conversión, `(IDispatch *)`, resuelve la ambigüedad con otro constructor que toma un puntero a una interfaz IUnknown.  
  
 Es fundamental, aunque raramente mencionado hecho, ADO es una interfaz IDispatch. Cada vez que se debe pasar un puntero a un objeto ADO como un **Variant**, debe convertir explícitamente ese puntero como un puntero a una interfaz IDispatch.  
  
 El último caso codifica explícitamente el segundo argumento booleano del constructor con su valor predeterminado opcional, de `true`. Este argumento hace que el **Variant** constructor al que se llame a su **AddRef**método (), que compensa a ADO automáticamente llamando el **_variant_t:: Release**() (método) Cuando se completa la llamada de método o propiedad de ADO.  
  
### <a name="safearray"></a>SafeArray  
 A **SafeArray** es un tipo de datos estructurados que contiene una matriz de otros tipos de datos. A **SafeArray** se denomina *seguro* porque contiene información sobre los límites de cada dimensión de la matriz y limita el acceso a elementos de la matriz dentro de esos límites.  
  
 Cuando la referencia de API de ADO indica que un método o propiedad acepta o devuelve una matriz, significa que el método o propiedad acepta o devuelve un **SafeArray**, no es una matriz de C o C++ nativo.  
  
 Por ejemplo, el segundo parámetro de la **conexión** objeto **OpenSchema** método requiere una matriz de **Variant** valores. Los **Variant** valores se deben pasar como elementos de un **SafeArray**y que **SafeArray** debe establecerse como el valor de otro **Variant** . Que otros **Variant** que se pasa como el segundo argumento de **OpenSchema**.  
  
 Tal como ejemplos, el primer argumento de la **buscar** método es un **Variant** cuyo valor es un unidimensional **SafeArray**; cada de los argumentos primeros y segundo opcionales de **AddNew** es un unidimensional **SafeArray**; y el valor devuelto de la **GetRows** método es un **Variant** cuyo valor es un bidimensional **SafeArray**.  
  
## <a name="missing-and-default-parameters"></a>Parámetros predeterminados y ausentes  
 Visual Basic permite que falten parámetros en métodos. Por ejemplo, el **Recordset** objeto **abiertos** método tiene cinco parámetros, pero pueden omitir parámetros intermedios y no incluir parámetros finales. Valor predeterminado es **BSTR** o **Variant** se sustituirá según el tipo de datos del operando que falta.  
  
 En C o C++, deben especificarse todos los operandos. Si desea especificar un parámetro que falta cuyo tipo de datos es una cadena, especifique un **_bstr_t** que contiene una cadena nula. Si desea especificar un parámetro que falta cuyo tipo de datos es un **Variant**, especifique un **_variant_t** con un valor DISP_E_PARAMNOTFOUND y un tipo VT_ERROR. O bien, especifique el equivalente **_variant_t** constante, **vtMissing**, que se proporciona el **#import** directiva.  
  
 Tres métodos que constituyen excepciones al uso típico de **vtMissing**. Estos son los **Execute** métodos de la **conexión** y **comando** objetos y el **NextRecordset** método de la **Recordset** objeto. Éstos son sus firmas:  
  
```  
_RecordsetPtr <A HREF="mdmthcnnexecute.htm">Execute</A>( _bstr_t CommandText, VARIANT * RecordsAffected,   
        long Options );  // Connection  
_RecordsetPtr <A HREF="mdmthcmdexecute.htm">Execute</A>( VARIANT * RecordsAffected, VARIANT * Parameters,   
        long Options );  // Command  
_RecordsetPtr <A HREF="mdmthnextrec.htm">NextRecordset</A>( VARIANT * RecordsAffected );  // Recordset  
```  
  
 Los parámetros, *RecordsAffected* y *parámetros*, son punteros a un **Variant**. *Parámetros de* es un parámetro de entrada que especifica la dirección de un **Variant** que contiene un solo parámetro, o matriz de parámetros, que modificará el comando que se está ejecutando. *RecordsAffected* es un parámetro de salida que especifica la dirección de un **Variant**, donde se devuelve el número de filas afectadas por el método.  
  
 En el **comando** objeto **Execute** método, puede indicar que no se especifica ningún parámetro estableciendo *parámetros* como `&vtMissing` (lo que se recomienda) o a el puntero nulo (es decir, **NULL** o cero (0)). Si *parámetros* se establece como el puntero nulo, el método sustituye internamente el equivalente de **vtMissing**y, a continuación, completa la operación.  
  
 En todos los métodos, indique que no se debe devolver el número de registros afectados estableciendo *RecordsAffected* a un puntero nulo. En este caso, el puntero null no es tanto un parámetro que falta como una indicación de que el método debería descartar el número de registros afectados.  
  
 Por lo tanto, para estos tres métodos, es válido para algo de código, como:  
  
```  
pConnection->Execute("commandText", NULL, adCmdText);   
pCommand->Execute(NULL, NULL, adCmdText);  
pRecordset->NextRecordset(NULL);  
```  
  
## <a name="error-handling"></a>Tratamiento de errores  
 En COM, la mayoría de las operaciones devuelve un código de retorno HRESULT que indica si una función se ha completado correctamente. El **#import** directiva genera código que envuelve cada método "sin formato" o una propiedad y comprueba el HRESULT devuelto. Si el valor HRESULT indica error, el código de contenedor produce un error de COM llamada _com_issue_errorex () con el código de retorno HRESULT como argumento. Objetos de error COM se pueden capturar en una **intente**-**catch** bloque. (Para una mayor eficacia, detecte una referencia a un **_com_error** objeto.)  
  
 Recuerde que éstos son los errores de ADO: son el resultado de la operación de ADO. Los errores devueltos por el proveedor subyacente aparecen como **Error** objetos en el **conexión** objeto **errores** colección.  
  
 El **#import** directiva sólo crea errores rutinas de control para los métodos y propiedades declarados en la DLL de ADO. Sin embargo, puede sacar partido de este mismo mecanismo control de errores escribiendo su propia macro o una función insertada de comprobación de errores. Vea el tema [extensiones de Visual C++](../../../ado/guide/appendixes/visual-c-extensions-for-ado.md), o el código en las secciones siguientes para obtener ejemplos.  
  
## <a name="visual-c-equivalents-of-visual-basic-conventions"></a>Equivalentes de Visual C++ de las convenciones de Visual Basic  
 El siguiente es un resumen de diversas convenciones de la documentación de ADO, codificadas en Visual Basic, así como sus equivalentes en Visual C++.  
  
### <a name="declaring-an-ado-object"></a>Declarar un objeto ADO  
 En Visual Basic, una variable de objeto ADO (en este caso para un **Recordset** objeto) se declara como sigue:  
  
```  
Dim rst As ADODB.Recordset  
```  
  
 La cláusula "`ADODB.Recordset`", es el ProgID de la **Recordset** tal como se define en el registro del objeto. Una nueva instancia de un **registro** objeto se declara como sigue:  
  
```  
Dim rst As New ADODB.Recordset  
```  
  
 -O bien-  
  
```  
Dim rst As ADODB.Recordset  
Set rst = New ADODB.Recordset  
```  
  
 En Visual C++, el **#import** directiva genera declaraciones de tipo puntero inteligente para todos los objetos de ADO. Por ejemplo, una variable que apunta a un **_Recordset** objeto es de tipo **_RecordsetPtr**y se declara como sigue:  
  
```  
_RecordsetPtr  rs;  
```  
  
 Una variable que apunta a una nueva instancia de un **_Recordset** objeto se declara como sigue:  
  
```  
_RecordsetPtr  rs("ADODB.Recordset");  
```  
  
 -O bien-  
  
```  
_RecordsetPtr  rs;  
rs.CreateInstance("ADODB.Recordset");  
```  
  
 -O bien-  
  
```  
_RecordsetPtr  rs;  
rs.CreateInstance(__uuidof(_Recordset));  
```  
  
 Después de la **CreateInstance** se llama al método, la variable se puede utilizar como se indica a continuación:  
  
```  
rs->Open(...);  
```  
  
 Tenga en cuenta que en un caso, el "`.`" operador se utiliza como si la variable fuera una instancia de una clase (`rs.CreateInstance`) y en otro caso, el "`->`" operador se utiliza como si la variable fuera un puntero a una interfaz (`rs->Open`).  
  
 Una variable se puede usar de dos maneras porque el "`->`" operador está sobrecargado para permitir a una instancia de una clase se comporte como un puntero a una interfaz. Un miembro de clase privada de la variable de instancia contiene un puntero a la **_Recordset** interfaz; el "`->`" operador devuelve ese puntero; y el puntero devuelto obtiene acceso a los miembros de la **_Recordset ** objeto.  
  
### <a name="coding-a-missing-parameter--string"></a>Codificar un parámetro que falta: cadena  
 Cuando necesite una falta de código **cadena** operando en Visual Basic, simplemente omita el operando. Debe especificar el operando en Visual C++. Código de un **_bstr_t** que tiene una cadena vacía como un valor.  
  
```  
_bstr_t strMissing(L"");  
```  
  
### <a name="coding-a-missing-parameter--variant"></a>Codificar un parámetro que falta: Variant  
 Cuando necesite una falta de código **Variant** operando en Visual Basic, simplemente omita el operando. Debe especificar todos los operandos en Visual C++. Una falta de código **Variant** parámetro con un **_variant_t** establecida en el valor especial DISP_E_PARAMNOTFOUND y escriba VT_ERROR. O bien, especifique **vtMissing**, que es una constante predefinida equivalente proporciona el **#import** directiva.  
  
```  
_variant_t  vtMissingYours(DISP_E_PARAMNOTFOUND, VT_ERROR);   
```  
  
 - o utilice-  
  
```  
...vtMissing...;  
```  
  
### <a name="declaring-a-variant"></a>Declarar una variante  
 En Visual Basic, un **Variant** se declara con el **Dim** instrucción como se indica a continuación:  
  
```  
Dim VariableName As Variant  
```  
  
 En Visual C++, declare una variable como tipo **_variant_t**. Representación esquemática unos **_variant_t** declaraciones se muestran a continuación.  
  
> [!NOTE]
>  Estas declaraciones simplemente proporcionan una idea general de lo que debe incluir el código en su propio programa. Para obtener más información, vea los ejemplos siguientes y la documentación de Visual C++.  
  
```  
_variant_t  VariableName(value);  
_variant_t  VariableName((data type cast) value);  
_variant_t  VariableName(value, VT_DATATYPE);  
_variant_t  VariableName(interface * value, bool fAddRef = true);  
```  
  
### <a name="using-arrays-of-variants"></a>Utilizar matrices de variantes  
 En Visual Basic, matrices de **variantes** se pueden codificar con la **Dim** instrucción, o bien puede usar el **matriz** funcione, como se muestra en el ejemplo de código siguiente:  
  
```  
Public Sub ArrayOfVariants  
Dim cn As ADODB.Connection  
Dim rs As ADODB.Recordset  
Dim fld As ADODB.Field  
  
    cn.Open "DSN=pubs"  
    rs = cn.OpenSchema(adSchemaColumns, _  
        Array(Empty, Empty, "authors", Empty))  
    For Each fld in rs.Fields  
        Debug.Print "Name = "; fld.Name  
    Next fld  
    rs.Close  
    cn.Close  
End Sub  
```  
  
 El siguiente ejemplo de Visual C++ muestra cómo utilizar un **SafeArray** utilizar con un **_variant_t**.  
  
#### <a name="notes"></a>Notas  
 Las notas siguientes corresponden a secciones comentadas en el ejemplo de código.  
  
1.  Una vez más, se define la función inline TESTHR() para aprovechar el mecanismo de control de errores existente.  
  
2.  Solo necesita una matriz unidimensional, por lo que puede usar **SafeArrayCreateVector**, en lugar de propósito general **SAFEARRAYBOUND** declaración y **SafeArrayCreate** función. La siguiente es cuál sería que el código con **SafeArrayCreate**:  
  
    ```  
       SAFEARRAYBOUND   sabound[1];  
       sabound[0].lLbound = 0;  
       sabound[0].cElements = 4;  
       pSa = SafeArrayCreate(VT_VARIANT, 1, sabound);  
    ```  
  
3.  El esquema identificado por la constante enumerada, **adSchemaColumns**, está asociado con cuatro columnas de restricción: TABLE_CATALOG, TABLE_SCHEMA, TABLE_NAME y COLUMN_NAME. Por lo tanto, una matriz de **Variant** se crea valores con cuatro elementos. A continuación, se especifica un valor de restricción que corresponde a la tercera columna, TABLE_NAME.  
  
     El **Recordset** que se devuelve consta de varias columnas, un subconjunto de los cuales forman las columnas de restricción. Los valores de las columnas de restricción para cada fila devuelta deben ser el mismo que los valores de restricción correspondientes.  
  
4.  Aquellos que estén familiarizados con **SAFEARRAY** puede ser sorprende que **SafeArrayDestroy**() no se llama antes de la salida. De hecho, una llamada a **SafeArrayDestroy**() en este caso, se producirá una excepción de tiempo de ejecución. El motivo es que el destructor de `vtCriteria` llamará **VariantClear**() cuando el **_variant_t** sale del ámbito, que liberará el **SafeArray**. Al llamar a **SafeArrayDestroy**, sin borrar manualmente el **_variant_t**, provocará que el destructor intente borrar no válido **SafeArray** puntero.  
  
     Si **SafeArrayDestroy** estaban llama, el código sería similar al siguiente:  
  
    ```  
          TESTHR(SafeArrayDestroy(pSa));  
       vtCriteria.vt = VT_EMPTY;  
          vtCriteria.parray = NULL;  
    ```  
  
     Sin embargo, resulta mucho más fácil permitir que el **_variant_t** administrar la **SafeArray**.  
  
```  
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
  
### <a name="using-property-getputputref"></a>Uso de la propiedad Get/Put/PutRef  
 En Visual Basic, el nombre de una propiedad no se califican por si se recuperan, asignado o asigna una referencia.  
  
```  
Public Sub GetPutPutRef  
Dim rs As New ADODB.Recordset  
Dim cn As New ADODB.Connection  
Dim sz as Integer  
cn.Open "Provider=sqloledb;Data Source=yourserver;" & _  
         "Initial Catalog=pubs;Integrated Security=SSPI;"  
rs.PageSize = 10  
sz = rs.PageSize  
rs.ActiveConnection = cn  
rs.Open "authors",,adOpenStatic  
' ...  
rs.Close  
cn.Close  
End Sub  
```  
  
 Este ejemplo de Visual C++ se muestra la **obtener**/**colocar**/**PutRef***propiedad*.  
  
#### <a name="notes"></a>Notas  
 Las notas siguientes corresponden a secciones comentadas en el ejemplo de código.  
  
1.  Este ejemplo utiliza dos formas de un argumento de cadena que falta: una constante explícita, **strMissing**y una cadena que el compilador utilizará para crear un archivo temporal **_bstr_t** que existirá durante el ámbito de la ** Abra** método.  
  
2.  No es necesario convertir explícitamente el operando de `rs->PutRefActiveConnection(cn)` a `(IDispatch *)` porque el tipo del operando es ya `(IDispatch *)`.  
  
```  
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
  
### <a name="using-getitemx-and-itemx"></a>Usar GetItem e Item [x]  
 Este ejemplo de Visual Basic muestra la sintaxis estándar y alternativa para **elemento**().  
  
```  
Public Sub GetItemItem  
Dim rs As New ADODB.Recordset  
Dim name as String  
rs = rs.Open "authors", "DSN=pubs;", adOpenDynamic, _  
         adLockBatchOptimistic, adTable  
name = rs(0)  
' -or-  
name = rs.Fields.Item(0)  
rs(0) = "Test"  
rs.UpdateBatch  
' Restore name  
rs(0) = name  
rs.UpdateBatch  
rs.Close  
End Sub  
```  
  
 Se muestra en este ejemplo de Visual C++ **elemento**.  
  
> [!NOTE]
>  La nota siguiente corresponde a secciones comentadas en el ejemplo de código: cuando se tiene acceso a la colección con **elemento**, el índice, **2**, deben convertirse a **largo** para un se invocará el constructor adecuado.  
  
```  
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
 El siguiente ejemplo de Visual C++ se muestra el uso (IDispatch *) para punteros a objetos ADO cast.  
  
#### <a name="notes"></a>Notas  
 Las notas siguientes corresponden a secciones comentadas en el ejemplo de código.  
  
1.  Especificar un formato de archivo **conexión** objeto codificado explícitamente **Variant**. Conviértalo explícitamente con (IDispatch \*) por lo que se invocará el constructor correcto. Además, establezca explícitamente el segundo **_variant_t** parámetro en el valor predeterminado de **true**, por lo que el recuento de referencias de objeto serán las correctas cuando el **Recordset:: Open** finaliza la operación.  
  
2.  La expresión `(_bstr_t)`, no es una conversión de tipos, pero un **_variant_t** operador que extrae una **_bstr_t** de cadena de la **Variant** devuelto por **valor **.  
  
 La expresión `(char*)`, no es una conversión de tipos, pero un **_bstr_t** operador que extrae un puntero a la cadena encapsulada en un **_bstr_t** objeto.  
  
 Esta sección de código muestra algunos de los comportamientos útiles de **_variant_t** y **_bstr_t** operadores.  
  
```  
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
