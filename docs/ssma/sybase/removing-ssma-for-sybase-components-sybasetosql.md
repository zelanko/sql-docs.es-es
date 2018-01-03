---
title: "Eliminación de SSMA para Sybase componentes (SybaseToSQL) | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-sybase
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: aec09593-17d9-4ec2-ac56-3cd8851406fd
caps.latest.revision: "6"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b10969b1335ed8ba3d46303f15cbc68a34cc4b7b
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="removing-ssma-for-sybase-components-sybasetosql"></a>Eliminación de SSMA para Sybase componentes (SybaseToSQL)
Cuando termine de migrar bases de datos de Sybase Adaptive Server Enterprise (ASE) a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], debe desinstalar los componentes SSMA. Puede desinstalar los componentes de cliente en cualquier momento, pero no debe desinstalar el paquete de extensión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] a menos que esté seguro de que las bases de datos migrados ya no utilizarán las funciones de la **ssma_syb** esquema de la **sysdb** base de datos.  
  
## <a name="uninstalling-the-ssma-for-sybase-client"></a>Desinstalación de SSMA para Sybase cliente  
Puede desinstalar SSMA mediante **agregar o quitar programas**.  
  
**Para desinstalar SSMA**  
  
1.  En el Panel de Control, abra **agregar o quitar programas**.  
  
2.  Seleccione **Microsoft SQL Server Migration Assistant para Sybase**y, a continuación, haga clic en **quitar**.  
  
3.  Para confirmar que desea desinstalar SSMA, haga clic en **Sí**.  
  
## <a name="uninstalling-the-extension-pack"></a>Desinstalar el módulo de extensión  
Si está seguro de las bases de datos migradas no usan objetos en el **sysdb.ssma_syb** esquema, puede quitar el módulo de extensión mediante **agregar o quitar programas**.  
  
Desinstalar el paquete de extensión  
  
1.  En el Panel de Control, abra **agregar o quitar programas**.  
  
2.  Seleccione **Microsoft SQL Server Migration Assistant para Sybase: paquete de extensión**y, a continuación, haga clic en **quitar**.  
  
3.  Para confirmar que desea desinstalar el paquete de extensión, haga clic en **Sí**.  
  
4.  En las instancias con la página de secuencias de comandos de base de datos de utilidades, haga clic en **siguiente**.  
  
5.  En la página parámetros de conexión, seleccione el método de autenticación y, a continuación, haga clic en **siguiente**.  
  
    Autenticación de Windows usará las credenciales de Windows para intentar iniciar sesión en la instancia de SQL Server. Si selecciona autenticación de SQL Server, debe escribir un nombre de inicio de sesión de SQL Server y una contraseña.  
  
6.  En la página operación completada, haga clic en **Aceptar**.  
  
7.  En la página de finalización, haga clic en **Exit**.  
  
Después de desinstalar, puede confirmar que la **sysdb.ssma_syb** esquema y, posiblemente, todo el **sysdb** base de datos, se ha quitado mediante el uso de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]. Sin embargo, si utiliza otros productos SSMA, también usan el **sysdb** base de datos. Si la base de datos existe y está seguro de que ninguna otra base de datos hacen referencia a objetos en esta base de datos, puede separar la base de datos.  
  
## <a name="see-also"></a>Vea también  
[Instalación de SSMA para Sybase cliente &#40; SybaseToSQL &#41;](../../ssma/sybase/installing-ssma-for-sybase-client-sybasetosql.md)  
[Instalar componentes SSMA de SQL Server &#40; SybaseToSQL &#41;](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md)  
  
