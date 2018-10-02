---
title: Ejecución de pruebas unitarias de SQL Server | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- sql.data.tools.unittesting.testconfig
ms.assetid: febcc87f-eb18-4c12-ba30-82ef0d49aaa3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: bca70724235f19c257dfb34fb9dab323fb4d7fc5
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47840303"
---
# <a name="running-sql-server-unit-tests"></a>Ejecución de pruebas unitarias de SQL Server
Para mejorar y mantener la calidad del código, puede crear y ejecutar pruebas unitarias de SQL Server que comprueben el comportamiento de cualquier objeto de base de datos y después proteger esas pruebas en el control de versiones. Cuando usted o cualquier miembro del equipo cambie el esquema de la base de datos, ejecute pruebas unitarias de SQL Server y pruebas unitarias de software para comprobar que los cambios no interrumpen la funcionalidad existente. Puede ejecutar pruebas individuales o puede ejecutar grupos de prueba, que se denominan listas de pruebas. Para más información, consulte [Usar listas de pruebas (Visual Studio 2010)](http://msdn.microsoft.com/library/ms182461(VS.100).aspx).  
  
## <a name="ways-to-run-sql-server-unit-tests"></a>Maneras de ejecutar las pruebas unitarias de SQL Server  
Puede ejecutar pruebas unitarias de SQL Server de varias maneras, que varían según el software instalado, como se muestra a continuación:  
  
-   Ejecutar pruebas mediante la ventana **Vista de pruebas** de Visual Studio 2010. Para más información, consulte [Cómo: Ejecutar pruebas unitarias de SQL Server](../ssdt/how-to-run-sql-server-unit-tests.md) y [Cómo: Ejecutar pruebas automatizadas desde Microsoft Visual Studio 2010](http://msdn.microsoft.com/library/ms182470(VS.100).aspx). Para Visual Studio 2012, consulte [Cómo: Ejecutar pruebas automatizadas desde Microsoft Visual Studio 2012](http://msdn.microsoft.com/library/ms182470.aspx).  
  
-   Ejecutar pruebas mediante el comando MSTest.exe en un símbolo del sistema. Para más información, consulte [Cómo: Ejecutar pruebas automatizadas desde la línea de comandos usando MSTest (Visual Studio 2010)](http://msdn.microsoft.com/library/ms182487(VS.100).aspx) o [Cómo: Ejecutar pruebas automatizadas desde la línea de comandos usando MSTest (Visual Studio 2012)](http://msdn.microsoft.com/library/ms182487.aspx).  
  
-   Ejecutar pruebas desde el **Explorador de soluciones** ejecutando un proyecto de prueba. Para más información, consulte [Cómo: Ejecutar pruebas automatizadas desde Microsoft Visual Studio 2010](http://msdn.microsoft.com/library/ms182470(VS.100).aspx) o [Cómo: Ejecutar pruebas automatizadas desde Microsoft Visual Studio 2012](http://msdn.microsoft.com/library/ms182470.aspx).  
  
-   Volver a ejecutar pruebas desde la ventana **Resultados de las pruebas**. Para más información, consulte [Cómo: Volver a ejecutar una prueba (Visual Studio 2010)](http://msdn.microsoft.com/library/ms182472(VS.100).aspx).  
  
-   Ejecutar pruebas individuales o listas de pruebas (Visual Studio 2010) desde la ventana **Editor de listas de pruebas**. Para más información, consulte [Cómo: Ejecutar pruebas automatizadas desde Microsoft Visual Studio 2010](http://msdn.microsoft.com/library/ms182470(VS.100).aspx) o [Cómo: Ejecutar pruebas automatizadas desde Microsoft Visual Studio 2012](http://msdn.microsoft.com/library/ms182470.aspx).  
  
-   Ejecutar pruebas a medida que se compila un proyecto en Team Foundation Build. Para más información, consulte [Cómo: Configurar y ejecutar pruebas programadas después de compilar la aplicación (Visual Studio 2010)](http://msdn.microsoft.com/library/ms182465(VS.100).aspx) o [Cómo: Configurar y ejecutar pruebas programadas después de compilar la aplicación (Visual Studio 2012)](http://msdn.microsoft.com/library/ms182465.aspx).  
  
Puede ejecutar las pruebas unitarias de SQL Server en un orden determinado usando una prueba por orden. Para más información, consulte [Cómo: Crear una prueba ordenada (Visual Studio 2010)](http://msdn.microsoft.com/library/ms182631(VS.100).aspx) o [Cómo: Crear una prueba ordenada (Visual Studio 2012)](http://msdn.microsoft.com/library/ms182631.aspx).  
  
## <a name="interpreting-tests-results"></a>Interpretación de los resultados de pruebas  
Una vez ejecutadas las pruebas, la ventana **Resultados de pruebas** muestra qué pruebas han producido errores y cuáles se han realizado correctamente. Para más información, consulte [Interpretar los resultados de pruebas unitarias de SQL Server](../ssdt/interpreting-sql-server-unit-test-results.md). Para más información sobre cómo diagnosticar un error inesperado, consulte [Cómo: Depurar objetos de base de datos](../ssdt/how-to-debug-database-objects.md).  
  
## <a name="topics-in-this-section"></a>Temas de esta sección  
Esta sección contiene los siguientes temas:  
  
-   [Cómo: Depurar objetos de base de datos](../ssdt/how-to-debug-database-objects.md)  
  
-   [Cómo: Ejecutar pruebas unitarias de SQL Server desde Team Foundation Build](../ssdt/how-to-run-sql-server-unit-tests-from-team-foundation-build.md)  
  
-   [Cómo: Ejecutar pruebas unitarias de SQL Server](../ssdt/how-to-run-sql-server-unit-tests.md)  
  
-   [Interpretar los resultados de pruebas unitarias de SQL Server](../ssdt/interpreting-sql-server-unit-test-results.md)  
  
## <a name="related-scenarios"></a>Escenarios relacionados  
[Crear y definir pruebas unitarias de SQL Server](../ssdt/creating-and-defining-sql-server-unit-tests.md)  
Puede definir pruebas unitarias para comprobar el comportamiento de los objetos de base de datos y asociar cada proyecto de prueba con un plan de generación de datos, una configuración de implementación y una cadena de conexión diferentes.  
  
[Condiciones de prueba personalizadas para pruebas unitarias de SQL Server](../ssdt/custom-test-conditions-for-sql-server-unit-tests.md)  
Puede crear una condición de prueba personalizada para probar cualquier condición que no pueda comprobar mediante las condiciones de prueba predeterminadas.  
  
## <a name="see-also"></a>Ver también  
[Comprobar el código de base de datos con pruebas unitarias de SQL Server](../ssdt/verifying-database-code-by-using-sql-server-unit-tests.md)  
  
