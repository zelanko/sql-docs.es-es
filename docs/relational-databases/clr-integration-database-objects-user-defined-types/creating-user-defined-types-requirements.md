---
title: Requisitos de tipos definidos por el usuario | Microsoft Docs
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
ms.openlocfilehash: 7fc3da1474546f0719af20c52f44248baa8ce5da
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68028260"
---
# <a name="creating-user-defined-types---requirements"></a>Crear tipos definidos por el usuario: requisitos
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Debe tomar varias decisiones de diseño importantes al crear un tipo definido por el usuario (UDT) que se va [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]a instalar en. Para la mayoría de los UDT, se recomienda la creación del UDT como una estructura, aunque también puede crearse como una clase. La definición del UDT debe cumplir las especificaciones de creación de los UDT a fin de registrarse con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="requirements-for-implementing-udts"></a>Requisitos para implementar un UDT  
 El UDT, para poder ejecutarse en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], debe implementar los requisitos siguientes en la definición del UDT:  
  
 El UDT debe especificar **Microsoft. SqlServer. Server. SqlUserDefinedTypeAttribute**. El uso de **System. SerializableAttribute** es opcional, pero se recomienda.  
  
-   El UDT debe implementar la interfaz **System. Data. SqlTypes. INullable** en la clase o estructura mediante la creación de un método [!INCLUDE[msCoName](../../includes/msconame-md.md)] **null** **estático** público (**compartido** en Visual Basic). 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tiene en cuenta el valor NULL de forma predeterminada. Esto es necesario para que el código que se ejecuta en el UDT pueda reconocer un valor NULL.  
  
-   El UDT debe contener un método de **análisis** **estático** (o **compartido**) público que admita el análisis de y un método **ToString** público para convertir en una representación de cadena del objeto.  
  
-   Un UDT con un formato de serialización definido por el usuario debe implementar la interfaz **System. Data. IBinarySerialize** y proporcionar un método de **lectura** y **escritura** .  
  
-   El UDT debe implementar **System. Xml. Serialization. IXmlSerializable**, o todos los campos y propiedades públicos deben ser tipos que se pueden serializar o decorar con el atributo **XmlIgnore** si se requiere invalidar la serialización estándar.  
  
-   Solo debe haber una serialización de un objeto UDT. Se produce un error en la validación si las rutinas de serialización o deserialización reconocen más de una representación de un objeto determinado.  
  
-   **SqlUserDefinedTypeAttribute. IsByteOrdered** debe ser **true** para comparar los datos en orden de bytes. Si no se implementa la interfaz IComparable y **SqlUserDefinedTypeAttribute. IsByteOrdered** es **false**, se producirá un error en las comparaciones de orden de bytes.  
  
-   Un UDT definido en una clase debe tener un constructor público que no tome ningún argumento. Si lo desea, puede crear otros constructores de clase sobrecargados.  
  
-   El UDT debe exponer elementos de datos como procedimientos de propiedad o campos públicos.  
  
