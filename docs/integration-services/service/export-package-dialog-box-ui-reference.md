---
title: "Referencia de la interfaz de usuario del cuadro de di&#225;logo Exportar paquete | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.dtsserver.exportpackage.f1"
helpviewer_keywords: 
  - "Exportar paquete, cuadro de diálogo"
ms.assetid: 3742fe8a-ef57-444d-b2fb-cb25d16bae97
caps.latest.revision: 23
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 23
---
# Referencia de la interfaz de usuario del cuadro de di&#225;logo Exportar paquete
  Utilice el cuadro de diálogo **Exportar paquete** , disponible en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], para exportar un paquete de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] a una ubicación diferente y, opcionalmente, modificar el nivel de protección del paquete.  
  
## Opciones  
 **Ubicación del paquete**  
 Seleccione el tipo de almacenamiento al que desea exportar el paquete. Las siguientes opciones están disponibles:  
  
 **SQL Server**  
  
 **Sistema de archivos**  
  
 **Almacén de paquetes SSIS**  
  
 **Server**  
 Escriba un nombre de servidor o seleccione un servidor de la lista.  
  
 **Autenticación**  
 Seleccione Autenticación de Windows o Autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esta opción solo está disponible si la ubicación de almacenamiento es [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
>  Siempre que sea posible, utilice la autenticación de Windows.  
  
 **Tipo de autenticación**  
 Seleccione un tipo de autenticación.  
  
 **Nombre de usuario.**  
 Si usa la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], proporcione un nombre de usuario.  
  
 **Contraseña**  
 Si está usando la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], proporcione una contraseña.  
  
 **Ruta de acceso del paquete**  
 Escriba la ruta de acceso del paquete o haga clic en el botón Examinar **(…)** y busque la carpeta en la que quiera almacenar el paquete.  
  
 **Nivel de protección**  
 Haga clic en el botón Examinar **(…)** y actualice el nivel de protección del cuadro de diálogo **Nivel de protección de paquetes**. Para obtener más información, vea [Nivel de protección de paquetes y del proyecto, cuadro de diálogo](../../integration-services/packages/package-and-project-protection-level-dialog-box.md).  
  
## Vea también  
 [Guardar copia del paquete](../Topic/Save%20Copy%20of%20Package.md)   
 [Referencia de la interfaz de usuario del cuadro de diálogo Importar paquete](../../integration-services/service/import-package-dialog-box-ui-reference.md)   
 [Guardar paquetes](../../integration-services/save-packages.md)   
 [Importar y exportar paquetes &#40;servicio SSIS&#41;](../../integration-services/service/import-and-export-packages-ssis-service.md)  
  
  