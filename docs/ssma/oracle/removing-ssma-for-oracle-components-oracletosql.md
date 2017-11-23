---
title: "Eliminación de SSMA para los componentes de Oracle (OracleToSQL) | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Uninstalling the Extension Pack
ms.assetid: 8b527a56-4e52-487a-9ac9-2320388e6d7d
caps.latest.revision: "6"
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: Inactive
ms.openlocfilehash: e0dea581d93f996f710a64bf35c8d208740b1d17
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="removing-ssma--for-oracle-components-oracletosql"></a>Eliminación de SSMA para los componentes de Oracle (OracleToSQL)
Cuando termine de migrar bases de datos de Oracle en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], debe desinstalar los componentes SSMA. Puede desinstalar los componentes de cliente en cualquier momento. Sin embargo, no debe desinstalar el paquete de extensión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] a menos que las bases de datos migrados ya no use las funciones de la **ssma_oracle** esquema de la **sysdb** base de datos.  
  
## <a name="uninstalling-the-ssma-for-oracle-client"></a>Desinstalación de SSMA para cliente de Oracle  
Puede desinstalar SSMA mediante **agregar o quitar programas**.  
  
**Para desinstalar SSMA**  
  
1.  En el Panel de Control, abra **agregar o quitar programas**.  
  
2.  Seleccione  **[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Migration Assistant para Oracle**y, a continuación, haga clic en **quitar**.  
  
3.  Para confirmar que desea desinstalar SSMA, haga clic en **Sí**.  
  
## <a name="uninstalling-the-extension-pack"></a>Desinstalar el módulo de extensión  
Si está seguro de las bases de datos migradas no usan objetos en el **sysdb.ssma_oracle** esquema, puede quitar el módulo de extensión mediante **agregar o quitar programas**.  
  
**Desinstalar el paquete de extensión**  
  
1.  En el Panel de Control, abra **agregar o quitar programas**.  
  
2.  Seleccione **Microsoft SQL Server Migration Assistant para Oracle: paquete de extensión**y, a continuación, haga clic en **quitar**.  
  
3.  Para confirmar que desea desinstalar el paquete de extensión, haga clic en **Sí**.  
  
4.  En las instancias con la página de secuencias de comandos de base de datos de utilidades, seleccione una instancia y, a continuación, haga clic en **siguiente**.  
  
5.  En la página parámetros de conexión, seleccione el método de autenticación y, a continuación, haga clic en **siguiente**.  
  
    Autenticación de Windows usará las credenciales de Windows para intentar iniciar sesión en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Si selecciona [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] autenticación, debe escribir una [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] nombre de inicio de sesión y una contraseña.  
  
6.  En la página operación completada, haga clic en **Aceptar**.  
  
7.  En la página de finalización, haga clic en **Exit**.  
  
Después de la desinstalación, puede confirmar que los objetos en el **sysdb.ssma_oracle** esquema y, posiblemente, todo el **sysdb** base de datos, se ha quitado mediante el uso de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]. Sin embargo, si utiliza otros productos SSMA, también usan el **sysdb** base de datos. Si la base de datos existe y está seguro de que ninguna otra base de datos hacen referencia a objetos en esta base de datos, puede separar la base de datos.  
  
## <a name="see-also"></a>Vea también  
[Instalación de SSMA para cliente de Oracle &#40; OracleToSQL &#41;](../../ssma/oracle/installing-ssma-for-oracle-client-oracletosql.md)  
[Instalación de componentes SSMA en SQL Server &#40; OracleToSQL &#41;](../../ssma/oracle/installing-ssma-components-on-sql-server-oracletosql.md)  
  
