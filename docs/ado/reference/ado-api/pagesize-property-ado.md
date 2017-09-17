---
title: Propiedad PageSize (ADO) | Documentos de Microsoft
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
- Recordset15::PageSize
helpviewer_keywords:
- PageSize property [ADO]
ms.assetid: e57930a6-46c4-4a17-a3b6-f79e94d5c9c7
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: fde7e53b844ece01f85b7ecba7e309a71107029d
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="pagesize-property-ado"></a>Propiedad PageSize (ADO)
Indica cuántos registros constituyen una página en el [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un **largo** valor que indica el número de registros que se encuentra en una página. El valor predeterminado es **10**.  
  
## <a name="remarks"></a>Comentarios  
 Use la **PageSize** propiedad para determinar cuántos registros componen una página lógica de datos. Establecer un tamaño de página le permite usar la [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md) propiedad para desplazarse al primer registro de una página determinada. Esto es útil en escenarios de servidor Web cuando desea permitir al usuario desplazarse por los datos, ve un cierto número de registros a la vez.  
  
 Esta propiedad puede establecerse en cualquier momento y su valor se usará para calcular la ubicación del primer registro de una página determinada.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [AbsolutePage, PageCount y ejemplo de las propiedades PageSize (VB)](../../../ado/reference/ado-api/absolutepage-pagecount-and-pagesize-properties-example-vb.md)   
 [AbsolutePage, PageCount y ejemplo de las propiedades PageSize (VC ++)](../../../ado/reference/ado-api/absolutepage-pagecount-and-pagesize-properties-example-vc.md)   
 [Propiedad AbsolutePage (ADO)](../../../ado/reference/ado-api/absolutepage-property-ado.md)   
 [PageCount (propiedad, ADO)](../../../ado/reference/ado-api/pagecount-property-ado.md)

