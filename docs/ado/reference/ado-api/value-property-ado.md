---
title: Valor de propiedad (ADO) | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Field20::Value
- _Parameter::Value
helpviewer_keywords: Value property [ADO]
ms.assetid: 48919c74-86d4-462e-99b9-8854ceb8d683
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8be64c318d9857f847dfc82c709a7e718d4bb462
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="value-property-ado"></a>Value (propiedad) (ADO)
Indica el valor asignado a un [campo](../../../ado/reference/ado-api/field-object.md), [parámetro](../../../ado/reference/ado-api/parameter-object.md), o [propiedad](../../../ado/reference/ado-api/property-object-ado.md) objeto.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un **Variant** valor que indica el valor del objeto. Valor predeterminado depende del [tipo](../../../ado/reference/ado-api/type-property-ado.md) propiedad.  
  
## <a name="remarks"></a>Comentarios  
 Use la **valor** propiedad para establecer o devolver datos de **campo** objetos, para establecer o devolver valores de parámetro con **parámetro** objetos, o para establecer o devolver valores de propiedad con **Propiedad** objetos. Si el **valor** propiedad es de lectura/escritura o de sólo lectura depende de diversos factores??? vea los temas de objeto correspondiente para obtener más información.  
  
 ADO permite establecer y devolver datos binarios largos con la **valor** propiedad.  
  
> [!NOTE]
>  Para **parámetro** objetos, ADO lee la **valor** propiedad sólo una vez desde el proveedor. Si un comando contiene un **parámetro** cuyo **valor** propiedad está vacía y se crea un [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) del comando, asegúrese de que cierre el  **Conjunto de registros** antes de recuperar el **valor** propiedad. En caso contrario, para algunos proveedores, el **valor** propiedad puede estar vacía y no contendrá el valor correcto.  
>   
>  Para el nuevo **campo** objetos que se han anexado a la [campos](../../../ado/reference/ado-api/fields-collection-ado.md) colección de un [registro](../../../ado/reference/ado-api/record-object-ado.md) objeto, el **valor** se debe establecer la propiedad antes de cualquier otro **campo** propiedades pueden especificarse. Primero, un valor específico para el **valor** propiedad debe estar asignada y [actualización](../../../ado/reference/ado-api/update-method.md) en el **campos** colección denominada. A continuación, otras propiedades como [tipo](../../../ado/reference/ado-api/type-property-ado.md) o [atributos](../../../ado/reference/ado-api/attributes-property-ado.md) son accesibles.  
  
## <a name="applies-to"></a>Se aplica a  
  
||||  
|-|-|-|  
|[Objeto Field](../../../ado/reference/ado-api/field-object.md)|[Objeto Parameter](../../../ado/reference/ado-api/parameter-object.md)|[Objeto Property (ADO)](../../../ado/reference/ado-api/property-object-ado.md)|  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de la propiedad de valor (VB)](../../../ado/reference/ado-api/value-property-example-vb.md)   
 [Ejemplo de la propiedad de valor (VC ++)](../../../ado/reference/ado-api/value-property-example-vc.md)   
