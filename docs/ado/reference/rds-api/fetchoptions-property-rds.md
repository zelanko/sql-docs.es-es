---
title: Propiedad FetchOptions (RDS) | Documentos de Microsoft
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
- FetchOptions property [ADO]
ms.assetid: 7b2e254a-9354-4541-bc98-bb185276388f
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dcbb951a5d17c7b7f0d8be540bef5c74e96b101d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="fetchoptions-property-rds"></a>Propiedad FetchOptions (RDS)
Indica el tipo de recuperación asincrónica.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar a [servicio de datos de WCF](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="setting-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve uno de los valores siguientes.  
  
|Constante|Description|  
|--------------|-----------------|  
|**adcFetchUpFront**|Todos los registros de la [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) se capturan antes de que el control se devuelve a la aplicación. La sección completa **Recordset** se capturan antes de que la aplicación tiene que hacer nada con él.|  
|**adcFetchBackground**|Control puede devolver a la aplicación tan pronto como se ha recuperado el primer lote de registros. Leen un subsiguientes de la **Recordset** que intenta obtener acceso a un registro no recuperado en el primer lote se retrasará hasta que se recupere realmente el registro buscado, momento en el que el control vuelve a la aplicación.|  
|**adcFetchAsync**|Predeterminado: Control vuelve inmediatamente a la aplicación mientras se buscan los registros en segundo plano. Si la aplicación intenta leer un registro que aún no se ha recuperado, se leerá el registro más cercano al buscado y el control se devuelve inmediatamente, lo que indica que el final actual de la **Recordset** se ha alcanzado. Por ejemplo, una llamada a [MoveLast](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md) moverá la posición actual del registro al último registro realmente recuperado, aunque haya más registros continuará rellenar el **conjunto de registros**.|  
  
> [!NOTE]
>  Cada archivo ejecutable del cliente que utiliza estas constantes debe proporcionar declaraciones para ellos. Puede cortar y pegar las declaraciones de constante que desee desde el archivo Adcvbs.Inc que se encuentra en la carpeta de instalación predeterminada para la biblioteca RDS.  
  
## <a name="remarks"></a>Comentarios  
 En una aplicación Web, normalmente es conveniente usar **adcFetchAsync** (el valor predeterminado), ya que proporciona un mejor rendimiento. En una aplicación cliente compilada, normalmente es conveniente usar **adcFetchBackground**.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo ExecuteOptions y FetchOptions propiedades (VBScript)](../../../ado/reference/rds-api/executeoptions-and-fetchoptions-properties-example-vbscript.md)   
 [Cancel (método) (RDS)](../../../ado/reference/rds-api/cancel-method-rds.md)


