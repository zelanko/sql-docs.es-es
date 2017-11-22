---
title: Tutoriales de SQL Server R | Documentos de Microsoft
ms.custom: SQL2016_New_Updated
ms.date: 08/29/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
dev_langs: R
caps.latest.revision: "1"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 341ec619ee5976ca7488f3662f010358b4457437
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="sql-server-r-tutorials"></a>Tutoriales de SQL Server R

Este artículo proporciona una lista de tutoriales y ejemplos que muestran el uso de R con SQL Server 2016 o 2017 de SQL Server. A través de estos ejemplos y demostraciones, obtendrá información sobre:

+ Cómo ejecutar R de T-SQL
+ ¿Cuáles son los contextos de proceso remotos y locales, y cómo se puede ejecutar el código de R con el equipo de SQL Server
+ Cómo ajustar el código R en un procedimiento almacenado
+ Optimizar el código de R para un entorno de producción de SQL
+ Situaciones del mundo real para incrustar el aprendizaje automático de aplicaciones

Para obtener información sobre los requisitos y el programa de instalación, consulte [requisitos previos](#bkmk_Prerequisites).

## <a name="bkmk_sqltutorials"></a>Tutoriales de R

A menos que se indique lo contrario, los tutoriales se desarrollaron para SQL Server 2016 R Services y se esperan que funcione en servicios de aprendizaje de SQL Server de 2017 máquina sin cambios significativos.

Todos los tutoriales hacen un amplio uso de características en el paquete RevoScaleR para SQL Server contextos de proceso.

+ [Análisis detallado de ciencia de datos con R y SQL Server](../tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)

  Obtenga información acerca de cómo usar las funciones de los paquetes de RevoScaleR. Mover datos entre R y SQL Server y conmutador de contextos para adaptarse a una tarea determinada de proceso. Crear modelos y los gráficos y moverlos entre el entorno de desarrollo y el servidor de base de datos.

  **Público:** para científicos de datos o a los desarrolladores que ya están familiarizados con el lenguaje R, y que desean conocer los paquetes de R mejorados y las funciones de Microsoft R Revolution Analytics.

  **Requisitos:** cierto conocimiento básico de R. Acceso a un servidor con SQL Server R Services o servicios de aprendizaje de máquina con R. Para el programa de instalación, consulte [requisitos previos](#bkmk_Prerequisites).

+ [Análisis de R en bases de datos para desarrolladores de SQL](../tutorials/sqldev-in-database-r-for-sql-developers.md)

  Compilar e implementar una solución completa de R, utilizando solo [!INCLUDE[tsql](../../includes/tsql-md.md)] herramientas.

  Se centra en mover una solución en producción. Aprenderá cómo ajustar el código de R en un procedimiento almacenado, guardar un modelo de R en una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y realizar llamadas con parámetros al modelo de R para la predicción.

  **Público:** para programadores de SQL, los desarrolladores de aplicaciones o profesionales SQL que admiten soluciones en R y desean obtener información sobre cómo implementar modelos de R en SQL Server.

  **Requisitos:** no se necesita ningún entorno de R. Se proporciona todo el código de R y puede crear la solución completa usando solo [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e inteligencia empresarial familiarizado y herramientas de desarrollo de SQL. Sin embargo, algunos conocimientos básicos de R es útil.

  Debe tener acceso a un servidor SQL Server con el lenguaje R instalado y habilitado. Para el programa de instalación, consulte [requisitos previos](#bkmk_Prerequisites).

+ [Inicio rápido: Uso de R en T-SQL](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)

  Este tutorial rápido trata la sintaxis básica para poder usar R en [!INCLUDE[tsql](../../includes/tsql-md.md)].

  Aprenda a llamar el tiempo de ejecución de R de T-SQL, incluir funciones de R en el código SQL y ejecutar un procedimiento almacenado que guarda la salida de R y modelos de R en una tabla de SQL.

  **Público:** para las personas que están familiarizado con la característica y desean obtener información sobre los conceptos básicos de la llamada a R desde un procedimiento almacenado.

  **Requisitos:** ningún conocimiento de R o SQL necesarios. Sin embargo, se necesita SQL Server Management Studio o en otro cliente que puede conectarse a una base de datos y ejecutar instrucción T-SQL. Se recomienda gratuitamente [extensión MSSQL para el código de Visual Studio](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql) si está familiarizado con las consultas de T-SQL.

  También debe tener acceso a un servidor con SQL Server R Services o servicios de aprendizaje de máquina con R está habilitado. Para el programa de instalación, consulte [requisitos previos](#bkmk_Prerequisites).

+ [Tutorial integral de ciencia de datos](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)

  Muestra el proceso de ciencia de datos de principio a fin, adquirir los datos y guardarlo en SQL Server, analizar los datos con R y compilar gráficos.

  Aprenderá a mover gráficos entre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y R y compare la ingeniería de característica en T-SQL con funciones de R. Por último, aprenderá cómo utilizar el modelo de predicción en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para la puntuación del lote y la puntuación de varias filas.

  **Público:** para las personas que están familiarizados con R y con herramientas de desarrollo, como SQL Server Management Studio.

  **Requisitos:** debe tener acceso a un entorno de desarrollo de R y sabe cómo ejecutar comandos de R. Uso de PowerShell es necesario para descargar el conjunto de datos de ciudad de Nueva York taxi. Debe tener acceso a un servidor con SQL Server R Services o servicios de aprendizaje de máquina con R está habilitado. Para el programa de instalación, consulte [requisitos previos](#bkmk_Prerequisites).

## <a name ="bkmk_samples"></a>Muestras de productos

Estos ejemplos y demostraciones se proporcionan con el equipo de desarrollo de SQL Server para resaltar las muchas maneras en que puede usar análisis incrustado en las aplicaciones reales.

+ [Crear un modelo de predicción con R y SQL Server](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction)

  Obtenga información acerca de cómo una empresa de alquiler de ski puede usar el aprendizaje automático para predecir alquileres futuras, que le permite el plan de negocios y el personal para satisfacer la demanda futura.

+ [Realizar cliente agrupación en clústeres mediante R y SQL Server](https://microsoft.github.io/sql-ml-tutorials/R/customerclustering/)

  Usar aprendizaje supervisado a los clientes de segmento basándose en los datos de ventas.

## <a name="bkmk_Prerequisites"></a>Requisitos previos

Para usar estos tutoriales y ejemplos, debe instalar uno de los siguientes productos de servidor:

+ SQL Server 2016 R Services (In-Database)
  
  Es compatible con R. Asegúrese de instalar el características de aprendizaje automático y, a continuación, habilitar los scripts externos.

+ Servicios de aprendizaje de máquina (en bases de datos) de SQL Server de 2017
  
  Es compatible con R o Python. Debe seleccionar la máquina de aprendizaje de característica y el idioma que desea instalar y, a continuación, habilitar los scripts externos.

Después de ejecutar el programa de instalación de SQL Server, no olvide estos pasos importantes:

+ Habilitar la característica de ejecución de script externo mediante la ejecución`sp_configure 'external scripts enabled', 1`
+ Reiniciar el servidor
+ Asegúrese de que el servicio que llama el tiempo de ejecución externo tiene los permisos necesarios
+ Asegúrese de que la cuenta de usuario de Windows o inicio de sesión SQL tiene los permisos necesarios para conectarse al servidor, para leer los datos y para crear los objetos de base de datos requeridos por el ejemplo

Si experimenta problemas, consulte este artículo para algunos problemas comunes: [solución de problemas de servicios de aprendizaje de máquina](../machine-learning-troubleshooting-faq.md)
