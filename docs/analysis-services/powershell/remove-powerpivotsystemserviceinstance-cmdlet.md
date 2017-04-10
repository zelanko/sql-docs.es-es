---
title: "Cmdlet Remove-PowerPivotSystemServiceInstance | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: bc46094a-5584-47ba-8883-77dc79373a5d
caps.latest.revision: 10
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 10
---
# Cmdlet Remove-PowerPivotSystemServiceInstance
  Quita una instancia del Servicio de sistema de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] de la granja.  
  
 **Se aplica a:** SharePoint 2010 y SharePoint 2013.  
  
## Sintaxis  
  
```  
Remove-PowerPivotSystemServiceInstance [-Confirm <switch>] [-DeleteLocal <switch>] [-Identity <PowerPivotMidTierServiceInstancePipeBind>] [<CommonParameters>]  
```  
  
## Description  
 El cmdlet Remove-PowerPivotSystemServiceInstance quita la información de instancia del Servicio de sistema de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] de la granja. No quita los archivos de programa. Para quitar permanentemente los archivos de programa, debe desinstalarlos.  
  
 Si quita el Servicio de sistema de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)], asegúrese también de ejecutar Remove-PowerPivotEngineServiceInstance para quitar la instancia asociada de Analysis Services, seguida de Remove-PowerPivotServiceApplication para eliminar cualquier aplicación de PowerPivotservice. Las aplicaciones de servicio ya no se ejecutarán una vez que se quiten los servicios.  
  
 Para revertir este cambio, puede ejecutar New-PowerPivotSystemServiceInstance -Provision:$true para volver a habilitar la información de la instancia.  
  
## Parámetros  
  
### -Identity \<PowerPivotMidTierServiceInstancePipeBind>  
 Especifica el GUID de la instancia de Servicio de sistema de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] que desea quitar. Hay una instancia de servicio en cada servidor de aplicaciones que tenga una instalación de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint.  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|0|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|true|  
|¿Aceptar caracteres comodín?|false|  
  
### -DeleteLocal \<modificador>  
 Elimina la instancia del Servicio de sistema de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] instalada en el equipo local, permitiéndole quitar la instancia sin tener que especificar una identidad de objeto.  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|con nombre|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### -Confirm \<modificador>  
 Le solicita confirmación antes de ejecutar el comando. Este valor se habilita de forma predeterminada. Para omitir la respuesta de confirmación de un comando, especifique Confirm:$false en el comando.  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|con nombre|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### \<CommonParameters>  
 Este cmdlet admite parámetros comunes: Verbose, Debug, ErrorAction, ErrorVariable, WarningAction, WarningVariable,OutBuffer y OutVariable. Para más información, vea [about_CommonParameters](http://go.microsoft.com/fwlink/?linkID=227825).  
  
## Entradas y salidas  
 El tipo de entrada es el tipo de objetos que se pueden canalizar al cmdlet. El tipo de valor devuelto es el tipo de objeto que el cmdlet devuelve.  
  
|||  
|-|-|  
|Entradas|Ninguno.|  
|Salidas|Ninguno.|  
  
## Ejemplo 1  
  
```  
C:\PS>Remove-PowerPivotSystemServiceInstance -deletelocal  
```  
  
 En este ejemplo se muestra cómo quitar la instancia del Servicio de sistema de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] que se ejecuta en el servidor de aplicaciones local.  
  
## Ejemplo 2  
  
```  
C:\PS>Remove-PowerPivotSystemServiceInstance -identity 1234567-890a-bcde-fghijklmn  
```  
  
 En este ejemplo se muestra cómo eliminar un Servicio de sistema de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] concreto según su identidad.  
  
  