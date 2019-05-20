---
title: Interpretar los resultados de pruebas unitarias de SQL Server | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: fde3c95b-2f68-483d-a197-0f7161b72fa3
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 1c68ace0ccbd49b63404aaf52419a06dda297f8d
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/06/2019
ms.locfileid: "65088715"
---
# <a name="interpreting-sql-server-unit-test-results"></a>Interpretar los resultados de pruebas unitarias de SQL Server
Al ejecutar una prueba unitaria de SQL Server, los resultados de prueba se generan automáticamente, se guardan en el disco y se resumen en la ventana **Resultados de pruebas**. En cuanto se inicia una serie de pruebas, aparece la ventana **Resultados de pruebas**, que muestra el progreso de la serie de pruebas. Esta pantalla incluye las pruebas que se están ejecutando y las pruebas que se han completado.  
  
Para ver información detallada sobre un resultado de prueba, haga doble clic en la ventana **Resultados de pruebas** para mostrar la página **Detalles de resultados de la prueba**. Para obtener más información acerca de un resultado de pruebas, haga doble clic en él.  
  
Para obtener más información sobre cómo cambiar la presentación de la ventana **Resultados de pruebas**, vea [Cómo: Agregar o quitar columnas en ventanas de prueba (Visual Studio 2010)](https://msdn.microsoft.com/library/ms182508(VS.100).aspx) o [Cómo: Agregar o quitar columnas en ventanas de prueba (Visual Studio 2012)](https://msdn.microsoft.com/library/ms182508.aspx).  
  
## <a name="storing-test-results"></a>Almacenar los resultados de pruebas  
Los resultados de las pruebas unitarias se almacenan en el disco duro en archivos con la extensión .trx. Un archivo .trx es un archivo XML que contiene los detalles de una serie de pruebas. Puede cargar los archivos .trx de series de pruebas anteriores para revisar los resultados de esas series de pruebas o volver a ejecutar pruebas anteriores. Para más información, vea: [Cómo: Vuelva a ejecutar una prueba (Visual Studio 2010)](https://msdn.microsoft.com/library/ms182472(VS.100).aspx).  
  
> [!NOTE]  
> No puede ejecutar pruebas unitarias de forma remota.  
  
Si el equipo está usando un proyecto de equipo de Visual Studio Team Foundation Server para ayudar a administrar su trabajo, también puede publicar los datos de prueba en una base de datos de SQL Server conocida como almacén operativo.  
  
Para obtener más información sobre cómo guardar los resultados de pruebas, reutilizarlos y compartirlos con su equipo, vea [Cómo: Guardar y abrir resultados de pruebas en Visual Studio 2010](https://msdn.microsoft.com/library/ms404662(VS.100).aspx) o [Cómo: Guardar y abrir resultados de pruebas en Visual Studio 2012](https://msdn.microsoft.com/library/ms404662.aspx).  
  
## <a name="see-also"></a>Consulte también  
[Ejecutar pruebas unitarias de SQL Server](../ssdt/running-sql-server-unit-tests.md)  
  
