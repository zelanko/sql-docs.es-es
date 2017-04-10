---
title: "Copiar un paquete en herramientas de datos de SQL Server | Microsoft Docs"
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
  - "paquetes [Integration Services], copia"
  - "copiar paquetes"
  - "volver a generar GUID de paquete"
  - "actualizar propiedades del paquete"
ms.assetid: 03edc659-e76d-48c0-a749-5f1899b6b507
caps.latest.revision: 18
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 18
---
# Copiar un paquete en herramientas de datos de SQL Server
  En este tema se explica cómo crear un nuevo paquete [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] mediante la copia de un paquete existente y cómo actualizar las propiedades **Nombre** y **GUID** del nuevo paquete.  
  
### Para copiar un paquete  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contiene el paquete que desea copiar.  
  
2.  En el Explorador de soluciones, haga doble clic en el paquete.  
  
3.  Compruebe que el paquete que desea copiar está seleccionado en el Explorador de soluciones o que la pestaña del Diseñador SSIS que contiene el paquete es una pestaña activa.  
  
4.  En el menú **Archivo**, haga clic en **Guardar \<nombre del paquete> como**.  
  
    > [!NOTE]  
    >  El paquete se debe abrir en el Diseñador SSIS para que la opción **Guardar como** aparezca en el menú **Archivo**.  
  
5.  También puede examinar una carpeta diferente.  
  
6.  Actualice el nombre del archivo de paquete. Asegúrese de mantener la extensión de archivo .dtsx.  
  
7.  Haga clic en **Guardar**.  
  
8.  En el símbolo del sistema, elija si desea actualizar el nombre del objeto del paquete para que coincida con el nombre de archivo. Si hace clic en **Sí**, se actualiza la propiedad **Name** del paquete. El nuevo paquete se agrega al proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] y se abre en el Diseñador [!INCLUDE[ssIS](../includes/ssis-md.md)] .  
  
9. También puede hacer clic en el fondo de la pestaña **Flujo de control** y luego hacer clic en **Propiedades**.  
  
10. En la ventana Propiedades, haga clic en el valor de la propiedad ID y luego, en la lista desplegable, haga clic en **\<Generar nuevo Id.>**.  
  
11. En el menú **Archivo** , haga clic en **Guardar los elementos seleccionados** para guardar el nuevo paquete.  
  
## Vea también  
 [Guardar una copia de un paquete](../Topic/Save%20a%20Copy%20of%20a%20Package.md)   
 [Crear paquetes en herramientas de datos de SQL Server](../integration-services/create-packages-in-sql-server-data-tools.md)   
 [Paquetes de Integration Services &#40;SSIS&#41;](../integration-services/integration-services-ssis-packages.md)  
  
  