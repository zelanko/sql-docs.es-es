---
title: Eliminación de SSMA para componentes de Oracle (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Uninstalling the Extension Pack
ms.assetid: 8b527a56-4e52-487a-9ac9-2320388e6d7d
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: 0434f88c46d14672c84f5f7939488a827b229e27
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/16/2019
ms.locfileid: "68266558"
---
# <a name="removing-ssma--for-oracle-components-oracletosql"></a>Eliminación de componentes de SSMA para Oracle (OracleToSQL)
Cuando haya terminado de migrar bases de datos de Oracle a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], es posible que desee desinstalar componentes de SSMA. Puede desinstalar los componentes de cliente en cualquier momento. Sin embargo, no debe desinstalar el paquete de extensiones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a menos que las bases de datos migradas ya no utilizan las funciones de la **ssma_oracle** esquema de la **sysdb** base de datos.  
  
## <a name="uninstalling-the-ssma-for-oracle-client"></a>Desinstalación de SSMA para el cliente de Oracle  
Puede desinstalar SSMA mediante **agregar o quitar programas**.  
  
**Para desinstalar SSMA**  
  
1.  En el Panel de Control, abra **agregar o quitar programas**.  
  
2.  Seleccione  **[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant para Oracle**y, a continuación, haga clic en **quitar**.  
  
3.  Para confirmar que desea desinstalar SSMA, haga clic en **Sí**.  
  
## <a name="uninstalling-the-extension-pack"></a>Desinstalando el paquete de extensiones  
Si está seguro de las bases de datos migrados no usan objetos en el **sysdb.ssma_oracle** esquema, puede quitar el módulo de extensión mediante **agregar o quitar programas**.  
  
**Para desinstalar el paquete de extensiones**  
  
1.  En el Panel de Control, abra **agregar o quitar programas**.  
  
2.  Seleccione **Microsoft SQL Server Migration Assistant para Oracle: paquete de extensión**y, a continuación, haga clic en **quitar**.  
  
3.  Para confirmar que desea desinstalar el paquete de extensiones, haga clic en **Sí**.  
  
4.  En las instancias con la página de secuencias de comandos de base de datos de utilidades, seleccione una instancia y, a continuación, haga clic en **siguiente**.  
  
5.  En la página parámetros de conexión, seleccione el método de autenticación y, a continuación, haga clic en **siguiente**.  
  
    Autenticación de Windows usará las credenciales de Windows para intentar iniciar sesión en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Si selecciona [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticación, debe escribir un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nombre de inicio de sesión y la contraseña.  
  
6.  En la página operación completada, haga clic en **Aceptar**.  
  
7.  En la página de finalización, haga clic en **Exit**.  
  
Después de la desinstalación, puede confirmar que los objetos en el **sysdb.ssma_oracle** esquema y, posiblemente, toda la **sysdb** base de datos, se han quitado con [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Sin embargo, si usa otros productos SSMA, también usan el **sysdb** base de datos. Si la base de datos existe y está seguro de que no hay otras bases de datos hacen referencia a objetos en esta base de datos, puede separar la base de datos.  
  
## <a name="see-also"></a>Vea también  
[Instalación de SSMA para Oracle Client &#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-for-oracle-client-oracletosql.md)  
[Instalación de componentes de SSMA en SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-components-on-sql-server-oracletosql.md)  
  
