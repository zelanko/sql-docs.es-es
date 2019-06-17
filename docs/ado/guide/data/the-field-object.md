---
title: El objeto de campo | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Field object [ADO]
ms.assetid: 7d1c4ad5-4be3-42ab-b516-e7133ca300bc
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: a709b8c26c3cdee3a6087444e4acebbd212caf66
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66718655"
---
# <a name="the-field-object"></a>El objeto de campo
Cada **campo** objeto suele corresponder a una columna de una tabla de base de datos. Sin embargo, un **campo** también se puede representar un puntero a otro **Recordset**, que se denomina capítulo. Las excepciones, como columnas de capítulo, se explicará más adelante en esta guía.  
  
 Use la **valor** propiedad de **campo** objetos para establecer o devolver datos para el registro actual. Dependiendo de la funcionalidad expone el proveedor, algunas colecciones, métodos o propiedades de un **campo** objeto no esté disponible.  
  
 Con las colecciones, métodos y propiedades de un **campo** objeto, puede hacer lo siguiente:  
  
-   Devolver el nombre de un campo utilizando el **nombre** propiedad.  
  
-   Ver o cambiar los datos en el campo utilizando el **valor** propiedad. **Valor** es la propiedad predeterminada de la **campo** objeto.  
  
-   Devolver las características básicas de un campo utilizando el **tipo**, **precisión**, y **NumericScale** propiedades.  
  
-   Devolver el tamaño declarado de un campo utilizando el **DefinedSize** propiedad.  
  
-   Devolver el tamaño real de los datos en un campo determinado mediante la **ActualSize** propiedad.  
  
-   Determinar qué tipos de funcionalidad se admiten para un campo dado mediante el uso de la **atributos** propiedad y **propiedades** colección.  
  
-   Manipular los valores de los campos que contienen datos de caracteres largos o binarios largos utilizando el **AppendChunk** y **GetChunk** métodos.  
  
 Solucionar discrepancias en los valores de campo durante la actualización por lotes utilizando el **OriginalValue** y **UnderlyingValue** propiedades, si el proveedor admite las actualizaciones por lotes.  
  
## <a name="describing-a-field"></a>Que describe un campo  
 Los temas que siguen describen las propiedades de la [campo](../../../ado/reference/ado-api/field-object.md) objetos que representan la información que describe el **campo** propio objeto: es decir, los metadatos acerca del campo. Esta información puede usarse para determinar mucho sobre el esquema de la **Recordset**. Estas propiedades incluyen **tipo**, **DefinedSize** y **ActualSize**, **nombre**, y **NumericScale**y **precisión**.  
  
### <a name="discovering-the-data-type"></a>Detectar el tipo de datos  
 El **tipo** propiedad indica el tipo de datos del campo. El tipo de datos que se describen las constantes enumeradas que son compatibles con ADO en [DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md) en el *referencia del programador de ADO*.  
  
 Para tales tipos numéricos de punto flotante **adNumeric**, puede obtener más información. El **NumericScale** propiedad indica cuántos dígitos a la derecha del separador decimal se usará para representar los valores para el **campo**. El **precisión** propiedad especifica el número máximo de dígitos utilizados para representar valores para el **campo**.  
  
### <a name="determining-field-size"></a>Determinar el tamaño de campo  
 Use la **DefinedSize** propiedad para determinar la capacidad de datos de un **campo** objeto.  
  
 Use la **ActualSize** propiedad para devolver la longitud real de un **campo** valor del objeto. Todos los campos, el **ActualSize** propiedad es de solo lectura. Si ADO no puede determinar la longitud de la **campo** valor del objeto, el **ActualSize** propiedad devuelve **adUnknown**.  
  
 El **DefinedSize** y **ActualSize** propiedades tienen propósitos diferentes. Por ejemplo, considere un **campo** objeto con un tipo declarado de **parámetros** y un **DefinedSize** valor de propiedad de 50, que contiene un único carácter. El **ActualSize** devuelve el valor de propiedad es la longitud en bytes del carácter único.  
  
### <a name="determining-field-contents"></a>Determinar el contenido del campo  
 El identificador de la columna del origen de datos está representado por la **nombre** propiedad de la **campo**. El **valor** propiedad de la **campo** objeto devuelve o establece el contenido de los datos reales del campo. Se trata de la propiedad predeterminada.  
  
 Para cambiar los datos en un campo, establezca la **valor** propiedad igual a un valor nuevo del tipo correcto. El tipo de cursor debe admitir actualizaciones para cambiar el contenido de un campo. Validación de la base de datos no se hace aquí en modo por lotes, por lo que deberá comprobar si hay errores al llamar a **UpdateBatch** en este caso. Algunos proveedores también admiten la propiedad ADO **campo** del objeto **UnderlyingValue** y **OriginalValue** propiedades para ayudarle a resolver los conflictos cuando se intenta realizar actualizaciones por lotes. Para obtener más información sobre cómo resolver estos conflictos, consulte [modificar datos](../../../ado/guide/data/editing-data.md).  
  
> [!NOTE]
>  **Recordset Field** valores no se puede establecer al anexar nuevos **campos** a un **Recordset**. En su lugar, nueva **campos** se pueden anexar a un cerrado **Recordset**. El **Recordset** debe estar abierto y, a continuación, solo puede pueden asignar valores a estos **campos**.  
  
