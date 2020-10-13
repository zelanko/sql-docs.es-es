---
description: Comprobar la integridad de una base de datos con páginas sospechosas
title: Comprobación de la integridad de una base de datos con páginas sospechosas | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 3b1ec9fe-f6c5-46f7-aa63-6e671be1572d
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: fb78aa2fce1a416f280a1a62da723335366eb6f7
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/09/2020
ms.locfileid: "91892185"
---
# <a name="check-integrity-of-database-with-suspect-pages"></a>Comprobar la integridad de una base de datos con páginas sospechosas
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Esta regla comprueba las bases de datos de usuario que tienen el estado de base de datos establecido en sospechoso. Cuando el [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] lee una página de base de datos que contiene un error 824, la página se considera sospechosa, su identificador se registra en la tabla suspect_pages de msdb y la base de datos que la contiene se establece como sospechosa.  
  
 El error 824 indica que se detectó un error de coherencia lógica durante una operación de lectura. Este error suele indicar que los datos se han dañado debido a un componente del subsistema de E/S defectuoso. Se trata de una condición de error grave que amenaza la integridad de la base de datos y que se debe corregir de inmediato.  
  
## <a name="best-practices-recommendations"></a>Prácticas recomendadas  
  
-   Revise el registro de errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para obtener los detalles del error 824 para esta base de datos.  
  
-   Realice una comprobación completa de coherencia de la base de datos ([DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)).  
  
-   Implemente las acciones del usuario que se definen en [MSSQLSERVER_824](/previous-versions/sql/sql-server-2016/aa337274(v=sql.130)).  
  
## <a name="for-more-information"></a>Para obtener más información  
 [Administrar la tabla suspect_pages &#40;SQL Server&#41;](../../relational-databases/backup-restore/manage-the-suspect-pages-table-sql-server.md)  
  
