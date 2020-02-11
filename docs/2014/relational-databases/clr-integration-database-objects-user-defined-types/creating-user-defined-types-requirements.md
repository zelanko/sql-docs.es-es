---
title: Requisitos de tipos definidos por el usuario | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- UDTs [CLR integration], requirements
- serialization
- Native serialization format [CLR integration]
- attributes [CLR integration]
- XML serialization [CLR integration]
- user-defined types [CLR integration], requirements
- user-defined serialization [CLR integration]
- user-defined types [CLR integration], Native serialization
- UDTs [CLR integration], Native serialization
ms.assetid: bedc3372-50eb-40f2-bcf2-d6db6a63b7e6
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 63f297f1a2a3ae738e00e37acf381b830ced9e7b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62919662"
---
# <a name="user-defined-type-requirements"></a>Requisitos de tipos definidos por el usuario
  Debe tomar varias decisiones de diseño importantes al crear un tipo definido por el usuario (UDT) que se va [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]a instalar en. Para la mayoría de los UDT, se recomienda la creación del UDT como una estructura, aunque también puede crearse como una clase. La definición del UDT debe cumplir las especificaciones de creación de los UDT a fin de registrarse con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="requirements-for-implementing-udts"></a>Requisitos para implementar un UDT  
 El UDT, para poder ejecutarse en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], debe implementar los requisitos siguientes en la definición del UDT:  
  
 El UDT debe especificar `Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute`. El uso de `System.SerializableAttribute` es opcional, aunque recomendable.  
  
