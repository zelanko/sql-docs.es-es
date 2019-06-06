---
title: Procesamiento de transacciones | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- transactions [ADO]
- data updates [ADO], transaction processing
- updating data [ADO], transaction processing
- nested transactions [ADO]
ms.assetid: 74ab6706-e2dc-42cb-af77-dbc58a9cf4ce
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 032677452fa80502d37383af8172ff9475dea363
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2019
ms.locfileid: "66704815"
---
# <a name="transaction-processing"></a>Procesamiento de transacciones
Un *transacciones* delimita el principio y al final de una serie de operaciones de acceso a datos que se ejecuta a través de una conexión. Sujeto a las capacidades transaccionales del origen de datos, el **conexión** objeto también le permite crear y administrar las transacciones. Por ejemplo, mediante el proveedor Microsoft OLE DB para SQL Server para tener acceso a una base de datos en Microsoft SQL Server, puede crear varias transacciones anidadas para los comandos que ejecute.  
  
 ADO garantiza que se producen cambios en un origen de datos resultantes de operaciones en una transacción correctamente entre sí o no en absoluto.  
  
 Si cancela la transacción, o si se produce un error en uno de sus operaciones, el resultado será como si ninguna de las operaciones en la transacción se ha producido. El origen de datos permanecerá tal como estaba antes del comienzo de la transacción.  
  
 ADO proporciona los métodos siguientes para controlar las transacciones: **BeginTrans**, **CommitTrans**, y **RollbackTrans**. Utilice estos métodos con un **conexión** objeto cuando desea guardar o cancelar una serie de cambios realizados en los datos de origen como una sola unidad. Por ejemplo, para transferir dinero entre cuentas, resta una cantidad de uno y agregue la misma cantidad a las demás. Si se produce un error, actualice las cuentas ya no están equilibradas. Realizar estos cambios en una transacción abierta, se garantiza que todos o ninguno de los cambios se pasen a través.  
  
> [!NOTE]
>  No todos los proveedores admiten transacciones. Compruebe que la propiedad definida por el proveedor "**DDL de transacción**" aparece en el **conexión** del objeto [propiedades](../../../ado/reference/ado-api/properties-collection-ado.md) colección, que indica que el proveedor admite transacciones. Si el proveedor no admite transacciones, al llamar a uno de estos métodos, devolverá un error.  
  
 Después de llamar a la **BeginTrans** método, el proveedor ya no confirmará instantáneamente los cambios hasta que llame a **CommitTrans** o **RollbackTrans** para finalizar el transacción.  
  
 Una llamada a la **CommitTrans** método guarda los cambios realizados en una transacción abierta en la conexión y finaliza la transacción. Una llamada a la **RollbackTrans** método invierte los cambios realizados en una transacción abierta y finaliza la transacción. Al llamar a cualquiera de estos métodos cuando no hay ninguna transacción abierta, genera un error.  
  
 En función de la **conexión** del objeto [atributos](../../../ado/reference/ado-api/attributes-property-ado.md) propiedad, al llamar a la **CommitTrans** o **RollbackTrans** posible del método iniciar automáticamente una nueva transacción. Si el **atributos** propiedad está establecida en **adXactCommitRetaining**, el proveedor inicia automáticamente una nueva transacción después de un **CommitTrans** llamar. Si el **atributos** propiedad está establecida en **adXactAbortRetaining**, el proveedor inicia automáticamente una nueva transacción después de un **RollbackTrans** llamar.  
  
## <a name="transaction-isolation-level"></a>Nivel de aislamiento de transacción  
 Use la **IsolationLevel** propiedad para establecer el nivel de aislamiento de una transacción en un **conexión** objeto. La configuración no surte efecto hasta la próxima vez que se llama a la [BeginTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) método. Si el nivel de aislamiento solicitado no está disponible, el proveedor puede devolver el siguiente nivel superior de aislamiento. Hacer referencia a la **IsolationLevel** propiedad en la referencia del programador de ADO para obtener más detalles sobre los valores válidos.  
  
## <a name="nested-transactions"></a>Transacciones anidadas  
 Para los proveedores que admiten transacciones anidadas, llamar a la **BeginTrans** método dentro de una transacción abierta inicia una nueva transacción anidada. El valor devuelto indica el nivel de anidamiento: un valor devuelto de "1" indica que ha abierto una transacción de nivel superior (es decir, la transacción no está anidada dentro de otra transacción), "2" indica que ha abierto una transacción de segundo nivel (una transacción anidada dentro de una transacción de nivel superior), y así sucesivamente. Una llamada a **CommitTrans** o **RollbackTrans** afecta solo al máximo abierto recientemente la transacción; debe cerrar o revertir la transacción actual antes de resolver las transacciones de nivel superior.
