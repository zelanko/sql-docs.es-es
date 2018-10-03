---
title: GetString (método) (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset20::raw_GetString
- Recordset20::GetString
helpviewer_keywords:
- GetString method [ADO]
ms.assetid: 92452940-b2a7-456e-94fc-3780c71da33c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1570918c423291b6c4fdd212fcb82f518dfb766e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47708063"
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
 Un [StringFormatEnum](../../../ado/reference/ado-api/stringformatenum.md) valor que especifica cómo el **Recordset** deben convertirse en una cadena. El *RowDelimiter*, *ColumnDelimiter*, y *NullExpr* parámetros se usan solo con un *StringFormat* de  **adClipString**.  
  
 *NumRows*  
 Opcional. El número de filas que se van a convertir el **Recordset**. Si *NumRows* no se especifica, o si es mayor que el número total de filas de la **Recordset**, a continuación, todas las filas de la **Recordset** se convierten.  
  
 *ColumnDelimiter*  
 Opcional. Un delimitador utilizado entre columnas, si se especifica, en caso contrario, el carácter de tabulación.  
  
 *RowDelimiter*  
 Opcional. Un delimitador utilizado entre las filas, si se especifica, en caso contrario, el carácter de retorno de carro.  
  
 *NullExpr*  
 Opcional. Una expresión que se utiliza en lugar de un valor null, si se especifica, en caso contrario, una cadena vacía.  
  
## <a name="remarks"></a>Comentarios  
 Datos de fila, pero no hay datos de esquema, se guarda en la cadena. Por lo tanto, un **Recordset** no se puede abrir con esta cadena.  
  
 Este método es equivalente a la RDO **GetClipString** método.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo del método GetString (VB)](../../../ado/reference/ado-api/getstring-method-example-vb.md)