### <a name="getting-more-field-information"></a>Obtener más información acerca de campo  
 Los objetos ADO tienen dos tipos de propiedades: integradas y dinámicas. En este punto, solo las propiedades integradas de la **campo** se han explicado los objetos.  
  
 Las propiedades integradas son aquellas propiedades implementadas en ADO y disponibles inmediatamente para cualquier objeto nuevo, utilizando el `MyObject.Property` sintaxis. No aparecen como **propiedad** objetos en un objeto **propiedades** colección.  
  
 Propiedades dinámicas se definen mediante el proveedor de datos subyacente y aparecen en la **propiedades** colección para el objeto ADO apropiado. Por ejemplo, una propiedad específica del proveedor puede indicar si un **Recordset** objeto admite transacciones o actualizaciones. Estas propiedades adicionales aparecerán como **propiedad** objetos en el que **Recordset** del objeto **propiedades** colección. Propiedades dinámicas se pueden hacer referencia únicamente a través de la colección, utilizando la sintaxis `MyObject.Properties(0)` o `MyObject.Properties("Name")`.  
  
 No se puede eliminar cualquier tipo de propiedad.  
  
 Dinámico **propiedad** objeto tiene cuatro propiedades integradas de su propio:  
  
-   El **nombre** propiedad es una cadena que identifica la propiedad.  
  
-   El **tipo** propiedad es un entero que especifica el tipo de datos de propiedad.  
  
-   El **valor** propiedad es una variante que contiene el valor de propiedad. **Valor** es la propiedad predeterminada para un **propiedad** objeto.  
  
-   El **atributos** propiedad es un **largo** valor que indica características de la propiedad específica del proveedor.  
  
 El **propiedades** recopilación para el **campo** objeto contiene metadatos adicionales acerca del campo. El contenido de esta colección varía dependiendo del proveedor. El siguiente ejemplo de código examina el **propiedades** colección del ejemplo **Recordset** presentó al principio de esta sección. En primer lugar examina el contenido de la colección. Este código usa el [proveedor OLE DB para SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md), por lo que **propiedades** colección contiene información relativa a ese proveedor.  
  
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
 Use la [AppendChunk](../../../ado/reference/ado-api/appendchunk-method-ado.md) método en un **campo** objeto para llenarlo con datos binarios largos o de caracteres. En situaciones donde se limita la memoria del sistema, puede usar el **AppendChunk** método para manipular los valores largos en partes, en lugar de en su totalidad.  
  
 Si el **adFldLong** bit en el **atributos** propiedad de un **campo** objeto se establece en **True**, puede usar el  **AppendChunk** método para ese campo.  
  
 La primera **AppendChunk** llamar en un **campo** objeto escribe datos en el campo, sobrescribiendo los datos existentes. Posteriores **AppendChunk** agregan llamadas a los datos existentes. Si va a anexar datos a un campo y, a continuación, establecer o leer el valor de otro campo en el registro actual, ADO se da por supuesto que haya terminado de anexar datos al primer campo. Si se llama a la **AppendChunk** método en el primer campo de nuevo, ADO interpreta la llamada como un nuevo **AppendChunk** operación y sobrescribe los datos existentes. Obtener acceso a campos de otros **Recordset** objetos que no son clones del primer **Recordset** objeto, no se interrumpirán **AppendChunk** operaciones.  
  
 Use la **GetChunk** método en un **campo** objeto para recuperar la totalidad o parte de sus datos de caracteres o binarios largos. En situaciones donde se limita la memoria del sistema, puede usar el **GetChunk** método para manipular los valores largos en partes, en lugar de en su totalidad.  
  
 Los datos que un **GetChunk** devoluciones de llamada se asigna a *variable*. Si *tamaño* es mayor que los datos restantes, el **GetChunk** método devuelve sólo los datos restantes sin relleno *variable* con espacios en blanco. Si el campo está vacío, el **GetChunk** método devuelve un valor null.  
  
 Cada uno de ellos posteriores **GetChunk** llamada recupera datos a partir de dónde anterior **GetChunk** llamada lo dejó. Sin embargo, si está recuperando datos de un campo y, a continuación, establecer o leer el valor de otro campo en el registro actual, ADO supone que ha terminado de recuperar datos desde el primer campo. Si se llama a la **GetChunk** método en el primer campo de nuevo, ADO interpreta la llamada como un nuevo **GetChunk** operación y se inicia desde el principio de los datos de lectura. Obtener acceso a campos de otros **Recordset** objetos que no son clones del primer **Recordset** objeto, no se interrumpirán **GetChunk** operaciones.  
  
 Si el **adFldLong** bit en el **atributos** propiedad de un **campo** objeto se establece en **True**, puede usar el **GetChunk**  método para ese campo.  
  
 Si no hay ningún registro actual cuando se usa el **GetChunk** o **AppendChunk** método en un **campo** objeto, se produce el error 3021 (no hay registro actual).  
  
 Para obtener un ejemplo del uso de estos métodos para manipular datos binarios, vea el [método AppendChunk](../../../ado/reference/ado-api/appendchunk-method-ado.md) y [método GetChunk](../../../ado/reference/ado-api/getchunk-method-ado.md) ejemplos en los *referencia del programador de ADO*.
