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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67964121"
---
# <a name="fetchoptions-property-rds"></a>Propiedad FetchOptions (RDS)
Indica el tipo de recuperación asincrónica.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo de Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Deben migrar las aplicaciones que usan RDS a [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="setting-and-return-values"></a>Establecer y devolver valores  
 Establece o devuelve uno de los valores siguientes.  
  
|Constante|Descripción|  
|--------------|-----------------|  
|**adcFetchUpFront**|Todos los registros de la [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) se capturan antes de devolver el control a la aplicación. La completa **Recordset** se capturan antes de la aplicación puede hacer nada con ella.|  
|**adcFetchBackground**|Control puede volver a la aplicación tan pronto como el primer lote de registros se han obtenido. Lee una posterior de la **Recordset** que intenta obtener acceso a un registro no recuperado en el primer lote se retrasará hasta que se capturaron realmente el registro buscado, momento en el que el control vuelve a la aplicación.|  
|**adcFetchAsync**|Predeterminado: Control vuelve inmediatamente a la aplicación mientras se capturan los registros en segundo plano. Si la aplicación intenta leer un registro que aún no se han recuperado, se leerá el registro más cercano al buscado y el control se devuelve inmediatamente, lo que indica que el extremo actual de la **Recordset** se ha alcanzado. Por ejemplo, una llamada a [MoveLast](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md) moverá la posición actual del registro al último registro realmente recuperado, aunque haya más registros continuará rellenar el **Recordset**.|  
  
> [!NOTE]
>  Cada archivo ejecutable del lado cliente que usa estas constantes debe proporcionar declaraciones para ellos. Puede cortar y pegar las declaraciones de constante que desee desde el archivo Adcvbs.Inc que se encuentra en la carpeta de instalación predeterminada de la biblioteca de RDS.  
  
## <a name="remarks"></a>Comentarios  
 En una aplicación Web, normalmente es conveniente usar **adcFetchAsync** (el valor predeterminado), ya que proporciona un mejor rendimiento. En una aplicación cliente compilada, normalmente es conveniente usar **adcFetchBackground**.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo ExecuteOptions y FetchOptions propiedades (VBScript)](../../../ado/reference/rds-api/executeoptions-and-fetchoptions-properties-example-vbscript.md)   
 [Cancel (método) (RDS)](../../../ado/reference/rds-api/cancel-method-rds.md)


