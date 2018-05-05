---
title: MoveFirst, MoveLast, MoveNext y MovePrevious métodos (RDS) | Documentos de Microsoft
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
helpviewer_keywords:
- MoveLast method [RDS]
- MovePrevious method [RDS]
- MoveFirst method [RDS]
- MoveNext method [RDS]
ms.assetid: 45c80bb5-136f-4204-9df2-78740fa55574
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 315ebd2a4de1a98634a5077096c0909550d979e6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="movefirst-movelast-movenext-and-moveprevious-methods-rds"></a>MoveFirst, MoveLast, MoveNext y MovePrevious métodos (RDS)
Se mueve a la primera, última, siguiente o anterior registro en un determinado [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar a [servicio de datos de WCF](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DataControl.Recordset.{MoveFirst | MoveLast | MoveNext | MovePrevious}  
```  
  
#### <a name="parameters"></a>Parámetros  
 *DataControl*  
 Una variable de objeto que representa un [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) objeto.  
  
## <a name="remarks"></a>Comentarios  
 Puede usar el **mover** métodos con el **RDS. DataControl** objeto para navegar por los registros de datos en los controles enlazados a datos en una página Web. Por ejemplo, supongamos que muestra un **Recordset** en una cuadrícula enlazando a un **RDS. DataControl** objeto. A continuación, podrá incluir los botones primero, último, siguiente y anterior que los usuarios pueden hacer clic para moverse a la primera, última, siguiente o del registro anterior en la muestra **conjunto de registros**. Para ello, al llamar a la **MoveFirst**, **MoveLast**, **MoveNext**, y **MovePrevious** métodos de la **RDS. DataControl** objeto en los procedimientos onClick de los botones primero, último, siguiente y anterior, respectivamente. El [ejemplo de libreta de direcciones](../../../ado/guide/remote-data-service/address-book-navigation-buttons.md) muestra cómo hacerlo.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Vea también  
 [Move (método) (ADO)](../../../ado/reference/ado-api/move-method-ado.md)   
 [MoveFirst, MoveLast, MoveNext y MovePrevious métodos (ADO)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)   
 [Método MoveRecord (ADO)](../../../ado/reference/ado-api/moverecord-method-ado.md)


