---
title: Eliminación de SSMA para Sybase (SybaseToSQL) los componentes | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: aec09593-17d9-4ec2-ac56-3cd8851406fd
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: b3cebc9bb82778390716212fd3b5ae1bf800d3d3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62667939"
---
# <a name="removing-ssma-for-sybase-components-sybasetosql"></a>Eliminación de componentes de SSMA para Sybase (SybaseToSQL)
Cuando haya terminado de migrar bases de datos de Sybase Adaptive Server Enterprise (ASE) a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], es posible que desee desinstalar componentes de SSMA. Puede desinstalar los componentes de cliente en cualquier momento, pero no debe desinstalar el paquete de extensiones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a menos que esté seguro de que las bases de datos migradas ya no usar funciones en el **ssma_syb** esquema de la **sysdb** base de datos.  
  
## <a name="uninstalling-the-ssma-for-sybase-client"></a>Desinstalación de SSMA para Sybase cliente  
Puede desinstalar SSMA mediante **agregar o quitar programas**.  
  
**Para desinstalar SSMA**  
  
1.  En el Panel de Control, abra **agregar o quitar programas**.  
  
2.  Seleccione **Microsoft SQL Server Migration Assistant para Sybase**y, a continuación, haga clic en **quitar**.  
  
3.  Para confirmar que desea desinstalar SSMA, haga clic en **Sí**.  
  
## <a name="uninstalling-the-extension-pack"></a>Desinstalando el paquete de extensiones  
Si está seguro de las bases de datos migrados no usan objetos en el **sysdb.ssma_syb** esquema, puede quitar el módulo de extensión mediante **agregar o quitar programas**.  
  
Para desinstalar el paquete de extensiones  
  
1.  En el Panel de Control, abra **agregar o quitar programas**.  
  
2.  Seleccione **Microsoft SQL Server Migration Assistant para Sybase: paquete de extensión**y, a continuación, haga clic en **quitar**.  
  
3.  Para confirmar que desea desinstalar el paquete de extensiones, haga clic en **Sí**.  
  
4.  En las instancias con la página de secuencias de comandos de base de datos de utilidades, haga clic en **siguiente**.  
  
5.  En la página parámetros de conexión, seleccione el método de autenticación y, a continuación, haga clic en **siguiente**.  
  
    Autenticación de Windows usará las credenciales de Windows para intentar iniciar sesión en la instancia de SQL Server. Si selecciona autenticación de SQL Server, debe escribir un nombre de inicio de sesión de SQL Server y una contraseña.  
  
6.  En la página operación completada, haga clic en **Aceptar**.  
  
7.  En la página de finalización, haga clic en **Exit**.  
  
Después de desinstalar, puede confirmar que el **sysdb.ssma_syb** esquema y, posiblemente, toda la **sysdb** base de datos, se han quitado con [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Sin embargo, si usa otros productos SSMA, también usan el **sysdb** base de datos. Si la base de datos existe y está seguro de que no hay otras bases de datos hacen referencia a objetos en esta base de datos, puede separar la base de datos.  
  
## <a name="see-also"></a>Vea también  
[Instalación de SSMA para Sybase cliente &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-client-sybasetosql.md)  
[Instalación de componentes de SSMA en SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md)  
  
