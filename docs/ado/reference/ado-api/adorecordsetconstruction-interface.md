---
title: Interfaz ADORecordsetConstruction | Documentos de Microsoft
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
f1_keywords:
- ADORecordsetConstruction
helpviewer_keywords:
- ADORecordsetConstruction interface [ADO]
ms.assetid: 08386eba-f1f7-4879-8ffd-8733930ecb2f
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 3da6260d5e0d4e503dae54e6ffc13f6d35f1890d
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="adorecordsetconstruction-interface"></a>Interfaz ADORecordsetConstruction
El **ADORecordsetConstruction** interfaz se usa para construir un ADO **Recordset** objeto de OLE DB **conjunto de filas** objeto en una aplicación de C o C++.  
  
 Esta interfaz es compatible con las siguientes propiedades:  
  
## <a name="properties"></a>Propiedades  
  
|||  
|-|-|  
|[Capítulo](../../../ado/reference/ado-api/chapter-property-ado.md)|Lectura/escritura.<br />Obtiene o establece OLE DB **capítulo** objeto de/en este ADO **Recordset** objeto.|  
|[RowPosition](../../../ado/reference/ado-api/rowposition-property-ado.md)|Lectura/escritura.<br />Obtiene o establece OLE DB **RowPosition** objeto de/en este ADO **Recordset** objeto.|  
|[Conjunto de filas](../../../ado/reference/ado-api/rowset-property-ado.md)|Lectura/escritura.<br />Obtiene o establece OLE DB **conjunto de filas** objeto de/en este ADO **Recordset** objeto.|  
  
## <a name="methods"></a>Métodos  
 Ninguno.  
  
## <a name="events"></a>Eventos  
 Ninguno.  
  
## <a name="remarks"></a>Comentarios  
 Dado de OLE DB **conjunto de filas** objeto (`pRowset`), la construcción de ADO **Recordset** objeto (`adoRs`) equivale a las tres operaciones básicas siguientes:  
  
1.  Crear un ADO **Recordset** objeto:  
  
    ```  
    Recordset20Ptr adoRs;  
    adoRs.CreateInstance(__uuidof(Recordset));  
    ```  
  
2.  Consulta el **IADORecordsetConstruction** de la interfaz en el **Recordset** objeto:  
  
    ```  
    adoRecordsetConstructionPtr adoRsConstruct=NULL;  
    adoRs->QueryInterface(__uuidof(ADORecordsetConstruction),  
                         (void**)&adoRsConstruct);  
    ```  
  
3.  Llame a la `IADORecordsetConstruction::put_Rowset` método de propiedad para establecer OLE DB `Rowset` objeto ADO `Recordset` objeto:  
  
    ```  
    IUnknown *pUnk=NULL;  
    pRowset->QueryInterface(IID_IUnknown, (void**)&pUnk);  
    adoRsConstruct->put_Rowset(pUnk);  
    ```  
  
 El resultante `adoRs` ahora representa el objeto ADO **Recordset** objeto construido a partir de OLE DB **conjunto de filas** objeto.  
  
 También se puede construir un ADO **Recordset** objeto de OLE DB **capítulo** o **RowPosition** objeto.  
  
## <a name="requirements"></a>Requisitos  
 **Versión:** ADO 2.0 y versiones posteriores  
  
 **Biblioteca:** msado15.dll  
  
 **UUID:** 00000283-0000-0010-8000-00AA006D2EA4  
  
## <a name="see-also"></a>Vea también  
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Propiedad de conjunto de filas (ADO)](../../../ado/reference/ado-api/rowset-property-ado.md)

