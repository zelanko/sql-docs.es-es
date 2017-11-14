---
title: Utilizar extensiones de Visual C++ | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- C++
helpviewer_keywords:
- Visual C++ [ADO], using VC++ extensions
- ADO, Visual C++
ms.assetid: ff759185-df41-4507-8d12-0921894ffbd9
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 90ef5f49740a7e9e750ade714f0571f2642f0d47
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="visual-c-extensions"></a>Extensiones de Visual C++
## <a name="the-iadorecordbinding-interface"></a>La interfaz IADORecordBinding
 Las extensiones de Microsoft Visual C++ para ADO asocian o enlace, los campos de un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto a las variables de C o C++. Cada vez que la fila actual del límite de la **Recordset** cambia, todos los campos enlazados en el **Recordset** se copian en las variables de C o C++. Si es necesario, los datos copiados se convierten al tipo de datos declarado de la variable de C o C++.

 El **BindToRecordset** método de la **IADORecordBinding** interfaz enlaza los campos a las variables de C o C++. El **AddNew** método agrega una nueva fila al límite **conjunto de registros**. El **actualización** método rellena los campos en las nuevas filas de la **Recordset**, o actualiza los campos en las filas existentes con el valor de las variables de C o C++.

 El **IADORecordBinding** interfaz está implementada por la **Recordset** objeto. No código usted mismo la implementación.