-   El UDT debe implementar la interfaz `System.Data.SqlTypes.INullable` en la clase o estructura mediante la creación de un método público `static` (`Shared` en [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic) `Null`. 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tiene en cuenta el valor NULL de forma predeterminada. Esto es necesario para que el código que se ejecuta en el UDT pueda reconocer un valor NULL.  
  
-   El UDT debe contener un método `static` (o `Shared`) `Parse` público que admita el análisis y un método `ToString` público para la conversión en una representación de cadena del objeto.  
  
-   Un UDT con un formato de serialización definido por el usuario debe implementar la interfaz `System.Data.IBinarySerialize` y proporcionar un método `Read` y `Write`.  
  
-   El UDT debe implementar `System.Xml.Serialization.IXmlSerializable`, o el tipo de todas las propiedades y campos públicos debe ser serializable como XML o representarse con el atributo `XmlIgnore` si se requiere una invalidación de la serialización estándar.  
  
-   Solo debe haber una serialización de un objeto UDT. Se produce un error en la validación si las rutinas de serialización o deserialización reconocen más de una representación de un objeto determinado.  
  
-   
  `SqlUserDefinedTypeAttribute.IsByteOrdered` debe ser `true` para comparar los datos en orden de bytes. Si no se implementa la interfaz IComparable e `SqlUserDefinedTypeAttribute.IsByteOrdered` es `false`, las comparaciones del orden de bytes no se realizarán correctamente.  
  
-   Un UDT definido en una clase debe tener un constructor público que no tome ningún argumento. Si lo desea, puede crear otros constructores de clase sobrecargados.  
  
-   El UDT debe exponer elementos de datos como procedimientos de propiedad o campos públicos.  
  
-   Los nombres públicos no pueden tener más de 128 caracteres y deben ajustarse [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a las reglas de nomenclatura para los identificadores tal y como se definen en los [identificadores de base de datos](../databases/database-identifiers.md).  
  
-   Las columnas `sql_variant` no pueden contener instancias de un UDT.  
  
-   Los miembros heredados no son accesibles desde [!INCLUDE[tsql](../../includes/tsql-md.md)] porque el sistema de tipos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no es consciente de la jerarquía de herencia entre los UDT. Sin embargo, puede usar la herencia al estructurar sus clases y puede llamar a dichos métodos en la implementación del código administrado del tipo.  
  
-   No es posible sobrecargar los miembros, salvo el constructor de clase. Si crea un método sobrecargado, no se produce ningún error al registrar el ensamblado o crear el tipo en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La detección del método sobrecargado se produce en tiempo de ejecución, no cuando se crea el tipo. Puede haber métodos sobrecargados en la clase siempre y cuando no se invoquen nunca. Al invocar al método sobrecargado se produce un error.  
  
-   Los miembros `static` (o `Shared`) deben declararse como constantes o como de solo lectura. Los miembros estáticos no pueden ser mutables.  
  
-   Si el campo `SqlUserDefinedTypeAttribute.MaxByteSize` está establecido en -1, el UDT serializado puede ser tan grande como el límite de tamaño de un objeto grande (LOB), que actualmente es de 2 GB. El tamaño del UDT no puede superar el valor especificado en el campo `MaxByteSized`.  
  
> [!NOTE]  
>  Aunque el servidor no la usa para realizar comparaciones, también puede implementar la interfaz `System.IComparable`, que expone un método único, `CompareTo`. Se usa del lado cliente en situaciones en las que se desean realizar comparaciones precisas u ordenar los valores UDT.  
  
## <a name="native-serialization"></a>Serialización nativa  
 La elección de los atributos de serialización correctos para su UDT depende del tipo de UDT que está intentando crear. El formato de serialización `Native` usa una estructura muy simple que permite a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] almacenar en disco una representación nativa eficaz del UDT. Se recomienda el formato `Native` si el UDT es simple y solamente contiene campos de los tipos siguientes:  
  
 **bool**, **byte**, **SByte**, **Short**, **ushort**, **int**, **uint**, **Long**, **ULong**, **float**, **Double**, **SqlByte**, **SqlInt16**, **SqlInt32**, **SqlInt64**, **SqlDateTime**, **SqlSingle**, **SqlDouble**, **SqlMoney**, **SqlBoolean**  
  
 Los tipos de valor que se componen de los campos de los tipos `Native` anteriores son buenos candidatos `structs` para el formato, como en `Structures` Visual C#, (o tal como se conocen en Visual Basic). Por ejemplo, un UDT especificado con el formato de serialización `Native` puede contener un campo de otro UDT también especificado con el formato `Native`. Si la definición UDT es más compleja y contiene tipos de datos que no figuran en la lista anterior, debe especificar en su lugar el formato de serialización `UserDefined`.  
  
 El formato `Native` tiene los siguientes requisitos:  
  
-   El tipo no debe especificar un valor para `Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute.MaxByteSize`.  
  
-   Todos los campos deben ser serializables.  
  
-   Debe especificarse `System.Runtime.InteropServices.StructLayoutAttribute` como `StructLayout.LayoutKindSequential` si el UDT se define en una clase y no en una estructura. Este atributo controla el diseño físico de los campos de datos y se usa para imponer a los miembros que se coloquen en el orden en que aparecen. 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa este atributo para determinar el orden de los campos para los UDT con varios valores.  
  
 Para obtener un ejemplo de un UDT definido `Native` con serialización, vea el UDT Point en [codificar tipos definidos por el usuario](creating-user-defined-types-coding.md).  
  
## <a name="userdefined-serialization"></a>Serialización UserDefined  
 La configuración de formato `UserDefined` del atributo `Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute` otorga al desarrollador un control total sobre el formato binario. Al especificar la propiedad de atributo `Format` como `UserDefined`, debe hacer lo siguiente en el código:  
  
-   Especificar la propiedad de atributo `IsByteOrdered` opcional. El valor predeterminado es `false`.  
  
-   Especificar la propiedad `MaxByteSize` de `Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute`.  
  
-   Escribir código para implementar los métodos `Read` y `Write` del UDT implementando la interfaz `System.Data.Sql.IBinarySerialize`.  
  
 Para obtener un ejemplo de un UDT definido `UserDefined` con serialización, vea el UDT Currency en [codificar tipos definidos por el usuario](creating-user-defined-types-coding.md).  
  
> [!NOTE]  
>  Los campos UDT deben usar la serialización nativa o conservarse para indizarse.  
  
## <a name="serialization-attributes"></a>Atributos de serialización  
 Los atributos determinan el modo de usar la serialización para construir la representación de almacenamiento de los UDT y para transmitirlos por valor al cliente. Es necesario que especifique `Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute` al crear el UDT. El atributo `Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute` indica que la clase es un UDT y especifica el almacenamiento para el UDT. Si lo desea, puede especificar el atributo `Serializable`, aunque [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no lo requiere.  
  
 
  `Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute` tiene las siguientes propiedades.  
  
 `Format`  
 Especifica el formato de serialización, que puede ser `Native` o `UserDefined`, en función de los tipos de datos del UDT.  
  
 `IsByteOrdered`  
 Valor `Boolean` que determina la forma en que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] realiza comparaciones binarias en el UDT.  
  
 `IsFixedLength`  
 Indica si todas las instancias de este UDT tienen la misma longitud.  
  
 `MaxByteSize`  
 Tamaño máximo de la instancia, expresado en bytes. Es preciso especificar `MaxByteSize` con el formato de serialización `UserDefined`. En el caso de un UDT que tenga especificada una serialización definida por el usuario, `MaxByteSize` hace referencia al tamaño total del UDT en su formato serializado, tal y como lo defina el usuario. El valor de `MaxByteSize` debe estar comprendido en el intervalo de 1 a 8000 o estar establecido en -1 para indicar que el UDT es superior a 8000 bytes (el tamaño total no puede superar el tamaño LOB máximo). Consideremos un UDT en el que la propiedad sea una cadena de 10 caracteres (`System.Char`). Cuando el UDT se serialice mediante BinaryWriter, el tamaño total de la cadena serializada será de 22 bytes: 2 bytes por carácter Unicode UTF-16, multiplicados por el número máximo de caracteres, más 2 bytes de control por la sobrecarga que se produce al serializar un flujo binario. De modo que, al determinar el valor de `MaxByteSize`, el tamaño total del UDT serializado debe considerarse como el tamaño de los datos serializados en formato binario más la sobrecarga producida por la serialización.  
  
 `ValidationMethodName`  
 Nombre del método utilizado para validar las instancias del UDT.  
  
### <a name="setting-isbyteordered"></a>Valor IsByteOrdered  
 Cuando la propiedad `Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute.IsByteOrdered` se establece en `true`, se garantiza que los datos binarios serializados puedan usarse para la clasificación semántica de la información. De esta forma, cada instancia de un objeto UDT ordenado por bytes solamente puede tener una representación serializada. Cuando se lleva a cabo una operación de comparación en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en los bytes serializados, los resultados deben ser los mismos que si se hubiese realizado la misma operación de comparación en código administrado. También se admiten las características siguientes cuando `IsByteOrdered` se establece en `true`:  
  
-   Funcionalidad para crear los índices de las columnas de este tipo.  
  
-   Funcionalidad para crear las claves principal y externa, así como las restricciones CHECK y UNIQUE en las columnas de este tipo.  
  
-   Funcionalidad para usar las cláusulas [!INCLUDE[tsql](../../includes/tsql-md.md)] ORDER BY, GROUP BY y PARTITION BY. En estos casos, la representación binaria del tipo se usa para determinar el orden.  
  
-   Funcionalidad para usar los operadores de comparación en instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
-   Funcionalidad para conservar las columnas calculadas de este tipo.  
  
 Tenga en cuenta que los formatos de serialización `Native` y `UserDefined` admiten los siguientes operadores de comparación cuando `IsByteOrdered` se establece en `true`:  
  
-   Igual a (=)  
  
-   Distinto de (!=)  
  
-   Mayor que (>)  
  
-   Menor que (\<)  
  
-   Mayor o igual que (>=)  
  
-   Menor o igual que (<=)  
  
### <a name="implementing-nullability"></a>Implementar la nulabilidad  
 Además de especificar correctamente los atributos de los ensamblados, la clase también debe admitir la nulabilidad. Se tiene en cuenta el valor NULL de los UDT cargados en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], pero para que el UDT reconozca un valor NULL, es necesario que la clase implemente la interfaz `INullable`. Para obtener más información y un ejemplo de cómo implementar la nulabilidad en un UDT, vea [codificar tipos definidos por el usuario](creating-user-defined-types-coding.md).  
  
