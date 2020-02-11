---
title: Propiedad FetchOptions (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- FetchOptions property [ADO]
ms.assetid: 7b2e254a-9354-4541-bc98-bb185276388f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4e4e0943a675ef7cf3684ccddd2699fba02dac9e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67964121"
---
# <a name="fetchoptions-property-rds"></a>Propiedad FetchOptions (RDS)
Indica el tipo de captura asincrónica.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, los componentes de servidor RDS ya no se incluyen en el sistema operativo Windows (consulte la guía de compatibilidad de Windows 8 y [Windows server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obtener más detalles). Los componentes de cliente RDS se quitarán en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar al [servicio de datos de WCF](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="setting-and-return-values"></a>Establecer y devolver valores  
 Establece o devuelve uno de los valores siguientes.  
  
|Constante|Descripción|  
|--------------|-----------------|  
|**adcFetchUpFront**|Se capturan todos los registros del [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) antes de que se devuelva el control a la aplicación. Se captura el **conjunto de registros** completo antes de que la aplicación pueda hacer nada con él.|  
|**adcFetchBackground**|El control puede volver a la aplicación en cuanto se ha capturado el primer lote de registros. Una lectura posterior del **conjunto de registros** que intenta tener acceso a un registro que no se captura en el primer lote se retrasará hasta que se recupere realmente el registro buscado, momento en el que el control de tiempo vuelve a la aplicación.|  
|**adcFetchAsync**|Default. El control vuelve inmediatamente a la aplicación mientras se capturan los registros en segundo plano. Si la aplicación intenta leer un registro que todavía no se ha capturado, el registro más cercano al registro buscado se leerá y el control se devolverá inmediatamente, lo que indica que se ha alcanzado el final actual del **conjunto de registros** . Por ejemplo, una llamada a [MoveLast](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md) moverá la posición del registro actual al último registro que se ha capturado realmente, aunque más registros continúen rellenando el **conjunto de registros**.|  
  
> [!NOTE]
>  Cada archivo ejecutable del lado cliente que utiliza estas constantes debe proporcionar declaraciones para ellas. Puede cortar y pegar las declaraciones de constantes que desee del archivo Adcvbs. Inc, que se encuentra en la carpeta de instalación predeterminada de la biblioteca RDS.  
  
## <a name="remarks"></a>Observaciones  
 En una aplicación Web, normalmente querrá usar **adcFetchAsync** (el valor predeterminado), ya que proporciona un mejor rendimiento. En una aplicación cliente compilada, normalmente querrá usar **adcFetchBackground**.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de las propiedades ExecuteOptions y FetchOptions (VBScript)](../../../ado/reference/rds-api/executeoptions-and-fetchoptions-properties-example-vbscript.md)   
 [Cancel (método) (RDS)](../../../ado/reference/rds-api/cancel-method-rds.md)


