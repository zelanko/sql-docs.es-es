---
title: Requery (método) | Documentos de Microsoft
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
- Recordset15::Requery
- Recordset15::raw_Requery
helpviewer_keywords:
- Requery method [ADO]
ms.assetid: d81ab76f-1aa8-4ccf-92ec-b65254dc3ea1
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0473cd2c2e8faae5f5ca5805a4cf4e141225f9f9
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2018
ms.locfileid: "35281314"
---
# <a name="requery-method"></a>Requery (método)
Actualiza los datos en un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto volviendo a ejecutar la consulta en el que se basa el objeto.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
recordset.Requery Options  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Opciones*  
 Opcional. Máscara de bits que contiene [ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md) y [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) valores que afectan a esta operación.  
  
> [!NOTE]
>  Si *opciones* está establecido en **adAsyncExecute**, esta operación se ejecutará de forma asincrónica y un [RecordsetChangeComplete](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md) se emitirán los eventos cuando llegue a la conclusión. El **ExecuteOpenEnum** valores de **adExecuteNoRecords** o **adExecuteStream** no debe usarse con **Requery**.  
  
## <a name="remarks"></a>Notas  
 Use la **Requery** método para actualizar todo el contenido de un **Recordset** objeto desde el origen de datos, volver a emitir el comando original y recuperando los datos por segunda vez. Llamar a este método equivale a llamar a la [cerrar](../../../ado/reference/ado-api/close-method-ado.md) y [abiertos](../../../ado/reference/ado-api/open-method-ado-recordset.md) métodos en sucesión. Si está modificando el registro actual o agregando un nuevo registro, se produce un error.  
  
 Mientras el **Recordset** objeto está abierto, las propiedades que definen la naturaleza del cursor ([CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md), [LockType](../../../ado/reference/ado-api/locktype-property-ado.md), [MaxRecords](../../../ado/reference/ado-api/maxrecords-property-ado.md) y así sucesivamente) son de solo lectura. Por lo tanto, la **Requery** método solo puede actualizar el cursor actual. Para cambiar cualquiera de las propiedades de cursor y ver los resultados, debe utilizar el [cerrar](../../../ado/reference/ado-api/close-method-ado.md) método para que las propiedades vuelvan a ser de lectura/escritura. A continuación, puede cambiar la configuración de las propiedades y llamar a la [abiertos](../../../ado/reference/ado-api/open-method-ado-recordset.md) método para volver a abrir el cursor.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Execute, Requery y Clear ejemplo de los métodos (VB)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vb.md)   
 [Execute, Requery y Clear métodos ejemplo (VBScript)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vbscript.md)   
 [Execute, Requery y Clear ejemplo de los métodos (VC ++)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vc.md)   
 [Propiedad CommandText (ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md)
