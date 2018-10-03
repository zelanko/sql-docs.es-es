---
title: Requisitos de tipo definido por el usuario | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
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
ms.openlocfilehash: 6faf51099d0a5eced6543704d5f45b6fc922f522
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47697124"
---
# <a name="creating-user-defined-types---requirements"></a>Crear tipos definidos por el usuario: requisitos
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Debe realizar varias decisiones de diseño importante al crear un tipo definido por el usuario (UDT) se instale en [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para la mayoría de los UDT, se recomienda la creación del UDT como una estructura, aunque también puede crearse como una clase. La definición del UDT debe cumplir las especificaciones de creación de los UDT a fin de registrarse con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="requirements-for-implementing-udts"></a>Requisitos para implementar un UDT  
 El UDT, para poder ejecutarse en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], debe implementar los requisitos siguientes en la definición del UDT:  
  
 El UDT debe especificar el **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute**. El uso de la **System.SerializableAttribute con** es opcional pero recomendable.  
  
-   El UDT debe implementar la **System.Data.SqlTypes.INullable** interfaz en la clase o estructura mediante la creación de un público **estático** (**Shared** en [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic) **Null** método. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tiene en cuenta el valor NULL de forma predeterminada. Esto es necesario para que el código que se ejecuta en el UDT pueda reconocer un valor NULL.  
  
-   El UDT debe contener una pública **estático** (o **Shared**) **analizar** método que admita el análisis y una pública **ToString** método para convertir en una representación de cadena del objeto.  
  
-   Debe implementar un UDT con un formato de serialización definido por el usuario la **System.Data.IBinarySerialize** interfaz y proporcionar un **lectura** y un **escribir** método.  
  
-   El UDT debe implementar **System.Xml.Serialization.IXmlSerializable**, o todos los campos públicos y propiedades deben ser de tipos que son serializables con XML o representarse con el **XmlIgnore** atributo si es necesario invalidar la serialización estándar.  
  
-   Solo debe haber una serialización de un objeto UDT. Se produce un error en la validación si las rutinas de serialización o deserialización reconocen más de una representación de un objeto determinado.  
  
-   **SqlUserDefinedTypeAttribute.IsByteOrdered** debe ser **true** para comparar los datos en orden de bytes. Si no se implementa la interfaz IComparable y **SqlUserDefinedTypeAttribute.IsByteOrdered** es **false**, se producirá un error en las comparaciones de orden de bytes.  
  
-   Un UDT definido en una clase debe tener un constructor público que no tome ningún argumento. Si lo desea, puede crear otros constructores de clase sobrecargados.  
  
-   El UDT debe exponer elementos de datos como procedimientos de propiedad o campos públicos.  
  
-   Nombres públicos no puede tener más de 128 caracteres y debe cumplir la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] reglas de nomenclatura para los identificadores tal como se define en [identificadores de base de datos](../../relational-databases/databases/database-identifiers.md).  
  
-   **sql_variant** columnas no pueden contener instancias de un UDT.  
  
-   Los miembros heredados no son accesibles desde [!INCLUDE[tsql](../../includes/tsql-md.md)] porque el sistema de tipos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no es consciente de la jerarquía de herencia entre los UDT. Sin embargo, puede usar la herencia al estructurar sus clases y puede llamar a dichos métodos en la implementación del código administrado del tipo.  
  
-   No es posible sobrecargar los miembros, salvo el constructor de clase. Si crea un método sobrecargado, no se produce ningún error al registrar el ensamblado o crear el tipo en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La detección del método sobrecargado se produce en tiempo de ejecución, no cuando se crea el tipo. Puede haber métodos sobrecargados en la clase siempre y cuando no se invoquen nunca. Al invocar al método sobrecargado se produce un error.  
  
-   Cualquier **estático** (o **Shared**) los miembros deben declararse como constantes o como de solo lectura. Los miembros estáticos no pueden ser mutables.  
  
-   Si el **SqlUserDefinedTypeAttribute.MaxByteSize** campo se establece en -1, el UDT serializado puede ser tan grande como el límite de tamaño de objetos grandes (LOB) (actualmente 2 GB). El tamaño del UDT no puede superar el valor especificado en el **MaxByteSized** campo.  
  
> [!NOTE]  
>  Aunque no se usa el servidor para realizar comparaciones, también puede implementar la **System.IComparable** interfaz, que expone un único método, **CompareTo**. Se usa del lado cliente en situaciones en las que se desean realizar comparaciones precisas u ordenar los valores UDT.  
  
