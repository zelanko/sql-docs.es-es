---
title: Propiedad ReadyState (RDS) | Documentos de Microsoft
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.prod: sql
ms.prod_service: drivers
ms.component: reference
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- ReadyState property [ADO]
ms.assetid: 5be75bc7-1171-4440-a37e-c8cc6b5cd865
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 78a5b98cdf0eff5cb84165e8fd38b58c2b87e58a
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2018
---
# <a name="readystate-property-rds"></a>Propiedad ReadyState (RDS)
Indica el progreso de un [DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) objeto tal y como recupera datos en su [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar a [servicio de datos de WCF](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve uno de los valores siguientes.  
  
|Value|Description|  
|-----------|-----------------|  
|**adcReadyStateLoaded**|Todavía se está ejecutando la consulta actual y no se han capturado ninguna fila. El **DataControl** del objeto **Recordset** no está disponible para su uso.|  
|**adcReadyStateInteractive**|Un conjunto inicial de filas recuperadas por la consulta actual se ha almacenado en el **DataControl** del objeto **Recordset** y están disponibles para su uso. Las filas restantes están siendo recuperadas.|  
|**adcReadyStateComplete**|Todas las filas recuperadas por la consulta actual se han almacenado en el **DataControl** del objeto **Recordset** y están disponibles para su uso.<br /><br /> Este estado también existirá si se anula una operación debido a un error, o si la **Recordset** no se ha inicializado el objeto.|  
  
> [!NOTE]
>  Cada archivo ejecutable del cliente que utiliza estas constantes debe proporcionar declaraciones para ellos. Puede cortar y pegar las declaraciones de constante que desee desde el archivo Adcvbs.Inc que se encuentra en la carpeta de instalación predeterminada para la biblioteca RDS.  
  
## <a name="remarks"></a>Comentarios  
 Use la [onReadyStateChange](../../../ado/reference/rds-api/onreadystatechange-event-rds.md) eventos para supervisar los cambios en el **ReadyState** propiedad durante una operación de consulta asincrónica. Esto es más eficiente que comprobar periódicamente el valor de la propiedad.  
  
 Si se produce un error durante una operación asincrónica, la **ReadyState** propiedad cambia a **adcReadyStateComplete**, [estado](../../../ado/reference/ado-api/state-property-ado.md) cambios en las propiedades de **adStateExecuting** a **adStateClosed**y el **Recordset** objeto [valor](../../../ado/reference/ado-api/value-property-ado.md) propiedad permanece *nada* .  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de la propiedad ReadyState (VBScript)](../../../ado/reference/rds-api/readystate-property-example-vbscript.md)   
 [Cancel (método) (RDS)](../../../ado/reference/rds-api/cancel-method-rds.md)   
 [Propiedad ExecuteOptions (RDS)](../../../ado/reference/rds-api/executeoptions-property-rds.md)


