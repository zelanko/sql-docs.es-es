---
description: Interfaz ADORecordConstruction
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
ms.openlocfilehash: f93370ae23cd50e1fb494d484756505f69514df1
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/24/2020
ms.locfileid: "88776613"
---
# <a name="adorecordconstruction-interface"></a>Interfaz ADORecordConstruction
La interfaz **ADORecordConstruction**se utiliza para construir un objeto **Record** de ADO a partir de un objeto de **fila** OLE DB en una aplicación de C/C++.  
  
 Esta interfaz admite las siguientes propiedades:  
  
## <a name="properties"></a>Propiedades  
  
|Propiedad|Descripción|  
|-|-|  
|[ParentRow](./parentrow-property-ado.md)|De solo escritura.<br />Establece el contenedor de un objeto de **fila** OLE DB en este objeto **Record** de ADO.|  
|[Columna](./row-property-ado.md)|Lectura y escritura.<br />Obtiene o establece un objeto de **fila** OLE DB de/en este objeto **Record** de ADO.|  
  
## <a name="methods"></a>Métodos  
 Ninguno.  
  
## <a name="events"></a>Eventos  
 Ninguno.  
  
## <a name="remarks"></a>Observaciones  
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
  
 **Biblioteca:** msado15.dll  
  
 **UUID:** 00000567-0000-0010-8000-00AA006D2EA4