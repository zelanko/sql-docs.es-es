---
title: GetString (método) (ADO) | Documentos de Microsoft
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset20::raw_GetString
- Recordset20::GetString
helpviewer_keywords:
- GetString method [ADO]
ms.assetid: 92452940-b2a7-456e-94fc-3780c71da33c
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 373ef70e69d528d41fc2631610a7f31f72c3eec7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="getstring-method-ado"></a>GetString (método) (ADO)
Devuelve el [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) como una cadena.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Variant = recordset.GetString(StringFormat, NumRows, ColumnDelimiter, RowDelimiter, NullExpr)  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve el **Recordset** como un valor de cadena **Variant** (BSTR).  
  
#### <a name="parameters"></a>Parámetros  
 *StringFormat*  
 A [StringFormatEnum](../../../ado/reference/ado-api/stringformatenum.md) valor que especifica cómo la **Recordset** deben convertirse en una cadena. El *RowDelimiter*, *ColumnDelimiter*, y *NullExpr* parámetros sólo se utilizan con un *StringFormat* de  **adClipString**.  
  
 *NumRows*  
 Opcional. El número de filas que se van a convertir el **conjunto de registros**. Si *NumRows* no se especifica, o si es mayor que el número total de filas de la **Recordset**, a continuación, todas las filas de la **conjunto de registros** se convierten.  
  
 *ColumnDelimiter*  
 Opcional. Delimitador que se utiliza entre las columnas, si se especifica, en caso contrario, el carácter de tabulación.  
  
 *rowDelimiter*  
 Opcional. Delimitador que se utiliza entre las filas, si se especifica, en caso contrario, el carácter de retorno de carro.  
  
 *NullExpr*  
 Opcional. Una expresión que se utiliza en lugar de un valor null, si se especifica, en caso contrario, la cadena vacía.  
  
## <a name="remarks"></a>Comentarios  
 Datos de las filas, pero ningún dato de esquema, se guarda en la cadena. Por lo tanto, un **Recordset** no se puede volver a abrirse mediante esta cadena.  
  
 Este método es equivalente a la RDO **GetClipString** método.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo del método GetString (VB)](../../../ado/reference/ado-api/getstring-method-example-vb.md)
