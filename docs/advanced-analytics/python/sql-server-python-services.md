---
title: "Los servicios con Python de aprendizaje automático | Documentos de Microsoft"
ms.date: 11/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ba1dea65-40ea-484a-b767-53680c954934
caps.latest.revision: "38"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: 665d307f37bca34669de291a2ea0c71d231288a8
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/01/2017
---
# <a name="machine-learning-services-with-python"></a>Los servicios con Python de aprendizaje automático

Python es un lenguaje que ofrece gran flexibilidad y eficacia para una variedad de tareas de aprendizaje automático. Las bibliotecas de código abierto para Python incluyen varias plataformas para redes neurales personalizables, así como las populares bibliotecas para el procesamiento de lenguaje natural. Ahora, se admite este idioma ampliamente utilizado en SQL Server de 2017 CTP 2.0 y versiones posteriores.

Dado que Python está integrado con el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] motor de base de datos, puede realizar el análisis en lugar donde residen los datos y eliminar los costos y riesgos de seguridad asociados con el movimiento de datos.  Puede implementar soluciones de aprendizaje de máquina basadas en Python con prácticas y sencillas herramientas como Visual Studio. Las aplicaciones de producción pueden obtener predicciones, modelos, o procedimiento almacenan de objetos visuales del tiempo de ejecución de Python 3.5 mediante la llamada a un instrucción T-SQL.

Esta versión incluye la distribución de Anaconda de Python, así como la nueva [revoscalepy](../python/what-is-revoscalepy.md) biblioteca, para mejorar la escalabilidad y rendimiento de sus soluciones de aprendizaje automático.

Puede instalar todo lo que necesita para empezar a trabajar con Python mediante el programa de instalación de SQL Server 2017:

+ **Servicios de aprendizaje de máquina (In-Database):** instale esta característica, junto con el motor de base de datos de SQL Server, para habilitar la ejecución segura de scripts de Python en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] equipo.
  
     Cuando seleccione esta característica, las extensiones se instalan en el motor de base de datos para admitir la ejecución de scripts de Python y se crea un nuevo servicio, el [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)], para administrar las comunicaciones entre el tiempo de ejecución de Python y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instancia.

+ **Servidor de aprendizaje de máquina (independiente):** si no necesita la integración de SQL Server, instale esta característica para obtener compatibilidad con Python y R para el aprendizaje automático distribuida. También puede implementar la solución de Python como un servicio web mediante **mrsdeploy**.
  
     No instale esta característica en el mismo equipo que ejecuta Servicios de aprendizaje de máquina de SQL Server.


## <a name="additional-resources"></a>Recursos adicionales

[Configurar servicios de bases de datos de aprendizaje de automático de Python](setup-python-machine-learning-services.md)

[Tutoriales de Python](../tutorials/sql-server-python-tutorials.md)
