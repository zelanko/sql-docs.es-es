---
title: Requisitos de tipo definidos por el usuario ? Microsoft Docs
description: En este artículo se describen las decisiones de diseño importantes que debe tomar al crear un UDT para instalarlo en SQL Server.
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
ms.openlocfilehash: 2b19a9179cba2225a2209255ce48220669e4bbef
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2020
ms.locfileid: "81486984"
---
# <a name="creating-user-defined-types---requirements"></a>Crear tipos definidos por el usuario: requisitos
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Debe tomar varias decisiones de diseño importantes al crear un tipo [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]definido por el usuario (UDT) que se va a instalar en . Para la mayoría de los UDT, se recomienda la creación del UDT como una estructura, aunque también puede crearse como una clase. La definición del UDT debe cumplir las especificaciones de creación de los UDT a fin de registrarse con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="requirements-for-implementing-udts"></a>Requisitos para implementar un UDT  
 El UDT, para poder ejecutarse en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], debe implementar los requisitos siguientes en la definición del UDT:  
  
 El UDT debe especificar **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute**. El uso de **System.SerializableAttribute** es opcional, pero se recomienda.  
  
-   El UDT debe implementar el **System.Data.SqlTypes.INullable** interfaz en la clase [!INCLUDE[msCoName](../../includes/msconame-md.md)] o estructura mediante la creación de un público **estático** (**Compartido** en Visual Basic) **Null** método. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tiene en cuenta el valor NULL de forma predeterminada. Esto es necesario para que el código que se ejecuta en el UDT pueda reconocer un valor NULL.  
  
-   El UDT debe contener un método **de análisis** **estático** (o **compartido)** público que admita el análisis desde y un método **ToString** público para convertir en una representación de cadena del objeto.  
  
-   Un UDT con un formato de serialización definido por el usuario debe implementar el **System.Data.IBinarySerialize** interfaz y proporcionar un **Read** y un **Write** método.  
  
-   El UDT debe implementar **System.Xml.Serialization.IXmlSerializable**, o todos los campos públicos y propiedades deben ser de tipos que son serializables XML o decorados con el **atributo XmlIgnore** si se requiere la invalidación de la serialización estándar.  
  
-   Solo debe haber una serialización de un objeto UDT. Se produce un error en la validación si las rutinas de serialización o deserialización reconocen más de una representación de un objeto determinado.  
  
-   **SqlUserDefinedTypeAttribute.IsByteOrdered** debe ser **true** para comparar datos en orden de bytes. Si no se implementa la interfaz IComparable y **SqlUserDefinedTypeAttribute.IsByteOrdered** es **false**, se producirá un error en las comparaciones de orden de bytes.  
  
-   Un UDT definido en una clase debe tener un constructor público que no tome ningún argumento. Si lo desea, puede crear otros constructores de clase sobrecargados.  
  
-   El UDT debe exponer elementos de datos como procedimientos de propiedad o campos públicos.  
  
-   Los nombres públicos no pueden tener más de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 128 caracteres y deben ajustarse a las reglas de nomenclatura de los identificadores tal como se definen en [Identificadores](../../relational-databases/databases/database-identifiers.md)de base de datos .  
  
-   **sql_variant** columnas no pueden contener instancias de un UDT.  
  
-   Los miembros heredados no son accesibles desde [!INCLUDE[tsql](../../includes/tsql-md.md)] porque el sistema de tipos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no es consciente de la jerarquía de herencia entre los UDT. Sin embargo, puede usar la herencia al estructurar sus clases y puede llamar a dichos métodos en la implementación del código administrado del tipo.  
  
-   No es posible sobrecargar los miembros, salvo el constructor de clase. Si crea un método sobrecargado, no se produce ningún error al registrar el ensamblado o crear el tipo en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La detección del método sobrecargado se produce en tiempo de ejecución, no cuando se crea el tipo. Puede haber métodos sobrecargados en la clase siempre y cuando no se invoquen nunca. Al invocar al método sobrecargado se produce un error.  
  
-   Los miembros **estáticos** (o **compartidos)** deben declararse como constantes o como de solo lectura. Los miembros estáticos no pueden ser mutables.  
  
-   Si el campo **SqlUserDefinedTypeAttribute.MaxByteSize** se establece en -1, el UDT serializado puede ser tan grande como el límite de tamaño de objeto grande (LOB) (actualmente 2 GB). El tamaño del UDT no puede superar el valor especificado en el campo **MaxByteSized.**  
  
> [!NOTE]  
>  Aunque el servidor no lo utiliza para realizar comparaciones, puede implementar opcionalmente la interfaz **System.IComparable,** que expone un único método, **CompareTo**. Se usa del lado cliente en situaciones en las que se desean realizar comparaciones precisas u ordenar los valores UDT.  
  
