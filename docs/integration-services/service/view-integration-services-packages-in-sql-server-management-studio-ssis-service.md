---
title: "Ver paquetes de Integration Services en SQL Server Management Studio (servicio SSIS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "ver paquetes"
  - "conexiones [Integration Services], paquetes"
ms.assetid: 783e653c-0f1f-45ed-b3ef-5ba07b019f27
caps.latest.revision: 24
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 24
---
# Ver paquetes de Integration Services en SQL Server Management Studio (servicio SSIS)
    
> [!IMPORTANT]  
>  En este tema se describe el servicio de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , un servicio Windows para administrar paquetes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] admite el servicio para mantener la compatibilidad con versiones anteriores de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. A partir de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], puede administrar objetos como paquetes en el servidor de Integration Services.  
  
 En este procedimiento se explica cómo conectarse a [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] y ver una lista de los paquetes que administra el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
### Para conectarse a Integration Services  
  
1.  Haga clic en **Inicio**, elija **Todos los programas**, **Microsoft SQL Server**y, a continuación, haga clic en **SQL Server Management Studio**.  
  
2.  En el cuadro de diálogo **Conectar al servidor** , seleccione **Integration Services** en la lista **Tipo de servidor** , proporcione un nombre de servidor en el cuadro **Nombre de servidor** y haga clic en **Conectar**.  
  
    > [!IMPORTANT]  
    >  Si no puede conectarse a [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], es probable que no se esté ejecutando el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Para conocer el estado del servicio, haga clic en **Inicio**, elija sucesivamente **Todos los programas**, **Microsoft SQL Server**, **Herramientas de configuración**, y haga clic en **Administrador de configuración de SQL Server**. En el panel izquierdo, haga clic en **Servicios de SQL Server**. En el panel derecho, busque el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Inicie el servicio, si no se está ejecutando todavía.  
  
     [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] . De forma predeterminada, la ventana del Explorador de objetos está abierta y colocada en la esquina inferior izquierda del estudio. Si el Explorador de objetos no está abierto, haga clic en **Explorador de objetos** en el menú **Ver** .  
  
### Para ver los paquetes que administra el servicio Integration Services  
  
1.  En el Explorador de objetos, expanda la carpeta Paquetes almacenados.  
  
2.  Expanda las subcarpetas de Paquetes almacenados para mostrar los paquetes.  
  
## Vea también  
 [Administración de paquetes &#40;servicio SSIS&#41;](../../integration-services/service/package-management-ssis-service.md)   
 [Usar SQL Server Management Studio](../../ssms/use-sql-server-management-studio.md)  
  
  