## <a name="native-serialization"></a>Serialización nativa  
 La elección de los atributos de serialización correctos para su UDT depende del tipo de UDT que está intentando crear. El **nativo** formato de serialización usa una estructura muy simple que permite [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para almacenar una representación nativa eficaz del UDT en el disco. El **nativo** formato se recomienda si el UDT es simple y solamente contiene campos de los siguientes tipos:  
  
 **BOOL**, **bytes**, **sbyte**, **corto**, **ushort**, **int**,  **uint**, **largo**, **ulong**, **float**, **doble**, **SqlByte**, **SqlInt16**, **SqlInt32**, **SqlInt64**, **SqlDateTime**, **SqlSingle**,  **SqlDouble**, **SqlMoney**, **SqlBoolean**  
  
 Tipos de valor que se compone de campos de los tipos anteriores son buenos candidatos para **nativo** dar formato, como **structs** en Visual C# (o **estructuras** tal como se conocen en Visual Basic). Por ejemplo, un UDT especificado con el **nativo** formato de serialización puede contener un campo de otro UDT también especificado con el **nativo** formato. Si la definición UDT es más compleja y contiene tipos de datos no están en la lista anterior, debe especificar el **UserDefined** en su lugar, el formato de serialización.  
  
 El **nativo** formato tiene los siguientes requisitos:  
  
-   El tipo no debe especificar un valor para **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute.MaxByteSize**.  
  
-   Todos los campos deben ser serializables.  
  
-   El **System.Runtime.InteropServices.StructLayoutAttribute** debe especificarse como **StructLayout.LayoutKindSequential** si el UDT se define en una clase y no en una estructura. Este atributo controla el diseño físico de los campos de datos y se usa para imponer a los miembros que se coloquen en el orden en que aparecen. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa este atributo para determinar el orden de los campos para los UDT con varios valores.  
  
 Para obtener un ejemplo de un UDT definido con **nativo** serialización, vea el UDT Point en [codificación de tipos](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-coding.md).  
  
## <a name="userdefined-serialization"></a>Serialización UserDefined  
 El **UserDefined** configuración de formato el **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute** proporciona atributo al desarrollador pleno control sobre el formato binario. Al especificar el **formato** la propiedad de atributo **UserDefined**, debe hacer lo siguiente en el código:  
  
-   Especifique el valor opcional **IsByteOrdered** propiedad de atributo. El valor predeterminado es **false**.  
  
-   Especifique el **MaxByteSize** propiedad de la **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute**.  
  
-   Escribir código para implementar **lectura** y **escribir** métodos para el UDT implementando la **System.Data.Sql.IBinarySerialize** interfaz.  
  
 Para obtener un ejemplo de un UDT definido con **UserDefined** serialización, vea el UDT Currency en [codificación de tipos](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-coding.md).  
  
> [!NOTE]  
>  Los campos UDT deben usar la serialización nativa o conservarse para indizarse.  
  
## <a name="serialization-attributes"></a>Atributos de serialización  
 Los atributos determinan el modo de usar la serialización para construir la representación de almacenamiento de los UDT y para transmitirlos por valor al cliente. Se debe especificar el **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute** al crear el UDT. El **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute** atributo indica que la clase es un UDT y especifica el almacenamiento para el UDT. Opcionalmente, puede especificar el **Serializable** atributo aunque [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no requiere esto.  
  
 El **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute** tiene las siguientes propiedades.  
  
 **Formato**  
 Especifica el formato de serialización, que puede ser **nativo** o **UserDefined**, en función de los tipos de datos del UDT.  
  
 **IsByteOrdered**  
 Un **booleano** valor que determina cómo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] realiza comparaciones binarias en el UDT.  
  
 **IsFixedLength**  
 Indica si todas las instancias de este UDT tienen la misma longitud.  
  
 **MaxByteSize**  
 Tamaño máximo de la instancia, expresado en bytes. Debe especificar **MaxByteSize** con el **UserDefined** formato de serialización. Para un UDT con serialización definida por el usuario especificado, **MaxByteSize** se refiere al tamaño total del UDT en su formato serializado, tal como se define por el usuario. El valor de **MaxByteSize** debe estar en el intervalo de 1 a 8000 o se establece en -1 para indicar que el UDT es superior a 8000 bytes (el tamaño total no puede superar el tamaño LOB máximo). Considere la posibilidad de un UDT con una propiedad de una cadena de 10 caracteres (**System.Char**). Cuando el UDT se serialice mediante BinaryWriter, el tamaño total de la cadena serializada será de 22 bytes: 2 bytes por carácter Unicode UTF-16, multiplicados por el número máximo de caracteres, más 2 bytes de control por la sobrecarga que se produce al serializar un flujo binario. Por lo tanto, al determinar el valor de **MaxByteSize**, el tamaño total del UDT serializado debe considerarse: el tamaño de los datos serializados en formato binario más la sobrecarga producida por la serialización.  
  
 **ValidationMethodName**  
 Nombre del método utilizado para validar las instancias del UDT.  
  
### <a name="setting-isbyteordered"></a>Valor IsByteOrdered  
 Cuando el **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute.IsByteOrdered** propiedad está establecida en **true**, en realidad lo que garantiza que los datos binarios serializados pueden usarse para semántica clasificación de la información. De esta forma, cada instancia de un objeto UDT ordenado por bytes solamente puede tener una representación serializada. Cuando se lleva a cabo una operación de comparación en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en los bytes serializados, los resultados deben ser los mismos que si se hubiese realizado la misma operación de comparación en código administrado. Las siguientes características están también admiten cuando **IsByteOrdered** está establecido en **true**:  
  
-   Funcionalidad para crear los índices de las columnas de este tipo.  
  
-   Funcionalidad para crear las claves principal y externa, así como las restricciones CHECK y UNIQUE en las columnas de este tipo.  
  
-   Funcionalidad para usar las cláusulas [!INCLUDE[tsql](../../includes/tsql-md.md)] ORDER BY, GROUP BY y PARTITION BY. En estos casos, la representación binaria del tipo se usa para determinar el orden.  
  
-   Funcionalidad para usar los operadores de comparación en instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
-   Funcionalidad para conservar las columnas calculadas de este tipo.  
  
 Tenga en cuenta que tanto el **nativo** y **UserDefined** formatos de serialización admiten los siguientes operadores de comparación cuando **IsByteOrdered** está establecido en **true** :  
  
-   Igual a (=)  
  
-   Distinto de (!=)  
  
-   Mayor que (>)  
  
-   Menor que (\<)  
  
-   Mayor o igual que (>=)  
  
-   Menor o igual que (<=)  
  
### <a name="implementing-nullability"></a>Implementar la nulabilidad  
 Además de especificar correctamente los atributos de los ensamblados, la clase también debe admitir la nulabilidad. Los UDT cargados en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] son compatibles con null, pero para el UDT reconozca un valor null, la clase debe implementar la **INullable** interfaz. Para obtener más información y un ejemplo de cómo implementar la nulabilidad en un UDT, vea [codificación de tipos](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-coding.md).  
  
