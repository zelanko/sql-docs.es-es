---
title: Valor de propiedad (ADO) | Documentos de Microsoft
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 03/20/2018
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Field20::Value
- _Parameter::Value
helpviewer_keywords:
- Value property [ADO]
ms.assetid: 48919c74-86d4-462e-99b9-8854ceb8d683
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e5c1dd26184e4f869cab7edbde5c0de3ca36a03c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="value-property-ado"></a>Value (propiedad) (ADO)

Indica el valor asignado a un [campo](../../../ado/reference/ado-api/field-object.md), [parámetro](../../../ado/reference/ado-api/parameter-object.md), o [propiedad](../../../ado/reference/ado-api/property-object-ado.md) objeto.
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos

Establece o devuelve un **Variant** valor que indica el valor del objeto. Valor predeterminado depende del [tipo](../../../ado/reference/ado-api/type-property-ado.md) propiedad.
  
## <a name="remarks"></a>Comentarios

Use la **valor** propiedad para establecer o devolver datos de **campo** objetos, para establecer o devolver valores de parámetro con **parámetro** objetos, o para establecer o devolver valores de propiedad con **Propiedad** objetos. Si el **valor** propiedad es de lectura/escritura o de sólo lectura depende de diversos factores. vea los temas de objeto correspondiente para obtener más información.

ADO permite establecer y devolver datos binarios largos con la **valor** propiedad.
  
> [!NOTE]
> Para **parámetro** objetos, ADO lee la **valor** propiedad sólo una vez desde el proveedor. Si un comando contiene un **parámetro** cuyo **valor** propiedad está vacía y se crea un [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) del comando, asegúrese de que cierre el  **Conjunto de registros** antes de recuperar el **valor** propiedad. En caso contrario, para algunos proveedores, el **valor** propiedad puede estar vacía y no contendrá el valor correcto.
> 
> Para el nuevo **campo** objetos que se han anexado a la [campos](../../../ado/reference/ado-api/fields-collection-ado.md) colección de un [registro](../../../ado/reference/ado-api/record-object-ado.md) objeto, el **valor** se debe establecer la propiedad antes de cualquier otro **campo** propiedades pueden especificarse. Primero, un valor específico para el **valor** propiedad debe estar asignada y [actualización](../../../ado/reference/ado-api/update-method.md) en el **campos** colección denominada. A continuación, otras propiedades como [tipo](../../../ado/reference/ado-api/type-property-ado.md) o [atributos](../../../ado/reference/ado-api/attributes-property-ado.md) son accesibles.
  
## <a name="applies-to"></a>Se aplica a
  
||||  
|-|-|-|  
|[Objeto Field](../../../ado/reference/ado-api/field-object.md)|[Objeto Parameter](../../../ado/reference/ado-api/parameter-object.md)|[Objeto Property (ADO)](../../../ado/reference/ado-api/property-object-ado.md)|
  
## <a name="see-also"></a>Vea también

[Valor de ejemplo de la propiedad (VB)](../../../ado/reference/ado-api/value-property-example-vb.md)
[valor ejemplo de la propiedad (VC ++)](../../../ado/reference/ado-api/value-property-example-vc.md) 
