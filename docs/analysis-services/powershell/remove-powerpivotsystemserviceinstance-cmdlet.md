---
title: Cmdlet Remove-PowerPivotSystemServiceInstance | Documentos de Microsoft
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: bc46094a-5584-47ba-8883-77dc79373a5d
caps.latest.revision: "10"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 64bb88fb6bc4a86228fef718f1ba8382ef492039
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/08/2017
---
# <a name="remove-powerpivotsystemserviceinstance-cmdlet"></a>Cmdlet Remove-PowerPivotSystemServiceInstance
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Quita un [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] instancia del servicio de sistema de la granja de servidores.  

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
|Salidas|Ninguno.|  
  
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
  
  
