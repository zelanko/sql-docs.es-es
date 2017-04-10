---
title: "Crear flujos de trabajo que usan R en SQL Server | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "05/31/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 34c3b1c2-97db-4cea-b287-c7f4fe4ecc1b
caps.latest.revision: 11
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 11
---
# Crear flujos de trabajo que usan R en SQL Server
  Una base de datos relacional es una tecnología muy optimizada para ofrecer soluciones escalables para procesamiento, almacenamiento y consulta de datos de transacciones. Sin embargo, tradicionalmente generalmente han dependido soluciones R sobre cómo importar datos desde diversos orígenes, a menudo, en formato CSV, para realizar el modelado y la exploración de datos adicional. Tales prácticas no solo son poco eficaces, sino que entrañan riesgos.  
  
 Con [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] ofrece varias ventajas:  
  
-   Seguridad de los datos. La potencia de R se incorporen a la base de datos está cerca del origen de datos. Evita el movimiento de datos de una pérdida de tiempo o no seguros.  
  
-   Velocidad. Las bases de datos están optimizados para operaciones basadas en conjunto. Además, las recientes innovaciones en las bases de datos como tablas en memoria y almacenamiento de datos en columnas más mejoran la ciencia de datos realizando agregaciones muy veloces.  
  
-   Integración. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es el punto central de operaciones para muchas otras tareas de administración de datos y aplicaciones que consumen la empresa. Ya usando datos en la base de datos garantiza que los datos son coherentes y actualizados. En lugar de procesar datos en R, puede confiar en las canalizaciones de datos empresariales incluidos [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] y factoría de datos. Informes de análisis o de resultados están fácil a través de Power BI o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
 Si usan la combinación adecuada de SQL y R para distintas tareas de procesamiento y análisis de datos, los científicos de datos y los desarrolladores lograrán ser más productivos. En esta sección se describe cómo se puede integrar R con otras soluciones empresariales para realizar tareas de transformación, análisis e informes de datos.  
  
##  <a name="bkmk_ssis"></a> Crear flujos de trabajo eficaces que usan R y la base de datos  
 Los flujos de trabajo de ciencia de datos son tremendamente iterativos y conllevan una enorme transformación de los datos, como los ajustes de escala, las agregaciones, el cálculo de probabilidades y cambiar los atributos de nombre y combinarlos. Los científicos de datos están acostumbrados a realizar muchas de estas tareas en R, Python u otro idioma; Sin embargo, requiere una integración perfecta con procesos y herramientas ETL ejecutar estos flujos de trabajo en datos de la empresa.  
  
 Porque [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] permite ejecutar operaciones complejas de R a través de Transact-SQL y procedimientos almacenados, puede integrar las tareas específicas de R con los procesos ETL existentes sin necesidad de trabajo mínima en desarrollo nuevo. En lugar de realizar una cadena de tareas de ntensive de memoria en R, preparación de datos puede optimizarse mediante las herramientas más eficaces, incluidos [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] y [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 Por ejemplo, puede combinar R con [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en escenarios como los siguientes:  
  
-   Use [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] tareas para crear los objetos necesarios en la base de datos SQL  
  
-   Usar bifurcaciones condicionales para alternar el contexto de ejecución de trabajos de R  
  
-   Ejecutar trabajos de R que generan sus propios datos  
  
-   Usar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para llamar a un script de R guardado en una variable de texto  
  
### Ejemplos y recursos  
 [Aplicar el proyecto de aprendizaje automático mediante SQL Server 2016 SSIS y los servicios de R](https://blogs.msdn.microsoft.com/ssis/2016/01/11/operationalize-your-machine-learning-project-using-sql-server-2016-ssis-and-r-services/)  
  
 En esta entrada de blog, aprenderá cómo:  
  
-   Uso de R en la tarea Ejecutar SQL para generar los datos y guardar en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   Utilizar un procedimiento almacenado para entrenar un modelo de R y almacenarlo en la base de datos  
  
-   Realizar la puntuación en el modelo mediante la tarea de secuencia de comandos y la tarea Ejecutar SQL  
  
##  <a name="bkmk_ssrs"></a> Crear visualizaciones que usan R y herramientas de informes empresariales  
 Aunque R puede crear gráficos y visualizaciones interesantes, no se integra bien con orígenes de datos externos, lo que significa que cada gráfico debe representarse individualmente. Uso compartido también puede ser difícil.  
  
 Con [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], puede ejecutar operaciones complejas de R a través de [!INCLUDE[tsql](../../includes/tsql-md.md)] procedimientos almacenados, que pueden utilizarse fácilmente una gran variedad de herramientas, como de informes empresariales [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y Power BI.  
  
-   Visualizar objetos gráficos devueltos desde un script de R   
    usar [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
-   Utilice la tabla de Power BI  
  
## Ejemplos y recursos  
 [Dispositivo de gráficos de R para Microsoft Reporting Services (SSRS)](https://rgraphicsdevice.codeplex.com/)  
  
 Este proyecto CodePlex proporciona el código para ayudarle a crear un elemento de informe personalizado que representa el resultado de gráficos de R como una imagen que puede usarse en [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] informes.  Mediante el elemento de informe personalizado, puede:  
  
-   Publicar gráficos y gráficos creados con el dispositivo de gráficos de R [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] paneles  
  
-   Pasar [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] parámetros para los gráficos de R  
  
> [!NOTE]  
>  Tenga en cuenta que el código que admite el dispositivo de gráficos de R para Reporting Services debe estar instalado en el servidor de Reporting Services, así como en Visual Studio. También se requiere configuración y compilación manual.  
  
  