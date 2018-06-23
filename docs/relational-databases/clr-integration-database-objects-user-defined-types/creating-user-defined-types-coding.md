---
title: Codificar tipos definidos por el usuario | Documentos de Microsoft
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: reference
ms.tgt_pltfrm: ''
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- validation [CLR integration]
- UDTs [CLR integration], coding
- UserDefined serialization format [CLR integration]
- Point UDT
- Parse method
- null values [CLR integration]
- ToString method
- ValidatePoint method
- attributes [CLR integration]
- coding user-defined types [CLR integration]
- Read method
- Write method
- nullability [CLR integration]
- user-defined types [CLR integration], coding
- Currency UDT
- validating UDT values
- exposing UDT properties [CLR integration]
ms.assetid: 1e5b43b3-4971-45ee-a591-3f535e2ac722
caps.latest.revision: 37
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: b3a698c63fa5fc7e5a0802716b3112df31cf241f
ms.sourcegitcommit: a78fa85609a82e905de9db8b75d2e83257831ad9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2018
ms.locfileid: "35697906"
---
# <a name="creating-user-defined-types---coding"></a>Crear tipos definidos por el usuario - codificación
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Al codificar la definición de un tipo definido por el usuario (UDT), debe implementar varias características, en función de si implementa el UDT como una clase o como una estructura, así como de las opciones de formato y serialización que haya elegido.  
  
 En el ejemplo de esta sección muestra cómo implementar un **punto** UDT como una **struct** (o **estructura** en Visual Basic). El **punto** UDT consta de X y coordenadas Y se implementan como procedimientos de propiedad.  
  
 Para definir un UDT, se requieren los espacios de nombres siguientes:  
  
```vb  
Imports System  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
```  
  
```csharp  
using System;  
using System.Data.SqlTypes;  
using Microsoft.SqlServer.Server;  
```  
  
 El **Microsoft.SqlServer.Server** espacio de nombres contiene los objetos necesarios para varios atributos del UDT y **System.Data.SqlTypes** espacio de nombres contiene las clases que representan [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipos de datos nativos disponibles para el ensamblado. Es obvio que puede haber espacios de nombres adicionales que el ensamblado necesite para funcionar correctamente. El **punto** UDT también usa el **System.Text** espacio de nombres para trabajar con cadenas.  
  
> [!NOTE]  
>  Objetos de base de datos de Visual C++, como UDT, compilados con **/CLR: pure** no se admiten para la ejecución.  
  
## <a name="specifying-attributes"></a>Especificar atributos  
 Los atributos determinan el modo de usar la serialización para construir la representación de almacenamiento de los UDT y para transmitirlos por valor al cliente.  
  
 El **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute** es necesario. El **Serializable** atributo es opcional. También puede especificar el **Microsoft.SqlServer.Server.SqlFacetAttribute** para proporcionar información sobre el tipo de valor devuelto de un UDT. Para obtener más información, vea [Atributos personalizados para las rutinas CLR](../../relational-databases/clr-integration/database-objects/clr-integration-custom-attributes-for-clr-routines.md).  
  
### <a name="point-udt-attributes"></a>Atributos del UDT Point  
 El **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute** establece el formato de almacenamiento para el **punto** UDT **nativo**. **IsByteOrdered** está establecido en **true**, lo que garantiza que los resultados de las comparaciones son los mismos en SQL Server como si la comparación mismo hubiera tenido lugar en código administrado. El UDT implementa la **System.Data.SqlTypes.INullable** interfaz para hacer compatible con el carácter null de UDT.  
  
 El siguiente fragmento de código muestra los atributos para el **punto** UDT.  
  
```vb  
<Serializable(), SqlUserDefinedTypeAttribute(Format.Native, _  
  IsByteOrdered:=True)> _  
  Public Structure Point  
    Implements INullable  
```  
  
```csharp  
[Serializable]  
[Microsoft.SqlServer.Server.SqlUserDefinedType(Format.Native,  
  IsByteOrdered=true)]  
public struct Point : INullable  
{  
```  
  
## <a name="implementing-nullability"></a>Implementar la nulabilidad  
 Además de especificar correctamente los atributos de los ensamblados, el UDT también debe admitir la nulabilidad. UDT cargados en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] son compatibles con null, pero en orden para el UDT reconozca un valor null, el UDT debe implementar la **System.Data.SqlTypes.INullable** interfaz.  
  
 Debe crear una propiedad denominada **IsNull**, que es necesaria para determinar si un valor es null en el código de CLR. Cuando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] encuentra una instancia NULL de un UDT, el UDT se conserva mediante los métodos habituales de control de valores NULL. El servidor no pierde tiempo serializando o deserializando el UDT sin necesidad y no desaprovecha espacio para almacenar un UDT NULL. Esta comprobación de valores NULL se realiza cada vez que se usa un UDT de CLR, lo que significa que el uso de la construcción IS NULL de [!INCLUDE[tsql](../../includes/tsql-md.md)] para comprobar los UDT que son NULL debería funcionar siempre. El **IsNull** propiedad también se utiliza el servidor para comprobar si una instancia es null. Una vez que el servidor determina que el UDT es NULL, puede usar su propio control de valores NULL nativos.  
  
 El **get()** método **IsNull** no es usar la grafía especial en absoluto. Si un **punto** variable **@p** es **Null**, a continuación, **@p.IsNull** , de forma predeterminada, evaluará como "NULL", no como "1". Esto es porque el **SqlMethod(OnNullCall)** atributo de la **get() IsNull** método el valor predeterminado es false. Dado que el objeto es **Null**, cuando se solicita la propiedad no se deserializa el objeto, no se llama al método y se devuelve un valor predeterminado es "NULL".  
  
