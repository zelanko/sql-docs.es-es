---
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
ms.openlocfilehash: 23ee532329e8104d3a0e02c9547d9ca7813b42a2
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/28/2020
ms.locfileid: "87242825"
---
# <a name="adorecordsetconstruction-interface"></a>Interfaz ADORecordsetConstruction
La interfaz **ADORecordsetConstruction** se utiliza para construir un objeto de **conjunto de registros** ADO a partir de un objeto de conjunto de **filas** OLE DB en una aplicación de C/C++.  
  
 Esta interfaz admite las siguientes propiedades:  
  
## <a name="properties"></a>Propiedades  
  
|Propiedad|Descripción|  
|-|-|  
|[Capítulo](../../../ado/reference/ado-api/chapter-property-ado.md)|Lectura y escritura.<br />Obtiene o establece un OLE DB objeto **Chapter** en este objeto **Recordset** de ADO.|  
|[RowPosition](../../../ado/reference/ado-api/rowposition-property-ado.md)|Lectura y escritura.<br />Obtiene o establece un objeto **RowPosition** OLE DB a partir de este objeto de **conjunto de registros** de ADO.|  
|[Conjunto de filas](../../../ado/reference/ado-api/rowset-property-ado.md)|Lectura y escritura.<br />Obtiene o establece un objeto de **conjunto de filas** de OLE DB de este objeto de conjunto de **registros** de ADO.|  
  
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
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Propiedad Rowset (ADO)](../../../ado/reference/ado-api/rowset-property-ado.md)