-   Los nombres públicos no pueden tener más de 128 caracteres y deben ajustarse [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a las reglas de nomenclatura para los identificadores tal y como se definen en los [identificadores de base de datos](../../relational-databases/databases/database-identifiers.md).  
  
-   **sql_variant** columnas no pueden contener instancias de un UDT.  
  
-   Los miembros heredados no son accesibles desde [!INCLUDE[tsql](../../includes/tsql-md.md)] porque el sistema de tipos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no es consciente de la jerarquía de herencia entre los UDT. Sin embargo, puede usar la herencia al estructurar sus clases y puede llamar a dichos métodos en la implementación del código administrado del tipo.  
  
-   No es posible sobrecargar los miembros, salvo el constructor de clase. Si crea un método sobrecargado, no se produce ningún error al registrar el ensamblado o crear el tipo en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La detección del método sobrecargado se produce en tiempo de ejecución, no cuando se crea el tipo. Puede haber métodos sobrecargados en la clase siempre y cuando no se invoquen nunca. Al invocar al método sobrecargado se produce un error.  
  
-   Los miembros **estáticos** (o **compartidos**) se deben declarar como constantes o como de solo lectura. Los miembros estáticos no pueden ser mutables.  
  
-   Si el campo **SqlUserDefinedTypeAttribute. MaxByteSize** está establecido en-1, el UDT serializado puede ser tan grande como el límite de tamaño de objetos grandes (LOB) (actualmente 2 GB). El tamaño del UDT no puede superar el valor especificado en el campo **MaxByteSized** .  
  
> [!NOTE]  
>  Aunque el servidor no lo usa para realizar comparaciones, puede implementar opcionalmente la interfaz **System. IComparable** , que expone un método único, **CompareTo**. Se usa del lado cliente en situaciones en las que se desean realizar comparaciones precisas u ordenar los valores UDT.  
  
## <a name="native-serialization"></a>Serialización nativa  
 La elección de los atributos de serialización correctos para su UDT depende del tipo de UDT que está intentando crear. El formato de serialización **nativa** emplea una estructura muy sencilla que permite [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] almacenar una representación nativa eficaz del UDT en el disco. Se recomienda usar el formato **nativo** si el UDT es sencillo y solo contiene campos de los siguientes tipos:  
  
 **bool**, **byte**, **SByte**, **Short**, **ushort**, **int**, **uint**, **Long**, **ULong**, **float**, **Double**, **SqlByte**, **SqlInt16**, **SqlInt32**, **SqlInt64**, **SqlDateTime**, **SqlSingle**, **SqlDouble**, **SqlMoney**, **SqlBoolean**  
  
 Los tipos de valor que se componen de los campos de los tipos anteriores son buenos candidatos para el formato **nativo** , como **Structs** en Visual C#, (o **estructuras** como se conocen en Visual Basic). Por ejemplo, un UDT especificado con el formato de serialización **nativa** puede contener un campo de otro UDT que también se especificó con el formato **nativo** . Si la definición de UDT es más compleja y contiene tipos de datos que no están en la lista anterior, debe especificar el formato de serialización **UserDefined** en su lugar.  
  
 El formato **nativo** tiene los siguientes requisitos:  
  
-   El tipo no debe especificar un valor para **Microsoft. SqlServer. Server. SqlUserDefinedTypeAttribute. MaxByteSize**.  
  
-   Todos los campos deben ser serializables.  
  
-   **System. Runtime. InteropServices. StructLayoutAttribute** debe especificarse como **StructLayout. LAYOUTKINDSEQUENTIAL** si el UDT se define en una clase y no en una estructura. Este atributo controla el diseño físico de los campos de datos y se usa para imponer a los miembros que se coloquen en el orden en que aparecen. 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa este atributo para determinar el orden de los campos para los UDT con varios valores.  
  
 Para obtener un ejemplo de un UDT definido con serialización **nativa** , vea el UDT Point en [codificar tipos definidos por el usuario](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-coding.md).  
  
## <a name="userdefined-serialization"></a>Serialización UserDefined  
 La configuración de formato **UserDefined** para el atributo **Microsoft. SqlServer. Server. SqlUserDefinedTypeAttribute** proporciona al desarrollador control total sobre el formato binario. Al especificar la propiedad de atributo **Format** como **UserDefined**, debe hacer lo siguiente en el código:  
  
-   Especifique la propiedad de atributo **IsByteOrdered** opcional. El valor predeterminado es **false**.  
  
-   Especifique la propiedad **MaxByteSize** de **Microsoft. SqlServer. Server. SqlUserDefinedTypeAttribute**.  
  
-   Escriba código para implementar métodos de **lectura** y **escritura** para el UDT implementando la interfaz **System. Data. SQL. IBinarySerialize** .  
  
 Para obtener un ejemplo de un UDT definido con serialización **UserDefined** , vea el UDT Currency en [codificar tipos definidos por el usuario](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-coding.md).  
  
> [!NOTE]  
>  Los campos UDT deben usar la serialización nativa o conservarse para indizarse.  
  
## <a name="serialization-attributes"></a>Atributos de serialización  
 Los atributos determinan el modo de usar la serialización para construir la representación de almacenamiento de los UDT y para transmitirlos por valor al cliente. Se le pedirá que especifique **Microsoft. SqlServer. Server. SqlUserDefinedTypeAttribute** al crear el UDT. El atributo **Microsoft. SqlServer. Server. SqlUserDefinedTypeAttribute** indica que la clase es un UDT y especifica el almacenamiento para el UDT. Opcionalmente, puede especificar el atributo **serializable** , aunque [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no es necesario.  
  
 **Microsoft. SqlServer. Server. SqlUserDefinedTypeAttribute** tiene las siguientes propiedades.  
  
 **Aplique**  
 Especifica el formato de serialización, que puede ser **nativo** o **UserDefined**, en función de los tipos de datos del UDT.  
  
 **IsByteOrdered**  
 Valor **booleano** que determina cómo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] realiza las comparaciones binarias en el UDT.  
  
 **IsFixedLength**  
 Indica si todas las instancias de este UDT tienen la misma longitud.  
  
 **MaxByteSize**  
 Tamaño máximo de la instancia, expresado en bytes. Debe especificar **MaxByteSize** con el formato de serialización **UserDefined** . En el caso de un UDT con serialización definida por el usuario especificada, **MaxByteSize** hace referencia al tamaño total del UDT en su forma serializada, tal como la define el usuario. El valor de **MaxByteSize** debe estar en el intervalo comprendido entre 1 y 8000, o bien establecerse en-1 para indicar que el UDT es superior a 8000 bytes (el tamaño total no puede superar el tamaño de LOB máximo). Considere un UDT con una propiedad de una cadena de 10 caracteres (**System. Char**). Cuando el UDT se serialice mediante BinaryWriter, el tamaño total de la cadena serializada será de 22 bytes: 2 bytes por carácter Unicode UTF-16, multiplicados por el número máximo de caracteres, más 2 bytes de control por la sobrecarga que se produce al serializar un flujo binario. Por lo tanto, al determinar el valor de **MaxByteSize**, debe tenerse en cuenta el tamaño total del UDT serializado: el tamaño de los datos serializados en formato binario más la sobrecarga en la que se incurre por la serialización.  
  
 **ValidationMethodName**  
 Nombre del método utilizado para validar las instancias del UDT.  
  
### <a name="setting-isbyteordered"></a>Valor IsByteOrdered  
 Cuando la propiedad **Microsoft. SqlServer. Server. SqlUserDefinedTypeAttribute. IsByteOrdered** está establecida en **true**, tiene la garantía de que los datos binarios serializados se pueden usar para el orden semántico de la información. De esta forma, cada instancia de un objeto UDT ordenado por bytes solamente puede tener una representación serializada. Cuando se lleva a cabo una operación de comparación en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en los bytes serializados, los resultados deben ser los mismos que si se hubiese realizado la misma operación de comparación en código administrado. También se admiten las siguientes características cuando **IsByteOrdered** está establecido en **true**:  
  
-   Funcionalidad para crear los índices de las columnas de este tipo.  
  
-   Funcionalidad para crear las claves principal y externa, así como las restricciones CHECK y UNIQUE en las columnas de este tipo.  
  
-   Funcionalidad para usar las cláusulas [!INCLUDE[tsql](../../includes/tsql-md.md)] ORDER BY, GROUP BY y PARTITION BY. En estos casos, la representación binaria del tipo se usa para determinar el orden.  
  
-   Funcionalidad para usar los operadores de comparación en instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
-   Funcionalidad para conservar las columnas calculadas de este tipo.  
  
 Tenga en cuenta que los formatos de serialización **nativo** y **UserDefined** admiten los siguientes operadores de comparación cuando **IsByteOrdered** está establecido en **true**:  
  
-   Igual a (=)  
  
-   Distinto de (!=)  
  
-   Mayor que (>)  
  
-   Menor que (\<)  
  
-   Mayor o igual que (>=)  
  
-   Menor o igual que (<=)  
  
### <a name="implementing-nullability"></a>Implementar la nulabilidad  
 Además de especificar correctamente los atributos de los ensamblados, la clase también debe admitir la nulabilidad. Los UDT cargados en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tienen reconocimiento nulo, pero para que el UDT reconozca un valor null, la clase debe implementar la interfaz **INullable** . Para obtener más información y un ejemplo de cómo implementar la nulabilidad en un UDT, vea [codificar tipos definidos por el usuario](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-coding.md).  
  
### <a name="string-conversions"></a>Conversiones de cadenas  
 Para admitir la conversión de cadenas a y desde el UDT, debe proporcionar un método **Parse** y un método **ToString** en la clase. El método **Parse** permite convertir una cadena en un UDT. Debe declararse como **static** (o **compartirse** en Visual Basic) y tomar un parámetro de tipo **System. Data. SqlTypes. SqlString**. Para obtener más información y un ejemplo de cómo implementar los métodos **Parse** y **ToString** , vea [codificar tipos definidos por el usuario](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-coding.md).  
  
## <a name="xml-serialization"></a>Serialización XML  
 Los UDT deben admitir la conversión a y desde el tipo de datos **XML** conforme al contrato para la serialización XML. El espacio de nombres **System. Xml. Serialization** contiene clases que se utilizan para serializar objetos en documentos o secuencias de formato XML. Puede optar por implementar la serialización **XML** mediante la interfaz **IXmlSerializable** , que proporciona un formato personalizado para la serialización y deserialización XML.  
  
 Además de realizar conversiones explícitas de UDT a **XML**, la serialización XML permite:  
  
-   Use **XQuery** en valores de instancias de UDT después de la conversión al tipo de datos **XML** .  
  
-   Usar los UDT en consultas con parámetros y en métodos web con servicios web XML nativos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Usar los UDT para recibir una carga masiva de datos XML.  
  
-   Serializar conjuntos de datos que contengan tablas con columnas UDT.  
  
 Los UDT no se serializan en consultas FOR XML. Para ejecutar una consulta FOR XML que muestre la serialización XML de los UDT, convierta explícitamente cada columna UDT al tipo de datos **XML** en la instrucción SELECT. También puede convertir explícitamente las columnas a **varbinary**, **VARCHAR**o **nvarchar**.  
  
## <a name="see-also"></a>Consulte también  
 [Crear un tipo definido por el usuario](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types.md)  
  
  
