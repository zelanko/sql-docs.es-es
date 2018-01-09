---
title: "Introducción a Microsoft R Server (independiente) | Microsoft Docs"
ms.custom: 
ms.date: 10/31/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 52347d0d-ce60-4bb8-98d2-6163e87716b0
caps.latest.revision: "21"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.openlocfilehash: 7c68e4a44ea410d3ad54ee39a103695eb47b6473
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="getting-started-with-machine-learning-server-standalone"></a>Introducción a servidor de aprendizaje de máquina (independiente)
 
En SQL Server 2016, Microsoft R Server (independiente) ayudaron a poner el lenguaje de código abierto R en la empresa, para habilitar la integración con otras aplicaciones empresariales y las soluciones de análisis de alto rendimiento.  

En SQL Server 2017, el nombre se cambió al servidor de aprendizaje de máquina (independiente) para reflejar la adición de compatibilidad con el lenguaje de Python. Ambas versiones están disponibles gratuitamente para los usuarios de Enterprise Edition o Software Assurance.

Este artículo proporciona una descripción general de cómo puede usar servidor de aprendizaje de máquina (o servidor de R) y cómo empezar a trabajar con la instalación y ejemplos.

## <a name="why-use-a-standalone-server-for-machine-learning"></a>¿Por qué usar un servidor independiente para el aprendizaje automático

Si no es necesario integrar sus soluciones con datos de SQL Server de aprendizaje automático, el servidor de aprendizaje de máquina le ofrece la misma compatibilidad distribuida y escalable para R y Python y además admite la implementación de soluciones de Hadoop, Spark o Linux.

Servidor de aprendizaje de máquina también incluye los modelos previamente entrenados para análisis de imágenes y análisis de opiniones, que puede usar inmediatamente en las aplicaciones.

Las características de puesta en marcha de aprendizaje de máquina Server admiten la implementación y distribución de R y Python soluciones mediante el uso de servicios web, con la ejecución remota, topologías de clúster de Spark y Hadoop MapReduce y compatibilidad con Windows o Linux.

**SQL Server 2016**

+ Instalar a Microsoft R Server (independiente) desde el programa de instalación de SQL Server 2016.

    Esta opción crea un servidor independiente que es completamente independiente de R Services (In-Database). Esta versión solo admite R. El programa de instalación de un servidor independiente se incluye en la directiva de soporte técnico de SQL Server Enterprise Edition. Para obtener más información, consulte [Crear un R Server independiente](../../advanced-analytics/r/create-a-standalone-r-server.md).

+ Instalar a servidor de R mediante el instalador independiente de Windows.

    Este instalador crea una instancia nueva de Microsoft R Server que utiliza la directiva de soporte técnico de Microsoft de ciclo de vida Software moderno. También puede instalar a R Server para Linux, Cloudera, Teradata y Hadoop.
    
    Para obtener más información, consulte [instalar R Server 9.1 para Windows](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows).

**SQL Server 2017**

+ Instalar a servidor de aprendizaje de máquina (independiente) desde el programa de instalación de SQL Server 2017. 

    Esta opción crea un servidor independiente para admitir la puesta en marcha de la máquina de aprendizaje en R, Python o ambos. El programa de instalación de un servidor independiente se incluye en la directiva de soporte técnico de SQL Server Enterprise Edition. Para obtener más información, consulte [Crear un R Server independiente](../../advanced-analytics/r/create-a-standalone-r-server.md).  

+ Use el nuevo instalador independiente de Windows.

    Este método de instalación crea una nueva instancia del servidor de aprendizaje de máquina que utiliza la directiva de soporte técnico de Microsoft de ciclo de vida Software moderno. También puede instalar el servidor de aprendizaje de máquina en Hadoop, Spark o Linux sin costo adicional alguno.
    
    Para obtener más información, consulte [instalar servidor para aprendizaje máquina con Windows](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install).

**Actualizar un servidor existente**

+ Si tiene un servidor existente o una instancia que desea actualizar, descargue y ejecute el programa de instalación basado en Windows para obtener las actualizaciones. 

    Para obtener más información, consulte [utilizando SqlBindR para actualizar una instancia](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md).

## <a name="start-using-machine-learning-server"></a>Empezar a utilizar servidor de aprendizaje de máquina

 Una vez haya configurado los componentes de servidor y configurar el IDE para usar los archivos binarios del servidor de aprendizaje de máquina, puede empezar a desarrollar la solución con las nuevas API, como RevoScaleR y revoscalepy, MicrosoftML y olapR.
    
Para empezar, consulte a estas guías:

+ [Plantillas de solución](https://docs.microsoft.com/machine-learning-server/r/sample-solutions)

    Ejemplos de esta, encontrará soluciones a los que se muestran cómo aplicar el aprendizaje automático en industrias específicas. Escenarios actuales están en marketing, finanzas, sanitaria y comercial.

+ [Explorar R y ScaleR en 25 funciones](https://docs.microsoft.com/machine-learning-server/r/tutorial-r-to-revoscaler): explorar esta colección de funciones analíticas distribuibles que proporcionan alto rendimiento y escalabilidad para soluciones de R. Incluye versiones que se pueden usar en parelelo de muchos de los paquetes de R más conocidos, como agrupación en clústeres k-means, árboles y bosques de decisión, y herramientas para la manipulación de datos.

- [MicrosoftML](https://msdn.microsoft.com/library/mt790482.aspx)

    El paquete MicrosoftML es un conjunto de algoritmos y transformaciones que se desarrollan a Microsoft y que son rápidas y escalables de aprendizaje de nueva máquina. Puede utilizarlo en R o Python. Para obtener más información, consulte [MicrosoftML para Python](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) y [MicrosoftML para R](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package).

## <a name="see-also"></a>Vea también

[Introducción a servicios de aprendizaje de máquina SQL Server](../../advanced-analytics/r/getting-started-with-sql-server-r-services.md)