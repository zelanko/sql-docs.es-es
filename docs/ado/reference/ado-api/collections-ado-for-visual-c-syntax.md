---
title: Colecciones (ADO para la sintaxis de Visual C++) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
dev_langs:
- C++
helpviewer_keywords:
- ADO for Visual C++ syntax [ADO]
- syntax indexes [ADO], ADO for Visual C++ syntax
- collections [ADO], ADO for Visual C++ syntax
ms.assetid: 6a0109a0-f2d9-4f7c-8e1e-42763f9acaea
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d94570a337f564588b2709fd292eab5ed5396dc4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63126707"
---
# <a name="collections-ado-for-visual-c-syntax"></a>Colecciones (ADO para la sintaxis Visual C++)
## <a name="parameters"></a>Parámetros  
  
### <a name="methods"></a>Métodos  
  
```  
Append(IDispatch *Object);  
Delete(VARIANT Index);  
Refresh(void);  
```  
  
 Para obtener más información, vea  
  
-   [Append (método) (ADO)](../../../ado/reference/ado-api/append-method-ado.md)  
  
-   [Método Delete (colección de parámetros de ADO)](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)  
  
-   [Actualizar (método, ADO)](../../../ado/reference/ado-api/refresh-method-ado.md)  
  
### <a name="properties"></a>Propiedades  
  
```  
get_Count(long *c);  
get_Item(VARIANT Index, _ADOParameter **ppvObject);  
```  
  
 Para obtener más información, vea  
  
-   [Count (propiedad, ADO)](../../../ado/reference/ado-api/count-property-ado.md)  
  
-   [Propiedad Item (ADO)](../../../ado/reference/ado-api/item-property-ado.md)  
  
## <a name="fields"></a>Campos  
  
### <a name="methods"></a>Métodos  
  
```  
Append(BSTR bstrName, DataTypeEnum Type, long DefinedSize, FieldAttributeEnum Attrib);  
Delete(VARIANT Index);  
Refresh(void);  
```  
  
 Para obtener más información, vea  
  
-   [Append (método) (ADO)](../../../ado/reference/ado-api/append-method-ado.md)  
  
-   [Método Delete (colección de parámetros de ADO)](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)  
  
-   [Actualizar (método, ADO)](../../../ado/reference/ado-api/refresh-method-ado.md)  
  
### <a name="properties"></a>Propiedades  
  
```  
get_Count(long *c);  
get_Item(VARIANT Index, ADOField **ppvObject);  
```  
  
 Para obtener más información, vea  
  
-   [Count (propiedad, ADO)](../../../ado/reference/ado-api/count-property-ado.md)  
  
-   [Propiedad Item (ADO)](../../../ado/reference/ado-api/item-property-ado.md)  
  
## <a name="errors"></a>Errores  
  
### <a name="methods"></a>Métodos  
  
```  
Clear(void);  
Refresh(void);  
```  
  
 Para obtener más información, vea  
  
-   [Clear (método) (ADO)](../../../ado/reference/ado-api/clear-method-ado.md)  
  
-   [Actualizar (método, ADO)](../../../ado/reference/ado-api/refresh-method-ado.md)  
  
### <a name="properties"></a>Propiedades  
  
```  
get_Count(long *c);  
get_Item(VARIANT Index, ADOError **ppvObject);  
```  
  
 Para obtener más información, vea  
  
-   [Count (propiedad, ADO)](../../../ado/reference/ado-api/count-property-ado.md)  
  
-   [Propiedad Item (ADO)](../../../ado/reference/ado-api/item-property-ado.md)  
  
## <a name="properties"></a>Propiedades  
  
### <a name="methods"></a>Métodos  
  
```  
Refresh(void);  
```  
  
 Para obtener más información, vea  
  
-   [Actualizar (método, ADO)](../../../ado/reference/ado-api/refresh-method-ado.md)  
  
### <a name="properties"></a>Propiedades  
  
```  
get_Count(long *c);  
get_Item(VARIANT Index, ADOProperty **ppvObject);  
```  
  
 Para obtener más información, vea  
  
-   [Count (propiedad, ADO)](../../../ado/reference/ado-api/count-property-ado.md)  
  
-   [Propiedad Item (ADO)](../../../ado/reference/ado-api/item-property-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Colección de errores (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)   
 [Colección de campos (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)   
 [Colección de parámetros (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)   
 [Colección de propiedades (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
