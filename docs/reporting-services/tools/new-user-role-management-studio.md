---
title: "Nuevo rol de usuario (Management Studio) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.swb.reportserver.newrole.f1"
ms.assetid: 9f76a235-0b58-479c-8e5b-50588091b71c
caps.latest.revision: 26
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 26
---
# Nuevo rol de usuario (Management Studio)
  Utilice esta página para crear una definición de roles de nivel de elemento. Una definición de roles de nivel de elemento es una colección con nombre de las tareas que puede realizar un usuario con las carpetas, los informes, los modelos, los recursos y los orígenes de datos compartidos. Un ejemplo de definición de roles de nivel de elemento sería el rol predefinido Explorador, que identifica los tipos de acciones que podría necesitar el usuario final de un informe para navegar por carpetas y ver informes.  
  
 Se pretende que el número de definiciones de roles sea reducido. La mayoría de las organizaciones solo requieren algunas. Sin embargo, si las definiciones de roles predefinidos no son suficientes, se pueden modificar o se pueden crear otras nuevas.  
  
> [!NOTE]  
>  Las definiciones de roles solo se utilizan en un servidor de informes que se ejecute en modo nativo. Si el servidor de informes está configurado para la integración con SharePoint, esta página no está disponible.  
  
## Opciones  
 **Nombre**  
 Escriba el nombre de la definición de roles. Un nombre de definición de roles debe ser único en el espacio de nombres del servidor de informes. El nombre debe incluir al menos un carácter alfanumérico. También puede incluir espacios y algunos símbolos. No utilice los caracteres siguientes al especificar un nombre:  
  
 ; ? : @ & = + , $ / * \< >  
  
 " /  
  
 **Description**  
 Escriba una descripción que explique cómo usar el rol y que especifique el rol que admite.  
  
 **Tarea**  
 Seleccione las tareas que se pueden realizar mediante este rol. No puede crear nuevas tareas ni modificar las tareas existentes que admite [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Solo las tareas de nivel de elemento pueden utilizarse en una definición de roles de nivel de elemento.  
  
 **Descripción de la tarea**  
 Muestra una descripción de la tarea con las operaciones o los permisos que ésta admite.  
  
## Vea también  
 [Servidor de informes en Management Studio ayuda F1](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)   
 [Definiciones de roles](../../reporting-services/security/role-definitions.md)  
  
  