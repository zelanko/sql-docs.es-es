---
title: Creación y definición de pruebas unitarias de SQL Server | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql.data.tools.unittesting.DatabaseMethodNameDialog
- sql.data.tools.unittesting.designer
ms.assetid: 3c082177-a2b1-4fde-8833-b49b2a351815
caps.latest.revision: 10
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4b52fc60f3102e7b6a38d254fba682ab4321d804
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/17/2018
ms.locfileid: "39088337"
---
# <a name="creating-and-defining-sql-server-unit-tests"></a>Crear y definir pruebas unitarias de SQL Server
Puede ejecutar pruebas unitarias de SQL Server para comprobar si los cambios en uno o varios objetos de base de datos en un esquema han interrumpido la funcionalidad existente en una aplicación de base de datos. Estas pruebas complementan las pruebas unitarias creadas por los desarrolladores de software. Debe ejecutar ambos tipos de pruebas para comprobar el comportamiento de la aplicación.  
  
Puede comprobar el comportamiento de cualquier objeto en el esquema si agrega una prueba unitaria de SQL Server y agrega un script de Transact\-SQL para probar dicho objeto. Como alternativa, puede generar automáticamente un código stub de un script de Transact\-SQL si desea comprobar el comportamiento de una función, un desencadenador o un procedimiento almacenado determinado. Después de generar el código stub, debe personalizarlo para obtener resultados significativos.  
  
> [!NOTE]  
> Puede crear una prueba vacía, agregarle código y ejecutarlo sin tener un proyecto de base de datos de SQL Server abierto. Sin embargo, no puede generar automáticamente un código stub de Transact\-SQL que pruebe una función, un desencadenador o un procedimiento almacenado sin abrir el proyecto que contiene el objeto que desea probar.  
  
## <a name="common-tasks"></a>Tareas comunes  
En la siguiente tabla, puede buscar las descripciones de tareas comunes que admiten este escenario y vínculos a más información acerca de cómo completar correctamente esas tareas.  
  
