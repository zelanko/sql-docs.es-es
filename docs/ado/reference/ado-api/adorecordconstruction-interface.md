---
title: Interfaz ADORecordConstruction | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADORecordConstruction
helpviewer_keywords:
- ADORecordConstruction interface [ADO]
ms.assetid: 52a5429e-5829-455e-be3b-31f05cbecf2d
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 925eefdbe8f5ff9196689026edb685c8f76d7d0a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66718169"
---
# <a name="adorecordconstruction-interface"></a>Interfaz ADORecordConstruction
El **ADORecordConstruction**interfaz se usa para construir un ADO **registro** objeto de OLE DB **fila** objeto en una aplicación de C o C++.  
  
 Esta interfaz admite las siguientes propiedades:  
  
## <a name="properties"></a>Propiedades  
  
|||  
|-|-|  
|[ParentRow](../../../ado/reference/ado-api/parentrow-property-ado.md)|De solo escritura.<br />Establece el contenedor de OLE DB **fila** objeto este ADO **registro** objeto.|  
|[Fila](../../../ado/reference/ado-api/row-property-ado.md)|Lectura/escritura.<br />Obtiene o establece OLE DB **fila** objeto desde/en este ADO **registro** objeto.|  
  
## <a name="methods"></a>Métodos  
 Ninguno.  
  
## <a name="events"></a>Events  
 Ninguno.  
  
## <a name="remarks"></a>Comentarios  
 Dada una OLE DB **fila** objeto (`pRow`), la construcción de ADO **registro** objeto (`adoR`), equivale a las tres operaciones básicas siguientes:  
  
1.  Crear un ADO **registro** objeto:  
  
    ```  
    _RecordPtr adoR;  
    adoRs.CreateInstance(__uuidof(_Record));  
    ```  
  
2.  Consulta el **IADORecordConstruction** interfaz en el **registro** objeto:  
  
    ```  
    adoRecordConstructionPtr adoRConstruct=NULL;  
    adoR->QueryInterface(__uuidof(ADORecordConstruction),  
                        (void**)&adoRConstruct);  
    ```  
  
3.  Llame a la **IADORecordConstruction:: put Row** método de propiedad para establecer la OLE DB **fila** objeto ADO **registro** objeto:  
  
    ```  
    IUnknown *pUnk=NULL;  
    pRow->QueryInterface(IID_IUnknown, (void**)&pUnk);  
    adoRConstruct->put_Row(pUnk);  
    ```  
  
 El resultante **adoR** ahora representa el objeto ADO **registro** objeto construido a partir de OLE DB **fila** objeto.  
  
 ADO **registro** también se puede construir el objeto desde el contenedor de OLE DB **fila** objeto.  
  
## <a name="requirements"></a>Requisitos  
 **Versión:** ADO 2.0 y versiones posterior  
  
 **Library:** msado15.dll  
  
 **UUID:** 00000567-0000-0010-8000-00AA006D2EA4
