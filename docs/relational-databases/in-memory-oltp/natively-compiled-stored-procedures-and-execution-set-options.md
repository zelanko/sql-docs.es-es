---
title: Procedimientos almacenados compilados de forma nativa y opciones SET
description: Las opciones SET de una sesión no afectan a la ejecución de un procedimiento almacenado, salvo que determinadas opciones SET hacen que los procedimientos almacenados no se ejecuten.
ms.custom: seo-dt-2019
ms.date: 10/26/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: c1869cf7-9030-4d18-85d6-0e419a4e9af7
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e86ab52348e4e51a2b060bab50aecf2d3c453fc3
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97485287"
---
# <a name="natively-compiled-stored-procedures-and-execution-set-options"></a>Procedimientos almacenados compilados de forma nativa y opciones SET de ejecución.
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Las opciones de sesión se fijan en bloques atomic, como se describe en [Bloques ATOMIC](atomic-blocks-in-native-procedures.md). La ejecución de un procedimiento almacenado no se ve afectada por las opciones SET de una sesión, puesto que se necesitan bloques atomic. Sin embargo, ciertas opciones SET, como SET NOEXEC y SET SHOWPLAN_XML, causan que no se ejecuten los procedimientos almacenados (incluidos los compilados de forma nativa).   
  
 Cuando un procedimiento almacenado de forma nativa se ejecuta con la opción STATISTICS activada, las estadísticas se obtienen para el procedimiento en su conjunto y no para cada instrucción. Para obtener más información, vea [SET STATISTICS IO &#40;Transact-SQL&#41;](../../t-sql/statements/set-statistics-io-transact-sql.md), [SET STATISTICS PROFILE &#40;Transact-SQL&#41;](../../t-sql/statements/set-statistics-profile-transact-sql.md), [SET STATISTICS TIME &#40;Transact-SQL&#41;](../../t-sql/statements/set-statistics-time-transact-sql.md) y [SET STATISTICS XML &#40;Transact-SQL&#41;](../../t-sql/statements/set-statistics-xml-transact-sql.md). Para obtener estadísticas de ejecución de nivel de instrucción para los procedimientos almacenados compilados de forma nativa, use una sesión de eventos extendidos en el evento sp_statement_completed, que se inicia cuando finaliza cada una de las consultas de una ejecución de procedimientos almacenados. Para obtener más información sobre cómo crear sesiones de eventos extendidos, vea [CREATE EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/create-event-session-transact-sql.md).  
  
 **SHOWPLAN_XML** se admite para procedimientos almacenados compilados de forma nativa. **SHOWPLAN_ALL** y **SHOWPLAN_TEXT** no son compatibles con los procedimientos almacenados compilados de forma nativa.  
  
 **SET FMTONLY** no es compatible con los procedimientos almacenados compilados de forma nativa. Use en su lugar [sp_describe_first_result_set &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md).  
  
## <a name="see-also"></a>Consulte también  
 [Procedimientos almacenados compilados de forma nativa](./a-guide-to-query-processing-for-memory-optimized-tables.md)  
  
