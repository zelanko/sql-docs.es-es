---
title: Pruebas con objetos de base de datos (OracleToSQL) migrados | Microsoft Docs
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
ms.openlocfilehash: 037a58fc3fc9402c7148ec49d3a27ea0c0ace309
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/14/2018
ms.locfileid: "40392581"
---
# <a name="testing-migrated-database-objects-oracletosql"></a>Pruebas con objetos de base de datos migrados (OracleToSQL)
[!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant para Oracle evaluador (SSMA evaluador) comprueba automáticamente la conversión del objeto de base de datos y la migración de datos realizadas por SSMA. Una vez finalizados todos los pasos de migración de SSMA, use el evaluador de SSMA para comprobar que los objetos convertidos funcionan del mismo modo, y que todos los datos se transfirió correctamente.  
  
Puede probar los siguientes tipos de objeto con SSMA evaluador:  
  
-   Tablas  
  
-   Procedimientos almacenados, incluidos los procedimientos empaquetados.  
  
-   Definido por el usuario funciones, incluidas las funciones empaquetadas.  
  
-   Vistas.  
  
-   Instrucciones independientes.  
  
SSMA Tester ejecuta los objetos seleccionados para realizar pruebas en Oracle y sus homólogos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Después de eso, comparan los resultados según los criterios siguientes:  
  
-   ¿Son los cambios en los datos de la tabla idénticas?  
  
-   ¿Son los valores de parámetros de salida para los procedimientos y funciones idénticas?  
  
-   ¿Las funciones devuelven los mismos resultados?  
  
-   ¿Son que los conjuntos de resultados idénticos?  
  
> [!NOTE]  
> ¡Atención! Nunca utilice SSMA evaluador en sistemas de producción. Durante la ejecución de la herramienta de comprobación se modifican el esquema de origen y los datos. Mientras tanto, la restauración completa del estado original puede ser imposible para algunos tipos de código probado.  
  
## <a name="prerequisites"></a>Requisitos previos  
Si desea usar SSMA evaluador, instalar SSMA módulo de extensión de Oracle con el **instalar base de datos de evaluador** opción activada.  
  
Para habilitar la comparación de los datos resultantes de la tabla, establecer el **columna generar ROWID** opción **Sí** antes de inicia la conversión de esquema. SSMA agregará una columna ROWID a todas las tablas durante la ejecución de la **convertir esquema** comando.  
  
Además, compruebe lo siguiente:  
  
-   Las herramientas de cliente de Oracle están instaladas en el equipo donde [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se ejecuta.  
  
-   Se ha habilitado la integración de Common Language Runtime (CLR) en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] motor de base de datos.  
  
Tenga en cuenta que la versión actual de SSMA evaluador no admite la ejecución paralela por usuarios diferentes en el mismo servidor de origen o destino.  
  
## <a name="getting-started"></a>Introducción  
[Crear casos de prueba &#40;OracleToSQL&#41;](../../ssma/oracle/creating-test-cases-oracletosql.md)  
  
## <a name="see-also"></a>Vea también  
[Instalación de componentes de SSMA en SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-components-on-sql-server-oracletosql.md)  
[Configuración del proyecto &#40;conversión&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-conversion-oracletosql.md)  
  
