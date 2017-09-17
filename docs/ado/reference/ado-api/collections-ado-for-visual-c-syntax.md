---
title: Colecciones (ADO para la sintaxis Visual C++) | Documentos de Microsoft
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
dev_langs:
- C++
helpviewer_keywords:
- ADO for Visual C++ syntax [ADO]
- syntax indexes [ADO], ADO for Visual C++ syntax
- collections [ADO], ADO for Visual C++ syntax
ms.assetid: 6a0109a0-f2d9-4f7c-8e1e-42763f9acaea
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d16122393fb3a81f90b6e8d708377745a2ef1236
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

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
 [Fields (colección) (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)   
 [Colección de parámetros (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)   
 [Colección de propiedades (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