### <a name="string-conversions"></a>Conversiones de cadenas  
 Para admitir la conversión de cadenas al UDT y desde el UDT, debe proporcionar un método `Parse` y un método `ToString` en la clase. El método `Parse` permite convertir una cadena en un UDT. Debe declararse como `static` (o `Shared` en Visual Basic) y tomar un parámetro de tipo `System.Data.SqlTypes.SqlString`. Para obtener más información y un ejemplo de cómo implementar los `Parse` métodos `ToString` y, vea [codificar tipos definidos por el usuario](creating-user-defined-types-coding.md).  
  
## <a name="xml-serialization"></a>Serialización XML  
 Los UDT deben admitir la conversión al tipo de datos `xml` y desde el mismo, ajustándose al contrato de la serialización XML. El espacio de nombres `System.Xml.Serialization` contiene clases que se usan para serializar objetos en flujos o documentos con formato XML. Puede decidir implementar la serialización `xml` mediante la interfaz `IXmlSerializable`, que proporciona un formato personalizado para la serialización y deserialización XML.  
  
 Además de realizar conversiones explícitas de UDT a `xml`, la serialización XML permite:  
  
-   Usar `Xquery` en los valores de instancias UDT, tras la conversión al tipo de datos `xml`.  
  
-   Usar los UDT en consultas con parámetros y en métodos web con servicios web XML nativos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Usar los UDT para recibir una carga masiva de datos XML.  
  
-   Serializar conjuntos de datos que contengan tablas con columnas UDT.  
  
 Los UDT no se serializan en consultas FOR XML. Para ejecutar una consulta FOR XML que muestre la serialización XML de los UDT, convierta explícitamente cada columna UDT al tipo de datos `xml` en la instrucción SELECT. También puede convertir explícitamente las columnas a `varbinary`, `varchar` o `nvarchar`.  
  
## <a name="see-also"></a>Consulte también  
 [Crear un tipo definido por el usuario](creating-user-defined-types.md)  
  
  
