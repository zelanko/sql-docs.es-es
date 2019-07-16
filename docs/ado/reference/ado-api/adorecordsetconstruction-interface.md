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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1e1d14255acd4cc7f18abea1c494353ef970903c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67920793"
---
# <a name="adorecordsetconstruction-interface"></a>Interfaz ADORecordsetConstruction
El **ADORecordsetConstruction** interfaz se usa para construir un ADO **Recordset** objeto de OLE DB **conjunto de filas** objeto en una aplicación de C o C++.  
  
 Esta interfaz admite las siguientes propiedades:  
  
## <a name="properties"></a>Propiedades  
  
|||  
|-|-|  
|[Capítulo](../../../ado/reference/ado-api/chapter-property-ado.md)|Lectura/escritura.<br />Obtiene o establece OLE DB **capítulo** objeto desde/en este ADO **Recordset** objeto.|  
|[RowPosition](../../../ado/reference/ado-api/rowposition-property-ado.md)|Lectura/escritura.<br />Obtiene o establece OLE DB **RowPosition** objeto desde/en este ADO **Recordset** objeto.|  
|[Rowset](../../../ado/reference/ado-api/rowset-property-ado.md)|Lectura/escritura.<br />Obtiene o establece OLE DB **conjunto de filas** objeto desde/en este ADO **Recordset** objeto.|  
  
## <a name="methods"></a>Métodos  
 Ninguno.  
  
## <a name="events"></a>Events  
 Ninguno.  
  
## <a name="remarks"></a>Comentarios  
 Dado de OLE DB **conjunto de filas** objeto (`pRowset`), la construcción de ADO **Recordset** objeto (`adoRs`) equivale a las tres operaciones básicas siguientes:  
  
1.  Crear un ADO **Recordset** objeto:  
  
    ```  
    Recordset20Ptr adoRs;  
    adoRs.CreateInstance(__uuidof(Recordset));  
    ```  
  
2.  Consulta el **IADORecordsetConstruction** interfaz en el **Recordset** objeto:  
  
    ```  
    adoRecordsetConstructionPtr adoRsConstruct=NULL;  
    adoRs->QueryInterface(__uuidof(ADORecordsetConstruction),  
                         (void**)&adoRsConstruct);  
    ```  
  
3.  Llame a la `IADORecordsetConstruction::put_Rowset` método de propiedad para establecer la OLE DB `Rowset` objeto ADO `Recordset` objeto:  
  
    ```  
    IUnknown *pUnk=NULL;  
    pRowset->QueryInterface(IID_IUnknown, (void**)&pUnk);  
    adoRsConstruct->put_Rowset(pUnk);  
    ```  
  
 El resultante `adoRs` ahora representa el objeto ADO **Recordset** objeto construido a partir de OLE DB **conjunto de filas** objeto.  
  
 También se puede construir un ADO **Recordset** objeto de OLE DB **capítulo** o **RowPosition** objeto.  
  
## <a name="requirements"></a>Requisitos  
 **Versión:** ADO 2.0 y versiones posterior  
  
 **Biblioteca:** msado15.dll  
  
 **UUID:** 00000283-0000-0010-8000-00AA006D2EA4  
  
## <a name="see-also"></a>Vea también  
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Propiedad Rowset (ADO)](../../../ado/reference/ado-api/rowset-property-ado.md)
