---
title: Eliminación de SSMA para componentes de MySQL (MySQLToSql) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Uninstalling, Extension pack
- Uninstalling, SSMA for MySQL client
ms.assetid: 87cdbd49-a0c9-4b00-8a93-34188b18d11a
caps.latest.revision: 10
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: adab686126cb608ae32870a9a138720b77d212bf
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/16/2018
ms.locfileid: "40392186"
---
# <a name="removing-the-ssma-for-mysql-components-mysqltosql"></a>Eliminación de los componentes de SSMA para MySQL (MySQLToSql)
Cuando haya terminado de migrar bases de datos de MySQL a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], es posible que desee desinstalar componentes de SSMA. Puede desinstalar los componentes de cliente en cualquier momento. Sin embargo, si desinstala el paquete de extensiones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , a continuación, SSMA ya no será compatible con migración de datos de MySQL para la base de datos de destino (SQL Server o SQL Azure) mediante el motor de migración de datos del servidor.  
  
## <a name="uninstalling-the-ssma-for-mysql-client"></a>Desinstalación de SSMA para MySQL cliente  
Puede desinstalar SSMA mediante **agregar o quitar programas**.  
  
**Para desinstalar SSMA**  
  
1.  En el Panel de Control, abra **agregar o quitar programas**.  
  
2.  Seleccione **Microsoft SQL Server Migration Assistant para MySQL**y, a continuación, haga clic en **quitar**.  
  
3.  Para confirmar que desea desinstalar SSMA, haga clic en **Sí**.  
  
## <a name="uninstalling-the-extension-pack"></a>Desinstalando el paquete de extensiones  
Puede quitar el módulo de extensión mediante **agregar o quitar programas**.  
  
**Para desinstalar el paquete de extensiones**  
  
1.  En el Panel de Control, abra **agregar o quitar programas**.  
  
2.  Seleccione **Microsoft SQL Server Migration Assistant para MySQL: paquete de extensión**y, a continuación, haga clic en **quitar**.  
  
3.  Para confirmar que desea desinstalar el paquete de extensiones, haga clic en **Sí**.  
  
4.  En las instancias con la página de secuencias de comandos de base de datos de utilidades, seleccione una instancia y, a continuación, haga clic en **siguiente**.  
  
5.  En la página parámetros de conexión, seleccione el método de autenticación y, a continuación, haga clic en **siguiente**.  
  
    Autenticación de Windows usará las credenciales de Windows para intentar iniciar sesión en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Si selecciona [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticación, debe escribir un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nombre de inicio de sesión y la contraseña.  
  
6.  En la página operación completada, haga clic en **Aceptar**.  
  
7.  En la página de finalización, haga clic en **Exit**.  
  
Una vez completado el proceso de desinstalación, puede confirmar que los objetos en el **sysdb.ssma_MySQL** esquema y, posiblemente, toda la **sysdb** base de datos, se han quitado con [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Sin embargo, si usa otros productos SSMA, también usan el **sysdb** base de datos. Si la base de datos existe y está seguro de que no hay otras bases de datos hacen referencia a los objetos de esta base de datos, puede separar la base de datos.  
  
## <a name="see-also"></a>Vea también  
[Instalación de SSMA para MySQL cliente &#40;MySQLToSQL&#41;](../../ssma/mysql/installing-ssma-for-mysql-client-mysqltosql.md)  
[Instalación de componentes de SSMA en SQL Server](installing-ssma-components-on-sql-server-mysqltosql.md)  
  
