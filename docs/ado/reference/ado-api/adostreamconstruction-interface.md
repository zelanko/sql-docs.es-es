---
title: Interfaz ADOStreamConstruction | Documentos de Microsoft
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADOStreamConstruction
helpviewer_keywords:
- ADOStreamConstruction interface [ADO]
ms.assetid: 92f5a939-3e1a-4b14-a9dd-90e6ce2dec74
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 693ccde4f48d5c358f65b83654d137745f97acff
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="adostreamconstruction-interface"></a>Interfaz ADOStreamConstruction
El **ADOStreamConstruction** interfaz se usa para construir un ADO **flujo** objeto de OLE DB **IStream** objeto en una aplicación de C o C++.  
  
## <a name="properties"></a>Propiedades  
  
|||  
|-|-|  
|[Propiedad de la secuencia](../../../ado/reference/ado-api/stream-property.md)|Lectura/escritura. Obtiene o establece OLE DB **flujo** objeto.|  
  
## <a name="methods"></a>Métodos  
 Ninguno.  
  
## <a name="events"></a>Eventos  
 Ninguno.  
  
## <a name="remarks"></a>Comentarios  
 Dado de OLE DB **IStream** objeto (`pStream`), la construcción de ADO **flujo** objeto (`adoStr`) equivale a las tres operaciones básicas siguientes:  
  
1.  Crear un ADO **flujo** objeto:  
  
    ```  
    Stream20Ptr adoStr;  
    adoStr.CreateInstance(__uuidof(Stream));  
    ```  
  
2.  Consulta el **IADOStreamConstruction** de la interfaz en el **flujo** objeto:  
  
    ```  
    adoStreamConstructionPtr adoStrConstruct=NULL;  
    adoStr->QueryInterface(__uuidof(ADOStreamConstruction),  
                         (void**)&adoStrConstruct);  
    ```  
  
 Llame a la `IADOStreamConstruction::get_Stream` método de propiedad para establecer OLE DB **IStream** objeto ADO **flujo** objeto:  
  
```  
IUnknown *pUnk=NULL;  
pRowset->QueryInterface(IID_IUnknown, (void**)&pUnk);  
adoStrConstruct->put_Stream(pUnk);  
```  
  
 El resultante `adoStr` ahora representa el objeto ADO **flujo** objeto construido a partir de OLE DB **IStream** objeto.  
  
## <a name="requirements"></a>Requisitos  
 **Versión:** ADO 2.0 o una versión posterior  
  
 **Biblioteca:** msado15.dll  
  
 **UUID:** 00000283-0000-0010-8000-00AA006D2EA4  
  
## <a name="see-also"></a>Vea también  
 [Referencia de la API de ADO](../../../ado/reference/ado-api/ado-api-reference.md)
