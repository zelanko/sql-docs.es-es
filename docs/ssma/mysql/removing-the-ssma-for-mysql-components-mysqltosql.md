---
title: "Eliminación de SSMA para los componentes de MySQL (MySQLToSql) | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
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
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 765696847ddb1abd44dfac3463fdfd75f9a5c97a
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="removing-the-ssma-for-mysql-components-mysqltosql"></a>Eliminación de SSMA para los componentes de MySQL (MySQLToSql)
Cuando termine de migrar bases de datos de MySQL a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], debe desinstalar los componentes SSMA. Puede desinstalar los componentes de cliente en cualquier momento. Sin embargo, si se desinstala el paquete de extensión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] , a continuación, SSMA dejará de admitir la migración de datos de MySQL a la base de datos de destino (SQL Server o SQL Azure) utilizando el motor de migración de datos de servidor.  
  
## <a name="uninstalling-the-ssma-for-mysql-client"></a>Desinstalación de SSMA para cliente de MySQL  
Puede desinstalar SSMA mediante **agregar o quitar programas**.  
  
**Para desinstalar SSMA**  
  
1.  En el Panel de Control, abra **agregar o quitar programas**.  
  
2.  Seleccione **Microsoft SQL Server Migration Assistant para MySQL**y, a continuación, haga clic en **quitar**.  
  
3.  Para confirmar que desea desinstalar SSMA, haga clic en **Sí**.  
  
## <a name="uninstalling-the-extension-pack"></a>Desinstalar el módulo de extensión  
Puede quitar el módulo de extensión mediante **agregar o quitar programas**.  
  
**Desinstalar el paquete de extensión**  
  
1.  En el Panel de Control, abra **agregar o quitar programas**.  
  
2.  Seleccione **Microsoft SQL Server Migration Assistant para MySQL: paquete de extensión**y, a continuación, haga clic en **quitar**.  
  
3.  Para confirmar que desea desinstalar el paquete de extensión, haga clic en **Sí**.  
  
4.  En las instancias con la página de secuencias de comandos de base de datos de utilidades, seleccione una instancia y, a continuación, haga clic en **siguiente**.  
  
5.  En la página parámetros de conexión, seleccione el método de autenticación y, a continuación, haga clic en **siguiente**.  
  
    Autenticación de Windows usará las credenciales de Windows para intentar iniciar sesión en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Si selecciona [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] autenticación, debe escribir una [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] nombre de inicio de sesión y una contraseña.  
  
6.  En la página operación completada, haga clic en **Aceptar**.  
  
7.  En la página de finalización, haga clic en **Exit**.  
  
Una vez completado el proceso de desinstalación, puede confirmar que los objetos en el **sysdb.ssma_MySQL** esquema y, posiblemente, todo el **sysdb** base de datos, se ha quitado mediante el uso de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]. Sin embargo, si utiliza otros productos SSMA, también usan el **sysdb** base de datos. Si la base de datos existe y está seguro de que ninguna otra base de datos hacen referencia a los objetos en esta base de datos, puede separar la base de datos.  
  
## <a name="see-also"></a>Vea también  
[Instalación de SSMA para cliente de MySQL &#40; MySQLToSQL &#41;](../../ssma/mysql/installing-ssma-for-mysql-client-mysqltosql.md)  
[Instalar componentes SSMA en SQL Server](http://msdn.microsoft.com/en-us/6772d0c5-258f-4d7b-afb0-b5f810e71af1)  
  

