---
title: BeginTrans, CommitTrans y RollbackTrans métodos (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::raw_RollbackTrans
- Connection15::CommitTrans
- Connection15::raw_CommitTrans
- Connection15::raw_BeginTrans
- Connection15::BeginTrans
- Connection15::RollbackTrans
helpviewer_keywords:
- BeginTrans method [ADO]
- CommitTrans method [ADO]
- RollbackTrans method [ADO]
ms.assetid: d4683472-4120-4236-8640-fa9ae289e23e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7c796cefc03092e944520a6517bc31c585a2dc42
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47613893"
---
# <a name="begintrans-committrans-and-rollbacktrans-methods-ado"></a>Métodos BeginTrans, CommitTrans y RollbackTrans (ADO)
Estos métodos de transacción administran el procesamiento de transacciones en un [conexión](../../../ado/reference/ado-api/connection-object-ado.md) objeto como sigue:  
  
-   **BeginTrans** inicia una transacción nueva.  
  
-   **CommitTrans** guarda los cambios y finaliza la transacción actual. También puede iniciar una nueva transacción.  
  
-   **RollbackTrans** cancela los cambios realizados durante la transacción actual y termina la transacción. También puede iniciar una nueva transacción.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
level = object.BeginTrans()  
object.BeginTrans  
object.CommitTrans  
object.RollbackTrans  
```  
  
## <a name="return-value"></a>Valor devuelto  
 **BeginTrans** se pueden llamar como una función que devuelve un **largo** variable que indica el nivel de anidamiento de la transacción.  
  
#### <a name="parameters"></a>Parámetros  
 *object*  
 Un **conexión** objeto.  
  
## <a name="connection"></a>Conexión  
 Utilice estos métodos con un **conexión** objeto cuando desea guardar o cancelar una serie de cambios realizados en los datos de origen como una sola unidad. Por ejemplo, para transferir dinero entre cuentas, resta una cantidad de uno y agregue la misma cantidad a las demás. Si se produce un error, actualice las cuentas ya no están equilibradas. Realizar estos cambios en una transacción abierta, se garantiza que todos o ninguno de los cambios se pasen a través.  
  
> [!NOTE]
>  No todos los proveedores admiten transacciones. Compruebe que la propiedad definida por el proveedor "**DDL de transacción**" aparece en el **conexión** del objeto [propiedades](../../../ado/reference/ado-api/properties-collection-ado.md) colección, que indica que el proveedor admite transacciones. Si el proveedor no admite transacciones, al llamar a uno de estos métodos, devolverá un error.  
  
 Después de llamar a la **BeginTrans** método, el proveedor ya no confirmará instantáneamente los cambios hasta que llame a **CommitTrans** o **RollbackTrans** para finalizar el transacción.  
  
 Para los proveedores que admiten transacciones anidadas, llamar a la **BeginTrans** método dentro de una transacción abierta inicia una nueva transacción anidada. El valor devuelto indica el nivel de anidamiento: un valor devuelto de "1" indica que ha abierto una transacción de nivel superior (es decir, la transacción no está anidada dentro de otra transacción), "2" indica que ha abierto una transacción de segundo nivel (una transacción anidada dentro de una transacción de nivel superior), y así sucesivamente. Una llamada a **CommitTrans** o **RollbackTrans** afecta solo al máximo abierto recientemente la transacción; debe cerrar o revertir la transacción actual antes de resolver las transacciones de nivel superior.  
  
 Una llamada a la **CommitTrans** método guarda los cambios realizados en una transacción abierta en la conexión y finaliza la transacción. Una llamada a la **RollbackTrans** método invierte los cambios realizados en una transacción abierta y finaliza la transacción. Al llamar a cualquiera de estos métodos cuando no hay ninguna transacción abierta, genera un error.  
  
 En función de la **conexión** del objeto [atributos](../../../ado/reference/ado-api/attributes-property-ado.md) propiedad, al llamar a la **CommitTrans** o **RollbackTrans** puede que los métodos iniciar automáticamente una nueva transacción. Si el **atributos** propiedad está establecida en **adXactCommitRetaining**, el proveedor inicia automáticamente una nueva transacción después de un **CommitTrans** llamar. Si el **atributos** propiedad está establecida en **adXactAbortRetaining**, el proveedor inicia automáticamente una nueva transacción después de un **RollbackTrans** llamar.  
  
## <a name="remote-data-service"></a>Servicio de datos remotos  
 El **BeginTrans**, **CommitTrans**, y **RollbackTrans** métodos no están disponibles en un cliente **conexión** objeto.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conexión (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [BeginTrans, CommitTrans y ejemplo de los métodos RollbackTrans (VB)](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-example-vb.md)   
 [BeginTrans, CommitTrans y ejemplo de los métodos RollbackTrans (VC ++)](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-example-vc.md)   
 [Propiedad Attributes (ADO)](../../../ado/reference/ado-api/attributes-property-ado.md)
