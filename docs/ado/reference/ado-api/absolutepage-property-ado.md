---
title: Propiedad AbsolutePage (ADO) | Documentos de Microsoft
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::AbsolutePage
helpviewer_keywords:
- AbsolutePage property [ADO]
ms.assetid: ddb58a35-ec3a-423c-a504-3c65e62c23d4
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4bd0696e18e7719038a1b87448477b1b7f4d5bdf
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2018
ms.locfileid: "35274854"
---
# <a name="absolutepage-property-ado"></a>Propiedad AbsolutePage (ADO)
Indica en qué página reside el registro actual.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Para el código de 32 bits, Establece o devuelve un **largo** valor entre 1 y el número de páginas en el [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto ([PageCount](../../../ado/reference/ado-api/pagecount-property-ado.md)), o devuelve uno de los [PositionEnum ](../../../ado/reference/ado-api/positionenum.md) valores.  
  
 Para código de 64 bits, use un tipo de datos que proporciona para el almacenamiento de un valor de 64 bits. Por ejemplo, puede utilizar cualquiera **largo** o cualquier otro valor que puede ser de longitud de 64 bits como DBORDINAL. No utilice **PositionEnum** valores porque se limitan a la longitud de 32 bits.  
  
## <a name="remarks"></a>Notas  
 Esta propiedad puede utilizarse para identificar el número de página en el que se encuentra el registro actual. Usa el [PageSize](../../../ado/reference/ado-api/pagesize-property-ado.md) propiedad que se va a dividir lógicamente el número total de filas de la **Recordset** objeto en una serie de páginas, cada uno de los cuales tiene el número de registros equivalente a **PageSize** (excepto la última página, que puede tener menos registros). El proveedor debe admitir la funcionalidad adecuada para que esta propiedad esté disponible.  
  
-   Al obtener o establecer el **AbsolutePage** propiedad, ADO utiliza la [AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md) propiedad y el [PageSize](../../../ado/reference/ado-api/pagesize-property-ado.md) propiedad juntos, como se indica a continuación:  
  
-   Para obtener la **AbsolutePage**, ADO recupera primero el **AbsolutePosition**y, a continuación, lo divide por el **PageSize**.  
  
-   Para establecer el **AbsolutePage**, ADO mueve el **AbsolutePosition** como se indica a continuación: se multiplican los **PageSize** mediante la nueva **AbsolutePage** valor y, a continuación, se suma 1 al valor. Como resultado, la posición actual en el **Recordset** después de establecer correctamente **AbsolutePage** es el primer registro de esa página.  
  
 Al igual que el **AbsolutePosition** propiedad, **AbsolutePage** está basado en 1 y es igual a 1 cuando el registro actual es el primer registro de la **conjunto de registros**. Establezca esta propiedad para desplazarse al primer registro de una página determinada. Obtener el número total de páginas de la **PageCount** propiedad.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [AbsolutePage, PageCount y ejemplo de las propiedades PageSize (VB)](../../../ado/reference/ado-api/absolutepage-pagecount-and-pagesize-properties-example-vb.md)   
 [AbsolutePage, PageCount y ejemplo de las propiedades PageSize (VC ++)](../../../ado/reference/ado-api/absolutepage-pagecount-and-pagesize-properties-example-vc.md)   
 [Propiedad AbsolutePosition (ADO)](../../../ado/reference/ado-api/absoluteposition-property-ado.md)   
 [PageCount (propiedad, ADO)](../../../ado/reference/ado-api/pagecount-property-ado.md)   
 [Propiedad PageSize (ADO)](../../../ado/reference/ado-api/pagesize-property-ado.md)