## <a name="native-serialization"></a>Serialización nativa  
 La elección de los atributos de serialización correctos para su UDT depende del tipo de UDT que está intentando crear. El formato de serialización **nativo** utiliza [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] una estructura muy simple que permite almacenar una representación nativa eficaz del UDT en el disco. Se recomienda el formato **nativo** si el UDT es simple y solo contiene campos de los siguientes tipos:  
  
 **bool**, **byte**, **sbyte**, **short**, **ushort**, **int**, **uint**, **long**, **ulong**, **float**, **double**, **SqlByte**, **SqlInt16**, **SqlInt32**, **SqlInt64**, **SqlDateTime**, **SqlSingle**, **SqlDouble**, **SqlMoney**, **SqlBoolean**  
  
 Los tipos de valor que se componen de campos de los tipos anteriores son buenos candidatos para el formato **nativo,** como **structs** en Visual C, (o **estructuras** como se conocen en Visual Basic). Por ejemplo, un UDT especificado con el formato de serialización **nativo** puede contener un campo de otro UDT que también se especificó con el formato **nativo.** Si la definición de UDT es más compleja y contiene tipos de datos que no están en la lista anterior, debe especificar el formato de serialización **UserDefined** en su lugar.  
  
 El formato **nativo** tiene los siguientes requisitos:  
  
-   El tipo no debe especificar un valor para **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute.MaxByteSize**.  
  
-   Todos los campos deben ser serializables.  
  
-   **System.Runtime.InteropServices.StructLayoutAttribute** debe especificarse como **StructLayout.LayoutKindSequential** si el UDT se define en una clase y no en una estructura. Este atributo controla el diseño físico de los campos de datos y se usa para imponer a los miembros que se coloquen en el orden en que aparecen. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa este atributo para determinar el orden de los campos para los UDT con varios valores.  
  
 Para obtener un ejemplo de un UDT definido con serialización **nativa,** vea el UDT de punto en [Codificación de tipos definidos por](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-coding.md)el usuario .  
  
## <a name="userdefined-serialization"></a>Serialización UserDefined  
 El valor de formato **UserDefined** para el atributo **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute** proporciona al desarrollador control total sobre el formato binario. Al especificar la propiedad de atributo **Format** como **UserDefined**, debe hacer lo siguiente en el código:  
  
-   Especifique la propiedad de atributo **IsByteOrdered** opcional. El valor predeterminado es **false**.  
  
-   Especifique la propiedad **MaxByteSize** de **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute**.  
  
-   Escribir código para **implementar** read y **Write** métodos para el UDT mediante la implementación de la **System.Data.Sql.IBinarySerialize** interfaz.  
  
 Para obtener un ejemplo de un UDT definido con la serialización **UserDefined,** vea el UDT de moneda en Codificación de [tipos definidos por el usuario](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-coding.md).  
  
> [!NOTE]  
>  Los campos UDT deben usar la serialización nativa o conservarse para indizarse.  
  
## <a name="serialization-attributes"></a>Atributos de serialización  
 Los atributos determinan el modo de usar la serialización para construir la representación de almacenamiento de los UDT y para transmitirlos por valor al cliente. Debe especificar **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute** al crear el UDT. El atributo **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute** indica que la clase es un UDT y especifica el almacenamiento para el UDT. Opcionalmente, puede especificar el atributo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Serializable,** aunque no lo requiere.  
  
 El **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute** tiene las siguientes propiedades.  
  
 **Formato**  
 Especifica el formato de serialización, que puede ser **Native** o **UserDefined**, en función de los tipos de datos del UDT.  
  
 **IsByteOrdered**  
 Valor **booleano** que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] determina cómo realiza las comparaciones binarias en el UDT.  
  
 **IsFixedLength**  
 Indica si todas las instancias de este UDT tienen la misma longitud.  
  
 **MaxByteSize**  
 Tamaño máximo de la instancia, expresado en bytes. Debe especificar **MaxByteSize** con el **userDefined** formato de serialización. Para un UDT con la serialización definida por el usuario especificada, **MaxByteSize** hace referencia al tamaño total del UDT en su forma serializada según lo definido por el usuario. El valor de **MaxByteSize** debe estar en el intervalo de 1 a 8000, o establecerse en -1 para indicar que el UDT es mayor que 8000 bytes (el tamaño total no puede superar el tamaño máximo de LOB). Considere un UDT con una propiedad de una cadena de 10 caracteres (**System.Char**). Cuando el UDT se serialice mediante BinaryWriter, el tamaño total de la cadena serializada será de 22 bytes: 2 bytes por carácter Unicode UTF-16, multiplicados por el número máximo de caracteres, más 2 bytes de control por la sobrecarga que se produce al serializar un flujo binario. Por lo tanto, al determinar el valor de **MaxByteSize**, se debe tener en cuenta el tamaño total del UDT serializado: el tamaño de los datos serializados en formato binario más la sobrecarga en la que incurre la serialización.  
  
 **ValidationMethodName**  
 Nombre del método utilizado para validar las instancias del UDT.  
  
