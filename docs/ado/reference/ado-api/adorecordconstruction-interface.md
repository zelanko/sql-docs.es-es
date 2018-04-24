---
title: Interfaz ADORecordConstruction | Documentos de Microsoft
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
- ADORecordConstruction
helpviewer_keywords:
- ADORecordConstruction interface [ADO]
ms.assetid: 52a5429e-5829-455e-be3b-31f05cbecf2d
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 079bc873b78a40248d60c36e994750d4c95c076d
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2018
---
# <a name="adorecordconstruction-interface"></a>Interfaz ADORecordConstruction
El **ADORecordConstruction**interfaz se usa para construir un ADO **registro** objeto de OLE DB **fila** objeto en una aplicación de C o C++.  
  
 Esta interfaz es compatible con las siguientes propiedades:  
  
## <a name="properties"></a>Propiedades  
  
|||  
|-|-|  
|[ParentRow](../../../ado/reference/ado-api/parentrow-property-ado.md)|De solo escritura.<br />Establece el contenedor de OLE DB **fila** objeto en este ADO **registro** objeto.|  
|[Fila](../../../ado/reference/ado-api/row-property-ado.md)|Lectura/escritura.<br />Obtiene o establece OLE DB **fila** objeto de/en este ADO **registro** objeto.|  
  
## <a name="methods"></a>Métodos  
 Ninguno.  
  
## <a name="events"></a>Eventos  
 Ninguno.  
  
## <a name="remarks"></a>Comentarios  
 Dado OLE DB **fila** objeto (`pRow`), la construcción de ADO **registro** objeto (`adoR`), los importes de las tres operaciones básicas siguientes:  
  
1.  Crear un ADO **registro** objeto:  
  
    ```  
    _RecordPtr adoR;  
    adoRs.CreateInstance(__uuidof(_Record));  
    ```  
  
2.  Consulta el **IADORecordConstruction** de la interfaz en el **registro** objeto:  
  
    ```  
    adoRecordConstructionPtr adoRConstruct=NULL;  
    adoR->QueryInterface(__uuidof(ADORecordConstruction),  
                        (void**)&adoRConstruct);  
    ```  
  
3.  Llame a la **IADORecordConstruction:: put Row** método de propiedad para establecer OLE DB **fila** objeto ADO **registro** objeto:  
  
    ```  
    IUnknown *pUnk=NULL;  
    pRow->QueryInterface(IID_IUnknown, (void**)&pUnk);  
    adoRConstruct->put_Row(pUnk);  
    ```  
  
 El resultante **adoR** ahora representa el objeto ADO **registro** objeto construido a partir de OLE DB **fila** objeto.  
  
 ADO **registro** también se puede construir el objeto desde el contenedor de OLE DB **fila** objeto.  
  
## <a name="requirements"></a>Requisitos  
 **Versión:** ADO 2.0 y versiones posteriores  
  
 **Biblioteca:** msado15.dll  
  
 **UUID:** 00000567-0000-0010-8000-00AA006D2EA4
