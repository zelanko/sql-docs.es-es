---
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
ms.openlocfilehash: f0be2586d83aaf859ba6b5f4b57f08a4d679b9be
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "68109882"
---
# <a name="check-integrity-of-database-with-suspect-pages"></a>Comprobar la integridad de una base de datos con páginas sospechosas
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Esta regla comprueba las bases de datos de usuario que tienen el estado de base de datos establecido en sospechoso. Cuando el [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] lee una página de base de datos que contiene un error 824, la página se considera sospechosa, su identificador se registra en la tabla suspect_pages de msdb y la base de datos que la contiene se establece como sospechosa.  
  
 El error 824 indica que se detectó un error de coherencia lógica durante una operación de lectura. Este error suele indicar que los datos se han dañado debido a un componente del subsistema de E/S defectuoso. Se trata de una condición de error grave que amenaza la integridad de la base de datos y que se debe corregir de inmediato.  
  
## <a name="best-practices-recommendations"></a>Prácticas recomendadas  
  
-   Revise el registro de errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para obtener los detalles del error 824 para esta base de datos.  
  
-   Realice una comprobación completa de coherencia de la base de datos ([DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)).  
  
-   Implemente las acciones del usuario que se definen en [MSSQLSERVER_824](https://go.microsoft.com/fwlink/?LinkId=81397).  
  
## <a name="for-more-information"></a>Para obtener más información  
 [Administrar la tabla suspect_pages &#40;SQL Server&#41;](../../relational-databases/backup-restore/manage-the-suspect-pages-table-sql-server.md)  
  
  
