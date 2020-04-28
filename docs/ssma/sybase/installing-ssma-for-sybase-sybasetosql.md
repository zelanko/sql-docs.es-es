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
ms.openlocfilehash: 91a4dfcf8add3900c51e33a6e40fa874ce9f9798
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "68028975"
---
# <a name="installing-ssma-for-sap-ase-sybasetosql"></a>Instalación de SSMA para SAP ASE (SybaseToSQL)
[!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Migration Assistant (SSMA) para SAP Adaptive Server Enterprise (ASE) se compone de una aplicación cliente que se utiliza para realizar una migración desde el ASE [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de SAP a o Azure SQL Database. También contiene un paquete de extensión que admite la migración de datos y el uso de funciones del sistema ASE en las bases de datos migradas.  
  
Instale la aplicación cliente en el equipo desde el que va a realizar los pasos de migración. Instale los archivos del paquete de extensión en el equipo que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ejecuta en el que se van a hospedar las bases de datos migradas.  
  
## <a name="upgrading-ssma-for-sap-ase"></a>Actualización de SSMA para SAP ASE  
Si desea actualizar a una versión posterior de SSMA para SAP ASE, primero debe desinstalar el cliente y el paquete de extensiones de servidor. A continuación, instale la versión más reciente.  
  
Si abre un proyecto de una versión anterior de SSMA para SAP ASE, SSMA le pregunta si desea convertir el proyecto a la versión más reciente. Haga clic en **sí** para trabajar con el proyecto en la versión más reciente de SSMA.  
  
## <a name="contents"></a>Contenido  
  
|Artículo|Descripción|  
|---------|---------------|  
|[Instalación de SSMA para el cliente de SAP ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-client-sybasetosql.md)|Proporciona información e instrucciones para instalar el cliente de SSMA para SAP ASE.|  
|[Instalación de componentes de SSMA en SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md)|Proporciona información e instrucciones para instalar el paquete de extensión en las instancias [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]de.|  
|[Quitar SSMA para componentes de SAP ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/removing-ssma-for-sybase-components-sybasetosql.md)|Proporciona instrucciones para desinstalar el programa cliente y el paquete de extensión.|  
  
## <a name="see-also"></a>Consulte también  
[Migración de bases de datos de SAP ASE a SQL Server Azure SQL Database &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
