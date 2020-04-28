---
title: Interfaz ADOStreamConstruction | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADOStreamConstruction
helpviewer_keywords:
- ADOStreamConstruction interface [ADO]
ms.assetid: 92f5a939-3e1a-4b14-a9dd-90e6ce2dec74
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 70a6dd02722a34159b345a83b32897aa8c38d0ff
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "67920787"
---
# <a name="adostreamconstruction-interface"></a>Interfaz ADOStreamConstruction
La interfaz **ADOStreamConstruction** se utiliza para construir un objeto de **secuencia** de ADO a partir de un OLE DB objeto **IStream** en una aplicación de C/C++.  
  
## <a name="properties"></a>Propiedades  
  
|||  
|-|-|  
|[Propiedad de la secuencia](../../../ado/reference/ado-api/stream-property.md)|Lectura y escritura. Obtiene o establece un objeto de **secuencia** de OLE DB.|  
  
## <a name="methods"></a>Métodos  
 Ninguno.  
  
## <a name="events"></a>Events  
 Ninguno.  
  
## <a name="remarks"></a>Observaciones  
 Dado un OLE DB objeto **IStream** (`pStream`), la construcción de un objeto de **secuencia** de`adoStr`ADO () se suma a las tres operaciones básicas siguientes:  
  
1.  Cree un objeto de **secuencia** de ADO:  
  
    ```  
    Stream20Ptr adoStr;  
    adoStr.CreateInstance(__uuidof(Stream));  
    ```  
  
2.  Consulte la interfaz **IADOStreamConstruction** en el objeto de **flujo** :  
  
    ```  
    adoStreamConstructionPtr adoStrConstruct=NULL;  
    adoStr->QueryInterface(__uuidof(ADOStreamConstruction),  
                         (void**)&adoStrConstruct);  
    ```  
  
 Llame al `IADOStreamConstruction::get_Stream` método de propiedad para establecer el OLE DB objeto **IStream** en el objeto de **secuencia** de ADO:  
  
```  
IUnknown *pUnk=NULL;  
pRowset->QueryInterface(IID_IUnknown, (void**)&pUnk);  
adoStrConstruct->put_Stream(pUnk);  
```  
  
 El `adoStr` objeto resultante representa ahora el objeto de **secuencia** de ADO construido a partir del OLE DB objeto **IStream** .  
  
## <a name="requirements"></a>Requisitos  
 **Versión:** ADO 2,0 o una versión posterior  
  
 **Biblioteca:** msado15. dll  
  
 **UUID:** 00000283-0000-0010-8000-00AA006D2EA4  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de la API de ADO](../../../ado/reference/ado-api/ado-api-reference.md)
