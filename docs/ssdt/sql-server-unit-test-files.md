---
title: Archivos de prueba unitaria de SQL Server | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: cee093c9-b97d-4fb0-b80f-806d071259dc
caps.latest.revision: 9
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e23304a429b77bcb4a5fc6a4c1001f2f28cf7885
ms.sourcegitcommit: 2f07d285824a8982c279f3816b220e61a2d91b06
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/29/2018
ms.locfileid: "37094797"
---
# <a name="sql-server-unit-test-files"></a>Archivos de prueba unitaria de SQL Server
Al igual que las pruebas unitarias para código administrado, las pruebas unitarias de SQL Server residen en proyectos de prueba. Puede ver los elementos que conforman una prueba unitaria de SQL Server en la jerarquía de un proyecto de prueba en el **Explorador de soluciones**.  
  
Una prueba unitaria de SQL Server consta de varios elementos incluidos en varios archivos. En la tabla siguiente se describen los archivos que interactúan para formar una prueba unitaria de SQL Server.  
  
|**Archivo**|**Descripción**|  
|------------|-------------------|  
|.cs o .vb|Este archivo de código fuente contiene una clase que se representa con el atributo [TestClass]. Esta clase contiene un único método de prueba para cada una de las pruebas unitarias de SQL Server independientes. Estos métodos se representan con el atributo [TestMethod].<br /><br />Cada método de prueba contiene el código adecuado para ejecutar el script de prueba Transact\-SQL. Este código se genera cuando se crean los métodos de prueba, y puede modificarse.<br /><br />**NOTA:** Si hace doble clic en este archivo en el **Explorador de soluciones**, la clase de prueba se abrirá en el Diseñador de pruebas unitarias de SQL Server. Para abrir el archivo .cs o .vb para ver el código fuente, haga clic con el botón derecho en el archivo en el **Explorador de soluciones** y, a continuación, haga clic en **Ver código**.|  
|.resx|Este archivo de recursos contiene los scripts Transact\-SQL para todas las pruebas del archivo .cs o .vb asociado. Este grupo de scripts incluye el script anterior a la prueba, el script de prueba y el script posterior a la prueba. El archivo de recursos contiene XML, que se puede modificar. El archivo de recursos se compila en el ensamblado de prueba.<br /><br />Debe codificar los scripts Transact\-SQL mediante el **Diseñador de pruebas unitarias de SQL Server**. Para más información sobre los scripts que se usan en las pruebas unitarias de SQL Server, consulte [Scripts de pruebas unitarias de SQL Server](../ssdt/scripts-in-sql-server-unit-tests.md).|  
|app.config|Este archivo almacena las cadenas de conexión de base de datos para el proyecto de prueba, además de otras opciones de configuración de la prueba unitaria de SQL Server, como el tiempo de espera para un comando. Para más información, consulte [Scripts de pruebas unitarias de SQL Server](../ssdt/scripts-in-sql-server-unit-tests.md).|  
|SQLDatabaseSetup.cs o SQLDatabaseSetup.vb|Este archivo contiene una clase que prepara el entorno de prueba para todas las pruebas unitarias de SQL Server del proyecto de prueba. Según la configuración del archivo app.config, puede implementar un proyecto de base de datos de SQL Server en la base de datos de prueba.|  
  
## <a name="see-also"></a>Ver también  
[Crear y definir pruebas unitarias de SQL Server](../ssdt/creating-and-defining-sql-server-unit-tests.md)  
[Crear y definir pruebas unitarias de SQL Server](../ssdt/creating-and-defining-sql-server-unit-tests.md)  
[Comprobar el código de base de datos con pruebas unitarias de SQL Server](../ssdt/verifying-database-code-by-using-sql-server-unit-tests.md)  
[Scripts de pruebas unitarias de SQL Server](../ssdt/scripts-in-sql-server-unit-tests.md)  
  