### <a name="setting-isbyteordered"></a>Valor IsByteOrdered  
 Cuando el **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute.IsByteOrdered** propiedad está establecida en **true**, en efecto, garantiza que los datos binarios serializados se pueden utilizar para el orden semántico de la información. De esta forma, cada instancia de un objeto UDT ordenado por bytes solamente puede tener una representación serializada. Cuando se lleva a cabo una operación de comparación en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en los bytes serializados, los resultados deben ser los mismos que si se hubiese realizado la misma operación de comparación en código administrado. Las siguientes características también se admiten cuando **IsByteOrdered** se establece en **true:**  
  
-   Funcionalidad para crear los índices de las columnas de este tipo.  
  
-   Funcionalidad para crear las claves principal y externa, así como las restricciones CHECK y UNIQUE en las columnas de este tipo.  
  
-   Funcionalidad para usar las cláusulas [!INCLUDE[tsql](../../includes/tsql-md.md)] ORDER BY, GROUP BY y PARTITION BY. En estos casos, la representación binaria del tipo se usa para determinar el orden.  
  
-   Funcionalidad para usar los operadores de comparación en instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
-   Funcionalidad para conservar las columnas calculadas de este tipo.  
  
 Tenga en cuenta que los formatos de serialización **Native** y **UserDefined** admiten los siguientes operadores de comparación cuando **IsByteOrdered** se establece en **true:**  
  
-   Igual a (=)  
  
-   Distinto de (!=)  
  
-   Mayor que (>)  
  
-   Menor que (\<)  
  
-   Mayor o igual que (>=)  
  
-   Menor o igual que (<=)  
  
### <a name="implementing-nullability"></a>Implementar la nulabilidad  
 Además de especificar correctamente los atributos de los ensamblados, la clase también debe admitir la nulabilidad. Los UDT [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cargados en son compatibles con null, pero para que el UDT reconozca un valor nulo, la clase debe implementar la interfaz **INullable.** Para obtener más información y un ejemplo de cómo implementar la nulabilidad en un UDT, vea Codificación de [tipos definidos por](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-coding.md)el usuario .  
  
### <a name="string-conversions"></a>Conversiones de cadenas  
 Para admitir la conversión de cadenas a y desde el UDT, debe proporcionar un **Parse** método y un **ToString** método en la clase. El **método Parse** permite convertir una cadena en un UDT. Debe declararse como **estático** (o **Compartido** en Visual Basic) y tomar un parámetro de tipo **System.Data.SqlTypes.SqlString**. Para obtener más información y un ejemplo de cómo implementar los métodos **Parse** y **ToString,** vea Codificación de [tipos definidos por](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-coding.md)el usuario .  
  
## <a name="xml-serialization"></a>Serialización XML  
 Los UDT deben admitir la conversión hacia y desde el tipo de datos **xml** de acuerdo con el contrato para la serialización XML. El espacio de nombres **System.Xml.Serialization** contiene clases que se usan para serializar objetos en documentos o secuencias en formato XML. Puede elegir implementar la serialización **xml** mediante la interfaz **IXmlSerializable,** que proporciona formato personalizado para la serialización y deserialización XML.  
  
 Además de realizar conversiones explícitas de UDT a **xml,** la serialización XML le permite:  
  
-   Utilice **Xquery** sobre los valores de las instancias UDT después de la conversión al tipo de datos **xml.**  
  
-   Usar los UDT en consultas con parámetros y en métodos web con servicios web XML nativos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Usar los UDT para recibir una carga masiva de datos XML.  
  
-   Serializar conjuntos de datos que contengan tablas con columnas UDT.  
  
 Los UDT no se serializan en consultas FOR XML. Para ejecutar una consulta FOR XML que muestre la serialización XML de UDT, convierta explícitamente cada columna UDT al tipo de datos **xml** de la instrucción SELECT. También puede convertir explícitamente las columnas a **varbinary**, **varchar**o **nvarchar**.  
  
## <a name="see-also"></a>Consulte también  
 [Crear un tipo definido por el usuario](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types.md)  
  
  
