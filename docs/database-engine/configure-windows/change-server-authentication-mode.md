---
title: Cambiar el modo de autenticación del servidor | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- sa account
- authentication [SQL Server], changing modes
- server authentication mode [SQL Server]
- modifying server authentication mode
ms.assetid: 79babcf8-19fd-4495-b8eb-453dc575cac0
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: a688bae85e0ea6bd30bbde50df0151a97fd6f505
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68012990"
---
# <a name="change-server-authentication-mode"></a>Cambiar el modo de autenticación del servidor
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  En este tema se describe cómo cambiar el modo de autenticación del servidor en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Durante la instalación, [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] se establece en **Modo de autenticación de Windows** o **Modo de autenticación de Windows y SQL Server**. Tras la instalación, puede cambiar el modo de autenticación en cualquier momento.  
  
 Si se selecciona **Modo de autenticación de Windows** durante la instalación, el inicio de sesión de sa está deshabilitado y el programa de instalación asigna una contraseña. Si posteriormente se cambia al **Modo de autenticación de Windows y SQL Server**, el inicio de sesión de sa permanece deshabilitado. Para usar el inicio de sesión de sa, use la instrucción ALTER LOGIN para habilitar el inicio de sesión de sa y asignar una nueva contraseña. El inicio de sesión de sa solo se puede conectar al servidor mediante la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Seguridad](#Security)  
  
-   **Para cambiar el modo de autenticación del servidor, utilizando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Security"></a> Seguridad  
 La cuenta sa es una cuenta conocida de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y suele ser el objetivo de los usuarios malintencionados. No habilite la cuenta sa a menos que su aplicación lo requiera. Es muy importante que utilice una contraseña segura para el inicio de sesión de sa.  
  
##  <a name="SSMSProcedure"></a> Uso de SQL Server Management Studio  
  
#### <a name="to-change-security-authentication-mode"></a>Para cambiar el modo de autenticación de seguridad  
  
1.  En el Explorador de objetos de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , haga clic con el botón derecho en el servidor y, después, haga clic en **Propiedades**.  
  
2.  En la página **Seguridad** , bajo **Autenticación de servidor**, seleccione el nuevo modo de autenticación del servidor y haga clic en **Aceptar**.  
  
3.  En el cuadro de diálogo [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , haga clic en **Aceptar** para confirmar el requisito de reiniciar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
4.  En el Explorador de objetos, haga clic con el botón derecho en el servidor y, después, haga clic en **Reiniciar**. Si el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se está ejecutando, también debe reiniciarse.  
  
#### <a name="to-enable-the-sa-login"></a>Para habilitar el inicio de sesión sa  
  
1.  En el Explorador de objetos, expanda **Seguridad**, expanda Inicios de sesión, haga clic con el botón derecho en **sa**y, después, haga clic en **Propiedades**.  
  
2.  En la página **General** , quizás tenga que crear y confirmar una contraseña para el inicio de sesión.  
  
3.  En la página **Estado** , en la sección **Inicio de sesión** , haga clic en **Habilitado**y, a continuación, en **Aceptar**.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 **Para habilitar el inicio de sesión sa**  
  
1.  En el Explorador de objetos, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue uno de los ejemplos siguientes en la ventana de consulta y haga clic en **Ejecutar**. 


    -  En el ejemplo siguiente se habilita el inicio de sesión de sa y se establece una nueva contraseña.  
  
       ```sql  
       ALTER LOGIN sa ENABLE ;  
       GO  
       ALTER LOGIN sa WITH PASSWORD = '<enterStrongPasswordHere>' ;  
       GO  
       ```  
    -  En el ejemplo siguiente se cambia la autenticación del servidor de modo mixto (Windows+SQL) a solo Windows.

       ```sql
       USE [master]
       GO
       EXEC xp_instance_regwrite N'HKEY_LOCAL_MACHINE', 
                                 N'Software\Microsoft\MSSQLServer\MSSQLServer',      
                                 N'LoginMode', REG_DWORD, 1
       GO
       ```
  
## <a name="see-also"></a>Consulte también  
 [Contraseñas seguras](../../relational-databases/security/strong-passwords.md)   
 [Consideraciones de seguridad para una instalación de SQL Server](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)   
 [ALTER LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/alter-login-transact-sql.md)   
 [Conectarse a SQL Server cuando los administradores del sistema no tienen acceso](../../database-engine/configure-windows/connect-to-sql-server-when-system-administrators-are-locked-out.md)  
  
  
