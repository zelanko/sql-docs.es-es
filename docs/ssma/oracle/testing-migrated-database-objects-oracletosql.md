---
title: Pruebas migran objetos de base de datos (OracleToSQL) | Documentos de Microsoft
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: f03ef5e1-66e6-4c84-ada2-252dd5ada82f
caps.latest.revision: 7
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 3b908317227b497911084e4c5de1c27ccb8361d1
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2018
ms.locfileid: "34778021"
---
# <a name="testing-migrated-database-objects-oracletosql"></a>Pruebas migran objetos de base de datos (OracleToSQL)
[!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Migration Assistant para Oracle evaluador (SSMA evaluador) prueba automáticamente la conversión del objeto de base de datos y la migración de datos realizadas por SSMA. Después de que haya finalizado todos los pasos de migración de SSMA, use SSMA evaluador para comprobar que los objetos convertidos funcionan del mismo modo y que todos los datos se transfirió correctamente.  
  
Puede probar los siguientes tipos de objeto con la herramienta de comprobación de SSMA:  
  
-   Tablas  
  
-   Procedimientos almacenados, incluidos empaquetadas.  
  
-   Funciones definidas por el usuario, incluidos los empaquetan funciones.  
  
-   Vistas.  
  
-   Instrucciones independientes.  
  
SSMA evaluador ejecuta objetos seleccionados para realizar pruebas en Oracle y sus homólogos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. A continuación, compara los resultados según los criterios siguientes:  
  
-   ¿Son los cambios en los datos de la tabla idénticas?  
  
-   ¿Son los valores de parámetros de salida para los procedimientos y funciones idénticas?  
  
-   ¿Las funciones devuelven los mismos resultados?  
  
-   ¿Son que los conjuntos de resultados idéntico?  
  
> [!NOTE]  
> ¡Atención! Nunca utilice SSMA evaluador en sistemas de producción. Durante la ejecución de la herramienta de comprobación se modifican el esquema de origen y los datos. Mientras tanto, la restauración completa del estado original puede ser imposible para algunos tipos de código probado.  
  
## <a name="prerequisites"></a>Requisitos previos  
Si desea usar la herramienta de comprobación de SSMA, instalar el módulo de extensión de SSMA Oracle con el **instalar bases de datos de evaluador** opción activada.  
  
Para habilitar la comparación de los datos resultantes de la tabla, establecer el **columna generar ROWID** opción **Sí** antes de que comience la conversión de esquema. SSMA agregará una columna ROWID a todas las tablas durante la ejecución de la **convertir esquema** comando.  
  
Además, compruebe lo siguiente:  
  
-   Herramientas de cliente de Oracle están instaladas en el equipo donde [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] se ejecuta.  
  
-   Se ha habilitado la integración de Common Language Runtime (CLR) en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] motor de base de datos.  
  
Tenga en cuenta que la versión actual de la herramienta de comprobación de SSMA no admite la ejecución en paralelo por usuarios diferentes en el mismo servidor de origen o de destino.  
  
## <a name="getting-started"></a>Introducción  
[Crear casos de prueba &#40;OracleToSQL&#41;](../../ssma/oracle/creating-test-cases-oracletosql.md)  
  
## <a name="see-also"></a>Vea también  
[Instalar componentes SSMA en SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-components-on-sql-server-oracletosql.md)  
[Configuración del proyecto &#40;conversión&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-conversion-oracletosql.md)  
  
