---
title: Método CancelUpdate (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- CancelUpdate method [RDS]
ms.assetid: 76d8a6e9-bc6c-4ea0-8e7a-2bae5ed06650
author: rothja
ms.author: jroth
ms.openlocfilehash: 05426b2d4fba81e70a8bae35db215bcd750d3169
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2020
ms.locfileid: "82746346"
---
# <a name="cancelupdate-method-rds"></a>Método CancelUpdate (RDS)
Cancela los cambios realizados en la fila actual o nueva de un objeto de [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) .  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, los componentes de servidor RDS ya no se incluyen en el sistema operativo Windows (consulte la guía de compatibilidad de Windows 8 y [Windows server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obtener más detalles). Los componentes de cliente RDS se quitarán en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar al [servicio de datos de WCF](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DataControl.CancelUpdate  
```  
  
#### <a name="parameters"></a>Parámetros  
 *DataControl*  
 Variable de objeto que representa un objeto [RDS. Objeto DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) .  
  
## <a name="remarks"></a>Comentarios  
 El servicio de cursor para OLE DB mantiene una copia de los valores originales y una memoria caché de cambios. Cuando se llama a **CancelUpdate**, la memoria caché de los cambios se restablece en Empty y los controles enlazados se actualizan con los datos originales.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo del método CancelUpdate (VBScript)](../../../ado/reference/rds-api/cancelupdate-method-example-vbscript.md)   
 [Botones de comando de la libreta de direcciones](../../../ado/guide/remote-data-service/address-book-command-buttons.md)   
 [CANCEL (método) (ADO)](../../../ado/reference/ado-api/cancel-method-ado.md)   
 [Método CANCEL (RDS)](../../../ado/reference/rds-api/cancel-method-rds.md)   
 [CancelBatch (método) (ADO)](../../../ado/reference/ado-api/cancelbatch-method-ado.md)   
 [CancelUpdate (método) (ADO)](../../../ado/reference/ado-api/cancelupdate-method-ado.md)   
 [Método Refresh (RDS)](../../../ado/reference/rds-api/refresh-method-rds.md)   
 [Método SubmitChanges (RDS)](../../../ado/reference/rds-api/submitchanges-method-rds.md)


