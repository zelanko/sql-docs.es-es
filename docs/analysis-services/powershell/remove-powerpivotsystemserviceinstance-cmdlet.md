---
title: Cmdlet Remove-PowerPivotSystemServiceInstance | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ''
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c3f6f960d0f2b39fa877203ede26f5e66b5c3c37
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="remove-powerpivotsystemserviceinstance-cmdlet"></a>Cmdlet Remove-PowerPivotSystemServiceInstance
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Quita una instancia del Servicio de sistema de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] de la granja.  

>[!NOTE] 
>En este artículo puede contener información no actualizada y ejemplos. Use el cmdlet Get-Help para la versión más reciente.
  
 **Se aplica a:** SharePoint 2010 y SharePoint 2013.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
Remove-PowerPivotSystemServiceInstance [-Confirm <switch>] [-DeleteLocal <switch>] [-Identity <PowerPivotMidTierServiceInstancePipeBind>] [<CommonParameters>]  
```  
  
## <a name="description"></a>Description  
 El cmdlet Remove-PowerPivotSystemServiceInstance quita la información de instancia del Servicio de sistema de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] de la granja. No quita los archivos de programa. Para quitar permanentemente los archivos de programa, debe desinstalarlos.  
  
 Si quita el Servicio de sistema de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , asegúrese también de ejecutar Remove-PowerPivotEngineServiceInstance para quitar la instancia asociada de Analysis Services, seguida de Remove-PowerPivotServiceApplication para eliminar cualquier aplicación de PowerPivotservice. Las aplicaciones de servicio ya no se ejecutarán una vez que se quiten los servicios.  
  
 Para revertir este cambio, puede ejecutar New-PowerPivotSystemServiceInstance -Provision:$true para volver a habilitar la información de la instancia.  
  
## <a name="parameters"></a>Parámetros  
  
### <a name="-identity-powerpivotmidtierserviceinstancepipebind"></a>-Identity \<PowerPivotMidTierServiceInstancePipeBind >  
 Especifica el GUID de la instancia de Servicio de sistema de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] que desea quitar. Hay una instancia de servicio en cada servidor de aplicaciones que tenga una instalación de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint.  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|0|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|true|  
|¿Aceptar caracteres comodín?|false|  
  
### <a name="-deletelocal-switch"></a>-DeleteLocal \<cambiar >  
 Elimina la instancia del Servicio de sistema de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] instalada en el equipo local, permitiéndole quitar la instancia sin tener que especificar una identidad de objeto.  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|con nombre|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### <a name="-confirm-switch"></a>-Confirme \<cambiar >  
 Le solicita confirmación antes de ejecutar el comando. Este valor se habilita de forma predeterminada. Para omitir la respuesta de confirmación de un comando, especifique Confirm:$false en el comando.  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|con nombre|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### <a name="commonparameters"></a>\<CommonParameters >  
 Este cmdlet admite parámetros comunes: Verbose, Debug, ErrorAction, ErrorVariable, WarningAction, WarningVariable,OutBuffer y OutVariable. Para obtener más información, vea [about_Commonparameters](http://go.microsoft.com/fwlink/?linkID=227825).  
  
## <a name="inputs-and-outputs"></a>Entradas y salidas  
 El tipo de entrada es el tipo de objetos que se pueden canalizar al cmdlet. El tipo de valor devuelto es el tipo de objeto que el cmdlet devuelve.  
  
|||  
|-|-|  
|Entradas|Ninguno.|  
|Resultados|Ninguno.|  
  
## <a name="example-1"></a>Ejemplo 1  
  
```  
C:\PS>Remove-PowerPivotSystemServiceInstance -deletelocal  
```  
  
 En este ejemplo se muestra cómo quitar la instancia del Servicio de sistema de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] que se ejecuta en el servidor de aplicaciones local.  
  
## <a name="example-2"></a>Ejemplo 2  
  
```  
C:\PS>Remove-PowerPivotSystemServiceInstance -identity 1234567-890a-bcde-fghijklmn  
```  
  
 En este ejemplo se muestra cómo eliminar un Servicio de sistema de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] concreto según su identidad.  
  
  
