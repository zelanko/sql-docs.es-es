---
title: Pruebas con objetos de base de datos (SybaseToSQL) migrados | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 4937f6b4-86bd-4070-88df-3d216306c33a
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: e29fac8b9cdb955ddaff6643eacae352e9c39bf6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47749189"
---
# <a name="testing-migrated-database-objects-sybasetosql"></a>Pruebas con objetos de base de datos migrados (SybaseToSQL)
Microsoft SQL Server Migration Assistant para Sybase evaluador (SSMA evaluador) comprueba automáticamente la conversión del objeto de base de datos y la migración de datos realizadas por SSMA. Una vez finalizados todos los pasos de migración de SSMA, use el evaluador de SSMA para comprobar que los objetos convertidos funcionan del mismo modo, y que todos los datos se transfirió correctamente.  
  
> [!NOTE]  
> El componente herramienta de comprobación está deshabilitado en el caso de conectividad de Azure.  
  
Puede probar los siguientes tipos de objeto con SSMA evaluador:  
  
-   Tablas  
  
-   Procedimientos almacenados  
  
-   Vistas.  
  
-   Instrucciones independientes.  
  
SSMA Tester ejecuta los objetos seleccionados para realizar pruebas en Sybase y sus homólogos en SQL Server. Después de eso, comparan los resultados según los criterios siguientes:  
  
-   ¿Son los cambios en los datos de la tabla idénticas?  
  
-   ¿Son los valores de parámetros de salida para los procedimientos y funciones idénticas?  
  
-   ¿Las funciones devuelven los mismos resultados?  
  
-   ¿Son que los conjuntos de resultados idénticos?  
  
> [!NOTE]  
> ¡Atención! Nunca utilice SSMA evaluador en sistemas de producción. Durante la ejecución de la herramienta de comprobación se modifican el esquema de origen y los datos. Mientras tanto, la restauración completa del estado original puede ser imposible para algunos tipos de código probado.  
  
## <a name="prerequisites"></a>Requisitos previos  
Si desea usar SSMA evaluador, instalar el paquete de extensión de Sybase de SSMA con el **instalar base de datos de evaluador** opción activada.  
  
Además, compruebe lo siguiente:  
  
-   Proveedor OLE DB de Sybase está instalado en el equipo donde [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se ejecuta.  
  
-   Se ha habilitado la integración de Common Language Runtime (CLR) en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] motor de base de datos.  
  
Tenga en cuenta que la versión actual de SSMA evaluador no admite la ejecución paralela por usuarios diferentes en el mismo servidor de origen o destino.  
  
## <a name="getting-started"></a>Introducción  
[Crear casos de prueba &#40;SybaseToSQL&#41;](../../ssma/sybase/creating-test-cases-sybasetosql.md)  
  
## <a name="see-also"></a>Vea también  
[Instalación de componentes de SSMA en SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md)  
[Configuración del proyecto &#40;conversión&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-conversion-sybasetosql.md)  
  
