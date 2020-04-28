---
title: Métodos MoveFirst, MoveLast, MoveNext y MovePrevious (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- MoveLast method [RDS]
- MovePrevious method [RDS]
- MoveFirst method [RDS]
- MoveNext method [RDS]
ms.assetid: 45c80bb5-136f-4204-9df2-78740fa55574
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8e99ff17cad2bebcfaed509788ea3721ddfeb0ce
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "67963887"
---
# <a name="movefirst-movelast-movenext-and-moveprevious-methods-rds"></a>MoveFirst, MoveLast, MoveNext y MovePrevious métodos (RDS)
Se desplaza al registro primero, último, siguiente o anterior de un objeto de [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) especificado.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, los componentes de servidor RDS ya no se incluyen en el sistema operativo Windows (consulte la guía de compatibilidad de Windows 8 y [Windows server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obtener más detalles). Los componentes de cliente RDS se quitarán en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar al [servicio de datos de WCF](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DataControl.Recordset.{MoveFirst | MoveLast | MoveNext | MovePrevious}  
```  
  
#### <a name="parameters"></a>Parámetros  
 *DataControl*  
 Variable de objeto que representa un objeto [RDS. Objeto DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) .  
  
## <a name="remarks"></a>Observaciones  
 Puede usar los métodos **Move** con el **objeto RDS. Objeto DataControl** para navegar por los registros de datos de los controles enlazados a datos en una página web. Por ejemplo, supongamos que se muestra un **conjunto de registros** en una cuadrícula enlazando a un **objeto RDS. Objeto DataControl** . Después, puede incluir los botones primero, último, siguiente y anterior en los que los usuarios pueden hacer clic para moverse al registro primero, último, siguiente o anterior del **conjunto de registros**mostrado. Para ello, debe llamar a los métodos **MoveFirst**, **MoveLast**, **MoveNext**y **MovePrevious** de **RDS. Objeto DataControl** en los procedimientos OnClick para los botones primero, último, siguiente y anterior, respectivamente. En el ejemplo de la [Libreta de direcciones](../../../ado/guide/remote-data-service/address-book-navigation-buttons.md) se muestra cómo hacerlo.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Consulte también  
 [Move (método) (ADO)](../../../ado/reference/ado-api/move-method-ado.md)   
 [Métodos MoveFirst, MoveLast, MoveNext y MovePrevious (ADO)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)   
 [Método MoveRecord (ADO)](../../../ado/reference/ado-api/moverecord-method-ado.md)