## <a name="binding-entries"></a>Entradas de enlace
 Extensiones de Visual C++ para ADO asignan los campos de un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto a las variables de C o C++. La definición de una asignación entre un campo y una variable se denomina un *enlace entrada*. Las macros proporcionan entradas de enlace de datos numéricos, de longitud fija y de longitud variable. Las entradas de enlace y las variables de C o C++ se declaran en una clase derivada de la clase de extensiones de Visual C++, **CADORecordBinding**. El **CADORecordBinding** clase definen internamente las macros de entrada de enlace.

 ADO asigna internamente los parámetros de estas macros para OLE DB **DBBINDING** permite organizar y crea OLE DB **descriptor de acceso** objeto para administrar el movimiento y la conversión de datos entre los campos y las variables. OLE DB define los datos como que consta de tres partes: un *búfer* donde se almacenan los datos; un *estado* que indica si un campo se almacenó correctamente en el búfer o cómo debe restaurarse la variable a el campo; y el *longitud* de los datos. (Consulte [obtener y establecer los datos (OLE DB)](http://msdn.microsoft.com/en-us/4369708b-c9fb-4d48-a321-bf949b41a369)en referencia de la base de datos del programador de OLE, para obtener más información.)

## <a name="header-file"></a>Archivo de encabezado
 En la aplicación para usar las extensiones de Visual C++ para ADO, incluya el archivo siguiente:

```
#include <icrsint.h>
```

## <a name="binding-recordset-fields"></a>Enlazar campos de conjunto de registros

#### <a name="to-bind-recordset-fields-to-cc-variables"></a>Enlazar campos de conjunto de registros a las Variables de C o C++

1.  Crear una clase derivada de la **CADORecordBinding** clase.

2.  Especifique las entradas de enlace y las variables de C o C++ correspondientes en la clase derivada. Inserte las entradas de enlace entre **BEGIN ADO Binding** y **end ADO Binding** macros. No termine las macros con comas o punto y coma. Cada macro especifica automáticamente los delimitadores apropiados.

     Especifique una entrada de enlace para cada campo que debe asignarse a una variable de C o C++. Utilice un miembro apropiado de la **ADO Fixed Length Entry**, **ADO NUMERIC ENTRY**, o **ADO variable Length Entry** familia de macros.

3.  En la aplicación, cree una instancia de la clase derivada de **CADORecordBinding**. Obtener la **IADORecordBinding** interfaz desde el **conjunto de registros**. A continuación, llame a la **BindToRecordset** método para enlazar el **conjunto de registros** campos a las variables de C o C++.

 Para obtener más información, consulte el [ejemplo de extensiones de Visual C++](../../../ado/guide/appendixes/visual-c-extensions-example.md).

## <a name="interface-methods"></a>Métodos de interfaz
 El **IADORecordBinding** interfaz tiene tres métodos: **BindToRecordset**, **AddNew**, y **actualización**. El único argumento para cada método es un puntero a una instancia de la clase derivada de **CADORecordBinding**. Por lo tanto, la **AddNew** y **actualización** métodos no pueden especificar cualquiera de los parámetros de los homónimos de ADO.

## <a name="syntax"></a>Sintaxis
 El **BindToRecordset** método asocia la **Recordset** campos con variables de C o C++.

```
BindToRecordset(CADORecordBinding *binding)
```

 El **AddNew** método invoca su homónimo, ADO [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md) método, para agregar una nueva fila a la **conjunto de registros**.

```
AddNew(CADORecordBinding *binding)
```

 El **actualizar** método invoca su homónimo, ADO [actualizar](../../../ado/reference/ado-api/update-method.md) método para actualizar la **conjunto de registros**.

```
Update(CADORecordBinding *binding)
```

## <a name="binding-entry-macros"></a>Macros de entrada de enlace
 Macros de entradas de enlace definen la asociación de un **Recordset** campo y una variable. Una macro inicial y final delimita el conjunto de entradas de enlace.

 Familias de macros se proporcionan para los datos de longitud fija, como **adDate** o **adBoolean**; numérico datos, como **excepto adVarNumeric**, **son también tipos**, o **longitud fija**; y los datos de longitud variable, como **cada**, **parámetros** o **adVarBinary**. Todos los tipos numéricos, excepto para **adVarNumeric**, son también tipos de longitud fija. Cada familia tiene diferentes conjuntos de parámetros para que se puede excluir la información de enlace que no es de interés.

 Para obtener más información, consulte [Apéndice A: tipos de datos](http://msdn.microsoft.com/en-us/e3a0533a-2196-4eb0-a31e-92fe9556ada6), de referencia de la base de datos del programador de OLE.

### <a name="begin-binding-entries"></a>Empezar a entradas de enlace
 **BEGIN ADO Binding**(*clase*)

### <a name="fixed-length-data"></a>Datos de longitud fija
 **ADO Fixed Length Entry**(*Ordinal, tipo de datos, búfer, estado, modificar*)

 **ADO_FIXED_LENGTH_ENTRY2**(*Ordinal, el tipo de datos de búfer, modificar*)

### <a name="numeric-data"></a>Datos numéricos
 **ADO NUMERIC ENTRY**(*Ordinal, tipo de datos, búfer, precisión, escala, estado, modificar*)

 **ADO_NUMERIC_ENTRY2**(*Ordinal, tipo de datos, búfer, precisión, escala, modificar*)

### <a name="variable-length-data"></a>Datos de longitud variable
 **ADO variable Length Entry**(*Ordinal, tipo de datos, búfer, tamaño, estado, longitud, modificar*)

 **ADO_VARIABLE_LENGTH_ENTRY2**(*Ordinal, el tipo de datos, búfer, tamaño, estado, modificar*)

 **ADO_VARIABLE_LENGTH_ENTRY3**(*Ordinal, tipo de datos, el búfer, tamaño, longitud, modificar*)

 **ADO_VARIABLE_LENGTH_ENTRY4**(*Ordinal, tipo de datos, búfer, tamaño, modificar*)

### <a name="end-binding-entries"></a>Final de entradas de enlace
 **END ADO BINDING**)

|Parámetro|Description|
|---------------|-----------------|
|*Clase*|Clase en que se definen las entradas de enlace y las variables de C o C++.|
|*Ordinal*|Número ordinal, a partir de 1, de la **Recordset** campo correspondiente a la variable de C o C++.|
|*Tipo de datos*|Tipo de datos de ADO equivalente de la variable de C o C++ (vea [DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md) para obtener una lista de tipos de datos válidos). El valor de la **Recordset** campo se convertirá en este tipo de datos si es necesario.|
|*Búfer*|Nombre de la variable de C o C++ donde la **Recordset** se almacenará el campo.|
|*Tamaño*|Tamaño máximo en bytes de *búfer*. Si *búfer* contendrá una cadena de longitud variable, deje espacio para un cero de terminación.|
|*Estado*|Nombre de una variable que indicará si el contenido de *búfer* son válidos y si la conversión del campo a *DataType* fue correcta.<br /><br /> Los dos valores más importantes de esta variable son **adFldOK**, lo que significa que la conversión fue correcta; y **adFldNull**, lo que significa que el valor del campo sería una variante de tipo VT_NULL y no simplemente vacía.<br /><br /> Valores posibles de *estado* se muestran en la tabla siguiente, "Valores de Status".|
|*Modificar*|Marca booleana; Si es TRUE, indica que ADO puede actualizar el correspondiente **Recordset** campo con el valor contenido en *búfer*.<br /><br /> Establece el valor booleano *modificar* parámetro en TRUE para permitir que ADO actualizar el campo enlazado y FALSE si desea examinar el campo pero no cambiarlo.|
|*Precisión*|Número de dígitos que se pueden representar en una variable numérica.|
|*Escala*|Número de posiciones decimales en una variable numérica.|
|*Longitud*|Nombre de una variable de cuatro bytes que va a contener la longitud real de los datos de *búfer*.|

## <a name="status-values"></a>Valores de estado
 El valor de la *estado* variable indica si un campo se ha copiado correctamente a una variable.

 Al establecer los datos, *estado* se puede establecer en **adFldNull** para indicar el **Recordset** campo debe establecerse en null.

|Constante|Valor|Description|
|--------------|-----------|-----------------|
|**adFldOK**|0|Se devolvió un valor de campo distinto de null.|
|**adFldBadAccessor**|1|Enlace no era válido.|
|**adFldCantConvertValue**|2|Valor no pudo convertir por motivos distintos a un error de coincidencia de signos, desbordamiento de datos.|
|**adFldNull**|3|Al obtener un campo, indica que se devolvió un valor null.<br /><br /> Al establecer un campo, indica que el campo debe establecerse en **NULL** cuando no puede codificar el campo **NULL** por sí mismo (por ejemplo, una matriz de caracteres o un entero).|
|**adFldTruncated**|4|Se truncaron los datos de longitud variable o dígitos numéricos.|
|**adFldSignMismatch**|5|El valor tiene signo y el tipo de datos de la variable es sin signo.|
|**adFldDataOverFlow**|6|Valor es mayor que se puede almacenar en el tipo de datos de la variable.|
|**adFldCantCreate**|7|Tipo de columna desconocido y campo ya está abierto.|
|**adFldUnavailable**|8|No se pudo determinar el valor del campo, por ejemplo, en un campo nuevo, sin asignar con ningún valor predeterminado.|
|**adFldPermissionDenied**|9|Al actualizar, no tiene permiso para escribir los datos.|
|**adFldIntegrityViolation**|10|Al actualizar, el valor de campo infringirá integridad de la columna.|
|**adFldSchemaViolation**|11|Al actualizar, el valor de campo infringirá el esquema de columna.|
|**adFldBadStatus**|12|Al actualizar, parámetro de estado no válido.|
|**adFldDefault**|13|Al actualizar, se usa un valor predeterminado.|

## <a name="see-also"></a>Vea también
 [Ejemplo de extensiones de Visual C++](../../../ado/guide/appendixes/visual-c-extensions-example.md) [encabezado de extensiones de Visual C++](../../../ado/guide/appendixes/visual-c-extensions-header.md)

