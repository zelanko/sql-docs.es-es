---
title: Origen (propiedad, ADO Recordset) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::putref_Source
- Recordset15::Source
- Recordset15::PutSource
- Recordset15::get_Source
- Recordset15::GetSource
- Recordset15::PutRefSource
- Recordset15::put_Source
helpviewer_keywords:
- Source property [ADO Recordset]
ms.assetid: a05ba2c9-2821-4343-8607-4de9b764ec91
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 718124fce3c2ce7a1adf9e6dbdb1d54e8a834fca
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47655613"
---
# <a name="source-property-ado-recordset"></a>Propiedad Source (ADO Recordset)
Indica el origen de datos para un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Conjuntos de un **cadena** valor o [comando](../../../ado/reference/ado-api/command-object-ado.md) objeto de referencia; sólo devuelve un **cadena** valor que indica el origen de la **Recordset**.  
  
## <a name="remarks"></a>Comentarios  
 Use la **origen** propiedad para especificar un origen de datos para un **Recordset** objeto utilizando uno de los siguientes: un **comando** objeto variable, una instrucción SQL, un procedimiento almacenado, o un nombre de tabla.  
  
 Si establece la **origen** propiedad a un **comando** objeto, el [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) propiedad de la **Recordset** objeto heredará el valor de la **ActiveConnection** propiedad para el elemento especificado **comando** objeto. Sin embargo, leer el **origen** propiedad no devuelve un **comando** objeto; en su lugar, devuelve el [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) propiedad de la **comando** objeto al que se establecen los **origen** propiedad.  
  
 Si el **origen** propiedad es una instrucción SQL, un procedimiento almacenado o un nombre de tabla, puede optimizar el rendimiento pasando adecuado *opciones* argumento con el [abrir](../../../ado/reference/ado-api/open-method-ado-recordset.md)llamada al método.  
  
 El **origen** propiedad es de lectura/escritura de cerrará **Recordset** objetos y de solo lectura para abrir **Recordset** objetos.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de la propiedad de origen (VB)](../../../ado/reference/ado-api/source-property-example-vb.md)   
 [Propiedad Source (Error de ADO)](../../../ado/reference/ado-api/source-property-ado-error.md)   
 [Propiedad Source (Record ADO)](../../../ado/reference/ado-api/source-property-ado-record.md)
