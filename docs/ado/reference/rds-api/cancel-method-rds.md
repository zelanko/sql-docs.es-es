---
title: Método CANCEL (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Cancel method [RDS]
ms.assetid: 560b5b3d-fba9-4275-8920-9c3e186134f7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 90d3e60a77df15d1b2db302df8a3c1d4a39de245
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "67964614"
---
# <a name="cancel-method-rds"></a>Cancel (método) (RDS)
Cancela la ejecución de una llamada de método pendiente y asincrónica.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, los componentes de servidor RDS ya no se incluyen en el sistema operativo Windows (consulte la guía de compatibilidad de Windows 8 y [Windows server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obtener más detalles). Los componentes de cliente RDS se quitarán en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar al [servicio de datos de WCF](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
RDS.DataControl.Cancel  
```  
  
## <a name="remarks"></a>Observaciones  
 Cuando se llama a **Cancel**, [ReadyState](../../../ado/reference/rds-api/readystate-property-rds.md) se establece automáticamente en **AdcReadyStateLoaded**y el [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) estará vacío.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo del método CANCEL (VBScript)](../../../ado/reference/rds-api/cancel-method-example-vbscript.md)   
 [CANCEL (método) (ADO)](../../../ado/reference/ado-api/cancel-method-ado.md)   
 [CancelBatch (método) (ADO)](../../../ado/reference/ado-api/cancelbatch-method-ado.md)   
 [CancelUpdate (método) (ADO)](../../../ado/reference/ado-api/cancelupdate-method-ado.md)   
 [Método CancelUpdate (RDS)](../../../ado/reference/rds-api/cancelupdate-method-rds.md)   
 [Propiedad ExecuteOptions (RDS)](../../../ado/reference/rds-api/executeoptions-property-rds.md)


