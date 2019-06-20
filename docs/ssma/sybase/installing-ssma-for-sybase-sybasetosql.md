---
title: Instalación de SSMA para SAP ASE (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/29/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 8d5a4ce6-b747-46e3-9184-645d56e8b35c
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: b859c3b9841945241ac0ec9c5238a479a5ba3343
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63302817"
---
# <a name="installing-ssma-for-sap-ase-sybasetosql"></a>Instalación de SSMA para SAP ASE (SybaseToSQL)
[!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant (SSMA) para SAP Adaptive Server Enterprise (ASE) consta de una aplicación cliente que utilice para realizar una migración de SAP ASE para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Azure SQL Database. También contiene un paquete de extensión que admite la migración de datos y el uso de funciones del sistema ASE en las bases de datos migrados.  
  
Instale la aplicación cliente en el equipo desde el que va a realizar los pasos de migración. Instalar los archivos del módulo de extensión en el equipo que ejecuta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en cuáles son las bases de datos migradas a hospedarse.  
  
## <a name="upgrading-ssma-for-sap-ase"></a>Actualización de SSMA para SAP ASE  
Si desea actualizar a una versión posterior de SSMA para SAP ASE, primero debe desinstalar el cliente y el paquete de extensiones de servidor. A continuación, instale la versión más reciente.  
  
Si abre un proyecto desde una versión anterior de SSMA para SAP ASE, SSMA le pregunta si desea convertir el proyecto a la versión más reciente. Haga clic en **Sí** para trabajar con el proyecto en la versión más reciente de SSMA.  
  
## <a name="contents"></a>Contenido  
  
|Artículo|Descripción|  
|---------|---------------|  
|[Instalación de SSMA para SAP ASE cliente &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-client-sybasetosql.md)|Proporciona información sobre e instrucciones para la instalación de SSMA para el cliente de SAP ASE.|  
|[Instalación de componentes de SSMA en SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md)|Proporciona información sobre e instrucciones para instalar el módulo de extensión en instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[Eliminación de SSMA para los componentes SAP ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/removing-ssma-for-sybase-components-sybasetosql.md)|Proporciona instrucciones para desinstalar al cliente de paquete de programa y la extensión.|  
  
## <a name="see-also"></a>Vea también  
[Migración de SAP ASE bases de datos a SQL Server: base de datos de SQL Azure &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
