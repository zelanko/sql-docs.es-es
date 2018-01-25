---
title: Compatibilidad de DAC con las versiones y objetos de SQL Server | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: data-tier-applications
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-data-tier-apps
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data-tier application [SQL Server], supported objects
- objects [SQL Server], data-tier applications
ms.assetid: b1b78ded-16c0-4d69-8657-ec57925e68fd
caps.latest.revision: "19"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 12b99446025274f0f3652a7552f53775283af7ac
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/17/2018
---
# <a name="dac-support-for-sql-server-objects-and-versions"></a>Compatibilidad de DAC con las versiones y objetos de SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Una aplicación de capa de datos (DAC) admite los objetos [!INCLUDE[ssDE](../../includes/ssde-md.md)] que se usan más.  
  
 **En este tema**  
  
-   [Objetos de SQL Server admitidos](#SupportedObjects)  
  
-   [Compatibilidad de aplicaciones de la capa de datos con versiones de SQL Server](#SupportByVersion)  
  
-   [Limitaciones de la implementación de datos](#DeploymentLimitations)  
  
-   [Consideraciones adicionales para las acciones de implementación](#Considerations)  
  
##  <a name="SupportedObjects"></a> Objetos de SQL Server admitidos  
 Solo los objetos admitidos se pueden especificar en una aplicación de capa de datos cuando se está creando o modificando. No se puede extraer, registrar o importar una DAC de una base de datos existente que contenga objetos que no se admitan en una DAC. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] admite los siguientes objetos en una DAC.  
  
|||  
|-|-|  
|ROL DE BASE DE DATOS|FUNCIÓN: insertada con valores de tabla|  
|FUNCIÓN: con valores de tabla de múltiples instrucciones|FUNCIÓN: escalar|  
|ÍNDICE: clúster|ÍNDICE: no clúster|  
|INDEX: espacial|ÍNDICE: único|  
|LOGIN|Permisos|  
|Pertenencias al rol|SCHEMA|  
|Estadísticas|PROCEDIMIENTO ALMACENADO: Transact-SQL|  
|Sinónimos|TABLA: restricción CHECK|  
|TABLA: intercalación|TABLA: columna, incluidas las columnas calculadas|  
|TABLA: restricción, predeterminada|TABLA: restricción, clave externa|  
|TABLA: restricción, índice|TABLA: restricción, clave principal|  
|TABLA: restricción, única|DESENCADENADOR: DML|  
|TIPO: HIERARCHYID, GEOMETRY, GEOGRAPHY|TIPO: tipo de datos definido por el usuario|  
|TIPO: tipo de tabla definida por el usuario|USER|  
|VIEW||  
  
##  <a name="SupportByVersion"></a> Compatibilidad de aplicaciones de la capa de datos con versiones de SQL Server  
 Las versiones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tienen niveles diferentes de compatibilidad con las operaciones DAC. Todas las operaciones DAC admitidas por una versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] son admitidas por todas las ediciones de esa versión.  
  
 Las instancias del [!INCLUDE[ssDE](../../includes/ssde-md.md)] admiten las siguientes operaciones DAC:  
  
-   La exportación y la extracción se admiten en todas las versiones compatibles de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Todas las operaciones se admiten en [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)] y en todas las versiones de [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]y [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)].  
  
-   Todas las operaciones se admiten en [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] Service Pack 2 (SP2) o posterior y en [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP4 o posterior.  
  
 DAC Framework consta de las herramientas del lado cliente para compilar y procesar los paquetes DAC y los archivos de exportación. Los productos siguientes incluyen DAC Framework  
  
-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] incluye DAC Framework 3.0, que admite todas las operaciones DAC.  
  