### <a name="example"></a>Ejemplo  
 En el ejemplo siguiente, la variable `is_Null` es privada y contiene el estado NULL para la instancia del UDT. El código debe mantener un valor adecuado para `is_Null`. El UDT también debe tener una propiedad estática denominada **Null** que devuelve una instancia de valor null del UDT. Esto permite al UDT devolver un valor NULL si la instancia también es NULL en la base de datos.  
  
```vb  
Private is_Null As Boolean  
  
Public ReadOnly Property IsNull() As Boolean _  
   Implements INullable.IsNull  
    Get  
        Return (is_Null)  
    End Get  
End Property  
  
Public Shared ReadOnly Property Null() As Point  
    Get  
        Dim pt As New Point  
        pt.is_Null = True  
        Return (pt)  
    End Get  
End Property  
```  
  
```csharp  
private bool is_Null;  
  
public bool IsNull  
{  
    get  
    {  
        return (is_Null);  
    }  
}  
  
public static Point Null  
{  
    get  
    {  
        Point pt = new Point();  
        pt.is_Null = true;  
        return pt;  
    }  
}  
```  
  
### <a name="is-null-vs-isnull"></a>IS NULL frente a IsNull  
 Considere la posibilidad de una tabla que contiene el esquema Points (id int, punto de ubicación), donde **punto** es un UDT de CLR y las consultas siguientes:  
  
```  
--Query 1  
SELECT ID  
FROM Points  
WHERE NOT (location IS NULL) -- Or, WHERE location IS NOT NULL;  
```  
  
```  
--Query 2:  
SELECT ID  
FROM Points  
WHERE location.IsNull = 0;  
```  
  
 Ambas consultas devuelven los identificadores de puntos con no -**Null** ubicaciones. En la consulta 1 (Query 1), se usa el control habitual de valores NULL y no se requiere ninguna deserialización de UDT. Consulta 2, por otro lado, tiene que deserializar cada uno de ellos no -**Null** objeto y llamar a CLR para obtener el valor de la **IsNull** propiedad. Evidentemente, mediante **IS NULL** tendrá mejor rendimiento y nunca debe ser un motivo para leer el **IsNull** propiedad de un UDT de [!INCLUDE[tsql](../../includes/tsql-md.md)] código.  
  
 Por lo tanto, ¿qué es el uso de la **IsNull** propiedad? En primer lugar, es necesario para determinar si un valor es **Null** desde el código CLR. En segundo lugar, el servidor necesita una manera de probar si una instancia es **Null**, por lo que esta propiedad se usa en el servidor. Una vez que determina que es **Null**, puede usar su propio control null nativos para administrarla.  
  
