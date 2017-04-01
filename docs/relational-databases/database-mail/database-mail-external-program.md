---
title: "Programa externo Correo electr&#243;nico de base de datos | Microsoft Docs"
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
  - "programas externos [Correo electrónico de base de datos]"
  - "DatabaseMail90.exe"
  - "Correo electrónico de base de datos [SQL Server], programas externos"
ms.assetid: bc124164-eb6e-4b7f-bf66-98a3113d02f7
caps.latest.revision: 40
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 40
---
# Programa externo Correo electr&#243;nico de base de datos
  El ejecutable externo de Correo electrónico de base de datos es **DatabaseMail.exe**, que está ubicado en el directorio **MSSQL\Binn directory** de la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Correo electrónico de base de datos utiliza la activación de Service Broker para iniciar el programa externo cuando es necesario procesar mensajes de correo electrónico. Correo electrónico de base de datos inicia una instancia del programa externo. El programa externo se ejecuta en el contexto de seguridad de la cuenta de servicio de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **En este tema:**  
  
-   [Conceptos del programa externo de Correo electrónico de base de datos](#ComponentsAndConcepts)  
  
-   [Tareas relacionadas con la configuración del programa externo de Correo electrónico de base de datos](#RelatedTasks)  
  
##  <a name="ComponentsAndConcepts"></a> Conceptos del programa externo de Correo electrónico de base de datos  
 Cuando se inicia el programa externo, se conecta a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante la autenticación de Windows y empieza a procesar los mensajes de correo electrónico. El programa termina cuando ya no hay mensajes para enviar durante el período de tiempo de espera especificado. Si lo desea, puede configurar el tiempo que el programa debe esperar antes de terminar mediante el Asistente para configuración de Correo electrónico de base de datos o los procedimientos almacenados de Correo electrónico de base de datos. Para obtener más información, vea [sysmail_configure_sp &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-configure-sp-transact-sql.md).  
  
 El programa externo almacena información de las tablas del sistema en la base de datos **msdb** . Si el programa externo no puede comunicarse con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], registrará una serie de errores en el registro de eventos de aplicación de Microsoft Windows. Se proporcionan funciones de registro de mensajes adicionales cuando el nivel de registro está establecido en **Detallado** en el cuadro de diálogo **Configurar parámetros del sistema** del **Asistente para configuración de Correo electrónico de base de datos**.  
  
 Por motivos de eficacia, el programa externo almacena en la memoria caché la información de la cuenta y del perfil. Por lo tanto, los cambios de configuración que se realicen en las cuentas y los perfiles no surtirán efecto en el programa externo hasta pasados unos minutos.  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas con la configuración del programa externo de Correo electrónico de base de datos  
  
|Tarea de configuración|Vínculo de tema|  
|------------------------|----------------|  
|Especifique el tiempo que el programa externo espera antes de salir.|[sysmail_configure_sp &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-configure-sp-transact-sql.md)|  
  
## Vea también  
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)   
 [Registro y auditorías del Correo electrónico de base de datos](../../relational-databases/database-mail/database-mail-log-and-audits.md)   
 [Correo electrónico de base de datos](../../relational-databases/database-mail/database-mail.md)  
  
  