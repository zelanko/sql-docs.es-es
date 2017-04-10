---
title: "Introducci&#243;n a Microsoft R Server (independiente) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "r-server"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 52347d0d-ce60-4bb8-98d2-6163e87716b0
caps.latest.revision: 21
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 16
---
# Introducci&#243;n a Microsoft R Server (independiente)
  Microsoft R Server (independiente) le ayuda a implementar en la empresa el popular lenguaje de código abierto R, que le permitirá habilitar las soluciones de análisis de alto rendimiento y la integración con otras aplicaciones empresariales.  
  
## ¿Qué es Microsoft R Server?  
 Microsoft R Server (independiente) incluye los paquetes mejorados de R desarrollados por Revolution Analytics y admite las conexiones con diversos orígenes de datos, como Hadoop o Teradata, entre otros. Al instalar el servidor independiente, puede crear un entorno de servidor para ejecutar trabajos de R complejos y escalables.  
  
## Ventajas de usar el servidor de Microsoft R (independiente)  
 R constituye el lenguaje de programación más eficaz del mundo para la computación estadística, el aprendizaje automático y la creación de gráficos, y cuenta con el respaldo de una comunidad global muy activa de usuarios, desarrolladores y colaboradores. Tradicionalmente, el uso de R en un entorno empresarial presenta determinados retos, en especial a medida que aumente el volumen de datos o cuando tenga que implementar soluciones en entornos de producción. Microsoft R Server resuelve los problemas de implementación y la puesta en marcha del código R.  
  
 Microsoft R Server puede instalarse en cualquier equipo con Windows e incluye todos los paquetes de R y herramientas de conectividad para habilitar el contexto del proceso remoto y para admitir soluciones escalables, puede paralelizar.  
  
 Servidor de Microsoft R (independiente) es compatible con estos escenarios:  
  
-   **Uso de un servidor central para poner en marcha soluciones de R**  
  
     El servidor independiente proporciona un rendimiento mejorado de R sin necesidad de depender de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Cálculos complejos o de gran cantidad de recursos se pueden ejecutar en el servidor en un equipo portátil o de desarrollo que podría haber limitado a los recursos.  
  
     También puede centralizar los trabajos, por ejemplo, si necesita puntuación contra un modelo predictivo en producción o usar represente el servidor R como un único punto de contacto para R y predicciones se utilizan en los informes. 
     
     También se recomienda instalar al servidor de R (independiente) en el equipo de SQL Server si con frecuencia necesitará ejecutar R fuera del contexto de SQL Server.
  
-   **Habilitación de una exploración de datos y un modelado de predicción más eficaces**  
  
     Los científicos de datos pueden usar cualquier estación de trabajo cliente y cualquier herramienta de desarrollo de R para compilar las soluciones en R. Si la solución usa las API del paquete RevoScaleR, los cálculos se pueden realizar en el servidor, que normalmente tiene más memoria y potencia de procesamiento. De este modo, las soluciones pueden trabajar con conjuntos de datos mucho más grandes y aprovechar los cálculos de varios procesos, núcleos y subprocesos.  
  
## ¿Cómo lo consigo?  
 Consulte en [Create a Standalone R Server](../../advanced-analytics/r-services/create-a-standalone-r-server.md)las instrucciones para la instalación. Todos los componentes se pueden instalar usando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] el programa de instalación.  
  
## Instalar herramientas adicionales de R  
 Si no tiene un entorno de desarrollo preferido de R, hay muchas opciones. Para obtener más información, consulte [el programa de instalación o configurar herramientas de R](../../advanced-analytics/r-services/setup-or-configure-r-tools.md). 
 
 Para conectarse al servidor de Microsoft R o R servicios de SQL Server desde una estación de trabajo de ciencia de datos, se recomienda la versión de [Microsoft R Client](http://aka.ms/rclient/download) (descargar).  
  
## Ejecutando Script de R en el servidor de Microsoft R (independiente)  
 Después de haber configurado los componentes de servidor e instalado su IDE favorito de R, puede comenzar a desarrollar la solución con el paquete RevoScaleR. Estas API permiten enviar comandos de R a un servidor remoto para su ejecución.  
  
-   [Utilizar otros equipos](https://msdn.microsoft.com/microsoft-r/scaler-getting-started): comience por explorar este conjunto de funciones analíticas distribuibles que proporcionan un alto rendimiento y escalado a soluciones de R. Incluye versiones puede paralelizar de muchos de los paquetes, como agrupación en clústeres k-means, árboles de decisión y los bosques de decisión y herramientas para la manipulación de datos de modelado R más popular. También puede utilizar HPC para construir su propio algoritmo paralelo.  
    
-   [DeployR](https://msdn.microsoft.com/microsoft-r/deployr-about): este marco opcional proporciona las herramientas para programadores de R usar Java, JavaScript o .net para integrar el análisis de R de salida con un paquete de terceros.  

Puede trabajar con datos en una variedad de formatos, incluidos los archivos SAS, SPSS, Hadoop y texto. Puede analizar los datos en su lugar, o mover los datos de manera eficaz en el entorno de desarrollo local de R con el formato de archivo .xdf.  
  
Para empezar a trabajar con el servidor de R, consulte esta guía en la biblioteca de MSDN: [R Server - Introducción](https://msdn.microsoft.com/microsoft-r/microsoft-r-getting-started)  
  
 Para obtener información sobre cómo utilizar los paquetes de utilizar otros equipos, vea [un Tutorial de R en 25 funciones](https://msdn.microsoft.com/microsoft-r/microsoft-r-getting-started#an-r-tutorial-in-25-functions-or-so)  
  
## Vea también  
 [Introducción a SQL Server R Services](../../advanced-analytics/r-services/getting-started-with-sql-server-r-services.md)  
  
  