## <a name="implementing-the-parse-method"></a>Implementar el método Parse  
 El **analizar** y **ToString** métodos permiten las conversiones entre las representaciones de cadena del UDT. El **analizar** método permite una cadena que se puede convertir en un UDT. Debe declararse como **estático** (o **Shared** en Visual Basic) y toman un parámetro de tipo **System.Data.SqlTypes.SqlString**.  
  
 El código siguiente implementa la **analizar** método para el **punto** UDT, que separa las coordenadas X e Y. El **analizar** método tiene un único argumento de tipo **System.Data.SqlTypes.SqlString**y se da por supuesto que los valores X e Y se proporcionan como una cadena delimitada por comas. Establecer el **Microsoft.SqlServer.Server.SqlMethodAttribute.OnNullCall** atribuir a **false** evita la **analizar** método puedan ser llamados desde una instancia null de Punto.  
  
```vb  
<SqlMethod(OnNullCall:=False)> _  
Public Shared Function Parse(ByVal s As SqlString) As Point  
    If s.IsNull Then  
        Return Null  
    End If  
  
    ' Parse input string here to separate out points.  
    Dim pt As New Point()  
    Dim xy() As String = s.Value.Split(",".ToCharArray())  
    pt.X = Int32.Parse(xy(0))  
    pt.Y = Int32.Parse(xy(1))  
    Return pt  
End Function  
```  
  
```csharp  
[SqlMethod(OnNullCall = false)]  
public static Point Parse(SqlString s)  
{  
    if (s.IsNull)  
        return Null;  
  
    // Parse input string to separate out points.  
    Point pt = new Point();  
    string[] xy = s.Value.Split(",".ToCharArray());  
    pt.X = Int32.Parse(xy[0]);  
    pt.Y = Int32.Parse(xy[1]);  
    return pt;  
}  
```  
  
## <a name="implementing-the-tostring-method"></a>Implementar el método ToString  
 El **ToString** método convierte el **punto** UDT en un valor de cadena. En este caso, se devuelve la cadena "NULL" para una instancia Null de la **punto** tipo. El **ToString** método invierte el **analizar** método mediante el uso de un **System.Text.StringBuilder** para devolver delimitada por comas **System.String**que consta de los valores de coordenadas X e Y. Dado que **InvokeIfReceiverIsNull** el valor predeterminado es false, la comprobación de una instancia null de **punto** no es necesario.  
  
```vb  
Private _x As Int32  
Private _y As Int32  
  
Public Overrides Function ToString() As String  
    If Me.IsNull Then  
        Return "NULL"  
    Else  
        Dim builder As StringBuilder = New StringBuilder  
        builder.Append(_x)  
        builder.Append(",")  
        builder.Append(_y)  
        Return builder.ToString  
    End If  
End Function  
```  
  
```csharp  
private Int32 _x;  
private Int32 _y;  
  
public override string ToString()  
{  
    if (this.IsNull)  
        return "NULL";  
    else  
    {  
        StringBuilder builder = new StringBuilder();  
        builder.Append(_x);  
        builder.Append(",");  
        builder.Append(_y);  
        return builder.ToString();  
    }  
}  
```  
  
## <a name="exposing-udt-properties"></a>Exponer las propiedades del UDT  
 El **punto** UDT expone las coordenadas X e Y que se implementan como propiedades públicas de lectura y escritura de tipo **System.Int32**.  
  
```vb  
Public Property X() As Int32  
    Get  
        Return (Me._x)  
    End Get  
  
    Set(ByVal Value As Int32)  
        _x = Value  
    End Set  
End Property  
  
Public Property Y() As Int32  
    Get  
        Return (Me._y)  
    End Get  
  
    Set(ByVal Value As Int32)  
        _y = Value  
    End Set  
End Property  
```  
  
```csharp  
public Int32 X  
{  
    get  
    {  
        return this._x;  
    }  
    set   
    {  
        _x = value;  
    }  
}  
  
public Int32 Y  
{  
    get  
    {  
        return this._y;  
    }  
    set  
    {  
        _y = value;  
    }  
}  
```  
  