-   [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP1 y Visual Studio 2010 SP1 incluían DAC Framework 1.1, que admite todas las operaciones DAC excepto la exportación y la importación.  
  
-   [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] y Visual Studio 2010 incluían DAC Framework 1.0, que admite todas las operaciones DAC excepto la exportación, la importación, y la actualización en contexto.  
  
-   Las herramientas cliente de versiones anteriores de SQL Server o de Visual Studio no admiten las operaciones DAC.  
  
 Un paquete DAC o un archivo de exportación compilado con una versión de DAC Framework no se puede procesar con una versión anterior de DAC. Por ejemplo, un paquete DAC extraído mediante las herramientas cliente [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] no se puede implementar usando las herramientas cliente [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] .  
  
 Un paquete DAC o un archivo de exportación compilado con una versión de DAC Framework se puede procesar con una versión posterior de DAC. Por ejemplo, un paquete DAC extraído mediante las herramientas cliente de [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] se puede implementar con [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP1 o con herramientas cliente posteriores.  
  
##  <a name="DeploymentLimitations"></a> Limitaciones de la implementación de datos  
 Tenga en cuenta estas limitaciones en la fidelidad del motor de implementación de datos de DAC Framework en SQL Server 2012 SP1. Las limitaciones se aplican a las siguientes acciones de DAC Framework: implementar o publicar un archivo .dacpac e importar un archivo .bacpac.  
  
1.  Pérdida de metadatos para ciertas condiciones y tipos base en columnas sql_variant. En los casos correspondientes, aparecerá una advertencia con el siguiente mensaje:  **Determinadas propiedades de determinados tipos de datos utilizados dentro de una columna sql_variant no se conservan al implementarlos DAC Framework**.  
  
    -   Tipos base MONEY, SMALLMONEY NUMERIC y DECIMAL: no se mantiene la precisión.  
  
        -   Tipos base DECIMAL/NUMERIC con precisión 38: los metadatos de sql_variant de “TotalBytes” siempre se establecen en 21.  
  
    -   Todos los tipos base de texto: la intercalación predeterminada de la base de datos se aplica a todo el texto.  
  
    -   Tipos base BINARY: no se mantiene la propiedad longitud máxima.  
  
    -   Tipos base TIME y DATETIMEOFFSET: la precisión se establece siempre en 7.  
  
2.  Pérdida de datos en las columnas sql_variant. En el caso correspondiente, aparecerá una advertencia con el siguiente mensaje: **Se perderán datos cuando DAC Framework implemente un valor en una columna sql_variant DATETIME2 con una escala mayor que 3. Durante la implementación, el valor DATETIME2 está limitado a una escala igual a 3.**  
  
    -   Tipo base DATETIME2 con una escala mayor que 3: el límite de la escala es 3.  
  
3.  La operación de implementación no se realiza correctamente para las condiciones en las columnas sql_variant. En los casos correspondientes, aparecerá un cuadro de diálogo con el siguiente mensaje:  **La operación no se realizó correctamente debido a limitaciones de datos en DAC Framework.**  
  
    -   Tipos base DATETIME2, SMALLDATETIME y DATE: si el valor no está comprendido en el intervalo de DATETIME (por ejemplo, el año es menor que 1753).  
  
    -   Tipo base DECIMAL, NUMERIC: cuando la precisión del valor es mayor que 28.  
  
##  <a name="Considerations"></a> Consideraciones adicionales para las acciones de implementación  
 Tenga en cuenta las siguientes consideraciones en acciones de implementación de datos de DAC Framework:  
  
-   **Extraer, exportar:** estas limitaciones no se aplican en acciones que usan DAC Framework para crear un paquete a partir de una base de datos como, por ejemplo, extraer un archivo .dacpac o exportar un archivo .bacpac. Los datos del paquete son una representación totalmente exacta de los datos en la base de datos de origen. Si el paquete incorpora alguna de estas condiciones, el registro de extracciones y exportaciones incluirá un resumen de los problemas que se enviaron en los mensajes indicados anteriormente. Con esto, se pretende advertir a los usuario de los potenciales problemas en la implementación de datos con el paquete que han creado. El usuario verá también el mensaje de resumen siguiente en el registro: **Estas limitaciones no afectan a la fidelidad de los tipos de datos y de los valores almacenados en el paquete DAC que ha creado DAC Framework; solo se aplican a los tipos de datos y a los valores resultantes al implementar un paquete DAC en una base de datos. Para obtener más información sobre los datos que se ven afectados y cómo evitar esta limitación, vea** [este tema](http://go.microsoft.com/fwlink/?LinkId=267086).  
  
-   **Implementar, publicar, importar:** estas limitaciones se aplican en acciones que usan DAC Framework para implementar un paquete en una base de datos como, por ejemplo, implementar o publicar un archivo .dacpac e importar un archivo .bacpac. Es posible que los datos que se obtienen en la base de datos de destino no contengan una representación totalmente exacta de los datos del paquete. El registro de implementaciones e importaciones contendrá un mensaje (arriba indicado) para cada instancia donde se produzca el problema. Si hay errores, estos bloquearán la operación (vea la categoría 3 de más arriba), pero seguirá con las otras advertencias.  
  
     Para obtener más información sobre los datos que se ven afectados en esta situación y cómo evitar esta limitación para implementar, publicar e importar acciones, vea [este tema](http://go.microsoft.com/fwlink/?LinkId=267087).  
  
-   **Soluciones alternativas:** las operaciones de extracción y exportación escribirán archivos de datos BCP totalmente exactos en archivos .dacpac o .bacpac. Para evitar limitaciones, utilice la utilidad de línea de comandos SQL Server BCP.exe con el fin de implementar datos totalmente exactos en una base de datos de destino a partir de un paquete DAC.  
  
## <a name="see-also"></a>Ver también  
 [Aplicaciones de capa de datos](../../relational-databases/data-tier-applications/data-tier-applications.md)  
  
  
