---
title: "Cmdlet Remove-PowerPivotServiceApplication | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: 2742b2a3-927c-4e7c-bd7d-43c072fa01ab
caps.latest.revision: 11
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 11
---
# Cmdlet Remove-PowerPivotServiceApplication
  Elimina una aplicación de servicio de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
 **Se aplica a:** SharePoint 2010 y SharePoint 2013.  
  
## Sintaxis  
  
```  
Remove-PowerPivotServiceApplication [-Identity <SPGeminiServiceApplicationPipeBind>] [-DeleteAll <switch>] [-RemoveData <switch>] [-Confirm <switch>] [<CommonParameters>]  
```  
  
## Description  
 El cmdlet Remove-PowerPivotServiceApplication elimina una aplicación de servicio de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] de la granja. Use DeleteAll para eliminar todas las aplicaciones de servicio a la vez o use el parámetro Identitiy para quitar una sola instancia. Para obtener información de la instancia, ejecute Get-PowerPivotServiceApplication para devolver todas las instancias de la granja.  
  
 Use el parámetro RemoveData para quitar si lo desea las bases de datos de aplicación de servicio y los archivos almacenados en memoria caché. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] permanecen en bibliotecas de contenido, pero ya no son funcionales una vez que se quita la aplicación de servicio.  
  
## Parámetros  
  
### -Identity \<SPGeminiServiceApplicationPipeBind>  
 Especifica el GUID de una aplicación de servicio de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] en la granja. Debe especificar el GUID si desea quitar simplemente una aplicación, dejando intactas otras aplicaciones de servicios.  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|0|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|true|  
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
  
### -DeleteAll \<modificador>  
 Elimina todas las aplicaciones de servicio de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , pero no elimina la base de datos de aplicación de servicio, ni los objetos de instancia de servicio de la granja. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] y Servicio de motor de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] siguen teniendo instancias después de quitar las aplicaciones de servicio, pero no inservibles.  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|con nombre|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### -RemoveData \<modificador>  
 Quita la base de datos de la aplicación de servicio que contiene las programaciones de las actualizaciones de datos, los datos de uso de libros, los mapas de instancias que se utilizan para realizar el seguimiento de las bases de datos que se cargan y otros datos internos.  
  
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
C:\PS>Remove-PowerPivotServiceApplication -identity 12345678-90ab-cdef-ghijklmnop  
```  
  
 En este ejemplo se elimina una única aplicación de servicio de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , pero no se quita su base de datos o la caché. Si no especifica una identidad, se le solicitará que proporcione una.  
  
## Ejemplo 2  
  
```  
C:\PS>Remove-PowerPivotServiceApplication -DeleteAll  
```  
  
 En este ejemplo se eliminan todas las aplicaciones de servicio de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] de la granja. Las bases de datos y la memoria caché no se eliminan.  
  
## Ejemplo 3  
  
```  
CC:\PS>Remove-PowerPivotServiceApplication -identity 12345678-90ab-cdef-ghijklmnop -RemoveData  
```  
  
 En este ejemplo se elimina una sola aplicación de servicio de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , junto con sus archivos de base de datos y caché.  
  
  