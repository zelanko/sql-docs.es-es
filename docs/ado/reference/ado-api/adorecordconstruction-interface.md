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
ms.openlocfilehash: c56ba0b9d7ebebbf4a9e4baf669bbdc6eb84355e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "67920808"
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
  
## <a name="events"></a>Events  
 Ninguno.  
  
## <a name="remarks"></a>Observaciones  
 Dado un OLE DB objeto **Row** (`pRow`), la construcción de un objeto **Record** de ADO`adoR`() se corresponde con las tres operaciones básicas siguientes:  
  
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
