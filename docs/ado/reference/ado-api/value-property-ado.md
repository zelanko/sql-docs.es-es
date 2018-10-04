---
title: Valor de propiedad (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 03/20/2018
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Field20::Value
- _Parameter::Value
helpviewer_keywords:
- Value property [ADO]
ms.assetid: 48919c74-86d4-462e-99b9-8854ceb8d683
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8c7e4d42bc58321c5b650df5e8e842290094fcf4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47715026"
---
# <a name="value-property-ado"></a>Value (propiedad) (ADO)

Indica el valor asignado a un [campo](../../../ado/reference/ado-api/field-object.md), [parámetro](../../../ado/reference/ado-api/parameter-object.md), o [propiedad](../../../ado/reference/ado-api/property-object-ado.md) objeto.
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos

Establece o devuelve un **Variant** valor que indica el valor del objeto. Valor predeterminado depende del [tipo](../../../ado/reference/ado-api/type-property-ado.md) propiedad.
  
## <a name="remarks"></a>Comentarios

Use la **valor** propiedad para establecer o devolver datos de **campo** objetos, para establecer o devolver los valores de parámetro con **parámetro** objetos, o para establecer o devolver valores de propiedad con **Propiedad** objetos. Si el **valor** propiedad es de lectura/escritura o de sólo lectura depende de varios factores. Vea los temas correspondientes de objeto para obtener más información.

ADO permite establecer y devolver datos binarios largos con la **valor** propiedad.
  
> [!NOTE]
> Para **parámetro** objetos, ADO lee la **valor** propiedad una sola vez desde el proveedor. Si contiene un comando un **parámetro** cuyo **valor** propiedad está vacía y se crea un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) desde el comando, asegúrese de cerrar primero el  **Conjunto de registros** antes de recuperar el **valor** propiedad. En caso contrario, para algunos proveedores, el **valor** propiedad puede estar vacía y no contendrá el valor correcto.
> 
> Para el nuevo **campo** objetos que se han anexado a la [campos](../../../ado/reference/ado-api/fields-collection-ado.md) colección de un [registro](../../../ado/reference/ado-api/record-object-ado.md) objeto, el **valor** se debe establecer la propiedad antes de cualquier otro **campo** se pueden especificar las propiedades. Primero, un valor específico para el **valor** propiedad debe tener asignada y [actualización](../../../ado/reference/ado-api/update-method.md) en el **campos** colección denominada. A continuación, otras propiedades como [tipo](../../../ado/reference/ado-api/type-property-ado.md) o [atributos](../../../ado/reference/ado-api/attributes-property-ado.md) se puede tener acceso.
  
## <a name="applies-to"></a>Se aplica a
  
||||  
|-|-|-|  
|[Objeto Field](../../../ado/reference/ado-api/field-object.md)|[Objeto Parameter](../../../ado/reference/ado-api/parameter-object.md)|[Objeto Property (ADO)](../../../ado/reference/ado-api/property-object-ado.md)|
  
## <a name="see-also"></a>Vea también

[Valor de ejemplo de la propiedad (VB)](../../../ado/reference/ado-api/value-property-example-vb.md)
[valor ejemplo de la propiedad (VC ++)](../../../ado/reference/ado-api/value-property-example-vc.md) 
