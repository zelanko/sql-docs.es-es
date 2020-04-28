---
title: Quitar los componentes de SSMA para MySQL (MySQLToSql) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Uninstalling, Extension pack
- Uninstalling, SSMA for MySQL client
ms.assetid: 87cdbd49-a0c9-4b00-8a93-34188b18d11a
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 3a5d6d1234cc294cc8e8cdd163ce8a9bd6ac3e3f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "67929384"
---
# <a name="removing-the-ssma-for-mysql-components-mysqltosql"></a>Eliminación de los componentes de SSMA para MySQL (MySQLToSql)
Cuando haya terminado de migrar las bases de datos de MySQL [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]a, es posible que desee desinstalar los componentes de SSMA. Puede desinstalar los componentes de cliente en cualquier momento. Sin embargo, Si desinstala el paquete de extensión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , SSMA dejará de admitir la migración de datos de MySQL a la base de datos de destino (SQL Server/SQL Azure) mediante el motor de migración de datos del lado servidor.  
  
## <a name="uninstalling-the-ssma-for-mysql-client"></a>Desinstalación de SSMA para el cliente MySQL  
Puede desinstalar SSMA mediante **Agregar o quitar programas**.  
  
**Para desinstalar SSMA**  
  
1.  En el Panel de control, abra **Agregar o quitar programas**.  
  
2.  Seleccione **Microsoft SQL Server Migration Assistant para MySQL**y, a continuación, haga clic en **quitar**.  
  
3.  Para confirmar que desea desinstalar SSMA, haga clic en **sí**.  
  
## <a name="uninstalling-the-extension-pack"></a>Desinstalación del paquete de extensiones  
Puede quitar el paquete de extensión mediante **Agregar o quitar programas**.  
  
**Para desinstalar el paquete de extensiones**  
  
1.  En el Panel de control, abra **Agregar o quitar programas**.  
  
2.  Seleccione **Microsoft SQL Server Migration Assistant para el paquete de extensiones de MySQL**y, a continuación, haga clic en **quitar**.  
  
3.  Para confirmar que desea desinstalar el paquete de extensión, haga clic en **sí**.  
  
4.  En la página instancias con scripts de base de datos de utilidades, seleccione una instancia y, a continuación, haga clic en **siguiente**.  
  
5.  En la página parámetros de conexión, seleccione el método de autenticación y, a continuación, haga clic en **siguiente**.  
  
    La autenticación de Windows utilizará las credenciales de Windows para intentar iniciar sesión en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]la instancia de. Si selecciona [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticación, debe escribir un nombre de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inicio de sesión y una contraseña.  
  
6.  En la página operación completada, haga clic en **Aceptar**.  
  
7.  En la página finalizar, haga clic en **salir**.  
  
Una vez completado el proceso de desinstalación, puede confirmar que los objetos del esquema **sysdb. ssma_MySQL** y, posiblemente, toda la base de datos de **sysdb** , se [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]han quitado mediante. Sin embargo, si utiliza otros productos de SSMA, también usarán la base de datos **sysdb** . Si la base de datos existe y está seguro de que no hay ninguna otra base de datos que haga referencia a los objetos de esta base de datos, puede separar la base de datos.  
  
## <a name="see-also"></a>Consulte también  
[Instalación de SSMA para MySQL Client &#40;MySQLToSQL&#41;](../../ssma/mysql/installing-ssma-for-mysql-client-mysqltosql.md)  
[Instalación de componentes de SSMA en SQL Server](installing-ssma-components-on-sql-server-mysqltosql.md)  
  
