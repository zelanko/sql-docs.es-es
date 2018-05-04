---
title: Cmdlet Get-PowerPivotSystemService | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ''
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: df353738db74393d9347064e0215daaa89d0087c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="get-powerpivotsystemservice-cmdlet"></a>Cmdlet Get-PowerPivotSystemService
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Devuelve las propiedades globales del objeto Servicio de sistema de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] en una granja. 

>[!NOTE] 
>En este artículo puede contener información no actualizada y ejemplos. Use el cmdlet Get-Help para la versión más reciente.
  
 **Se aplica a:** SharePoint 2010 y SharePoint 2013.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
Get-PowerPivotSystemService [-Identity <PowerPivotMidTierServicePipeBind>] [<CommonParameters>]  
```  
  
## <a name="description"></a>Description  
 El cmdlet Get-PowerPivotSystemService devuelve las propiedades globales del objeto Servicio de sistema de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Hay un objeto primario en cada granja, pero cada granja puede tener varias instancias del Servicio de sistema de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] que se ejecutan en servidores de aplicaciones individuales de la granja. El objeto primario muestra los valores del nivel de granja que no cambian según la instancia. Si la granja incluye varias instalaciones de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint, una lista delimitada por comas de las instancias indicará el número de instancias del Servicio de sistema de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] en la granja.  
  
## <a name="parameters"></a>Parámetros  
  
### <a name="-identity-powerpivotmidtierservicepipebind"></a>-Identity \<PowerPivotMidTierServicePipeBind >  
 Especifica el objeto primario que se va a obtener. El valor debe ser un GUID válido que identifique de forma única el objeto en la granja.  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|0|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|true|  
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
C:\PS>Get-PowerPivotSystemService  
```  
  
 Este ejemplo devuelve las propiedades globales del objeto primario y muestra las propiedades que pueden compartir todas las instancias del Servicio de sistema de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] en la granja.  
  
  
