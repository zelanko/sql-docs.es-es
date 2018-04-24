---
title: Propiedad ExecuteOptions (RDS) | Documentos de Microsoft
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- ExecuteOptions property [ADO], VBScript example
ms.assetid: 62a4fd88-afc3-4f1f-b978-40710a30c4e9
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 398e5f911baf4ef63dcec790f046da3784983964
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2018
---
# <a name="executeoptions-property-rds"></a>Propiedad ExecuteOptions (RDS)
Indica si está habilitada la ejecución asincrónica.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar a [servicio de datos de WCF](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve uno de los valores siguientes.  
  
|Constante|Description|  
|--------------|-----------------|  
|**adcExecSync**|Ejecuta la siguiente actualización de la [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) sincrónicamente.|  
|**adcExecAsync**|Predeterminado: Ejecuta la siguiente actualización de la **Recordset** asincrónicamente.|  
  
> [!NOTE]
>  Cada archivo ejecutable que utiliza estas constantes debe proporcionar declaraciones para ellos. Puede cortar y pegar las declaraciones de constante que desee desde el archivo Adcvbs.Inc que se encuentra en la carpeta de instalación predeterminada para la biblioteca RDS.  
  
## <a name="remarks"></a>Comentarios  
 Si **ExecuteOptions** está establecido en **adcExecAsync**, a continuación, ejecuta de forma asincrónica la siguiente **actualizar** llamar a en el [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) del objeto **conjunto de registros**.  
  
 Si intenta llamar a [restablecer](../../../ado/reference/rds-api/reset-method-rds.md), [actualizar](../../../ado/reference/rds-api/refresh-method-rds.md), [SubmitChanges](../../../ado/reference/rds-api/submitchanges-method-rds.md), [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md), o [conjunto de registros](../../../ado/reference/rds-api/recordset-sourcerecordset-properties-rds.md) mientras que otra operación asincrónica que podría cambiar el [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) del objeto **Recordset** se está ejecutando, se produce un error.  
  
 Si se produce un error durante una operación asincrónica, la **RDS. DataControl** del objeto [ReadyState](../../../ado/reference/rds-api/readystate-property-rds.md) cambia el valor de **adcReadyStateLoaded** a **adcReadyStateComplete**y el  **Conjunto de registros** sigue siendo el valor de la propiedad *nada*.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo ExecuteOptions y FetchOptions propiedades (VBScript)](../../../ado/reference/rds-api/executeoptions-and-fetchoptions-properties-example-vbscript.md)   
 [Cancel (método) (RDS)](../../../ado/reference/rds-api/cancel-method-rds.md)


