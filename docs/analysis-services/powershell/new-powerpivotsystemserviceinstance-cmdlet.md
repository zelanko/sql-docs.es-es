---
title: "Cmdlet New-PowerPivotSystemServiceInstance | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: 7ea94113-c0f1-4cca-9228-f1a034fba5db
caps.latest.revision: 10
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 10
---
# Cmdlet New-PowerPivotSystemServiceInstance
  Agrega una nueva instancia del Servicio de sistema de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] a un servidor de aplicaciones.  
  
 **Se aplica a:** SharePoint 2010 y SharePoint 2013.  
  
## Sintaxis  
  
```  
New-PowerPivotSystemServiceInstance [[-ParentService] <PowerPivotMidTierServicePipeBind>] [-SystemServiceInstanceName <string>] [-Provision] [<CommonParameters>]  
```  
  
## Description  
 El cmdlet New-PowerPivotSystemServiceInstance proporciona un nuevo objeto PowerPivotSystemService en el nivel de granja después de usar el programa de instalación de SQL Server para instalar [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint en el servidor de aplicaciones local. Puede proporcionar una sola instancia de servicio en cada servidor de aplicaciones.  Si el servicio ya se ha proporcionado, ya no podrá ejecutar este cmdlet.  
  
## Parámetros  
  
### -ParentService \<PowerPivotMidTierServicePipeBind>  
 Especifica el GUID del objeto primario del Servicio de sistema de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] en la granja. En esta versión, solo hay un objeto primario permitido. Puede usar Get-PowerPivotSystemService para devolver el objeto de servicio o su GUID.  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|0|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|true|  
|¿Aceptar caracteres comodín?|false|  
  
### -SystemServiceInstanceName \<cadena>  
 Especifica un nombre que identifica este objeto.  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|1|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### Provision [\<SwitchParameter>]  
 Hace que el servicio esté disponible en SharePoint. Los valores válidos son $true o $false.  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|con nombre|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### \<CommonParameters>  
 Este cmdlet admite parámetros comunes: Verbose, Debug, ErrorAction, ErrorVariable, WarningAction, WarningVariable,OutBuffer y OutVariable. Para obtener más información, vea [about_Commonparameters](http://go.microsoft.com/fwlink/?linkID=227825).  
  
## Entradas y salidas  
 El tipo de entrada es el tipo de objetos que se pueden canalizar al cmdlet. El tipo de valor devuelto es el tipo de objeto que el cmdlet devuelve.  
  
|||  
|-|-|  
|Entradas|Ninguno.|  
|Salidas|Ninguno.|  
  
## Ejemplo 1  
  
```  
C:\PS>New-PowerPivotSystemServiceInstance -Provision:$true  
```  
  
 Este ejemplo muestra el formato común del cmdlet. Registra el Servicio de sistema de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] en el servidor de aplicaciones local con la granja.  
  
## Ejemplo 2  
  
```  
C:\PS>New-PowerPivotSystemServiceInstance -SystemServiceInstanceName "MyPSSInstance" -provision:$false  
```  
  
 Este ejemplo denomina la instancia del Servicio de sistema de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , pero sin proporcionarla. Si no proporciona un nombre, en su lugar se usa el nombre predeterminado, la instancia del Servicio de sistema de SQL Server Analysis Services. Crear un nombre personalizado para el servicio es opcional. Podría denominar al servicio para admitir escenarios de prueba o si tiene una herramienta o script personalizados que proporcionen la instancia en un paso posterior.  
  
  