---
title: Pruebas migran objetos de base de datos (SybaseToSQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-sybase
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 4937f6b4-86bd-4070-88df-3d216306c33a
caps.latest.revision: 7
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 1d66b93de265c4976c1c570de7cffe828c7424ea
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="testing-migrated-database-objects-sybasetosql"></a>Pruebas migran objetos de base de datos (SybaseToSQL)
Microsoft SQL Server Migration Assistant para Sybase evaluador (SSMA evaluador) prueba automáticamente la conversión del objeto de base de datos y la migración de datos realizadas por SSMA. Después de que haya finalizado todos los pasos de migración de SSMA, use SSMA evaluador para comprobar que los objetos convertidos funcionan del mismo modo y que todos los datos se transfirió correctamente.  
  
> [!NOTE]  
> Componente de evaluador está deshabilitada en el caso de conectividad de Azure.  
  
Puede probar los siguientes tipos de objeto con la herramienta de comprobación de SSMA:  
  
-   Tablas  
  
-   Procedimientos almacenados  
  
-   Vistas.  
  
-   Instrucciones independientes.  
  
SSMA evaluador ejecuta objetos seleccionados para realizar pruebas en Sybase y sus homólogos en SQL Server. A continuación, compara los resultados según los criterios siguientes:  
  
-   ¿Son los cambios en los datos de la tabla idénticas?  
  
-   ¿Son los valores de parámetros de salida para los procedimientos y funciones idénticas?  
  
-   ¿Las funciones devuelven los mismos resultados?  
  
-   ¿Son que los conjuntos de resultados idéntico?  
  
> [!NOTE]  
> ¡Atención! Nunca utilice SSMA evaluador en sistemas de producción. Durante la ejecución de la herramienta de comprobación se modifican el esquema de origen y los datos. Mientras tanto, la restauración completa del estado original puede ser imposible para algunos tipos de código probado.  
  
## <a name="prerequisites"></a>Requisitos previos  
Si desea usar la herramienta de comprobación de SSMA, instalar paquete de extensión de SSMA Sybase con los **instalar bases de datos de evaluador** opción activada.  
  
Además, compruebe lo siguiente:  
  
-   Proveedor OLE DB de Sybase está instalado en el equipo donde [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] se ejecuta.  
  
-   Se ha habilitado la integración de Common Language Runtime (CLR) en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] motor de base de datos.  
  
Tenga en cuenta que la versión actual de la herramienta de comprobación de SSMA no admite la ejecución en paralelo por usuarios diferentes en el mismo servidor de origen o de destino.  
  
## <a name="getting-started"></a>Introducción  
[Crear casos de prueba &#40;SybaseToSQL&#41;](../../ssma/sybase/creating-test-cases-sybasetosql.md)  
  
## <a name="see-also"></a>Vea también  
[Instalar componentes SSMA en SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md)  
[Configuración del proyecto &#40;conversión&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-conversion-sybasetosql.md)  
  