|Tareas comunes|Contenido adicional|  
|----------------|----------------------|  
|**Obtener experiencia práctica**: puede realizar un tutorial de introducción para familiarizarse con la forma de crear y ejecutar una prueba unitaria simple de SQL Server.|-   [Tutorial: Crear y ejecutar una prueba unitaria de SQL Server](../ssdt/walkthrough-creating-and-running-a-sql-server-unit-test.md)|  
|**Obtener más información acerca de las pruebas unitarias de SQL Server**: puede obtener más información acerca de los archivos y scripts que forman una prueba unitaria de SQL Server. También puede obtener información sobre cómo usar las condiciones de prueba y las aserciones de Transact\-SQL en las pruebas unitarias.|-   [Scripts de pruebas unitarias de SQL Server](../ssdt/scripts-in-sql-server-unit-tests.md)<br />-   [Archivos de prueba unitaria de SQL Server](../ssdt/sql-server-unit-test-files.md)<br />-   [Usar condiciones de prueba en pruebas unitarias de SQL Server](../ssdt/using-test-conditions-in-sql-server-unit-tests.md)<br />-   [Usar aserciones de Transact-SQL en pruebas unitarias de SQL Server](../ssdt/using-transact-sql-assertions-in-sql-server-unit-tests.md)|  
|**Crear uno o más proyectos de prueba**: debe crear pruebas unitarias de SQL Server en un proyecto de prueba. Si crea una prueba unitaria de SQL Server mediante el Explorador de objetos de SQL Server antes de crear un proyecto de prueba, este se crea automáticamente. Puede crear más de un proyecto de prueba si, por ejemplo, desea usar distintos planes de generación de datos o varias configuraciones de implementación en distintos conjuntos de pruebas. Al crear el proyecto de prueba, puede configurar los valores de prueba (como la cadena de conexión), los valores de implementación y el plan de generación de datos que se usarán para ese proyecto.|-   [Cómo: Crear un proyecto de prueba para las pruebas unitarias de base de datos de SQL Server](../ssdt/how-to-create-a-test-project-for-sql-server-database-unit-testing.md)<br />-|  
|**Configurar la ejecución de la prueba unitaria**: puede especificar la cadena de conexión a la base de datos en la que se ejecutan las pruebas, el plan de generación de datos y la configuración de implementación. Configure estos valores la primera vez que agregue una prueba unitaria de SQL Server al proyecto de prueba, aunque también puede modificarlos posteriormente.|-   [Cómo: Configurar una ejecución de prueba unitaria de SQL Server](../ssdt/how-to-configure-sql-server-unit-test-execution.md)<br />-   [Información general acerca de las cadenas de conexión y los permisos](../ssdt/overview-of-connection-strings-and-permissions.md)|  
|**Crear una prueba unitaria de SQL Server**: puede crear automáticamente códigos stub de Transact\-SQL para las pruebas unitarias de SQL Server que comprueben el comportamiento de una función, un desencadenador o un procedimiento almacenado. También puede crear una prueba unitaria de SQL Server vacía y agregar después código de Transact\-SQL para probar otros tipos de objetos de base de datos.|-   [Cómo: Crear pruebas unitarias de SQL Server para funciones, desencadenadores y procedimientos almacenados](../ssdt/how-to-create-unit-tests-for-functions-triggers-stored-procedures.md)<br />-   [Cómo: Crear una prueba unitaria de SQL Server vacía](../ssdt/how-to-create-an-empty-sql-server-unit-test.md)|  
|**Escribir código para una prueba unitaria de SQL Server**: después de crear una prueba unitaria, modifique o escriba el código de Transact\-SQL para probar un objeto de base de datos. Para cada prueba, defina una o varias condiciones de prueba que determinen si la prueba se pasará o producirá un error. Para pruebas más complejas, puede modificar el código de Visual Basic o Visual C\# en el proyecto de base de datos. Por ejemplo, puede escribir una prueba unitaria que se ejecute en el ámbito de una única transacción.|-   [Cómo: Abrir una prueba unitaria de SQL Server para editarla](../ssdt/how-to-open-a-sql-server-unit-test-to-edit.md)<br />-   [Cómo: Agregar condiciones de prueba a pruebas unitarias de SQL Server](../ssdt/how-to-add-test-conditions-to-sql-server-unit-tests.md)<br />-   [Cómo: Escribir una prueba unitaria de SQL Server que se ejecuta en el ámbito de una única transacción](../ssdt/how-to-write-sql-server-unit-test-that-runs-in-single-transaction-scope.md)<br />-   [Métodos abreviados de teclado para el Diseñador de pruebas unitarias de SQL Server](../ssdt/keyboard-shortcuts-for-sql-server-unit-test-designer.md)|  
|**Solucionar problemas**: puede obtener más información acerca de cómo solucionar problemas comunes de SQL Server.|-   [Solucionar problemas con las pruebas unitarias de base de datos en SQL Server](../ssdt/troubleshooting-sql-server-database-unit-testing-issues.md)|  
  
## <a name="related-scenarios"></a>Escenarios relacionados  
[Ejecutar pruebas unitarias de SQL Server](../ssdt/running-sql-server-unit-tests.md)  
Después de crear las pruebas unitarias de SQL Server, puede ejecutarlas desde la ventana Vista de pruebas, el Diseñador de pruebas unitarias de SQL Server o mediante Team Foundation Build.  
  
[Escenario: Definir condiciones de prueba personalizadas para pruebas unitarias de base de datos](http://msdn.microsoft.com/library/dd193282(VS.100).aspx)  
Puede crear una condición de prueba personalizada para probar un comportamiento que las condiciones de prueba predeterminadas no pueden comprobar.  
  
## <a name="see-also"></a>Ver también  
[Comprobar el código de base de datos con pruebas unitarias de SQL Server](../ssdt/verifying-database-code-by-using-sql-server-unit-tests.md)  
  