## <a name="validating-udt-values"></a>Validar los valores UDT  
 Al trabajar con datos UDT, [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] convierte automáticamente los valores binarios en valores UDT. Este proceso de conversión implica la comprobación de que los valores son adecuados para el formato de serialización del tipo, así como asegurarse de que el valor puede deserializarse correctamente. Esto garantiza que el valor se puede convertir al formato binario. En el caso de los UDT ordenados por bytes, esto también garantiza que el valor binario resultante coincida con el valor binario original. De esta forma, se evita que los valores que no son válidos se conserven en la base de datos. En algunos casos, este nivel de comprobación puede resultar inadecuado. Puede ser necesaria una validación adicional cuando se exige que los valores UDT se encuentren en un dominio o intervalo esperado. Por ejemplo, un UDT que implementa una fecha podría exigir que el valor de día sea un número positivo que pertenezca a un intervalo determinado de valores válidos.  
  
 El **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute.ValidationMethodName** propiedad de la **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute** permite proporcionar el nombre de un método de validación que el servidor que ejecuta cuando los datos se asignan a un UDT o convertidos en un UDT. **ValidationMethodName** también se llama durante la ejecución de la utilidad bcp, BULK INSERT, DBCC CHECKDB, DBCC CHECKFILEGROUP, DBCC CHECKTABLE, consultas distribuidas y las operaciones de datos tabulares flujo TDS procedimiento remoto (RPC) de la llamada. El valor predeterminado de **ValidationMethodName** es null, que indica que no hay ningún método de validación.  
  
### <a name="example"></a>Ejemplo  
 El siguiente fragmento de código muestra la declaración de la **punto** (clase), que especifica un **ValidationMethodName** de **ValidatePoint**.  
  
```vb  
<Serializable(), SqlUserDefinedTypeAttribute(Format.Native, _  
  IsByteOrdered:=True, _  
  ValidationMethodName:="ValidatePoint")> _  
  Public Structure Point  
```  
  
```csharp  
[Serializable]  
[Microsoft.SqlServer.Server.SqlUserDefinedType(Format.Native,  
  IsByteOrdered=true,   
  ValidationMethodName = "ValidatePoint")]  
public struct Point : INullable  
{  
```  
  
 Si se especifica un método de validación, debe tener una firma de aspecto similar al fragmento de código siguiente.  
  
```vb  
Private Function ValidationFunction() As Boolean  
    If (validation logic here) Then  
        Return True  
    Else  
        Return False  
    End If  
End Function  
```  
  
```csharp  
private bool ValidationFunction()  
{  
    if (validation logic here)  
    {  
        return true;  
    }  
    else  
    {  
        return false;  
    }  
}  
```  
  
 El método de validación puede tener cualquier ámbito y debe devolver **true** si el valor es válido, y **false** en caso contrario. Si el método devuelve **false** o se producirá una excepción, el valor se trata no válido y un error se generan.  
  
 En el ejemplo siguiente, el código solamente permite valores iguales a cero o mayores que las coordenadas X e Y.  
  
```vb  
Private Function ValidatePoint() As Boolean  
    If (_x >= 0) And (_y >= 0) Then  
        Return True  
    Else  
        Return False  
    End If  
End Function  
```  
  
```csharp  
private bool ValidatePoint()  
{  
    if ((_x >= 0) && (_y >= 0))  
    {  
        return true;  
    }  
    else  
    {  
        return false;  
    }  
}  
```  
  
