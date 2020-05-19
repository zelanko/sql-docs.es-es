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
author: rothja
ms.author: jroth
ms.openlocfilehash: 12a9b2cae1c516ed3bf8caef8127034e6ff2a847
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2020
ms.locfileid: "82747174"
---
# <a name="adorecordconstruction-interface"></a>Interfaz ADORecordConstruction
La interfaz **ADORecordConstruction**se utiliza para construir un objeto **Record** de ADO a partir de un objeto de **fila** OLE DB en una aplicación de C/C++.  
  
 Esta interfaz admite las siguientes propiedades:  
  
## <a name="properties"></a>Propiedades  
  
|||  
|-|-|  
|[ParentRow](../../../ado/reference/ado-api/parentrow-property-ado.md)|De solo escritura.<br />Establece el contenedor de un objeto de **fila** OLE DB en este objeto **Record** de ADO.|  
|[Columna](../../../ado/reference/ado-api/row-property-ado.md)|Lectura y escritura.<br />Obtiene o establece un objeto de **fila** OLE DB de/en este objeto **Record** de ADO.|  
  
## <a name="methods"></a>Métodos  
 Ninguno.  
  
## <a name="events"></a>Eventos  
 Ninguno.  
  
## <a name="remarks"></a>Comentarios  
 Dado un OLE DB objeto **Row** ( `pRow` ), la construcción de un objeto **Record** de ADO ( `adoR` ) se corresponde con las tres operaciones básicas siguientes:  
  
1.  Cree un objeto de **registro** de ADO:  
  
    ```  
    _RecordPtr adoR;  
    adoRs.CreateInstance(__uuidof(_Record));  
    ```  
  
2.  Consulte la interfaz **IADORecordConstruction** en el objeto de **registro** :  
  
    ```  
    adoRecordConstructionPtr adoRConstruct=NULL;  
    adoR->QueryInterface(__uuidof(ADORecordConstruction),  
                        (void**)&adoRConstruct);  
    ```  
  
3.  Llame al método de propiedad **IADORecordConstruction::p ut_Row** para establecer el objeto de **fila** OLE DB en el objeto de **registro** de ADO:  
  
    ```  
    IUnknown *pUnk=NULL;  
    pRow->QueryInterface(IID_IUnknown, (void**)&pUnk);  
    adoRConstruct->put_Row(pUnk);  
    ```  
  
 El objeto **adoR** resultante representa ahora el objeto de **registro** de ADO construido a partir del objeto de **fila** OLE DB.  
  
 También se puede crear un objeto **Record** de ADO a partir del contenedor de un objeto de **fila** OLE DB.  
  
## <a name="requirements"></a>Requisitos  
 **Versión:** ADO 2,0 y versiones posteriores  
  
 **Biblioteca:** msado15. dll  
  
 **UUID:** 00000567-0000-0010-8000-00AA006D2EA4
