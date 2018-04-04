---
title: Los servicios con Python de aprendizaje automático | Documentos de Microsoft
ms.date: 03/16/2018
ms.reviewer: ''
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: python
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.workload: On Demand
ms.openlocfilehash: 275eedc011367e51e97c6bddae03858cdda932ee
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/04/2018
---
# <a name="machine-learning-services-with-python"></a>Los servicios con Python de aprendizaje automático
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Python es un lenguaje que ofrece gran flexibilidad y eficacia para una variedad de tareas de aprendizaje automático. Las bibliotecas de código abierto para Python incluyen varias plataformas para redes neurales personalizables, así como las populares bibliotecas para el procesamiento de lenguaje natural. Ahora, se admite este idioma usados en el aprendizaje automático de SQL Server de 2017.

Dado que Python está integrado con el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] motor de base de datos, puede realizar el análisis en lugar donde residen los datos y eliminar los costos y riesgos de seguridad asociados con el movimiento de datos.  Puede implementar soluciones de aprendizaje de máquina basadas en Python con prácticas y sencillas herramientas como Visual Studio. Las aplicaciones de producción pueden obtener predicciones, modelos, o procedimiento almacenan de objetos visuales del tiempo de ejecución de Python 3.5 mediante la llamada a un instrucción T-SQL.

Esta versión incluye la distribución de Anaconda de Python, así como el [revoscalepy](../python/what-is-revoscalepy.md) biblioteca, para mejorar la escalabilidad y rendimiento de sus soluciones de aprendizaje automático.

Puede instalar todo lo que necesita para empezar a trabajar con Python mediante el programa de instalación de SQL Server 2017:

+ [**Learning Services (In-Database) del equipo**](../install/sql-machine-learning-services-windows-install.md): instale esta característica, junto con el motor de base de datos de SQL Server, para habilitar la ejecución segura de scripts de Python en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] equipo.
  
     Cuando seleccione esta característica, las extensiones se instalan en el motor de base de datos para admitir la ejecución de scripts de Python y se crea un nuevo servicio, el [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)], para administrar las comunicaciones entre el tiempo de ejecución de Python y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instancia.

+ [**Aprendizaje Server (independiente) la máquina**](../install/sql-machine-learning-standalone-windows-install.md): si no necesita la integración de SQL Server, instale esta característica para obtener compatibilidad con Python y R para el aprendizaje automático distribuida.

## <a name="see-also"></a>Vea también

+ [SQL Server del equipo aprendizaje y R Services (en bases de datos)](../r/sql-server-r-services.md)
+ [SQL Server del equipo aprendizaje y R Server (independiente)](../r/r-server-standalone.md)
+ [Arquitectura de Python](architecture-overview-sql-server-python.md)
+ [Tutoriales de Python](../tutorials/sql-server-python-tutorials.md)
