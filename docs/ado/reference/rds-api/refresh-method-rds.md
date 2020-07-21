---
title: Método Refresh (RDS) | Microsoft Docs
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
apitype: COM
f1_keywords:
- Refresh
- RDS.DataControl::Refresh
- DataControl::Refresh
helpviewer_keywords:
- Refresh method [RDS]
ms.assetid: c90a8050-0ff4-4c83-9925-261f2f2ccfe9
author: rothja
ms.author: jroth
ms.openlocfilehash: 3e9fa606aab5d42a7b56171ca3720742d4d119a0
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2020
ms.locfileid: "82751058"
---
# <a name="refresh-method-rds"></a>Método Refresh (RDS)
Vuelve a consultar el origen de datos especificado en la propiedad [Connect](../../../ado/reference/rds-api/connect-property-rds.md) y actualiza los resultados de la consulta.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, los componentes de servidor RDS ya no se incluyen en el sistema operativo Windows (consulte la guía de compatibilidad de Windows 8 y [Windows server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obtener más detalles). Los componentes de cliente RDS se quitarán en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar al [servicio de datos de WCF](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DataControl.Refresh  
```  
  
#### <a name="parameters"></a>Parámetros  
 *DataControl*  
 Variable de objeto que representa un objeto [RDS. Objeto DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) .  
  
## <a name="remarks"></a>Observaciones  
 Debe establecer las propiedades [Connect](../../../ado/reference/rds-api/connect-property-rds.md), [Server](../../../ado/reference/rds-api/server-property-rds.md)y [SQL](../../../ado/reference/rds-api/sql-property.md) antes de usar el método **Refresh** . Todos los controles enlazados a datos del formulario asociados a un **objeto RDS. **El objeto DataControl reflejará el nuevo conjunto de registros. Se libera cualquier objeto de [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) ya existente y se descartan los cambios no guardados. El método **Refresh** convierte automáticamente el primer registro en el registro actual.  
  
 Se recomienda llamar al método **Refresh** periódicamente al trabajar con datos. Si recupera datos y, a continuación, los deja en un equipo cliente durante un tiempo, es probable que quede obsoleto. Es posible que se produzcan errores en cualquier cambio que realice, ya que otra persona podría haber cambiado el registro y enviado los cambios antes de usted.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo del método Refresh (VB)](../../../ado/reference/ado-api/refresh-method-example-vb.md)   
 [Ejemplo del método Refresh (VBScript)](../../../ado/reference/rds-api/refresh-method-example-vbscript.md)   
 [Botones de comando de la libreta de direcciones](../../../ado/guide/remote-data-service/address-book-command-buttons.md)   
 [Método CancelUpdate (RDS)](../../../ado/reference/rds-api/cancelupdate-method-rds.md)   
 [Refresh (método) (ADO)](../../../ado/reference/ado-api/refresh-method-ado.md)   
 [Método SubmitChanges (RDS)](../../../ado/reference/rds-api/submitchanges-method-rds.md)


