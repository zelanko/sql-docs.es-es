---
title: Cmdlet New-PowerPivotSystemServiceInstance | Documentos de Microsoft
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
ms.assetid: 7ea94113-c0f1-4cca-9228-f1a034fba5db
caps.latest.revision: "10"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: f4c67d1f5b8aea2537b04ebed1608834b13d8f61
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/08/2017
---
# <a name="new-powerpivotsystemserviceinstance-cmdlet"></a>Cmdlet New-PowerPivotSystemServiceInstance
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Agrega una nueva instancia de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] servicio de sistema para un servidor de aplicaciones.  

>[!NOTE] 
>En este artículo puede contener información no actualizada y ejemplos. Use el cmdlet Get-Help para la versión más reciente.
  
 **Se aplica a:** SharePoint 2010 y SharePoint 2013.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
New-PowerPivotSystemServiceInstance [[-ParentService] <PowerPivotMidTierServicePipeBind>] [-SystemServiceInstanceName <string>] [-Provision] [<CommonParameters>]  
```  
  
## <a name="description"></a>Description  
 El cmdlet New-PowerPivotSystemServiceInstance proporciona un nuevo objeto PowerPivotSystemService en el nivel de granja después de usar el programa de instalación de SQL Server para instalar [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint en el servidor de aplicaciones local. Puede proporcionar una sola instancia de servicio en cada servidor de aplicaciones.  Si el servicio ya se ha proporcionado, ya no podrá ejecutar este cmdlet.  
  
## <a name="parameters"></a>Parámetros  
  
### <a name="-parentservice-powerpivotmidtierservicepipebind"></a>-ParentService \<PowerPivotMidTierServicePipeBind >  
 Especifica el GUID del objeto primario del Servicio de sistema de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] en la granja. En esta versión, solo hay un objeto primario permitido. Puede usar Get-PowerPivotSystemService para devolver el objeto de servicio o su GUID.  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|0|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|true|  
|¿Aceptar caracteres comodín?|false|  
  
### <a name="-systemserviceinstancename-string"></a>-SystemServiceInstanceName \<cadena >  
 Especifica un nombre que identifica este objeto.  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|1|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### <a name="provision-switchparameter"></a>Aprovisionar [\<SwitchParameter >]  
 Hace que el servicio esté disponible en SharePoint. Los valores válidos son $true o $false.  
  
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
C:\PS>New-PowerPivotSystemServiceInstance -Provision:$true  
```  
  
 Este ejemplo muestra el formato común del cmdlet. Registra el Servicio de sistema de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] en el servidor de aplicaciones local con la granja.  
  
## <a name="example-2"></a>Ejemplo 2  
  
```  
C:\PS>New-PowerPivotSystemServiceInstance -SystemServiceInstanceName "MyPSSInstance" -provision:$false  
```  
  
 Este ejemplo denomina la instancia del Servicio de sistema de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , pero sin proporcionarla. Si no proporciona un nombre, en su lugar se usa el nombre predeterminado, la instancia del Servicio de sistema de SQL Server Analysis Services. Crear un nombre personalizado para el servicio es opcional. Podría denominar al servicio para admitir escenarios de prueba o si tiene una herramienta o script personalizados que proporcionen la instancia en un paso posterior.  
  
  
