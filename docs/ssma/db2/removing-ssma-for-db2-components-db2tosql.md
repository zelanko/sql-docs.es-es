---
title: Eliminación de SSMA para DB2 componentes (DB2ToSQL) | Microsoft Docs
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
ms.assetid: 4ee0d698-6246-48eb-b963-d62be81cab6a
caps.latest.revision: 6
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 6f93ca145c96e2cc9b6d86e0ebc8c2c9899afad9
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/14/2018
ms.locfileid: "40394104"
---
# <a name="removing-ssma-for-db2-components-db2tosql"></a>Eliminación de SSMA para DB2 componentes (DB2ToSQL)
Cuando haya terminado de migrar bases de datos desde DB2 a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], es posible que desee desinstalar componentes de SSMA. Puede desinstalar los componentes de cliente en cualquier momento. Sin embargo, no debe desinstalar el paquete de extensiones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a menos que las bases de datos migradas ya no utilizan las funciones de la **ssma_DB2** esquema de la **sysdb** base de datos.  
  
## <a name="uninstalling-the-ssma-for-db2-client"></a>Desinstalación de SSMA para DB2 cliente  
Puede desinstalar SSMA mediante **agregar o quitar programas**.  
  
**Para desinstalar SSMA**  
  
1.  En el Panel de Control, abra **agregar o quitar programas**.  
  
2.  Seleccione  **[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant para DB2**y, a continuación, haga clic en **quitar**.  
  
3.  Para confirmar que desea desinstalar SSMA, haga clic en **Sí**.  
  
## <a name="uninstalling-the-extension-pack"></a>Desinstalando el paquete de extensiones  
Si está seguro de las bases de datos migrados no usan objetos en el **sysdb.ssma_DB2** esquema, puede quitar el módulo de extensión eliminándolo del esquema: no hay es ninguna desinstalación de Windows  
  
## <a name="see-also"></a>Vea también  
[Instalación de SSMA para DB2 cliente &#40;DB2ToSQL&#41;](../../ssma/db2/installing-ssma-for-db2-client-db2tosql.md)  
[Instalación de componentes de SSMA en SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/installing-ssma-components-on-sql-server-db2tosql.md)  
  
