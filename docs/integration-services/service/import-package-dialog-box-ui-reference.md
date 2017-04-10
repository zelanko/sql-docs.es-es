---
title: "Referencia de la interfaz de usuario del cuadro de di&#225;logo Importar paquete | Microsoft Docs"
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
  - "sql13.dts.dtsserver.importpackage.f1"
helpviewer_keywords: 
  - "Importar paquete, cuadro de diálogo"
ms.assetid: 0e5fb127-c7ff-4dfa-b90e-d9bcf0ce763b
caps.latest.revision: 19
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 19
---
# Referencia de la interfaz de usuario del cuadro de di&#225;logo Importar paquete
  Utilice el cuadro de diálogo **Importar paquete** , disponible en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], para importar un paquete de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] y para establecer o modificar el nivel de protección del paquete.  
  
## Opciones  
 **Ubicación del paquete**  
 Seleccione el tipo de ubicación de almacenamiento a la que se importará el paquete. Las siguientes opciones están disponibles:  
  
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
 Si usa la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], indique un nombre de usuario.  
  
 **Contraseña**  
 Si usa la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], indique una contraseña.  
  
 **Ruta de acceso del paquete**  
 Escriba la ruta de acceso del paquete, o bien haga clic en el botón Examinar **(…)** y busque el paquete.  
  
 **Nombre del paquete**  
 También puede cambiar el nombre del paquete si lo desea. El nombre predeterminado es el nombre del paquete que se importará.  
  
 **Nivel de protección**  
 Haga clic en el botón Examinar **(…)** y, en el cuadro de diálogo **Nivel de protección de paquetes**, actualice el nivel de protección. Para más información, vea [Nivel de protección de paquetes y del proyecto, cuadro de diálogo](../../integration-services/packages/package-and-project-protection-level-dialog-box.md).  
  
## Vea también  
 [Guardar copia del paquete](../Topic/Save%20Copy%20of%20Package.md)   
 [Referencia de la interfaz de usuario del cuadro de diálogo Exportar paquete](../../integration-services/service/export-package-dialog-box-ui-reference.md)   
 [Guardar paquetes](../../integration-services/save-packages.md)   
 [Importar y exportar paquetes &#40;servicio SSIS&#41;](../../integration-services/service/import-and-export-packages-ssis-service.md)  
  
  