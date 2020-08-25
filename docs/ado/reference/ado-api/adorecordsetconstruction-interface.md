---
description: Interfaz ADORecordsetConstruction
title: Interfaz ADORecordsetConstruction | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADORecordsetConstruction
helpviewer_keywords:
- ADORecordsetConstruction interface [ADO]
ms.assetid: 08386eba-f1f7-4879-8ffd-8733930ecb2f
author: rothja
ms.author: jroth
ms.openlocfilehash: c17ccfe0a31714d5e2b3945960a4ff3d2ad55d1e
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/24/2020
ms.locfileid: "88776644"
---
# <a name="adorecordsetconstruction-interface"></a>Interfaz ADORecordsetConstruction
La interfaz **ADORecordsetConstruction** se utiliza para construir un objeto de **conjunto de registros** ADO a partir de un objeto de conjunto de **filas** OLE DB en una aplicación de C/C++.  
  
 Esta interfaz admite las siguientes propiedades:  
  
## <a name="properties"></a>Propiedades  
  
|Propiedad|Descripción|  
|-|-|  
|[Capítulo](./chapter-property-ado.md)|Lectura y escritura.<br />Obtiene o establece un OLE DB objeto **Chapter** en este objeto **Recordset** de ADO.|  
|[RowPosition](./rowposition-property-ado.md)|Lectura y escritura.<br />Obtiene o establece un objeto **RowPosition** OLE DB a partir de este objeto de **conjunto de registros** de ADO.|  
|[Conjunto de filas](./rowset-property-ado.md)|Lectura y escritura.<br />Obtiene o establece un objeto de **conjunto de filas** de OLE DB de este objeto de conjunto de **registros** de ADO.|  
  
## <a name="methods"></a>Métodos  
 Ninguno.  
  
## <a name="events"></a>Eventos  
 Ninguno.  
  
## <a name="remarks"></a>Observaciones  
 Dado un OLE DB objeto de **conjunto de filas** ( `pRowset` ), la construcción de un objeto de **conjunto de registros** ADO ( `adoRs` ) se suma a las tres operaciones básicas siguientes:  
  
1.  Cree un objeto de **conjunto de registros** ADO:  
  
    ```  
    Recordset20Ptr adoRs;  
    adoRs.CreateInstance(__uuidof(Recordset));  
    ```  
  
2.  Consulte la interfaz **IADORecordsetConstruction** en el objeto de **conjunto de registros** :  
  
    ```  
    adoRecordsetConstructionPtr adoRsConstruct=NULL;  
    adoRs->QueryInterface(__uuidof(ADORecordsetConstruction),  
                         (void**)&adoRsConstruct);  
    ```  
  
3.  Llame al `IADORecordsetConstruction::put_Rowset` método de propiedad para establecer el `Rowset` objeto de OLE DB en el `Recordset` objeto ADO:  
  
    ```  
    IUnknown *pUnk=NULL;  
    pRowset->QueryInterface(IID_IUnknown, (void**)&pUnk);  
    adoRsConstruct->put_Rowset(pUnk);  
    ```  
  
 El objeto resultante `adoRs` representa ahora el objeto de **conjunto de registros** ADO construido a partir del objeto de **conjunto de filas** OLE DB.  
  
 También puede crear un objeto de **conjunto de registros** ADO a partir de un OLE DB **capítulo** o un objeto **RowPosition** .  
  
## <a name="requirements"></a>Requisitos  
 **Versión:** ADO 2,0 y versiones posteriores  
  
 **Biblioteca:** msado15.dll  
  
 **UUID:** 00000283-0000-0010-8000-00AA006D2EA4  
  
## <a name="see-also"></a>Consulte también  
 [Objeto de conjunto de registros (ADO)](./recordset-object-ado.md)   
 [Propiedad Rowset (ADO)](./rowset-property-ado.md)