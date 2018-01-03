---
title: "Append (método) (ADO) | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: _DynaCollection::Append
helpviewer_keywords: Append method [ADO]
ms.assetid: f8a9bbed-ba9c-4698-945d-317ad22d2e92
caps.latest.revision: "18"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: d0c0c887da52e8c91caeab582c2b1973b491e81d
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="append-method-ado"></a>Append (método) (ADO)
Anexa un objeto a una colección. Si la colección es [campos](../../../ado/reference/ado-api/fields-collection-ado.md), un nuevo [campo](../../../ado/reference/ado-api/field-object.md) se puede crear el objeto antes de que se anexa a la colección.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
collection.Append object  
fields.Append Name, Type, DefinedSize, Attrib, FieldValue  
```  
  
#### <a name="parameters"></a>Parámetros  
 *colección*  
 Un objeto de colección.  
  
 *campos*  
 A **campos** colección.  
  
 *objeto*  
 Una variable de objeto que representa el objeto que se va a anexar.  
  
 *Nombre*  
 A **cadena** valor que contiene el nombre del nuevo **campo** de objetos y no debe ser el mismo nombre que cualquier otro objeto en *campos*.  
  
 *Tipo*  
 A [DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md) valor, cuyo valor predeterminado es **adEmpty**, que especifica el tipo de datos del nuevo campo. ADO no admite los siguientes tipos de datos y no debe usarse al anexar nuevos campos a un [conjunto de registros ADO (objetos)](../../../ado/reference/ado-api/recordset-object-ado.md): **adIDispatch**, **adIUnknown**, **adVariant**.  
  
 *DefinedSize*  
 Opcional. A **largo** valor que representa el tamaño definido, en caracteres o bytes, del nuevo campo. El valor predeterminado para este parámetro se deriva de *tipo*. Los campos que tienen un *DefinedSize* mayores que 255 bytes se tratan como columnas de longitud variable. El valor predeterminado de *DefinedSize* no está especificado.  
  
 *Attrib*  
 Opcional. A [FieldAttributeEnum](../../../ado/reference/ado-api/fieldattributeenum.md) valor, cuyo valor predeterminado es **adFldDefault**, que especifica los atributos para el nuevo campo. Si no se especifica este valor, el campo contendrá atributos derivados de *tipo*.  
  
 *FieldValue*  
 Opcional. A **Variant** que representa el valor para el nuevo campo. Si no se especifica, el campo se anexa con un valor null.  
  
## <a name="remarks"></a>Comentarios  
  
## <a name="parameters-collection"></a>Colección Parameters  
 Debe establecer el [tipo](../../../ado/reference/ado-api/type-property-ado.md) propiedad de un [parámetro](../../../ado/reference/ado-api/parameter-object.md) objeto antes de anexarlo a la [parámetros](../../../ado/reference/ado-api/parameters-collection-ado.md) colección. Si selecciona un tipo de datos de longitud variable, debe establecer también la [tamaño](../../../ado/reference/ado-api/size-property-ado-parameter.md) propiedad en un valor mayor que cero.  
  
 Describir personalmente los parámetros, las llamadas al proveedor y, por tanto, mejora el rendimiento cuando utilice procedimientos almacenados o consultas parametrizadas. Sin embargo, debe conocer las propiedades de los parámetros asociados con el procedimiento almacenado o parámetros de consulta que desea llamar.  
  
 Utilice la [CreateParameter](../../../ado/reference/ado-api/createparameter-method-ado.md) método para crear **parámetro** objetos con los valores de propiedad adecuados y utilice el **anexado** método para agregarlos a la [ Parámetros de](../../../ado/reference/ado-api/parameters-collection-ado.md) colección. Esto permite establecer y devolver valores de parámetro sin tener que llamar al proveedor para obtener la información de parámetro. Si está escribiendo en un proveedor que no proporcione información de parámetros, debe usar este método para rellenar manualmente el **parámetros** colección con el fin de usar parámetros en absoluto.  
  
## <a name="fields-collection"></a>Colección Fields  
 El *FieldValue* parámetro sólo es válido cuando se agrega un **campo** el objeto a un [registro](../../../ado/reference/ado-api/record-object-ado.md) objeto, no a un **Recordset** objeto. Con un **registro** de objeto, puede anexar campos y proporcionar valores al mismo tiempo. Con un **conjunto de registros** objeto, debe crear campos mientras el **conjunto de registros** está cerrado y, a continuación, abra el **conjunto de registros** y asignar valores a los campos.  
  
> [!NOTE]
>  Para el nuevo **campo** objetos que se han anexado a la **campos** colección de un **registro** objeto, el [valor](../../../ado/reference/ado-api/value-property-ado.md) se debe establecer la propiedad antes de cualquier otro **campo** propiedades pueden especificarse. Primero, un valor específico para el **valor** propiedad debe estar asignada y [actualización](../../../ado/reference/ado-api/update-method.md) en el **campos** colección denominada. A continuación, otras propiedades como [tipo](../../../ado/reference/ado-api/type-property-ado.md) o [atributos](../../../ado/reference/ado-api/attributes-property-ado.md) son accesibles. **Campo** objetos de los siguientes tipos de datos (**DataTypeEnum**) no se pueden anexar a la **campos** colección y se producirá un error que se produzca: **adArray**, **Dbtype_hchapter**, **adEmpty**, **adPropVariant**, y **adUserDefined**. Además, ADO no admite los siguientes tipos de datos: **adIDispatch**, **adIUnknown**, y **adIVariant**. Para estos tipos, se producirá ningún error cuando se anexa, pero uso puede producir resultados imprevisibles, incluso las pérdidas de memoria.  
  
## <a name="recordset"></a>Conjunto de registros  
 Si no establece la [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) propiedad antes de llamar a la **anexar** método **CursorLocation** se establecerá en **adUseClient** () un [CursorLocationEnum](../../../ado/reference/ado-api/cursorlocationenum.md) valor) automáticamente cuando el [abiertos](../../../ado/reference/ado-api/open-method-ado-recordset.md) método de la [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) se denomina objeto.  
  
 Se producirá un error de tiempo de ejecución si el **anexado** método se llama en el **campos** colección de abierto **Recordset**, o en un **conjunto de registros** donde la [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) se ha establecido la propiedad. Solo se pueden anexar campos a un **Recordset** que no está abierto y aún no se ha conectado a un origen de datos. Suele ser el caso cuando un **Recordset** objeto se crea con el [CreateRecordset](../../../ado/reference/rds-api/createrecordset-method-rds.md) método o asignado a una variable de objeto.  
  
## <a name="record"></a>Grabar  
 No se producirá un error de tiempo de ejecución si el **anexado** método se llama en el **campos** colección de abierto **registro**. El nuevo campo se agregará a la **campos** colección de la **registro** objeto. Si el **registro** se derivó de una **Recordset**, el nuevo campo no aparecerá en la **campos** colección de la **Recordset** objeto.  
  
 Se puede crear un campo inexistente y anexa a la **campos** colección asignando un valor para el objeto de campo como si ya existiese en la colección. La asignación desencadenará la creación automática y agregar información de la **campo** objeto y, a continuación, la asignación se llevará a cabo.  
  
 Después de anexar una **campo** a la **campos** colección de un **registro** objeto, llame a la **actualización** método de la **campos**  colección para guardar el cambio.  
  
## <a name="applies-to"></a>Se aplica a  
  
- [Fields (colección) (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)  
- [Colección de parámetros (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Anexar y ejemplo de los métodos CreateParameter (VB)](../../../ado/reference/ado-api/append-and-createparameter-methods-example-vb.md)   
 [Anexar y ejemplo de los métodos CreateParameter (VC ++)](../../../ado/reference/ado-api/append-and-createparameter-methods-example-vc.md)   
 [Método CreateParameter (ADO)](../../../ado/reference/ado-api/createparameter-method-ado.md)   
 [El método Delete (colección Fields de ADO)](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Método Delete (colección de parámetros de ADO)](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)   
 [Delete (método) (conjunto de registros ADO)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [Update (método)](../../../ado/reference/ado-api/update-method.md)