### <a name="string-conversions"></a>Conversiones de cadenas  
 Para admitir la conversión de cadena a y desde el UDT, debe proporcionar un **analizar** método y un **ToString** método en la clase. El **analizar** método permite una cadena que se va a convertir en un UDT. Se debe declarar como **estático** (o **Shared** en Visual Basic) y tomar un parámetro de tipo **System.Data.SqlTypes.SqlString**. Para obtener más información y un ejemplo de cómo implementar la **analizar** y **ToString** métodos, vea [codificación de tipos](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-coding.md).  
  
## <a name="xml-serialization"></a>Serialización XML  
 Los UDT deben admitir la conversión a y desde el **xml** tipo de datos mediante la conformidad con el contrato para la serialización XML. El **System.Xml.Serialization** espacio de nombres contiene clases que se utilizan para serializar objetos en secuencias o documentos con formato XML. Puede elegir implementar **xml** serialización mediante el uso de la **IXmlSerializable** interfaz, que proporciona un formato personalizado para la serialización y deserialización XML.  
  
 Además de realizar conversiones explícitas de UDT a **xml**, serialización XML le permite:  
  
-   Use **Xquery** sobre los valores de instancias UDT, tras la conversión a la **xml** tipo de datos.  
  
-   Usar los UDT en consultas con parámetros y en métodos web con servicios web XML nativos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Usar los UDT para recibir una carga masiva de datos XML.  
  
-   Serializar conjuntos de datos que contengan tablas con columnas UDT.  
  
 Los UDT no se serializan en consultas FOR XML. Para ejecutar una consulta FOR XML que muestra la serialización XML de los UDT, convierta explícitamente cada columna UDT en el **xml** tipo de datos en la instrucción SELECT. Las columnas que se puede convertir explícitamente **varbinary**, **varchar**, o **nvarchar**.  
  
## <a name="see-also"></a>Vea también  
 [Crear un tipo definido por el usuario](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types.md)  
  
  
