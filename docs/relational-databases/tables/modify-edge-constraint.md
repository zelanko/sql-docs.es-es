---
title: Modificación de restricciones perimetrales | Microsoft Docs
ms.custom: ''
ms.date: 09/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- alter edge constraints
- edge constraints [SQL Server]
- CONNECTION constraints
- edge constraints [Azure SQL Database]
- graph edge constraints
- SQL Graph
ms.assetid: ''
author: shkale-msft
ms.author: shkale
manager: craigg
monikerRange: '>=sql-server-2017||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e5b6a471156f0b1371c727ce96aac72f4f812dac
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62693305"
---
# <a name="modify-edge-constraints"></a>Modificación de restricciones perimetrales
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx.md](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

  Puede modificar una restricción perimetral en [!INCLUDE[ssNoversion](../../includes/ssnoversion-md.md)] mediante [!INCLUDE[tsql](../../includes/tsql-md.md)]. Puede modificar la restricción perimetral de una tabla perimetral cambiando el orden de cláusula de restricción perimetral o agregando una nueva cláusula.  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Seguridad](#Security)  
  
-   **Para modificar una restricción perimetral con:**  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Requiere el permiso ALTER en la tabla.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL
 Para modificar una restricción perimetral mediante Transact-SQL, deberá eliminar la restricción perimetral existente y, a continuación, volver a crearla con la nueva definición. Para obtener más información, consulte [Delete Edge Constraints](../../relational-databases/tables/delete-edge-constraint.md) y [Create Edge Constraints](../../relational-databases/tables/create-edge-constraints.md).    
 
