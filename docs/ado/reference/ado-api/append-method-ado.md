---
title: Append (método) (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _DynaCollection::Append
helpviewer_keywords:
- Append method [ADO]
ms.assetid: f8a9bbed-ba9c-4698-945d-317ad22d2e92
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5e03e29d5c9696efb55ef5ce6ec47fcf28fc0467
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47712401"
---
# <a name="append-method-ado"></a>Append (método) (ADO)
Anexa un objeto a una colección. Si la colección es [campos](../../../ado/reference/ado-api/fields-collection-ado.md), un nuevo [campo](../../../ado/reference/ado-api/field-object.md) se puede crear el objeto antes de se anexa a la colección.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
collection.Append object  
fields.Append Name, Type, DefinedSize, Attrib, FieldValue  
```  
  
#### <a name="parameters"></a>Parámetros  
 *colección*  
 Un objeto de colección.  
  
 *Campos*  
 Un **campos** colección.  
  
 *object*  
 Una variable de objeto que representa el objeto que se va a anexar.  
  
 *Nombre*  
 Un **cadena** valor que contiene el nombre del nuevo **campo** de objetos, y no debe ser el mismo nombre como cualquier otro objeto en *campos*.  
  
 *Tipo*  
 Un [DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md) valor, cuyo valor predeterminado es **adEmpty**, que especifica el tipo de datos del nuevo campo. No se admiten los siguientes tipos de datos ADO y no debe usarse al anexar nuevos campos a un [conjunto de registros ADO (objetos)](../../../ado/reference/ado-api/recordset-object-ado.md): **adIDispatch**, **adChapter**, **adVariant**.  
  
 *DefinedSize*  
 Opcional. Un **largo** valor que representa el tamaño definido, en caracteres o bytes, del nuevo campo. El valor predeterminado para este parámetro se deriva *tipo*. Los campos que tienen un *DefinedSize* mayores de 255 bytes se tratan como columnas de longitud variable. El valor predeterminado para *DefinedSize* no se ha especificado.  
  
 *Attrib*  
 Opcional. Un [FieldAttributeEnum](../../../ado/reference/ado-api/fieldattributeenum.md) valor, cuyo valor predeterminado es **adFldDefault**, que especifica los atributos para el nuevo campo. Si no se especifica este valor, el campo contendrá atributos derivados de *tipo*.  
  
 *FieldValue*  
 Opcional. Un **Variant** que representa el valor para el nuevo campo. Si no se especifica, el campo se anexa con un valor null.  
  
## <a name="remarks"></a>Comentarios  
  
## <a name="parameters-collection"></a>Colección Parameters  
 Debe establecer el [tipo](../../../ado/reference/ado-api/type-property-ado.md) propiedad de un [parámetro](../../../ado/reference/ado-api/parameter-object.md) objeto antes de agregarlo a la [parámetros](../../../ado/reference/ado-api/parameters-collection-ado.md) colección. Si selecciona un tipo de datos de longitud variable, también debe establecer el [tamaño](../../../ado/reference/ado-api/size-property-ado-parameter.md) propiedad en un valor mayor que cero.  
  
 Que describe parámetros minimiza las llamadas al proveedor y, por tanto, mejora el rendimiento al usar consultas parametrizadas o procedimientos almacenados. Sin embargo, debe conocer las propiedades de los parámetros asociados con el procedimiento almacenado o parámetros de consulta que desea llamar.  
  
 Usar el [CreateParameter](../../../ado/reference/ado-api/createparameter-method-ado.md) método para crear **parámetro** objetos con los valores de propiedad adecuados y el uso del **anexar** método para agregarlos a la [ Parámetros](../../../ado/reference/ado-api/parameters-collection-ado.md) colección. Esto le permite establecer y devolver valores de parámetro sin tener que llamar al proveedor para obtener la información de parámetro. Si está escribiendo en un proveedor que no proporcione información de parámetros, debe utilizar este método para rellenar manualmente el **parámetros** colección para poder usar parámetros en absoluto.  
  
## <a name="fields-collection"></a>Colección Fields  
 El *FieldValue* parámetro sólo es válido cuando se agrega un **campo** objeto a un [registro](../../../ado/reference/ado-api/record-object-ado.md) objeto, no a un **Recordset** objeto. Con un **registro** de objeto, puede anexar campos y proporcionar valores al mismo tiempo. Con un **Recordset** objeto, debe crear los campos mientras el **Recordset** está cerrado y, a continuación, abra el **conjunto de registros** y asignar valores a los campos.  
  
> [!NOTE]
>  Para el nuevo **campo** objetos que se han anexado a la **campos** colección de un **registro** objeto, el [valor](../../../ado/reference/ado-api/value-property-ado.md) se debe establecer la propiedad antes de cualquier otro **campo** se pueden especificar las propiedades. Primero, un valor específico para el **valor** propiedad debe tener asignada y [actualización](../../../ado/reference/ado-api/update-method.md) en el **campos** colección denominada. A continuación, otras propiedades como [tipo](../../../ado/reference/ado-api/type-property-ado.md) o [atributos](../../../ado/reference/ado-api/attributes-property-ado.md) se puede tener acceso. **Campo** objetos de los siguientes tipos de datos (**DataTypeEnum**) no se puede anexar el **campos** colección y se producirá un error que se produzca: **adArray**, **adChapter**, **adEmpty**, **adPropVariant**, y **adUserDefined**. Además, no se admiten los siguientes tipos de datos ADO: **adIDispatch**, **adChapter**, y **adIVariant**. Para estos tipos, no se producirá ningún error al anexar, pero uso puede producir resultados imprevisibles, incluidas las pérdidas de memoria.  
  
## <a name="recordset"></a>Conjunto de registros  
 Si no establece la [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) propiedad antes de llamar a la **Append** método **CursorLocation** se establecerá en **adUseClient** () un [CursorLocationEnum](../../../ado/reference/ado-api/cursorlocationenum.md) valor) automáticamente cuando el [abierto](../../../ado/reference/ado-api/open-method-ado-recordset.md) método de la [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) se denomina objeto.  
  
 Se producirá un error de tiempo de ejecución si el **Append** se llama al método en el **campos** colección de una abierta **Recordset**, o en un **Recordset** donde el [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) se estableció la propiedad. Sólo se pueden anexar campos a un **Recordset** que no está abierto y aún no se ha conectado a un origen de datos. Esto suele ser el caso cuando un **Recordset** objeto se crea con el [CreateRecordset](../../../ado/reference/rds-api/createrecordset-method-rds.md) método o asignado a una variable de objeto.  
  
## <a name="record"></a>Grabar  
 No se producirá un error de tiempo de ejecución si el **Append** se llama al método en el **campos** colección de una abierta **registro**. Se agregará el nuevo campo a la **campos** colección de la **registro** objeto. Si el **registro** se derivó de un **Recordset**, el nuevo campo no aparecerá en el **campos** colección de la **Recordset** objeto.  
  
 Se puede crear un campo inexistente y anexa a la **campos** colección asignando un valor para el objeto de campo como si ya existía en la colección. La asignación desencadenará la creación automática y anexe la **campo** objeto y, a continuación, la asignación se completará.  
  
 Después de anexar una **campo** a la **campos** colección de un **registro** de objeto, llame a la **actualización** método de la **campos**  colección para guardar el cambio.  
  
## <a name="applies-to"></a>Se aplica a  
  
- [Fields (colección) (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)  
- [Colección de parámetros (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Anexar y ejemplo de los métodos CreateParameter (VB)](../../../ado/reference/ado-api/append-and-createparameter-methods-example-vb.md)   
 [Anexar y ejemplo de los métodos CreateParameter (VC ++)](../../../ado/reference/ado-api/append-and-createparameter-methods-example-vc.md)   
 [Método CreateParameter (ADO)](../../../ado/reference/ado-api/createparameter-method-ado.md)   
 [El método Delete (colección Fields de ADO)](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Método Delete (colección de parámetros de ADO)](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)   
 [Eliminar método (ADO Recordset)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [Update (método)](../../../ado/reference/ado-api/update-method.md)
