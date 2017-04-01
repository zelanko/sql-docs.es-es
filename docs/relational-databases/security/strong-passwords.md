---
title: "Contrase&#241;as seguras | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "inicios de sesión [SQL Server], contraseñas"
  - "contraseñas [SQL Server], seguras"
  - "símbolos [SQL Server]"
  - "seguridad [SQL Server], contraseñas"
  - "contraseñas [SQL Server], símbolos"
  - "caracteres [SQL Server], directivas de contraseñas"
  - "contraseñas seguras [SQL Server]"
ms.assetid: 338548f4-c4d8-47ca-b597-5c9c0f2fa205
caps.latest.revision: 30
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 30
---
# Contrase&#241;as seguras
  Las contraseñas pueden constituir el vínculo más débil de una implementación de seguridad de servidor. Debe tener siempre mucho cuidado a la hora de elegir una contraseña. Una contraseña segura presenta las siguientes características:  
  
-   Tiene una longitud de 8 caracteres como mínimo.  
  
-   Contiene una combinación de letras, números y símbolos.  
  
-   No es una palabra que pueda encontrarse en el diccionario.  
  
-   No es el nombre de un comando.  
  
-   No es el nombre de una persona.  
  
-   No es el nombre de un usuario.  
  
-   No es el nombre de un equipo.  
  
-   Se cambia con frecuencia.  
  
-   Presenta diferencias notables con respecto a contraseñas anteriores.  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pueden contener hasta 128 caracteres, entre los que se pueden incluir letras, símbolos y dígitos. Dado que los inicios de sesión, nombres de usuario, roles y contraseñas se utilizan con frecuencia en instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)], determinados símbolos deberán estar incluidos entre comillas dobles (") o corchetes ([ ]). Utilice estos delimitadores en las instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] cuando el inicio de sesión, usuario, rol o contraseña de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] presente las siguientes características:  
  
-   Contiene o comienza por un carácter de espacio.  
  
-   Comienza por el carácter $ o @.  
  
 Si se utiliza en una cadena de conexión OLE DB u ODBC, el inicio de sesión o la contraseña no deben contener ninguno de los siguientes caracteres: [] {}() , ; ? * ! @. Estos caracteres se usan para inicializar una conexión o para separar valores de conexión.  
  
## Contenido relacionado  
 [Directiva de contraseñas](../../relational-databases/security/password-policy.md)  
  
  