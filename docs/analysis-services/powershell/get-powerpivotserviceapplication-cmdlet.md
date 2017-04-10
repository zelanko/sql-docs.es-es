---
title: "Cmdlet Get-PowerPivotServiceApplication | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: 99e4faa1-2f87-43c6-b7ec-a97d4112c5ac
caps.latest.revision: 10
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 10
---
# Cmdlet Get-PowerPivotServiceApplication
  Devuelve una o varias aplicaciones de servicio de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
 **Se aplica a:** SharePoint 2010 y SharePoint 2013.  
  
## Sintaxis  
  
```  
Get-PowerPivotServiceApplication [[-Identity] <SPGeminiServiceApplicationPipeBind>] [<CommonParameters>]  
```  
  
## Description  
 El cmdlet Get-PowerPivotServiceApplication devuelve la aplicación de servicio especificada por el parámetro Identity. Si no se especifica ningún parámetro, el cmdlet devuelve todas las aplicaciones de servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] en la granja de servidores. Cada aplicación se identifica mediante su nombre para mostrar, tipo de aplicación y GUID. Para ver propiedades adicionales de una aplicación de servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)], agregue la opción format-list al cmdlet.  
  
## Parámetros  
  
### -Identity \<SPGeminiServiceApplicationPipeBind>  
 Especifica la aplicación de servicio que se va a obtener. El valor debe ser un GUID válido que identifique de forma única el objeto en la granja.  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|0|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|true|  
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
C:\PS>Get-PowerPivotServiceApplication  
```  
  
 Este ejemplo devuelve una o varias aplicaciones de servicios de la granja.  
  
## Ejemplo 2  
  
```  
C:\PS>Get-PowerPivotServiceApplication | format-list  
```  
  
 Este ejemplo devuelve todas las propiedades de una aplicación de servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
## Ejemplo 3  
  
```  
C:\PS>get-PowerPivotServiceApplication -Identity 1234567-890a-bcde-fghijklm  
```  
  
 Este ejemplo devuelve una única aplicación de servicio y muestra el nombre para mostrar, el tipo de aplicación y el GUID de la aplicación. Si el nombre para mostrar es largo, se truncará. Use la opción format-list para ver el nombre completo.  
  
  