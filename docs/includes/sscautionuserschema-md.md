---
ms.openlocfilehash: 327fd6bac9bc1036a0dd07f7b955ee92cb7e40c8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68223540"
---
  El comportamiento de los esquemas cambió en SQL Server 2005. En consecuencia, el código que supone que los esquemas son equivalentes a los usuarios de base de datos puede dejar de devolver resultados correctos. No se deben usar vistas de catálogo antiguas, como sysobjects, en una base de datos en la que nunca se ha utilizado ninguna de las instrucciones DDL siguientes: CREATE SCHEMA, ALTER SCHEMA, DROP SCHEMA, CREATE USER, ALTER USER, DROP USER, CREATE ROLE, ALTER ROLE, DROP ROLE, CREATE APPROLE, ALTER APPROLE, DROP APPROLE, ALTER AUTHORIZATION. En esas bases de datos, debe usar las nuevas vistas de catálogo. En las nuevas vistas de catálogo se tiene en cuenta la separación de entidades de seguridad y esquemas que se estableció en SQL Server 2005. Para obtener más información sobre las vistas de catálogo, vea [Vistas de catálogo &#40;Transact-SQL&#41;](../relational-databases/system-catalog-views/catalog-views-transact-sql.md).
   