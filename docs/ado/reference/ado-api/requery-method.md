---
title: Requery (método) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::Requery
- Recordset15::raw_Requery
helpviewer_keywords:
- Requery method [ADO]
ms.assetid: d81ab76f-1aa8-4ccf-92ec-b65254dc3ea1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c3626f91018714fa4d67304c92ce464d82fb5c8e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "67917223"
---
# <a name="requery-method"></a>Requery (método)
Actualiza los datos de un objeto de [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) volviendo a ejecutar la consulta en la que se basa el objeto.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
recordset.Requery Options  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Opciones*  
 Opcional. Máscara de máscara que contiene valores de [ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md) y [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) que afectan a esta operación.  
  
> [!NOTE]
>  Si *Options* se establece en **adAsyncExecute**, esta operación se ejecutará de forma asincrónica y se emitirá un evento [RecordsetChangeComplete](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md) cuando finalice. Los valores **ExecuteOpenEnum** de **adExecuteNoRecords** o **adExecuteStream** no se deben usar con **Requery**.  
  
## <a name="remarks"></a>Observaciones  
 Use el método **Requery** para actualizar todo el contenido de un objeto de **conjunto de registros** desde el origen de datos, para lo que debe volver a emitir el comando original y recuperar los datos por segunda vez. Llamar a este método es equivalente a llamar a los métodos [Close](../../../ado/reference/ado-api/close-method-ado.md) y [Open](../../../ado/reference/ado-api/open-method-ado-recordset.md) en sucesión. Si está editando el registro actual o agregando un nuevo registro, se produce un error.  
  
 Mientras el objeto de **conjunto de registros** está abierto, las propiedades que definen la naturaleza del cursor ([CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md), [LockType](../../../ado/reference/ado-api/locktype-property-ado.md), [MaxRecords](../../../ado/reference/ado-api/maxrecords-property-ado.md), etc.) son de solo lectura. Por lo tanto, el método **Requery** solo puede actualizar el cursor actual. Para cambiar cualquiera de las propiedades del cursor y ver los resultados, debe utilizar el método [Close](../../../ado/reference/ado-api/close-method-ado.md) para que las propiedades se vuelvan a leer y escribir. Después, puede cambiar la configuración de las propiedades y llamar al método [Open](../../../ado/reference/ado-api/open-method-ado-recordset.md) para volver a abrir el cursor.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de los métodos Execute, Requery y Clear (VB)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vb.md)   
 [Ejemplo de métodos Execute, Requery y Clear (VBScript)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vbscript.md)   
 [Ejemplo de los métodos Execute, Requery y Clear (VC + +)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vc.md)   
 [Propiedad CommandText (ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md)
