---
title: El objeto Field | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Field object [ADO]
ms.assetid: 7d1c4ad5-4be3-42ab-b516-e7133ca300bc
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7ecd2382d15536a5c2ebd2b2098c89c41c78ba1f
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="the-field-object"></a>El objeto de campo
Cada **campo** objeto suele corresponder a una columna de una tabla de base de datos. Sin embargo, un **campo** también se puede representar un puntero a otro **Recordset**, que se denomina capítulo. Excepciones, como columnas de capítulo, se explicará más adelante en esta guía.  
  
 Use la **valor** propiedad de **campo** objetos para establecer o devolver datos para el registro actual. Dependiendo de la funcionalidad expone el proveedor, algunas colecciones, métodos o propiedades de un **campo** objeto no estén disponible.  
  
 Con las colecciones, métodos y propiedades de un **campo** del objeto, puede hacer lo siguiente:  
  
-   Devolver el nombre de un campo utilizando el **nombre** propiedad.  
  
-   Ver o cambiar los datos en el campo mediante el **valor** propiedad. **Valor** es la propiedad predeterminada de la **campo** objeto.  
  
-   Devolver las características básicas de un campo utilizando el **tipo**, **precisión**, y **NumericScale** propiedades.  
  
-   Devolver el tamaño declarado de un campo utilizando el **DefinedSize** propiedad.  
  
-   Devolver el tamaño real de los datos en un campo determinado mediante la **ActualSize** propiedad.  
  
-   Determinar qué tipos de funcionalidad se admiten para un campo determinado mediante el uso de la **atributos** propiedad y **propiedades** colección.  
  
-   Manipular los valores de campos que contienen datos de caracteres largos o binarios largos utilizando la **AppendChunk** y **GetChunk** métodos.  
  
 Resolver discrepancias en valores de campo durante una actualización por lotes utilizando el **OriginalValue** y **UnderlyingValue** propiedades, si el proveedor admite las actualizaciones por lotes.  
  
## <a name="describing-a-field"></a>Que describe un campo  
 Los temas que siguen describen las propiedades de la [campo](../../../ado/reference/ado-api/field-object.md) objetos que representan información que describe la **campo** propio objeto, es decir, metadatos acerca del campo. Esta información puede usarse para determinar mucho sobre el esquema de la **conjunto de registros**. Estas propiedades incluyen **tipo**, **DefinedSize** y **ActualSize**, **nombre**, y **NumericScale**y **precisión**.  
  
### <a name="discovering-the-data-type"></a>Detectar el tipo de datos  
 El **tipo** propiedad indica el tipo de datos del campo. El tipo de datos en el que se describen las constantes enumeradas que son compatibles con ADO [DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md) en el *referencia del programador de ADO*.  
  
 Para tales tipos numéricos de punto flotante **adNumeric**, puede obtener más información. El **NumericScale** propiedad indica cuántos dígitos a la derecha del separador decimal se usará para representar valores para el **campo**. El **precisión** propiedad especifica el número máximo de dígitos utilizados para representar valores para el **campo**.  
  
### <a name="determining-field-size"></a>Determinar el tamaño del campo  
 Use la **DefinedSize** propiedad para determinar la capacidad de datos de un **campo** objeto.  
  
 Use la **ActualSize** propiedad para devolver la longitud real de un **campo** valor del objeto. Para todos los campos, el **ActualSize** propiedad es de solo lectura. Si ADO no puede determinar la longitud de la **campo** valor de objeto, el **ActualSize** propiedad devuelve **adUnknown**.  
  
 El **DefinedSize** y **ActualSize** propiedades tienen propósitos diferentes. Por ejemplo, considere un **campo** objeto con un tipo declarado de **parámetros** y un **DefinedSize** valor de la propiedad de 50, que contiene un único carácter. El **ActualSize** devuelve el valor de propiedad es la longitud en bytes del carácter único.  
  
### <a name="determining-field-contents"></a>Determinar el contenido del campo  
 El identificador de la columna del origen de datos se representa mediante el **nombre** propiedad de la **campo**. El **valor** propiedad de la **campo** objeto devuelve o establece el contenido de los datos reales del campo. Se trata de la propiedad predeterminada.  
  
 Para cambiar los datos de un campo, establezca la **valor** propiedad igual a un valor nuevo del tipo correcto. El tipo de cursor debe admitir actualizaciones para cambiar el contenido de un campo. Validación de la base de datos no se hace aquí en modo por lotes, por lo que deberá comprobar si hay errores cuando se llama a **UpdateBatch** en este caso. Algunos proveedores también admiten la propiedad ADO **campo** del objeto **UnderlyingValue** y **OriginalValue** propiedades para ayudarle a resolver conflictos al intentar realizar actualizaciones por lotes. Para obtener más información acerca de cómo resolver tales conflictos, vea [modificar datos](../../../ado/guide/data/editing-data.md).  
  
> [!NOTE]
>  **Recordset Field** valores no se puede establecer al anexar nuevos **campos** a una **conjunto de registros**. En su lugar, nueva **campos** se pueden anexar a un cerrado **conjunto de registros**. La **Recordset** debe estar abierto y, a continuación, a continuación, solo puede asignar valores a estos **campos**.  
  