### <a name="validation-method-limitations"></a>Limitaciones del método de validación  
 El servidor llama al método de validación cuando está realizando conversiones, no cuando los datos se insertan mediante el establecimiento de propiedades individuales ni cuando los datos se insertan mediante una instrucción INSERT de [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 Debe llamar explícitamente al método de validación de establecedores de propiedad y el **analizar** método si desea que el método de validación debe ejecutar en todas las situaciones. No se trata de ningún requisito e incluso, en algunos casos, es posible que no se desee.  
  
### <a name="parse-validation-example"></a>Ejemplo de validación de Parse  
 Para asegurarse de que el **ValidatePoint** se invoca al método en el **punto** (clase), debe llamarlo desde el **analizar** método y desde los procedimientos de propiedad que establece X e Y valores de las coordenadas. El siguiente fragmento de código muestra cómo llamar a la **ValidatePoint** método de validación de la **analizar** función.  
  
```vb  
<SqlMethod(OnNullCall:=False)> _  
Public Shared Function Parse(ByVal s As SqlString) As Point  
    If s.IsNull Then  
        Return Null  
    End If  
  
    ' Parse input string here to separate out points.  
    Dim pt As New Point()  
    Dim xy() As String = s.Value.Split(",".ToCharArray())  
    pt.X = Int32.Parse(xy(0))  
    pt.Y = Int32.Parse(xy(1))  
  
    ' Call ValidatePoint to enforce validation  
    ' for string conversions.  
    If Not pt.ValidatePoint() Then  
        Throw New ArgumentException("Invalid XY coordinate values.")  
    End If  
    Return pt  
End Function  
```  
  
```csharp  
[SqlMethod(OnNullCall = false)]  
public static Point Parse(SqlString s)  
{  
    if (s.IsNull)  
        return Null;  
  
    // Parse input string to separate out points.  
    Point pt = new Point();  
    string[] xy = s.Value.Split(",".ToCharArray());  
    pt.X = Int32.Parse(xy[0]);  
    pt.Y = Int32.Parse(xy[1]);  
  
    // Call ValidatePoint to enforce validation  
    // for string conversions.  
    if (!pt.ValidatePoint())   
        throw new ArgumentException("Invalid XY coordinate values.");  
    return pt;  
}  
```  
  
### <a name="property-validation-example"></a>Ejemplo de validación de propiedad  
 El siguiente fragmento de código muestra cómo llamar a la **ValidatePoint** método de validación de los procedimientos de propiedad que establece las coordenadas X e Y.  
  
```vb  
Public Property X() As Int32  
    Get  
        Return (Me._x)  
    End Get  
  
    Set(ByVal Value As Int32)  
        Dim temp As Int32 = _x  
        _x = Value  
        If Not ValidatePoint() Then  
            _x = temp  
            Throw New ArgumentException("Invalid X coordinate value.")  
        End If  
    End Set  
End Property  
  
Public Property Y() As Int32  
    Get  
        Return (Me._y)  
    End Get  
  
    Set(ByVal Value As Int32)  
        Dim temp As Int32 = _y  
        _y = Value  
        If Not ValidatePoint() Then  
            _y = temp  
            Throw New ArgumentException("Invalid Y coordinate value.")  
        End If  
    End Set  
End Property  
```  
  
```csharp  
    public Int32 X  
{  
    get  
    {  
        return this._x;  
    }  
    // Call ValidatePoint to ensure valid range of Point values.  
    set   
    {  
        Int32 temp = _x;  
        _x = value;  
        if (!ValidatePoint())  
        {  
            _x = temp;  
            throw new ArgumentException("Invalid X coordinate value.");  
        }  
    }  
}  
  
public Int32 Y  
{  
    get  
    {  
        return this._y;  
    }  
    set  
    {  
        Int32 temp = _y;  
        _y = value;  
        if (!ValidatePoint())  
        {  
            _y = temp;  
            throw new ArgumentException("Invalid Y coordinate value.");  
        }  
    }  
}  
```  
  
## <a name="coding-udt-methods"></a>Codificar métodos UDT  
 Cuando codifique los métodos UDT, tenga en cuenta si el algoritmo usado podría cambiar con el tiempo. En ese caso, es posible que desee considerar la posibilidad de crear una clase independiente para los métodos que usa el UDT. Si el algoritmo cambia, puede volver a compilar la clase con el nuevo código, así como cargar el ensamblado en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sin que esto afecte al UDT. En muchos casos, los UDT pueden volver a cargarse mediante la instrucción ALTER ASSEMBLY de [!INCLUDE[tsql](../../includes/tsql-md.md)], pero eso podría causar problemas con los datos existentes. Por ejemplo, el **moneda** UDT incluido con el **AdventureWorks** usos de la base de datos de ejemplo un **ConvertCurrency** función para convertir los valores de moneda, que se implementa en una clase independiente. Es posible que en un futuro los algoritmos de conversión cambien de modo impredecible o que se necesite nueva funcionalidad. Separar la **ConvertCurrency** funcionar desde el **moneda** implementación de UDT proporciona mayor flexibilidad al planear los cambios futuros.  
  
### <a name="example"></a>Ejemplo  
 El **punto** clase contiene tres métodos simples para calcular la distancia: **distancia**, **DistanceFrom** y **DistanceFromXY**. Cada uno de ellos devuelve un **doble** calcula la distancia de **punto** a cero, la distancia desde un punto determinado a **punto**, y la distancia desde las coordenadas X e Y especificadas para **punto**. **Distancia** y **DistanceFrom** cada llamada **DistanceFromXY**y se muestra cómo usar argumentos distintos para cada método.  
  
```vb  
' Distance from 0 to Point.  
<SqlMethod(OnNullCall:=False)> _  
Public Function Distance() As Double  
    Return DistanceFromXY(0, 0)  
End Function  
  
' Distance from Point to the specified point.  
<SqlMethod(OnNullCall:=False)> _  
Public Function DistanceFrom(ByVal pFrom As Point) As Double  
    Return DistanceFromXY(pFrom.X, pFrom.Y)  
End Function  
  
' Distance from Point to the specified x and y values.  
<SqlMethod(OnNullCall:=False)> _  
Public Function DistanceFromXY(ByVal ix As Int32, ByVal iy As Int32) _  
    As Double  
    Return Math.Sqrt(Math.Pow(ix - _x, 2.0) + Math.Pow(iy - _y, 2.0))  
End Function  
```  
  
```csharp  
// Distance from 0 to Point.  
[SqlMethod(OnNullCall = false)]  
public Double Distance()  
{  
    return DistanceFromXY(0, 0);  
}  
  
// Distance from Point to the specified point.  
[SqlMethod(OnNullCall = false)]  
public Double DistanceFrom(Point pFrom)  
{  
    return DistanceFromXY(pFrom.X, pFrom.Y);  
}  
  
// Distance from Point to the specified x and y values.  
[SqlMethod(OnNullCall = false)]  
public Double DistanceFromXY(Int32 iX, Int32 iY)  
{  
    return Math.Sqrt(Math.Pow(iX - _x, 2.0) + Math.Pow(iY - _y, 2.0));  
}  
```  
  
### <a name="using-sqlmethod-attributes"></a>Usar atributos SqlMethod  
 El **Microsoft.SqlServer.Server.SqlMethodAttribute** clase proporciona atributos personalizados que pueden usarse para marcar las definiciones de método con el fin de especificar el determinismo en comportamientos de llamada null y para especificar si un método es un método mutador. Se asume el uso de valores predeterminados para estas propiedades y solamente se usa el atributo personalizado cuando se necesita un valor no predeterminado.  
  
> [!NOTE]  
>  El **SqlMethodAttribute** clase hereda de la **SqlFunctionAttribute** de la clase, por lo que **SqlMethodAttribute** hereda el **FillRowMethodName** y **TableDefinition** campos de **SqlFunctionAttribute**. Esto significa que es posible escribir un método con valores de tabla, que no es el caso. Compila el método y el ensamblado de implementar, pero un error sobre la **IEnumerable** devolver el tipo se genera en tiempo de ejecución con el siguiente mensaje: "método, propiedad o campo '\<nombre >' en clase\<(clase) >' en el ensamblado '\<ensamblado >' tiene el tipo de valor devuelto no válido. "  
  
 En la tabla siguiente se describe algunas de las partes significativas **Microsoft.SqlServer.Server.SqlMethodAttribute** propiedades que pueden usarse en métodos UDT y enumeran sus valores predeterminados.  
  
 DataAccess  
 Indica si la función implica el acceso a los datos de usuario almacenados en la instancia local de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Valor predeterminado es **DataAccessKind**. **Ninguno**.  
  
 IsDeterministic  
 Indica si la función genera los mismos valores de salida si se especifican los mismos valores de entrada y el mismo estado de la base de datos. Valor predeterminado es **false**.  
  
 IsMutator  
 Indica si el método produce un cambio de estado en la instancia del UDT. Valor predeterminado es **false**.  
  
 IsPrecise  
 Indica si la función implica cálculos imprecisos, como operaciones de punto flotante. Valor predeterminado es **false**.  
  
 OnNullCall  
 Indica si se llama al método cuando se especifican argumentos de entrada de referencia NULL. Valor predeterminado es **true**.  
  
### <a name="example"></a>Ejemplo  
 El **Microsoft.SqlServer.Server.SqlMethodAttribute.IsMutator** propiedad le permite marcar un método que permite un cambio en el estado de una instancia de un UDT. [!INCLUDE[tsql](../../includes/tsql-md.md)] no permite que el usuario establezca dos propiedades UDT en la cláusula SET de una instrucción UPDATE. Sin embargo, puede tener un método marcado como mutador que cambie los dos miembros.  
  
> [!NOTE]  
>  No se permite el uso de métodos mutadores en las consultas. Solo puede llamarse a estos métodos en instrucciones de asignación o en instrucciones de modificación de datos. Si un método marcado como mutador no devuelve **void** (o no es un **Sub** en Visual Basic), CREATE TYPE generará un error.  
  
 La instrucción siguiente asume la existencia de un **triángulos** UDT que tenga un **girar** método. El siguiente [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucción update, se invoca el **girar** método:  
  
```  
UPDATE Triangles SET t.RotateY(0.6) WHERE id=5  
```  
  
 El **girar** método se decora con el **SqlMethod** configuración del atributo **IsMutator** a **true** para que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede marcar el método como un método mutador. El código también establece **OnNullCall** a **false**, lo que indica al servidor que el método devuelve una referencia nula (**nada** en Visual Basic) si la entrada parámetros son referencias nulas.  
  
```vb  
<SqlMethod(IsMutator:=True, OnNullCall:=False)> _  
Public Sub Rotate(ByVal anglex as Double, _  
  ByVal angley as Double, ByVal anglez As Double)   
   RotateX(anglex)  
   RotateY(angley)  
   RotateZ(anglez)  
End Sub  
```  
  
```csharp  
[SqlMethod(IsMutator = true, OnNullCall = false)]  
public void Rotate(double anglex, double angley, double anglez)   
{  
   RotateX(anglex);  
   RotateY(angley);  
   RotateZ(anglez);  
}  
```  
  
## <a name="implementing-a-udt-with-a-user-defined-format"></a>Implementar un UDT con un formato definido por el usuario  
 Al implementar un UDT con un formato definido por el usuario, debe implementar **lectura** y **escribir** métodos que implementan la interfaz Microsoft.SqlServer.Server.IBinarySerialize para controlar la serialización y deserializar los datos UDT. También debe especificar el **MaxByteSize** propiedad de la **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute**.  
  
### <a name="the-currency-udt"></a>El UDT Currency  
 El **moneda** UDT se incluye con los ejemplos CLR que se pueden instalar con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], empezando por [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].  
  
 El **moneda** UDT permite administrar cantidades de dinero en el sistema monetario de una referencia cultural determinada. Debe definir dos campos: un **cadena** para **CultureInfo**, que especifica quién emitió la moneda (en-us, por ejemplo) y un **decimal** para  **CurrencyValue**, la cantidad de dinero.  
  
 Aunque el servidor no lo está usando para realizar comparaciones, el **moneda** UDT implementa la **System.IComparable** interfaz, que expone un método único,  **System.IComparable.CompareTo**. Se usa del lado cliente en situaciones en las que se desean realizar comparaciones precisas u ordenar valores de moneda dentro de las referencias culturales.  
  
 El código que se ejecuta en CLR compara por separado la referencia cultural y el valor de moneda. Para el código [!INCLUDE[tsql](../../includes/tsql-md.md)], las acciones siguientes determinan la comparación:  
  
1.  Establecer el **IsByteOrdered** en true, lo que indica el atributo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para usar la representación binaria almacenada en disco para las comparaciones.  
  
2.  Use la **escribir** método para el **moneda** UDT para determinar cómo el UDT se conserva en el disco y, por tanto, cómo valores UDT se comparan y pedidos para [!INCLUDE[tsql](../../includes/tsql-md.md)] operaciones.  
  
3.  Guardar el **moneda** UDT mediante el siguiente formato binario:  
  
    1.  Guarde la referencia cultural como una cadena codificada mediante UTF-16, con bytes del 0 al 19, que se rellena a la derecha con caracteres NULL.  
  
    2.  Use el byte 20 y los bytes siguientes para almacenar el valor decimal de la moneda.  
  
 El propósito del relleno es asegurarse de que la referencia cultural esté completamente separada del valor de moneda, de forma que al comparar un UDT con otro en código [!INCLUDE[tsql](../../includes/tsql-md.md)], los bytes de la referencia cultural se comparen con los bytes de la referencia cultural y los valores de bytes de moneda se comparen con los valores de bytes de moneda.  
  
 Para la lista de código completa la **moneda** UDT, siga las instrucciones para instalar el CLR ejemplos que encontrará en [ejemplos de motor de base de datos de SQL Server](http://msftengprodsamples.codeplex.com/).  
  
### <a name="currency-attributes"></a>Atributos de Currency  
 El **moneda** UDT se define con los siguientes atributos.  
  
```vb  
<Serializable(), Microsoft.SqlServer.Server.SqlUserDefinedType( _  
    Microsoft.SqlServer.Server.Format.UserDefined, _  
    IsByteOrdered:=True, MaxByteSize:=32), _  
    CLSCompliant(False)> _  
Public Structure Currency  
Implements INullable, IComparable, _  
Microsoft.SqlServer.Server.IBinarySerialize  
```  
  
```csharp  
[Serializable]  
[SqlUserDefinedType(Format.UserDefined,   
    IsByteOrdered = true, MaxByteSize = 32)]  
    [CLSCompliant(false)]  
    public struct Currency : INullable, IComparable, IBinarySerialize  
    {  
```  
  
## <a name="creating-read-and-write-methods-with-ibinaryserialize"></a>Crear métodos de lectura y escritura con IBinarySerialize  
 Cuando eliges **UserDefined** formato de serialización, también debe implementar la **IBinarySerialize** interfaz y crear sus propios **lectura** y **escribir**  métodos. Los procedimientos siguientes desde el **moneda** uso UDT el **System.IO.BinaryReader** y **System.IO.BinaryWriter** para leer y escribir en el UDT.  
  
```vb  
' IBinarySerialize methods  
' The binary layout is as follow:  
'    Bytes 0 - 19: Culture name, padded to the right with null  
'    characters, UTF-16 encoded  
'    Bytes 20+: Decimal value of money  
' If the culture name is empty, the currency is null.  
Public Sub Write(ByVal w As System.IO.BinaryWriter) _  
  Implements Microsoft.SqlServer.Server.IBinarySerialize.Write  
    If Me.IsNull Then  
        w.Write(nullMarker)  
        w.Write(System.Convert.ToDecimal(0))  
        Return  
    End If  
  
    If cultureName.Length > cultureNameMaxSize Then  
        Throw New ApplicationException(String.Format(CultureInfo.CurrentUICulture, _  
           "{0} is an invalid culture name for currency as it is too long.", cultureNameMaxSize))  
    End If  
  
    Dim paddedName As String = cultureName.PadRight(cultureNameMaxSize, CChar(vbNullChar))  
  
    For i As Integer = 0 To cultureNameMaxSize - 1  
        w.Write(paddedName(i))  
    Next i  
  
    ' Normalize decimal value to two places  
    currencyVal = Decimal.Floor(currencyVal * 100) / 100  
    w.Write(currencyVal)  
End Sub  
  
Public Sub Read(ByVal r As System.IO.BinaryReader) _  
  Implements Microsoft.SqlServer.Server.IBinarySerialize.Read  
    Dim name As Char() = r.ReadChars(cultureNameMaxSize)  
    Dim stringEnd As Integer = Array.IndexOf(name, CChar(vbNullChar))  
  
    If stringEnd = 0 Then  
        cultureName = Nothing  
        Return  
    End If  
  
    cultureName = New String(name, 0, stringEnd)  
    currencyVal = r.ReadDecimal()  
End Sub  
  
```  
  
```csharp  
// IBinarySerialize methods  
// The binary layout is as follow:  
//    Bytes 0 - 19:Culture name, padded to the right   
//    with null characters, UTF-16 encoded  
//    Bytes 20+:Decimal value of money  
// If the culture name is empty, the currency is null.  
public void Write(System.IO.BinaryWriter w)  
{  
    if (this.IsNull)  
    {  
        w.Write(nullMarker);  
        w.Write((decimal)0);  
        return;  
    }  
  
    if (cultureName.Length > cultureNameMaxSize)  
    {  
        throw new ApplicationException(string.Format(  
            CultureInfo.InvariantCulture,   
            "{0} is an invalid culture name for currency as it is too long.",   
            cultureNameMaxSize));  
    }  
  
    String paddedName = cultureName.PadRight(cultureNameMaxSize, '\0');  
    for (int i = 0; i < cultureNameMaxSize; i++)  
    {  
        w.Write(paddedName[i]);  
    }  
  
    // Normalize decimal value to two places  
    currencyValue = Decimal.Floor(currencyValue * 100) / 100;  
    w.Write(currencyValue);  
}  
public void Read(System.IO.BinaryReader r)  
{  
    char[] name = r.ReadChars(cultureNameMaxSize);  
    int stringEnd = Array.IndexOf(name, '\0');  
  
    if (stringEnd == 0)  
    {  
        cultureName = null;  
        return;  
    }  
  
    cultureName = new String(name, 0, stringEnd);  
    currencyValue = r.ReadDecimal();  
}  
```  
  
 Para la lista de código completa la **moneda** UDT, vea [ejemplos de motor de base de datos de SQL Server](http://msftengprodsamples.codeplex.com/).  
  
## <a name="see-also"></a>Vea también  
 [Crear un tipo definido por el usuario](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types.md)  
  
  
