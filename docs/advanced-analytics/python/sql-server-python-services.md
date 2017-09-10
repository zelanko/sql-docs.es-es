---
title: SQL Server R Services | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 06/22/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ba1dea65-40ea-484a-b767-53680c954934
caps.latest.revision: 38
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 140885b86f0f6fa1a56119246c859f143f596726
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="machine-learning-services-with-python"></a>Los servicios con Python de aprendizaje automático

Python es un lenguaje que ofrece gran flexibilidad y eficacia para una variedad de tareas de aprendizaje automático. Las bibliotecas de código abierto para Python incluyen varias plataformas para redes neurales personalizables, así como las populares bibliotecas para el procesamiento de lenguaje natural. Ahora, se admite este idioma ampliamente utilizado en SQL Server de 2017 CTP 2.0 y versiones posteriores.

Dado que Python está integrado con el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] motor de base de datos, puede realizar el análisis en lugar donde residen los datos y eliminar los costos y riesgos de seguridad asociados con el movimiento de datos.  Puede implementar soluciones de aprendizaje de máquina basadas en Python con prácticas y sencillas herramientas como Visual Studio. Las aplicaciones de producción pueden obtener predicciones, modelos, o procedimiento almacenan de objetos visuales del tiempo de ejecución de Python 3.5 mediante la llamada a un instrucción T-SQL.

Esta versión incluye la distribución de Anaconda de Python, así como la nueva [revoscalepy](../python/what-is-revoscalepy.md) biblioteca, para mejorar la escalabilidad y rendimiento de sus soluciones de aprendizaje automático.

Puede instalar todo lo que necesita para empezar a trabajar con Python mediante el programa de instalación de SQL Server 2017:

+ **Servicios de aprendizaje de máquina (In-Database):** instale esta característica, junto con el motor de base de datos de SQL Server, para habilitar la ejecución segura de scripts de R en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] equipo.
  
     Cuando seleccione esta característica, las extensiones se instalan en el motor de base de datos para admitir la ejecución de scripts de Python y se crea un nuevo servicio, el [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)], para administrar las comunicaciones entre el tiempo de ejecución de Python y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instancia.

+ **Servidor de aprendizaje de máquina (independiente):** si no necesita la integración de SQL Server, instale esta característica para obtener compatibilidad con Python en Microsoft R Server. Esto le permite poner soluciones de Python mediante **mrsdeploy**.
  
     No instale esta característica en el mismo equipo que ejecuta Servicios de aprendizaje de máquina de SQL Server.


## <a name="additional-resources"></a>Recursos adicionales

[Configurar servicios de bases de datos de aprendizaje de automático de Python](setup-python-machine-learning-services.md)

[Tutoriales de Python](../tutorials/sql-server-python-tutorials.md)