### <a name="getting-more-field-information"></a>Obtener más información de campo  
 Objetos ADO tienen dos tipos de propiedades: integradas y dinámicas. En este punto, solo las propiedades integradas de la **campo** objeto se han explicado.  
  
 Las propiedades integradas son aquellas propiedades implementadas en ADO y disponibles inmediatamente para cualquier objeto nuevo, utilizando el `MyObject.Property` sintaxis. No aparecen como **propiedad** objetos en un objeto **propiedades** colección.  
  
 Propiedades dinámicas se definen mediante el proveedor de datos subyacente y aparecen en la **propiedades** colección para el objeto ADO apropiado. Por ejemplo, una propiedad específica del proveedor puede indicar si una **Recordset** objeto admite transacciones o actualizaciones. Estas propiedades adicionales aparecerán como **propiedad** objetos que **Recordset** del objeto **propiedades** colección. Pueden hacer referencia a las propiedades dinámicas sólo a través de la colección mediante la sintaxis `MyObject.Properties(0)` o `MyObject.Properties("Name")`.  
  
 No se puede eliminar cualquier tipo de propiedad.  
  
 Dinámico **propiedad** objeto tiene cuatro propiedades integradas de su propio:  
  
-   El **nombre** propiedad es una cadena que identifica la propiedad.  
  
-   El **tipo** propiedad es un entero que especifica el tipo de datos de propiedad.  
  
-   El **valor** propiedad es una variante que contiene el valor de propiedad. **Valor** es la propiedad predeterminada para un **propiedad** objeto.  
  
-   El **atributos** propiedad es una **largo** valor que indica las características de la propiedad específica del proveedor.  
  
 El **propiedades** colección para el **campo** objeto contiene metadatos adicionales acerca del campo. El contenido de esta colección varía según el proveedor. En el ejemplo de código siguiente se examina la **propiedades** colección del ejemplo **Recordset** introdujo al principio de esta sección. Primero examina el contenido de la colección. Este código usa el [proveedor OLE DB para SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md), por lo que la **propiedades** colección contiene información relativa a ese proveedor.  
  
```  
'BeginFieldProps  
    Dim objProp As ADODB.Property  
  
    For intLoop = 0 To (objFields.Count - 1)  
        Debug.Print objFields.Item(intLoop).Name  
  
        For Each objProp In objFields(intLoop).Properties  
            Debug.Print vbTab & objProp.Name & " = " & objProp.Value  
        Next objProp  
    Next intLoop  
'EndFieldProps  
```  
  
### <a name="dealing-with-binary-data"></a>Trabajar con datos binarios  
 Use la [AppendChunk](../../../ado/reference/ado-api/appendchunk-method-ado.md) método en un **campo** objeto que se va a rellenar con datos binarios largos o de caracteres. En situaciones donde la memoria del sistema es limitada, puede usar el **AppendChunk** método para manipular los valores largos en partes en lugar de en su totalidad.  
  
 Si el **adFldLong** de bits en el **atributos** propiedad de un **campo** objeto se establece en **True**, puede usar el  **AppendChunk** método para ese campo.  
  
 La primera **AppendChunk** llamar en un **campo** objeto escribe datos en el campo, sobrescribiendo los datos existentes. Posteriores **AppendChunk** agregan llamadas a los datos existentes. Si va a anexar datos a un campo y, a continuación, establecer o leer el valor de otro campo en el registro actual, ADO supone que haya terminado de anexar datos al primer campo. Si se llama a la **AppendChunk** método en el primer campo una vez más, ADO interpreta la llamada como una nueva **AppendChunk** operación y sobrescribe los datos existentes. Obtener acceso a campos de otros **Recordset** objetos que no son clones del primer **Recordset** no interrumpirá el objeto **AppendChunk** operaciones.  
  
 Use la **GetChunk** método en un **campo** objeto que se va a recuperar la parte o la totalidad de sus datos binarios largos o de caracteres. En situaciones donde la memoria del sistema es limitada, puede usar el **GetChunk** método para manipular los valores largos en partes, en lugar de en su totalidad.  
  
 Los datos que un **GetChunk** devoluciones de llamada se asigna a *variable*. Si *tamaño* es mayor que el resto de los datos, el **GetChunk** método devuelve sólo los datos restantes sin relleno *variable* con espacios en blanco. Si el campo está vacío, el **GetChunk** método devuelve un valor null.  
  
 Cada uno de ellos posteriores **GetChunk** llamada recupera datos a partir de donde anterior **GetChunk** dejó de llamada. Sin embargo, si va a recuperar datos de un campo y, a continuación, establecer o leer el valor de otro campo en el registro actual, ADO supone que ha terminado de recuperar datos desde el primer campo. Si se llama a la **GetChunk** método en el primer campo una vez más, ADO interpreta la llamada como una nueva **GetChunk** operación e inicia leer desde el principio de los datos. Obtener acceso a campos de otros **Recordset** objetos que no son clones del primer **Recordset** no interrumpirá el objeto **GetChunk** operaciones.  
  
 Si el **adFldLong** de bits en el **atributos** propiedad de un **campo** objeto se establece en **True**, puede usar el **GetChunk**  método para ese campo.  
  
 Si no hay ningún registro actual cuando se usa el **GetChunk** o **AppendChunk** método en un **campo** del objeto, se produce el error 3021 (no hay registro actual).  
  
 Para obtener un ejemplo del uso de estos métodos para manipular datos binarios, consulte el [método AppendChunk](../../../ado/reference/ado-api/appendchunk-method-ado.md) y [método GetChunk](../../../ado/reference/ado-api/getchunk-method-ado.md) en los ejemplos de la *referencia del programador de ADO*.
